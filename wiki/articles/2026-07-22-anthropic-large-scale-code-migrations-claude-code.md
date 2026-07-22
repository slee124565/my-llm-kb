# How Anthropic Runs Large-Scale Code Migrations With Claude Code

## Source

- URL: https://x.com/i/status/2079654423828304282
- Author: ClaudeDevs @ClaudeDevs
- Published: unknown
- Captured: 2026-07-22T17:14:12+08:00
- Raw file: `raw/sources/2026/2026-07-22-anthropic-large-scale-code-migrations-claude-code.md`
- Source note: X.com 長文整理 Anthropic 以 Claude Code 進行 Bun Zig-to-Rust 與 Python-to-TypeScript 大型遷移的經驗；其中的成本、規模與成效為來源敘事，尚未在本 repo 獨立驗證。

## Main Claims

- 大型程式遷移的核心不是逐一修正 agent 生成的程式碼，而是修正產生程式碼的流程（loop）：先把成功定義、翻譯規則、待辦佇列與驗證器做成可重跑的系統，再讓 agent 依同一套迴圈大量執行。這把工程主管的注意力從追單一 bug，轉向找出「為何這類 bug 會反覆被生成」。
- 遷移開始前必須先建立強而可被推翻的評分器（judge）。既有測試要先分類、改寫成舊新版本都能執行的對外行為測試，並刻意對壞掉的版本測試它是否會失敗；缺少這個 exit condition，多 agent 的高輸出只會放大不確定性。
- `rulebook`、dependency map 與 gap inventory 是平行化之前的控制面。rulebook 將跨語言慣例與架構決策外部化；dependency map 決定哪些檔案能分批平行；gap inventory 則記下新語言必須補上的隱性契約，例如型別、介面或記憶體安全要求。先以少量檔案壓力測試這些規則，再把錯誤模式回寫規則，而不是保留試作程式碼一路手補。
- 實作、審查、修復應採分工的多 agent loop：較小模型負責高吞吐的翻譯，大模型或獨立 context 的 agent 做對抗式審查（adversarial review）；若兩個審查者不同意，再交由第三者裁決。重複發現的問題應修訂 rulebook 並重跑受影響批次，而不是只修那一個檔案。
- 工作佇列與昂貴操作要機械化。以檔案是否存在、編譯錯誤、smoke-test crash、行為 diff 等狀態重建 queue，可讓中斷後自然恢復；由單一 build daemon 批次重建與回歸測試，則避免多個 fixer 同時觸發最貴的編譯步驟。
- 來源主張 AI 改變了遷移的經濟性，但不是讓遷移免費：Bun 的案例仍消耗大量 token 與工程判斷。真正被壓縮的是人力逐檔轉寫與追錯的成本，因此適合重新評估那些已有明確商業痛點、但過去因工期太長而延後的遷移。

## Why It Matters

這篇把 repo 已有的 agent loop、long-running harness、evaluation 與 externalized state 串成一個高壓但具體的工程案例。它最重要的增量是指出：在可驗證的大型工作上，agent 的擴張性不是來自一次開更多 subagent，而是來自把「什麼算完成、下一件要做什麼、發現同類錯誤時如何改流程」變成機械而可審計的回授迴圈。

對採用 coding agent 的團隊而言，這也提供一個清楚的責任切分。人類先處理架構取捨、business case、rulebook 的初始 policy 與最終風險承擔；agent 處理大量可分片的翻譯、錯誤分類、實作與驗證迭代；compiler、測試與行為比較則擔任不依賴 agent 自我評價的 referee。這比「交給 agent 重寫，最後再人工 review」更容易恢復、擴大與追查。

## Relation To Existing Concepts

