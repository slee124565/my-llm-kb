# A single CLAUDE.md file just hit 192k GitHub stars

## Source

- URL: https://x.com/i/status/2077032502993256646
- Author: Akshay @akshay_pachaar
- Published: 2026-07-14
- Captured: 2026-07-15T07:38:09+08:00
- Raw file: `raw/sources/2026/2026-07-14-claude-md-behavioral-guidelines.md`
- Source note: X.com post about a Karpathy-derived `CLAUDE.md` rule file, predictable coding-agent mistakes, and the shift from using AI to write code toward engineering coding-agent behavior. The source includes only a preview of the quoted March 21 `Anatomy of the .claude/ folder` article, not the full quoted article.

## Main Claims

- 這篇的核心觀察是：coding agent 常見錯誤不是隨機的。過度工程化（over-engineering）、忽略既有 pattern、擅自加入依賴，這些都是跨 session 會重複出現的行為偏差；如果錯誤可預測，就可以被寫成 repo-local 指令、測試、hook 或 skill 來預防。
- `CLAUDE.md` 在這裡不是一般 README，而是專門面向 coding agent 的行為契約（behavior contract）。它把「請照我這個專案的工作方式做」從每次聊天重講，移到專案根目錄的持久 artifact，讓 agent 每次進 repo 都能重新載入相同邊界。
- 文章把一個低技術含量的 `.md` 檔案視為高槓桿工具，重點不在框架或工具複雜度，而在 project-level instructions 是否抓到真正會造成品質問題的穩定錯誤。這呼應 repo 既有的薄入口、厚文件、可驗證控制面的分層。
- 更大的趨勢是從「用 AI 寫程式」移到「設計 AI 的工作方式」。也就是說，AI-assisted development 的品質不只取決於模型能力，也取決於團隊如何設計 instructions、permissions、hooks、skills、agents、tests 與 review evidence。
- 這篇只提供 X.com 層級的宣稱與文化訊號；`192k GitHub stars` 和「讀者很多」代表社群需求強，不代表該 `CLAUDE.md` 已被嚴格證明能改善 code quality。可保留的是 steering pattern，不是把 star count 當成品質證據。

## Why It Matters

這篇值得收進 `my-llm-kb`，因為它補上一個很小但清楚的 adoption signal：coding-agent workflow 的關鍵資產，有時不是新工具，而是把重複錯誤與團隊判準寫成 agent 會讀、會遵守、也能被版本控制的 project artifact。

對工程主管或產品負責人來說，這個觀點的實務含義是：不要只問「哪個 coding agent 比較強」，也要問「我們有沒有把常見錯誤、不可違反的設計邊界、驗證方式與權限規則放到 agent 每次都能看見的位置」。否則每個 session 都要靠人類即時糾正，團隊其實沒有累積 agent operation memory。

對 repo workflow 來說，這篇同時提醒另一個風險：入口指令檔很容易變成 instruction blob。真正好的 `CLAUDE.md` / `AGENTS.md` 不是把所有事故後的規則都塞進去，而是只保留跨 session 都重要、且 code 本身推不出的穩定不變項；更窄的 workflow 應下沉到 docs、skills、hooks、tests、templates 或 task prompts。

## Relation To Existing Concepts

- [Prompt Migration And Agent Steerability](../concepts/prompt-migration-and-agent-steerability.md): 本文把 steerability 從單次 prompt 擴展到 repo-local behavior contract；重點是把 predictable mistakes 變成持久、可審查、可刪減的 instruction surface。
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md): `CLAUDE.md` / `AGENTS.md` 是 repo system of record 的入口層；它應指向 deeper docs 與可驗證控制面，而不是承擔整個知識庫。
- [Externalized Agent State](../concepts/externalized-agent-state.md): project instruction file 是外部化狀態的一種，保存的是未來 agent session 應重新載入的行為偏好、規則與錯誤預防。
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md): `CLAUDE.md` 是 advisory instruction surface；hooks、permissions、skills、subagents、MCP、tests 與 sandbox 是更具執行力或隔離性的 runtime surfaces，不能全部由自然語言規則代替。
- [Best Practices For Claude Code](best-practices-for-claude-code.md): 這篇 X.com post 與該文章的共同點是「入口檔要薄而有效」；真正困難是把規則分流到正確層級。
- [Lessons From Building Claude Code: How We Use Skills](lessons-from-building-claude-code-how-we-use-skills.md): 當 instruction 從 broad invariant 變成 task-specific procedure、gotcha、setup 或 verification routine，就應考慮升級成 skill，而不是繼續塞進 `CLAUDE.md`。
- [Codex Workflows](../maps/codex-workflows.md): 對 Codex 也有直接可比性：`AGENTS.md`、skills、repo docs、task prompt、tool affordance 與 validation evidence 應分層設計，避免一個越寫越長的 global instruction blob。

## Tensions Or Disagreements

- X.com post 的語氣偏 promotional，且把 star count、讀者數和 workflow 品質放在同一個敘事裡。這些是 adoption signals，不是 efficacy evidence；若要升級成強 claim，仍需要比較輸出品質、review 缺陷、依賴新增率、測試通過率或 agent transcript。
- 「一個 markdown file 改變行為」很吸引人，但也很容易誤導。若規則過多、過細、過期或互相衝突，`CLAUDE.md` 會變成 context pollution，讓 agent 花更多 token 讀取低訊號規則，甚至覆蓋更貼近當前任務的 repo pattern。
- 可預測錯誤不一定都應該寫進 instruction file。若錯誤可以被 test、lint、typecheck、hook、permission gate 或 code owner review 穩定阻止，應優先用更可靠的控制面承擔，而不是只靠 advisory prompt。
- Karpathy-derived coding rules 可作為 general default，但每個 repo 的設計品味、依賴政策、framework pattern 和 release workflow 不同。通用規則進入專案前，仍需被 local contract 校準。

## Open Questions

- 哪些 coding-agent 錯誤值得升級為永久入口規則？判準應該是發生頻率、修復成本、風險高低，還是可否用測試 / hook 阻止？
- `CLAUDE.md` / `AGENTS.md` 的最小有效內容是什麼：專案邊界、禁止事項、驗證方式、常見陷阱、還是只保留 routing 到 deeper docs？
- 如何衡量 instruction file 是否真的改善 agent behavior，而不是只是增加 context 成本？
- 當一條規則從「常見提醒」變成「不能違反的 invariant」時，應該留在 prompt、移到 hook、寫成 test，還是做成 skill？
- 對跨工具團隊而言，`CLAUDE.md`、`AGENTS.md`、Cursor rules、Copilot instructions 與其他 coding-agent entry files 應該共享同一份 source of truth，還是各自維護？

## Merge Candidates

- 可預測的 coding-agent 錯誤應被當成 workflow design input：若同一錯誤跨 session 重複發生，應轉成 repo-local instruction、test、hook、skill 或 review checklist。
- Project instruction file 是 behavior contract，不是文件垃圾桶；只應保留跨 session 穩定、code 無法自行推斷、且能預防真實錯誤的規則。
- Star count 和社群流行度只能證明需求，不足以證明 instruction file 提升品質；高價值規則仍需 validation evidence 與定期 pruning。
- AI-assisted development 的成熟度會從「提示模型寫 code」走向「設計 agent 行為、權限、驗證與知識載入方式」。
- `CLAUDE.md` / `AGENTS.md`、skills、hooks、permissions、tests 與 docs 應分層：自然語言指令負責 steerability，runtime / CI / review 控制面負責不可違反的保證。
