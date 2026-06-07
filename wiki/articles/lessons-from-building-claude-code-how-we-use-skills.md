# Lessons From Building Claude Code: How We Use Skills

## Source

- URL: https://claude.com/blog/lessons-from-building-claude-code-how-we-use-skills
- Author: Thariq Shihipar
- Publisher: Anthropic
- Published: 2026-06-03
- Captured: 2026-06-07
- Raw file: `raw/sources/2026/2026-06-03-lessons-from-building-claude-code-how-we-use-skills.md`

## Main Claims

- Claude Code 的 skills 不應被理解成「幾個 Markdown 檔」。它們是可被 agent 發現、按需展開、包含 instructions、scripts、assets、data、hooks 與 reference material 的資料夾。這把 skill 從 prompt snippet 提升成一種可版本化的程序記憶（procedural memory）與 runtime extension point。
- 有效的 skill 通常要有明確類型。Anthropic 把內部數百個 active skills 歸成九類：library / API reference、product verification、data fetching and analysis、business process automation、code scaffolding、code quality / review、CI/CD and deployment、runbooks、infrastructure operations。重要的不是分類本身，而是「一個 skill 最好乾淨落在一個目的上」；跨太多類型的 skill 會讓 agent 不知道何時使用。
- Verification skills 是最能直接改善輸出品質的類型。它們把測試、Playwright、tmux、影片紀錄、狀態斷言與 product flow 驗證固定成可重複程序，讓 agent 不只產出 diff，也能自己收集 evidence。
- Skill 的高訊號內容不是重述 agent 已經會做的事，而是記錄它常踩的陷阱、組織內部約束與 task-specific 判準。`Gotchas` section、reference snippets、setup config、logs 與 scripts 比抽象勵志規則更能改變行為。
- Skill description 是給模型做 routing 用的，不是給人看的簡介。描述應清楚說明什麼情境該觸發 skill、它解決什麼工作、需要哪些輸入與輸出；如果 description 寫得像 marketing copy，agent 會低觸發或誤觸發。
- Skill folder 是一種漸進揭露（progressive disclosure）機制。入口檔只應提供任務邊界與檔案地圖，詳細 API、範例、模板、scripts 與資料可以放在子檔案中，讓 agent 在需要時再讀，避免把所有 context 一次塞進主 prompt。
- Skills 可以被分享、上架、相依與測量，但這也把 skill catalog 變成需要治理的 shared runtime surface。marketplace、sandbox folder、PR promotion、usage logging 與 owner judgment 都是在處理「什麼程序記憶值得進入團隊共用層」。

## Why It Matters

這篇的增量不是「Claude Code 有 skills」這個功能介紹，而是把 skills 從 prompt engineering 拉到 agent runtime engineering。它說明一個成熟團隊如何把高頻工作流程、常見錯誤、驗證方法、內部 API 知識、runbook、部署步驟與維運邊界，拆成可被 agent 按需載入、可測量、可分享、可逐步演進的 artifact。

對 `my-llm-kb` 來說，這篇補上了 `Best Practices For Claude Code` 之後更細的一層：前者強調 context hygiene、verifier-first prompting、thin `CLAUDE.md`、hooks / skills / subagents 的分工；本文則回答「skills 本身應該怎麼設計」。它讓 `skill` 不再只是「把流程寫下來」，而是要同時考慮 routing description、folder structure、gotchas、scripts、setup、memory、distribution、composition 與 measurement。

## Relation To Existing Concepts

- [Externalized Agent State](../concepts/externalized-agent-state.md): skills 是程序記憶的一種外部化狀態；若它們會改變未來 agent 行為，就需要 provenance、ownership、review、rollback 與 usage evidence。
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md): Claude Code skills、hooks、plugins、MCP、scripts、CLI tools 與 permissions 組成不同 runtime extension surfaces；其中 skills 承接可重用 procedure 與 progressive disclosure。
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md): verification skills、runbooks、CI/CD skills 與 infra operation skills 都是在把長任務的驗證、調查、部署與維運步驟固定成 harness primitive。
- [Prompt Migration And Agent Steerability](../concepts/prompt-migration-and-agent-steerability.md): 文章把 steerability 從「寫更長 prompt」移到「把任務判準、gotchas、setup 與驗證程序放進正確的 skill surface」。
- [Agent Evaluations](../concepts/agent-evaluations.md): skill usage logging、verification skills 與 skill improvement feedback loop 都讓 procedural memory 可以被觀測與評估，而不是憑感覺維護。
- [Codex Workflows](../maps/codex-workflows.md): 對 Codex 類工作流，這篇可轉譯成 companion skill 設計原則：不要只寫操作說明，要把 command order、output discipline、approval gates、gotchas 與 verification evidence 固定下來。
- Related prior sources: [Best Practices For Claude Code](best-practices-for-claude-code.md), [Shell + Skills + Compaction](shell-skills-compaction-long-running-agents.md), [Hermes Agent Masterclass](hermes-agent-masterclass.md), [Bespoke CLIs for Codex](bespoke-clis-for-codex.md)

## Tensions Or Disagreements

- 文章鼓勵把高頻流程做成 skills，但也承認太靈活會造成選擇困難。真正的治理難題是分類、命名、description、owner 與 promotion policy，而不是把所有 workflow 都快速寫成 skill。
- Verification skills 的 impact 最高，但成本也最高。文章提到工程師花一週把 verification skills 做好可能值得；這隱含的判準是該 flow 足夠高頻、失敗成本足夠高、而且能被程式化驗證。
- Skill memory 很有用，但若只把先前結果寫進 log 或 config，沒有版本控制、更新規則與過期清理，會把舊判斷固化成未來行為。
- On-demand hooks 很適合只在特定 skill 啟用強約束，但也會讓 skill 從「提供建議」變成「改變 runtime policy」。這類 skill 應該比一般 reference skill 有更嚴格 review。
- Marketplace 能降低分享摩擦，但也會增加 context catalog 噪音。若 description 不準、scope 太寬或缺少 usage signal，skill 變多反而會讓 agent routing 更差。

## Open Questions

- 一個 team skill catalog 的 promotion gate 應該是使用次數、失敗案例修正數、verification coverage，還是 owner 明確承諾維護？
- 哪些 workflows 應該做成 full skill folder，哪些只需要 repo docs、task template、CLI help 或 MCP tool reference？
- Verification skill 的最小 evidence bundle 應包含什麼：programmatic assertion、screenshot、video、transcript、database state，還是依 workflow 風險分級？
- Skill description 的品質要如何測量：觸發率、誤觸發率、成功率，還是 reviewer 對 execution transcript 的判斷？
- 當 skills 可以依賴其他 skills 時，catalog 是否需要 dependency graph、版本相容性與 cycle detection？

## Merge Candidates

- Skills 是 procedural memory，不是 Markdown prompt snippets；它們可以包含 scripts、assets、data、config、hooks、reference snippets 與 logs。
- Skill descriptions are routing contracts: they should tell the model when to use the skill, what it does, and what evidence/output it should produce.
- High-signal skills encode gotchas, internal constraints, setup, examples, and verification routines rather than restating generic coding ability.
- Verification skills deserve priority when a workflow is high-frequency or high-risk because they let agents collect product evidence instead of only producing changes.
- Progressive disclosure is a skill-design principle: keep the entry file thin, point to deeper references, and let the agent load details only when needed.
- Team skill catalogs need governance: owner, category, promotion path, usage measurement, review policy, rollback, and deprecation are part of the runtime surface.
