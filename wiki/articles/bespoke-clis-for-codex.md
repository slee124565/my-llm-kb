# Bespoke CLIs for Codex

## Source

- URL: https://x.com/dotey/status/2042777337398210713
- Supporting article: https://developers.openai.com/codex/use-cases/agent-friendly-clis
- Author: 宝玉 @dotey, summarizing Nick Baumann's Codex workflow and the linked OpenAI Developers guide
- Published: 2026-04-12 inferred from workspace article date and capture context
- Captured: 2026-04-12
- Raw file: `raw/sources/2026/2026-04-12-bespoke-clis-for-codex.md`
- Supporting raw file: `raw/sources/2026/2026-04-12-openai-create-a-cli-codex-can-use.md`
- Imported from workspace path: `blog/2026-04-12-bespoke-clis-for-codex/2026-04-12-bespoke-clis-for-codex.md`

## Main Claims

- 當 Codex 反覆面對同一個 API、log source、export、local archive 或 team script 時，與其每次餵原始資料，不如先把常見操作編譯成可組合的 CLI
- MCP / connector 主要解決 access 問題，但 agent-friendly CLI 更直接解決 operability 問題，例如分頁搜尋、精準用 ID 讀取、輸出穩定 JSON、把大 payload 落成檔案
- 好的 CLI surface 應讓 Codex 能從任何資料夾執行、加 flag 縮小輸出、串接 `git`、`gh`、`rg` 與 repo scripts，而不是停在一次性 API 教學
- companion skill 和 CLI 應成對設計：CLI 提供可執行 command surface，skill 記錄哪些命令先跑、哪些 write action 需要 approval、哪些大輸出應存到哪裡
- `codex-threads`、`slack-cli`、`typefully-cli` 這三個例子共同說明：真正需要的不是「讓 agent 碰到更多原始資料」，而是「讓它用一套薄而穩定的工作面碰到正確資料」

## Why It Matters

這篇把 repo 裡原本較抽象的 `CLI-first operability` 進一步拉到可操作層。它不是在反對 MCP，而是在重新切分責任：connector 處理授權與接入，CLI 處理 agent 真正反覆需要的 search / read / download / draft / export 工作面。對 Codex workflow 來說，這意味著很多高頻外部操作其實值得被編譯成「CLI + companion skill」而不是每次重新 prompt。

## Relation To Existing Concepts

- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md)
- [Codex Workflows](../maps/codex-workflows.md)

## Tensions Or Disagreements

- 這個 framing 很強調 CLI 的薄抽象，但不代表 MCP / connector 不重要；若沒有既有 auth gateway 或 stable backend，CLI 可能只是把整合複雜度轉移到 shell glue
- CLI-first 很適合單一團隊或單一使用者的高頻工作面，但對跨團隊共享、強型別 schema、GUI-native interaction 而言，專門 protocol 仍可能更穩定
- 如果 CLI 預設輸出太大、write command 邊界不清楚、安裝方式不穩，反而會把 agent workflow 變得更脆弱，而不是更可操作

## Open Questions

- 什麼時候應該把 connector / MCP 再往上編譯成 CLI，而不是直接讓 agent 使用原始 integration
- CLI 的 output contract、download path 與 approval boundary，是否也應納入 repo-local knowledge artifacts 持續治理
- 「CLI + companion skill」是否會成為 Codex workflow 中比單純 API doc 更穩定的 reusable interface pattern

## Merge Candidates

- MCP / connector often solves access, while an agent-friendly CLI solves operability for repeated noisy data surfaces
- good agent-facing command surfaces should prefer exact reads by ID, narrow defaults, and file export for large payloads over giant inline blobs
- a reusable external workflow is often a pair: CLI for execution and companion skill for sequencing, output discipline, and approval boundaries

## Adoption Follow-Up

### Knowledge Delta

- 真正該優化的往往不是「讓 agent 接到更多資料」，而是把高噪音資料面編譯成更薄的 operability surface
- `connector / MCP` 和 `CLI` 不是互斥替代，而是兩層不同責任：前者處理 access，後者處理 repeated work 的 search / read / export / write discipline
- companion skill 的價值不是補充說明文件，而是把 command order、output discipline 與 approval boundary 固定下來
- 對成熟 routine 來說，真正穩定的分層常常是三層而不是兩層：底層 substrate CLI 解 access 與 raw API surface；task-native CLI 解 routine operability；companion skill / docs 解 mode、policy、guardrails 與 adoption

### Workflow Delta

