# Agent Runtime Surfaces

## Summary

Agent runtime surfaces 指的是：agent 實際在哪裡運行、由誰持有 memory 與 execution context、以及工具、狀態、權限與審計能力分別暴露在哪一層。它不是單純的 deployment choice，而是會直接影響 harness 設計、memory ownership、observability 與 portability 的架構分歧。

## Why It Matters

很多「agent 怎麼做比較好」的爭論，其實混在不同 runtime surface 之間。repo-local coding agent、provider-managed hosted agent、local personal agent，面對的狀態持有者、風險模型與人機互動面都不同。如果不先分清 runtime surface，就容易把某一種環境裡有效的做法，錯誤套用到另一種環境。

## Current Framing

- repo-local coding agent 傾向把 `AGENTS.md`、`docs/`、plans、logs 與可驗證 evidence 留在 repository 中，讓 repo 變成主要 system of record
- 隨 coding 本身被壓縮，repo-local coding agent 的工作面也可能向上游擴張：不只實作 feature，還會吸收 feedback triage、bug prioritization、PR drafting 與部分 product shaping
- provider-managed hosted agent 會把 sandbox lifecycle、session recovery、credential routing 與部分 orchestration 收斂到平台，由平台吸收模型快速演化帶來的 runtime churn
- local personal agent 則更強調 user-owned memory、conversation-first steerability、CLI-first operability 與對本地資料面的直接接觸
- 對 repo-local 或 local-personal agent 來說，MCP / connector 常先解決「能不能碰到資料」，但真正影響效果的往往是 operability：能否用 CLI 把搜尋、精讀、下載、草稿寫入與大 payload export 壓成可組合的小命令
- brain / hands / memory 分離是 hosted runtime 的重要 framing；repo docs / plans / logs 則是 repo-local coding agent 的對應 state surfaces
- memory ownership 不只是資料儲存位置問題，也決定誰能檢查、遷移、壓縮、審計與重用 agent state
- context storage 與 context management 可分開設計：歷史保存可以穩定留存，但摘要、裁剪、檢索與 handoff policy 可以隨模型能力改變
- runtime surface 的差異，會反過來影響 harness complexity：有些控制面應交給平台吸收，有些則必須保留在使用者自己的 repo 或本地檔案中
- hosted runtime 不只暴露 task execution surface，也隱含 quality-control surface：routing correctness、hardware equivalence、production eval coverage、rollback ability 與 privacy-safe debug tooling 都會直接影響使用者實際看到的 agent 品質

## Signals From Recent Articles

- [Claude Managed Agents](../articles/claude-managed-agents.md)
- [OpenClaw Takes Over The Internet](../articles/openclaw-takes-over-the-internet-peter-steinberger.md)
- [Deep Dive into LLMs like ChatGPT](../articles/deep-dive-into-llms-like-chatgpt.md)
- [Shipping at Inference-Speed](../articles/shipping-at-inference-speed-peter-steinberger.md)
- [Harness Engineering](../articles/harness-engineering-codex-agent-first-world.md)
- [Introducing Codex](../articles/introducing-codex.md)
- [Bespoke CLIs for Codex](../articles/bespoke-clis-for-codex.md)
- [What Happens After Coding Is Solved](../articles/what-happens-after-coding-is-solved-boris-cherny.md)
- [A Postmortem of Three Recent Issues](../articles/a-postmortem-of-three-recent-issues.md)

## Open Questions

- hosted runtime、repo-local runtime 與 local personal runtime 之間，最小可攜的 state contract 應長什麼樣子
- 哪些 memory surfaces 應由使用者自己持有，哪些可以安全讓渡給平台
- conversation-first 介面降低了多少摩擦，又犧牲了多少顯式 controllability 與 auditability
- MCP / connector 與 CLI surface 的分工邊界應如何定義，才能同時保留 access control 與 operability
- CLI-first operability 何時真的是更薄的 abstraction，何時只是把原本結構化的 protocol 問題推回 shell glue
- 隨 provider-managed agent infrastructure 成熟，repo-local knowledge base 會成為補充層，還是仍然是 load-bearing system of record
- 當 coding agent 開始讀取回饋、整理需求與建議優先順序時，runtime surface 會如何重畫 PM、design 與 engineering 的責任邊界
- provider-managed runtime 的品質問題若只在特定硬體、流量路由或 partner surface 上發生，使用者與 team 應透過哪些 artifact 才能看見並調試這些差異

## Related Pages

- [Externalized Agent State](externalized-agent-state.md)
- [Long-Running Agent Harnesses](long-running-agent-harnesses.md)
- [Repository Knowledge As System Of Record](repository-knowledge-as-system-of-record.md)
- [LLM Agents](../maps/llm-agents.md)
- [Long-Running Agents](../maps/long-running-agents.md)
