# Best Practices For Claude Code

## Source

- URL: https://code.claude.com/docs/en/best-practices
- Author: Anthropic / Claude Code Docs
- Published: not exposed on the captured page metadata
- Captured: 2026-04-14 (inferred from workspace source path)
- Raw file: `raw/sources/2026/2026-04-14-best-practices-for-claude-code.md`
- Workspace provenance: copied from `my-blog-kb/raw/sources/2026/2026-04-14-best-practices-for-claude-code/2026-04-14-best-practices-for-claude-code.md`
- Source note: this is a point-in-time capture of a living Claude Code documentation page.

## Main Claims

- Claude Code 的首要約束是上下文視窗（context window）會快速填滿，而且越接近上限越容易讓模型遺漏早先指令或累積錯誤。有效使用 coding agent，不只是把需求丟出去，而是管理它讀進去的檔案、命令輸出、對話歷史與驗證證據。
- 最高槓桿的提示不是「請寫得更好」，而是先給 Claude 可自我驗證的成功條件：測試案例、預期輸出、截圖比對、lint / build command，或明確的 root-cause 修復標準。這會把人類從唯一 feedback loop 變成驗收者。
- `Explore -> Plan -> Implement -> Commit` 是適合中大型、不確定或跨檔變更的工作法；小修小補則不該被過度流程化。真正的判準不是「永遠先 plan」，而是 scope、風險與不確定性是否高到需要先分離研究與實作。
- 好的任務提示要指定檔案、症狀、限制、現有 pattern、測試偏好與完成定義。這不是 micromanagement，而是讓 agent 的探索空間對齊 codebase 與團隊慣例，減少錯誤路徑。
- `CLAUDE.md` 應該短而可維護，只放 Claude 無法從 code 自己推斷、且跨 session 都適用的規則。更窄的 domain knowledge、工作法與工具流程，應下沉到 skills、hooks、subagents、MCP 或 repo-local docs，避免入口檔變成 instruction blob。
- 權限 allowlist、auto mode、sandbox、CLI tools、MCP servers、hooks、skills、subagents 與 plugins 是不同層級的控制面。它們分別處理安全邊界、外部工具觸達、零例外自動化、可重用知識與隔離式調查，不應全部用自然語言 prompt 承擔。
- Claude Code 的互動管理是一種 supervisor loop：及早 course-correct、在同一問題被修正多次後清 context、用 subagents 做重研究或 review、用 rewind/checkpoint 恢復錯誤路徑，都是讓人類保留方向控制與品質責任的方法。
- 多 session、non-interactive mode、fan-out 與 writer/reviewer pattern 可以放大 throughput，但前提是每個 session 有清楚任務邊界、隔離工作區與 review evidence。並行本身不是品質保證，真正有用的是 fresh-context review 和可比較的驗證結果。

## Why It Matters

這篇是 Claude Code 操作手冊，但對 `my-llm-kb` 的價值不是功能介紹，而是把「coding agent 好不好用」拆成一組可治理的工作面：上下文預算、任務契約、驗證、持久規則、權限、工具、隔離調查、session 管理與並行 review。

它和 repo 內既有 Codex workflow 內容形成互補。Codex 相關文章多強調 repo-local system of record、async delegation、Goals、side panel、sandbox 與 prompt contract；這篇則從 Claude Code 的使用者工作法出發，說明同一組原則如何落在 terminal coding agent：不要把所有知識塞進主對話、不要用長入口檔代替可維護 artifact、不要讓人類成為唯一 verifier、不要把 plan mode 變成所有任務的固定儀式。

## Relation To Existing Concepts

- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md): context management、verification、Plan Mode、subagents、parallel sessions 與 clean review boundaries 都是長任務 harness 的使用者層 primitive。
- [Externalized Agent State](../concepts/externalized-agent-state.md): `CLAUDE.md`、skills、hooks、subagents、spec files 與 compact instructions 都是在把可重用狀態搬出單次 conversation。
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md): 入口 instruction file 應保持薄， deeper workflow 和 domain knowledge 應由 repo docs、skills、templates 或 tool docs 承接。
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md): Claude Code 的 runtime surface 包含 terminal、filesystem、Bash、browser extension、permissions、sandbox、CLI tools、MCP、hooks、skills、subagents 與 plugin system。
- [Prompt Migration And Agent Steerability](../concepts/prompt-migration-and-agent-steerability.md): 文章把提示設計從抽象 prompt tips 拉回 outcome、constraints、examples、verification 與 task-scope selection。
- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md): course correction、rewind、review sessions 與 verifier-first prompting，把人類角色放在 supervisor / evidence reviewer，而不是逐步 operator。
- [Codex Workflows](../maps/codex-workflows.md): 這篇可作為 Codex workflow 的比較入口，用來區分 product-specific control surface 和跨 coding agent 通用工作法。

## Tensions Or Disagreements

- 文章強調 Claude Code 的 context window 管理，但它的建議預設使用者願意主動維護 session hygiene；在團隊流程中，這些做法還需要落成 repo docs、hooks、CI、PR policy 或 task template，才不會只靠個人習慣。
- `Plan Mode` 很適合不確定任務，但若被無差別套用，會讓小任務變慢，也可能累積過厚的 plan artifact。這和本 repo 的 long-running harness framing 一致：plan 是風險治理工具，不是每個任務的宗教儀式。
- `CLAUDE.md` 應保持短，但團隊往往會把每次事故後的規則直接塞進入口檔。真正困難的是分流：哪些是 hard invariant，哪些應該成為 test、hook、skill、doc、template 或 checklist。
- Parallel sessions 可以提高吞吐，也能提供 fresh-context review；但如果缺少工作區隔離、測試標準與 merge discipline，就會把 review bottleneck 和衝突成本推給人類。
- Hooks 是零例外控制面，比 instruction 更可靠；但也因此需要更高的變更審查，否則錯誤 hook 會把局部偏好變成所有 session 的硬性副作用。

## Open Questions

- Claude Code / Codex 這類 repo-local coding agent 的入口檔，應如何共同演化出「薄入口、厚 docs、可驗證 hooks / tests」的標準分層？
- 哪些常見 prompt rules 應該被刪掉，改由 tests、hooks、skills、MCP tool docs 或 task templates 承擔？
- Parallel coding agent sessions 的最小 review packet 應包含哪些內容，才能讓 fresh-context review 真正降低風險？
- 對 non-code knowledge work 而言，哪些 Claude Code session hygiene 原則可遷移，哪些高度依賴 codebase / tests / git checkpoint？

## Merge Candidates

- context window 是 coding agent 的核心工作資源；使用者應管理讀取範圍、命令輸出、對話歷史與 compaction policy，而不是只管理 prompt wording。
- verifier-first prompting 是 coding agent collaboration 的最高槓桿：tests、screenshots、expected outputs、lint/build command 與 root-cause standard 應放進 task contract。
- `Explore -> Plan -> Implement -> Commit` 應按任務不確定性和風險使用；小而清楚的變更可以直接執行。
- 入口 instruction file 應保持短，domain workflows 應下沉到 repo docs、skills、hooks、subagents、MCP 或 task-specific specs。
- hooks、skills、subagents、MCP、CLI tools、permissions 與 sandbox 是不同 runtime control surfaces，不應全靠一個 prompt 或入口檔承擔。
- 多 session fan-out 應以 isolated worktree、fresh-context review、writer/reviewer split 與驗證證據為基礎，否則只是把人類 review bottleneck 放大。
