# Claude Managed Agents

## Source

- URL: https://x.com/dotey/status/2042017036931305667
- Author: 宝玉 @dotey
- Published: 2026-04-10
- Captured: 2026-04-10
- Raw file: `raw/sources/2026/2026-04-10-claude-managed-agents.md`
- Imported from workspace path: `blog/2026-04-10-claude-managed-agents/2026-04-10-claude-managed-agents.md`
- Source note: 這是一篇二級整理稿，主體是對 Anthropic 發布與工程文章的綜合解讀，不是 Anthropic 的 primary source

## Main Claims

- Claude Managed Agents 把長任務 agent 所需的 runtime、sandbox、狀態恢復、權限與追蹤能力，打包成 hosted service，讓企業可直接把 agent 能力嵌進產品
- 它和 Claude Code 的核心差異，不是「會不會寫 code」，而是 execution surface：前者是企業可嵌入、可長時間背景運行的雲端 API，後者是個人開發者在本地終端使用的 agent tool
- provider-managed harness 的價值，在於模型供應商能比客戶更快依模型特性調整 orchestration；某些為舊模型缺陷設計的補丁，會隨模型升級失去必要性
- Anthropic 的 hosted 架構把 brain、hands、memory 拆開：模型與調度框架負責推理，sandbox 和工具負責執行，session log 負責持久化狀態
- 這種拆分帶來 lazy sandbox startup、故障隔離、憑證隔離與未來多 agent handoff 的空間，但也引入平台綁定、成本控制與上下文管理治理等新問題
- 託管式 agent infrastructure 可以大幅降低企業導入門檻，但不會自動解決任務定義、workflow design、信任建立與業務資料治理

## Why It Matters

這篇的新增價值，不只是「Anthropic 也做 hosted agents」這個產品訊號，而是把 long-running harness 從 repo-local pattern 往上推成 platform product。對這個 repo 來說，它補進了兩個重要 framing：一是 provider-managed harness 可能比 customer-built harness 更能承接模型快速演化；二是 brain / hands / memory 分離，可能是 hosted long-running agents 的 load-bearing architecture。

## Relation To Existing Concepts

- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [LLM Agents](../maps/llm-agents.md)
- [Long-Running Agents](../maps/long-running-agents.md)

## Tensions Or Disagreements

- 來源本身是二級整理稿，混合產品宣傳、案例摘要與作者評論；若要確認功能邊界、價格或可用性，仍應回到 Anthropic 的 primary source
- 「agent 基建的 AWS 時刻」是有啟發性的比喻，但它預設基礎設施會像雲計算一樣集中化，這仍是推論，不是已證實結論
- provider-managed harness 確實減少企業自建成本，但也把 portability、可觀測性與 runtime control 的一部分讓渡給平台供應商
- 文章列舉的案例很強，但可能低估了企業仍需自行承擔的任務拆解、驗收標準、資料權限與人機信任成本

## Open Questions

- hosted runtime 與 repo-local / local terminal harness 之間，哪些 control surfaces 應由平台承擔，哪些應保留在使用者側
- 若未來企業同時使用多家 agent platform，最小可攜的 task contract、state contract 與 tool contract 應長什麼樣子
- 獨立 session log、credential broker 與 lazy sandbox 這些設計，會不會成為 hosted agent infra 的通用 primitive
- 對 coding 以外的知識工作與營運工作，brain / hands / memory 分離是否同樣成立，還是需要不同的 execution surface

## Merge Candidates

- provider-managed harnesses can absorb model-specific orchestration churn better than customer-built harnesses
- decoupling brain, hands, and memory is a load-bearing architecture for hosted long-running agents
- context storage and context management should be separated so retention stays stable while policies evolve
- hosted agent infrastructure lowers runtime friction but does not solve task definition, trust, or workflow design
