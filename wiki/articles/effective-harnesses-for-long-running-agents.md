# Effective Harnesses for Long-Running Agents

## Source

- URL: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
- Author: Anthropic Engineering
- Published: 2025-11-26
- Captured: 2026-03-25
- Raw file: `raw/sources/2026/2026-03-25-claude-effective-harnesses-for-long-running-agents.md`
- Workspace provenance: copied from `my-blog-kb/raw/sources/2026/2026-03-25-claude-effective-harnesses-for-long-running-agents/2026-03-25-claude-effective-harnesses-for-long-running-agents.md`

## Main Claims

- 單靠壓縮（compaction）不足以支撐跨多個 context window 的長任務。文章的核心判斷是：模型可以被壓縮後繼續跑，但下一個 session 仍可能不知道「上一班工程師」到底完成了什麼、哪些東西還壞著、下一步應該從哪裡開始。因此 long-running agent 真正需要的是一組可回讀的 agent 執行框架（agent harness），而不是只靠更長或更會摘要的上下文。
- 長任務的主要失敗模式不是單一 bug，而是工作節奏失控。Claude 在實驗中會一次做太多、在 context 用完時留下半成品、看到部分進度就過早宣告完成，或把 feature 標成通過但沒有做端到端驗證（end-to-end verification）。這些問題對產品與工程管理的含義是：agent 長跑若沒有明確任務粒度與驗收標準，成本會轉嫁成後續清理與重工。
- 初始化代理（initializer agent）負責把模糊需求展開成可接手環境：`init.sh`、進度檔、feature list、初始 git commit。這不是形式上的 scaffolding，而是把未來 session 需要的狀態外部化，讓每次新 context 都能從 repo artifact 重新定向。
- 編碼代理（coding agent）每次只做一個 feature，並在結束前留下乾淨狀態、git commit 與進度紀錄。這裡的重點不是「agent 會不會 commit」，而是把 session 結束定義成可被下一位 agent 或人類接手的 main-branch-quality checkpoint。
- feature list 使用 JSON 而不是 Markdown，是一個很實際的 harness 設計訊號：當某個 artifact 會被 agent 反覆讀寫，格式本身會影響 drift 風險。把測試描述與 `passes` 狀態結構化，並明確禁止刪改測試，可以降低 agent 為了看起來完成而改掉驗收標準的機率。
- 測試工具必須接近人類使用路徑。文章指出，Claude 會跑 unit test 或 `curl`，但仍可能漏掉真正的使用者流程；明確要求使用 browser automation 做人類視角的測試後，效果明顯改善。這把 verification 從「跑過一些命令」推進到「用產品實際互動證明 feature 能用」。

## Why It Matters

這篇把 externalized state 從抽象概念落成具體 harness 設計，對 repo-based agent work 特別重要。它說明 long-running agent 的可靠性不是只由模型能力決定，而是由「任務如何被拆解、狀態如何被保存、下一個 session 如何上手、完成如何被驗證」共同決定。

對 `my-llm-kb` 來說，它是 `Long-Running Agent Harnesses` 與 `Externalized Agent State` 之間的橋接來源：progress file、git history、feature list、init script、端到端測試工具，都是把一次性對話轉成可恢復工程流程的狀態表面。

## Relation To Existing Concepts

- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Long-Running Agents](../maps/long-running-agents.md)

## Tensions Or Disagreements

- 文章偏向 full-stack web app 與 coding agent 場景；research、ops、knowledge work、finance modeling 等非 coding 長任務是否能直接套用同一套 initializer / coding-agent split，還需要重新定義 feature、clean state 與 verification。
- 它強調 session artifact，但沒有深入處理 artifact 本身的品質退化與過期治理。feature list、progress file 與 git history 如果被 agent 寫得含糊或失真，也可能變成新的錯誤來源。
- 文章把不同 prompt 的 initializer / coding agent 稱為不同 agents，但 footnote 也說底層 system prompt、tools 與 harness 相同。這提醒我們：多代理架構有時只是 role / prompt split，不一定代表真正獨立的 runtime 或 state boundary。
- JSON feature list 降低了 drift，但也增加了「驗收標準由誰寫、誰 review」的治理問題；如果 initializer 展開錯誤，後續 coding agent 可能只是高效完成錯誤的 spec。

## Open Questions

- feature list、progress log、spec、git commit 與 `init.sh` 之間的最小 contract 要多嚴格才夠？
- context reset、continuous session 與 compaction 應如何依任務風險、模型能力與 artifact 品質切換？
- 哪些 artifact 應 machine-readable，哪些保留人類可讀即可？
- 對非 UI 產品任務，等價於 browser automation 的 end-to-end verifier 應如何設計？
- initializer agent 展開 feature list 後，是否需要獨立 reviewer 或 human approval 才能進入長跑？

## Merge Candidates

- 壓縮（compaction）不是 long-running agent 的完整記憶方案；真正 load-bearing 的是可回讀、可驗證、可接手的外部狀態。
- initializer / coding-agent split 可以把「需求展開」與「逐步推進」分開，降低 agent 一次做太多與過早宣告完成的風險。
- JSON feature list、progress file、git history 與 `init.sh` 共同形成跨 session handoff contract。
- 一次只完成一個 feature，並以 clean state、commit、進度紀錄與端到端驗證收尾，比大範圍但未驗證的進度更可靠。
- 長任務 agent 的 verifier 應盡量貼近真實使用路徑；對 web app 而言，browser automation 比只看 code 或 curl 更能捕捉產品層 bug。
