# Notes From a Marketer Building a Real CLI With Codex

## Source

- URL: https://lindsaybrunner.com/thoughts/2026-04-11/building-a-cli-with-ai/
- Author: Lindsay Brunner
- Published: 2026-04-11
- Captured: 2026-04-16
- Raw file: `raw/sources/2026/2026-04-11-notes-from-a-marketer-building-a-real-cli-with-codex.md`
- Imported from workspace path: `blog/2026-04-16-building-a-cli-with-ai/2026-04-16-building-a-cli-with-ai.md`

## Main Claims

- 作者用 Codex 協作做出 `ChatGPT Thread Exporter`，把 shared link 匯出成 markdown、PDF，並可寫入 GitHub，核心目標是把 AI 對話變成可保存、可重用的工作 artifact
- 真正先該定義的是 guardrails 與 defaults：local-first、markdown default、PDF 作為更友善的輸出、唯一檔名、避免覆蓋、以及 public-safe examples
- 這次 build 的關鍵不是 prompt 技巧，而是用真實 shared links 反覆測試；只有在真實案例下，才看出 scaffold 看似完整但核心匯出仍然失效
- AI 能加速實作，但 product judgment 仍然在人：要看得出「技術上可行但體驗上不對」的狀況，並決定何時停下 feature creep
- 非工程背景的人也能有效做出工具，前提是他能持續從外部視角測試產物，並把「我會不會真的想保留這個」當成驗收標準

## Why It Matters

這篇把「用 agent 做工具」從工程話題拉回產品話題。對這個 repo 來說，它補上一個很實際的訊號：真正值得留存的 CLI，不只是能跑 API，而是能把工作 artifact 以安全、可讀、可回收的方式保存下來。它也強化了這個庫一貫的判準：人類不一定要先會寫 code，但一定要能持續判斷輸出是否符合真實用途。

## Relation To Existing Concepts

- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md)
- [Codex Workflows](../maps/codex-workflows.md)

## Tensions Or Disagreements

- 這篇非常有啟發性，但本質上是單一產品與單一作者的成功案例，不宜直接外推成所有 non-engineer + agent 協作都會長這樣
- `taste` 很有價值，但也很主觀；如果沒有落成可檢查的 defaults 與驗收標準，很容易退化成空泛形容詞
- 文章聚焦的是對話匯出與內容保存，不代表所有 CLI 都應優先做 markdown / PDF；輸出格式仍要看任務本身

## Open Questions

- 哪些 `taste` 與 guardrails 可以被編譯成 repo-local 規則，哪些必須保留給人類持續判斷
- 當 AI 對話成為可重用工作 artifact 時，最小可接受的匯出 contract 應包含哪些欄位與格式
- 對 agent-built tool 來說，真實 example testing 應該提升到多高的預設優先級

## Merge Candidates

- for user-facing agent-built tools, defaults matter as much as feature depth: local-first behavior, safe overwrite policy, readable filenames, and artifact-preserving exports should come before fancy polish
- real shared examples are a stronger truth test than scaffold completeness because they expose whether the core promise actually works
- when an agent helps build a tool, the human should keep product judgment and final acceptance while the agent provides implementation speed