- [Agent Evaluations](../concepts/agent-evaluations.md): 可攜的舊新版本測試、刻意破壞後必須失敗的 judge test，以及逐命令輸出比對，都說明 evaluator 是遷移 loop 的前置條件與完成閘門，不是最後的品質裝飾。
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md): rulebook、dependency-aware batching、可從磁碟重建的 queue、對抗式審查與 build daemon，共同構成可恢復的長任務 harness；昂貴的 compiler 被序列化，其他可平行工作才被安全 fan out。
- [Externalized Agent State](../concepts/externalized-agent-state.md): rulebook、gap inventory、dependency map、`TODO(port)` 標記、error list 與 queue 都是 agent 之間可交接的狀態，不應只藏在某次 session 或某個 orchestrator 的暫存記憶裡。
- [Codex Workflows](../maps/codex-workflows.md): 雖然案例採用 Claude Code，對 Codex 的 repo-local migration、dependency upgrade、large refactor 同樣可用：把 deterministic mechanics 下放 scripts，保留獨立 review context 與可回放的驗證 evidence。
- [Getting Started With Loops](2026-07-06-getting-started-with-loops.md): 前文提供 trigger / stop condition 的通用分類；本文補上大型遷移的完整 loop 實例，將 stop condition 落在 compiler、smoke test 與跨版本行為等可機械檢查的裁判。
- [A Field Guide to Fable: Finding Your Unknowns](2026-07-03-a-field-guide-to-fable-finding-your-unknowns.md): rulebook 與 gap inventory 是 migration 專用的 unknown-discovery artifact；它們先把跨語言或架構轉換的隱性差異找出，避免 agent 在錯誤假設上高效率地擴張。

## Tensions Or Disagreements

- 來源案例來自 Anthropic 內部專案與特定模型／工具配置，不能把「百萬行、兩週、全測試通過」直接當成一般團隊的可複製承諾。可遷移的是 verifier-first、規則回寫、queue recovery 與 review separation，不是 token 成本或速度數字。
- 原程式碼能作為規格，只在既有行為值得保存時成立。若原系統本身含有隱性缺陷、過期 UX 或架構債，行為 parity 可能會把舊問題一起固化；此時 rulebook 應明確區分「必須相容」與「刻意改變」。
- 對抗式審查能降低單一 context 的盲點，但會增加成本、延遲與協調複雜度。對小型或低風險遷移，先用強測試與 targeted review，未必需要三層 reviewer 架構。
- 編譯器、測試與行為 diff 都可能有盲區。若 portable tests 因改寫而弱化、測試覆蓋不含真實情境，系統仍可能以「全綠」掩蓋 regression；來源提及的 post-merge regressions 正是提醒。

## Open Questions

- 哪些 migration 或 large refactor 值得先投資 rulebook、dependency map 與 portable judge，哪些規模用一般 test-first workflow 即可？
- rulebook 的變更要如何 version、review 與與受影響 batch 對應，才能避免它本身成為無法追溯的隱性 prompt？
- 當舊系統的行為並非正確規格時，如何在 parity suite 中標示應保留、應刻意改變與尚待產品決策的行為？
- build daemon 應以哪些 queue depth、compile time、failure clustering 或 cost signals 決定 batch 大小與 parallelism？
- 多 agent 對抗式審查在何種錯誤類型與風險級別上，比單一 reviewer 加更完整 deterministic checks 更有經濟性？

## Merge Candidates

- 可驗證的大型 agent 工作應先建立能通過原版、且能抓到刻意破壞版本的 judge；沒有可反駁的 verifier，就沒有可靠 exit condition。
- 對重複出現的錯誤，優先修規則、測試或 queue 分類，然後重跑受影響批次；不要把人力耗在逐檔手補症狀。
- rulebook、gap inventory、dependency map、機械 queue 與 error list 是跨 agent 的 externalized control plane，必須可版本化、可審查、可從磁碟恢復。
- 將高吞吐 implementation、獨立 context 的對抗 review、以及 deterministic compiler / test / behavior checks 分離，能同時提高平行度與降低自我評價偏誤。
- 昂貴且共享的操作應由單一 daemon 或等價協調器批次化；agent 可平行寫 patch，但不應無限制平行觸發 rebuild。