- 當同一類外部資料面重複出現在工作流裡時，不應再把原始 docs、logs、exports 整包丟給 agent；應先判斷是否值得升級成 agent-friendly CLI
- 設計 CLI 時，應先定義 job 與 command surface，而不是先想實作用哪個 API 或哪種語言
- 對高噪音外部操作，後續應優先採用 `CLI + companion skill`，而不是只留下長 prompt 或散落的操作描述
- 針對已經存在通用底層 CLI 的 routine，不要急著替換底層工具；應先把底層 CLI 視為 substrate，再往上設計 task-native CLI surface，避免把 access layer 和 workflow layer 混在一起
- design 的重點不只是列 command，而是切清 responsibility split：哪些責任留在 substrate，哪些下沉到 task-native CLI，哪些保留給 companion skill / task docs

### Habit Delta

- 開始做：當某個資料面第三次讓你重複解釋同樣上下文時，主動問「這是不是該做成 CLI」
- 開始做：在設計 CLI 時，固定先列 `search/list`、`read by ID`、`export to file`、`write with approval` 這四類能力
- 開始做：若已經有底層通用 CLI，可先問「它缺的是 access 還是 operability」，不要本能地從零重做整個工具
- 開始做：在 routine task 中固定畫一張 responsibility split 表，至少拆成 `substrate`、`task-native CLI`、`companion skill/docs`
- 停止做：不要再把大型 API response、長 Slack thread、整份 log 直接當成預設輸入塞進 agent context
- 停止做：不要把「有 connector 能用」誤認為「workflow 已經足夠可操作」
- 停止做：不要讓 docs / prompts 長期承擔那些其實已經穩定到可以被 command surface 吸收的 operability 責任

### Next Adoption Experiment

- 下一次你遇到需要反覆查找同一資料面的任務時，刻意先不要補長篇解釋；先判斷它是否符合以下任一條件：
  - 需要分頁搜尋
  - 需要用 stable ID 精讀單筆資料
  - 需要把大 payload 落檔而不是 inline
  - 需要明確區分 safe read 與 gated write
- 若符合兩項以上，先做一輪 `CLI candidate review`，但不要直接跳到 implementation；先寫出：
  - 這個 routine 目前的 substrate 是什麼
  - 最小 task-native CLI surface 應包含哪些 commands
  - 哪些 mode / policy / approval boundary 應繼續留在 companion skill 或 task docs
- 若這份 split 在真實 routine 中仍然成立，再決定是否進 implementation

### Stop Doing

- 停止把 agent 反覆失焦，誤判為模型不夠強；先檢查是否其實是輸入 surface 太厚、太吵、太不穩定
- 停止用一次性 prompt 手工描述那些其實已經固定出現的 read / search / export 步驟
- 停止把所有 workflow friction 都歸因為底層工具不夠好；先檢查是不是 task-native surface 尚未被編譯出來

### Success Criteria

- 你在一次真實任務中，明確辨認出某個高噪音資料面值得做 CLI，而不是繼續用一次性 prompt 硬撐
- 你能先寫出一個最小 command surface，至少包含 discovery、exact read、large payload export 與 write boundary 中的三項
- 你能清楚說明某個 routine 中 `substrate`、`task-native CLI`、`companion skill/docs` 三層分別承擔什麼責任
- 該任務完成後，你能清楚描述舊做法和新做法的差異，而不是只覺得「好像比較順」

### Recommended Writeback Target

- 目前先留在 article level，作為單篇觸發的 adoption note
- 若後續 2 到 3 次真實任務都出現相同模式，下一步應回寫成 prompt / checklist 或 repo-local rule，而不只留在這篇 article card

### Issue Follow-Up Decision

- 值得建立 GitHub adoption issue
- 原因：
  - 這篇已經有具體且可短期嘗試的真實情境：下一次遇到 repeated noisy data surface 時，先做 `CLI candidate review`
  - success criteria 已足夠可檢查，不只是觀念提醒
  - 這個 adoption 的風險不在於「忘記理解」，而在於「理解了但沒有真的回到真實 routine 裡試」
- issue 應追蹤的最小內容：
  - source article：`Bespoke CLIs for Codex`
  - next adoption experiment：在真實 routine 中先做 `substrate vs task-native CLI vs companion skill/docs` split，再決定是否進 implementation
  - stop doing：不要再把 workflow friction 全部歸因為底層工具不夠好，也不要讓 docs / prompts 長期承擔已可被 command surface 吸收的 operability 責任
  - success criteria：能在一次真實任務中清楚畫出三層 responsibility split，並寫出最小 task-native command surface
