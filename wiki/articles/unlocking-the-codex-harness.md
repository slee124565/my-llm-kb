# Unlocking The Codex Harness

## Source

- URL: https://openai.com/zh-Hant/index/unlocking-the-codex-harness/
- Author: Celia Chen
- Publisher: OpenAI
- Published: 2026-02-04
- Captured: 2026-06-24
- Raw file: `raw/sources/2026/2026-02-04-unlocking-the-codex-harness.md`

## Main Claims

- Codex 的核心能力不只是一個模型或 CLI，而是一套可被多種介面重用的 agent 執行框架（agent harness）。Web、CLI、IDE extension 與 macOS app 都需要驅動同一個核心 agent loop，否則每個介面都會重新發明工作區探索、工具執行、串流進度、差異呈現與核准流程。
- Codex App Server 把核心 agent loop 包成雙向 JSON-RPC API。這個 API 的價值不是只讓外部程式送出一個 request，而是讓 client 可以接收一串結構化事件：thread 開始、turn 開始、item 開始、工具核准、delta 串流、item 完成與 turn 完成。
- App Server 的基本抽象是項目（item）、回合（turn）與對話串（thread）。這讓 Codex workflow 可以把使用者輸入、assistant 訊息、工具執行、核准要求與 diff 都放進同一條可呈現、可恢復、可串流的事件時間軸，而不是把 agent 行為壓扁成一次性文字回覆。
- 不同 Codex client 對 runtime 的責任不同。Local app / IDE 通常啟動本機 App Server 子程序，Codex Web 則在容器 worker 中啟動 App Server 並透過後端串流事件；TUI 歷史上是特殊 native client，但也正往 App Server client 收斂。
- OpenAI 對整合方式的排序很清楚：若要完整嵌入 Codex 體驗，優先使用 App Server；若只要把 Codex 當 MCP tool 或一次性 CLI command，也可以，但會失去較豐富的 session、diff、approval 與 UI event semantics。
- App Server 的設計把 agent product integration 從「呼叫模型」提升成「嵌入一個 long-running, stateful, user-controllable work runtime」。對產品團隊來說，真正要設計的是 client 如何呈現事件、處理 approval、保存 thread、重新連線、升級 server binary，並維持 protocol 相容性。

## Why It Matters

這篇補上了 `Harness Engineering` 比較少談的產品 runtime 層。先前 repo 已經有很多關於 `AGENTS.md`、repo docs、外部化狀態、eval、sandbox 與 long-running task 的材料；這篇則把 Codex 自身如何被包成可嵌入平台講清楚。

最重要的增量是：Codex harness 不只是任務規則或 repo 文件，而是一個 protocol surface。當 agent workflow 要進入 IDE、desktop app、web runtime 或第三方產品時，client 需要的是可重放、可串流、可核准、可恢復的事件模型。這會改變我們理解 coding agent 產品的方式：好的 agent UI 不是在 chat box 外面包一層殼，而是在正確粒度上呈現 thread、turn、item、tool call、diff 與 approval。

## Relation To Existing Concepts

- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md): App Server 是 Codex runtime 的正式 integration surface；它把 core agent loop、thread persistence、config/auth、tool execution、MCP/skills 與 approval policy 暴露給不同 client。
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md): thread persistence、client reconnect、server-side progress retention、turn lifecycle 與 approval pause 都是 long-running harness 的 runtime primitives。
- [Externalized Agent State](../concepts/externalized-agent-state.md): thread history、event stream、diff artifacts 與 tool execution records 是跨 client / session 可恢復的 state，不應只留在單次 UI context。
- [Codex Workflows](../maps/codex-workflows.md): 這篇把 Codex workflow 從「使用者如何提示 Codex」推進到「產品如何嵌入 Codex」。App Server 是 Codex as platform 的關鍵入口。
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md): App Server 不取代 repo-local knowledge；它提供 runtime channel，讓 client 能把 repo、tools、diff 與 approvals 呈現給人類 reviewer。

## Tensions Or Disagreements

- App Server 是最完整的整合方式，但整合成本也最高。對只需要 CI、one-shot automation 或簡單 MCP tool use 的團隊，完整 JSON-RPC client 可能過重。
- 文章把 App Server 定位成未來主要 integration path，但它也承認跨供應商 agent protocol 還在演進。這意味著 provider-specific richness 和 ecosystem portability 仍然有取捨。
- Local / IDE client 可以固定 tested binary；partner client 可能讓 server binary 更快升級。這提高了相容性要求，也讓 client/server version policy 成為產品責任，而不只是工程細節。
- App Server 讓 Codex 更容易嵌入其他產品，但也把 approval、credential、sandbox、thread retention 與 event log 隱私拉進整合者的責任範圍。

## Open Questions

- 哪些 Codex App Server event 應保存成 durable product trace，哪些只需要即時 UI 呈現？
- 如果第三方 client 將 Codex 嵌入自己的產品，approval UX、sandbox policy 與 credential status 應由 client、server 還是上層產品 policy 擁有？
- Codex App Server 和 MCP server 的邊界應如何切：何時需要完整 Codex session semantics，何時只需要 tool-like invocation？
- 若未來出現跨供應商 agent runtime protocol，Codex 的 thread / turn / item / approval / diff model 有哪些部分可以標準化，哪些會保持 provider-specific？

## Merge Candidates

- Codex App Server should be treated as a runtime integration surface, not just an API wrapper around a model.
- Thread, turn, item, tool approval, diff, and assistant deltas are the minimum event primitives for a rich coding-agent client.
- Long-running coding-agent UX needs server-side session persistence and reconnect semantics because browser tabs, local clients, and remote workers have different lifetimes.
- MCP-style tool exposure is useful for narrower workflows, but full Codex embedding needs richer session and UI event semantics.
- Agent product integration should design client/server versioning, approval UX, event persistence, and sandbox/credential boundaries as first-class harness responsibilities.
