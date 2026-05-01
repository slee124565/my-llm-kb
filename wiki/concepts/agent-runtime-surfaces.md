# Agent Runtime Surfaces

## Summary

Agent runtime surfaces 指的是：agent 實際在哪裡運行、由誰持有 memory 與 execution context、以及工具、狀態、權限與審計能力分別暴露在哪一層。它不是單純的 deployment choice，而是會直接影響 harness 設計、memory ownership、observability 與 portability 的架構分歧。

## Why It Matters

很多「agent 怎麼做比較好」的爭論，其實混在不同 runtime surface 之間。repo-local coding agent、provider-managed hosted agent、local personal agent，面對的狀態持有者、風險模型與人機互動面都不同。如果不先分清 runtime surface，就容易把某一種環境裡有效的做法，錯誤套用到另一種環境。

## Current Framing

- repo-local coding agent 傾向把 `AGENTS.md`、`docs/`、plans、logs 與可驗證 evidence 留在 repository 中，讓 repo 變成主要 system of record
- ticket-backed orchestrator 是另一種 runtime surface：issue tracker 持有 task state 與 dependency graph，repo 持有 workflow contract，agent runner 持有 per-issue workspace 與 session execution
- 隨 coding 本身被壓縮，repo-local coding agent 的工作面也可能向上游擴張：不只實作 feature，還會吸收 feedback triage、bug prioritization、PR drafting 與部分 product shaping
- provider-managed hosted agent 會把 sandbox lifecycle、session recovery、credential routing 與部分 orchestration 收斂到平台，由平台吸收模型快速演化帶來的 runtime churn
- local personal agent 則更強調 user-owned memory、conversation-first steerability、CLI-first operability 與對本地資料面的直接接觸
- 對 repo-local 或 local-personal agent 來說，MCP / connector 常先解決「能不能碰到資料」，但真正影響效果的往往是 operability：能否用 CLI 把搜尋、精讀、下載、草稿寫入與大 payload export 壓成可組合的小命令
- 當人類用 agent 共同打造自己的 CLI 或資料匯出工具時，真正的控制面不只在 access / operability，還包括 product judgment：defaults、overwrite policy、artifact format 與真實 example testing
- brain / hands / memory 分離是 hosted runtime 的重要 framing；repo docs / plans / logs 則是 repo-local coding agent 的對應 state surfaces
- memory ownership 不只是資料儲存位置問題，也決定誰能檢查、遷移、壓縮、審計與重用 agent state
- context storage 與 context management 可分開設計：歷史保存可以穩定留存，但摘要、裁剪、檢索與 handoff policy 可以隨模型能力改變
- runtime surface 的差異，會反過來影響 harness complexity：有些控制面應交給平台吸收，有些則必須保留在使用者自己的 repo 或本地檔案中
- hosted runtime 不只暴露 task execution surface，也隱含 quality-control surface：routing correctness、hardware equivalence、production eval coverage、rollback ability 與 privacy-safe debug tooling 都會直接影響使用者實際看到的 agent 品質
- harmony response format 顯示 prompt template 本身也是 runtime surface；roles、channels 與 stop-token 規則決定 reasoning、tool call 與 persisted history 如何流動
- gpt-oss verification guidance 進一步把 prompt formatting、reasoning transport 與 inference code 都拉進 runtime correctness 的定義裡，而不只是把它當成輸出品質問題
- 只要一個 stack 需要保留 raw reasoning 或 tool traces，runtime surface 就不只是輸入輸出 API，而是包含可恢復的內部狀態契約
- policy prompts 也是 runtime surface 的一部分：policy length、output format、reasoning effort 與 precedence 規則會直接決定 safety workflow 的品質
- 在 Trust & Safety 流程中，runtime 不是只有生成答案，而是生成可審計的 policy decision

## Signals From Recent Articles

- [Claude Managed Agents](../articles/claude-managed-agents.md)
- [OpenClaw Takes Over The Internet](../articles/openclaw-takes-over-the-internet-peter-steinberger.md)
- [Deep Dive into LLMs like ChatGPT](../articles/deep-dive-into-llms-like-chatgpt.md)
- [Shipping at Inference-Speed](../articles/shipping-at-inference-speed-peter-steinberger.md)
- [Harness Engineering](../articles/harness-engineering-codex-agent-first-world.md)
- [OpenAI Symphony Codex Orchestration](../articles/openai-symphony-codex-orchestration.md)
- [Introducing Codex](../articles/introducing-codex.md)
- [Bespoke CLIs for Codex](../articles/bespoke-clis-for-codex.md)
- [Notes From a Marketer Building a Real CLI With Codex](../articles/notes-from-a-marketer-building-a-real-cli-with-codex.md)
- [What Happens After Coding Is Solved](../articles/what-happens-after-coding-is-solved-boris-cherny.md)
- [A Postmortem of Three Recent Issues](../articles/a-postmortem-of-three-recent-issues.md)
- [OpenAI harmony response format](../articles/openai-harmony.md)
- [How to handle the raw chain of thought in gpt-oss](../articles/handle-raw-cot.md)
- [Verifying gpt-oss implementations](../articles/verifying-implementations.md)
- [User Guide For Gpt-Oss-Safeguard](../articles/gpt-oss-safeguard-guide.md)

## Open Questions

- hosted runtime、repo-local runtime 與 local personal runtime 之間，最小可攜的 state contract 應長什麼樣子
- 哪些 memory surfaces 應由使用者自己持有，哪些可以安全讓渡給平台
- conversation-first 介面降低了多少摩擦，又犧牲了多少顯式 controllability 與 auditability
- MCP / connector 與 CLI surface 的分工邊界應如何定義，才能同時保留 access control 與 operability
- CLI-first operability 何時真的是更薄的 abstraction，何時只是把原本結構化的 protocol 問題推回 shell glue
- product judgment 與 taste 能否被可靠地編成 repo-local rules，而不只是留在人的直覺裡
- 隨 provider-managed agent infrastructure 成熟，repo-local knowledge base 會成為補充層，還是仍然是 load-bearing system of record
- 當 coding agent 開始讀取回饋、整理需求與建議優先順序時，runtime surface 會如何重畫 PM、design 與 engineering 的責任邊界
- issue tracker、repo workflow file、agent app-server 與 dynamic tool calls 之間的權限邊界應如何切，才能讓 agent 操作 tracker 而不暴露完整 credential surface
- provider-managed runtime 的品質問題若只在特定硬體、流量路由或 partner surface 上發生，使用者與 team 應透過哪些 artifact 才能看見並調試這些差異
- harmony / reasoning / tool-call contract 是否應被視為 runtime surface 的核心層，而非單純的 model-specific adapter
- verification 的邊界要畫到哪裡：prompt format、response shape、reasoning transport，還是完整 eval bundle
- safety policy prompts 的控制面要落在 repo 文件、模板還是 runtime library

## Related Pages

- [Externalized Agent State](externalized-agent-state.md)
- [Long-Running Agent Harnesses](long-running-agent-harnesses.md)
- [Repository Knowledge As System Of Record](repository-knowledge-as-system-of-record.md)
- [LLM Agents](../maps/llm-agents.md)
- [Long-Running Agents](../maps/long-running-agents.md)
