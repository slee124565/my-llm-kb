# Vibe Coding is a Ticking Time Bomb

## Source

- URL: https://x.com/akshay_pachaar/status/2067646389291725258
- Author: Akshay Pachaar (@akshay_pachaar)
- Published: 2026-06-18
- Captured: 2026-06-24T17:10:01+08:00
- Raw file: `raw/sources/2026/2026-06-18-vibe-coding-runtime-safety-boundary.md`
- Source note: X.com long-form post / article about coding-agent generated internal tools, production writes, and runtime-level safety boundaries.

## Main Claims

- 這篇的核心主張是：coding agent 寫出的程式碼本身通常不是最弱的一環，真正危險的是它繼承了什麼權限、跑在哪個 runtime、哪些 write action 沒有 gate、誰能呼叫，以及事後是否可追溯。模型可以把 UI 和資料層做對，但它不會自動知道 production 的身份、授權、稽核與 blast radius。
- 作者用一個 support console demo 說明這個問題：agent 依照 prompt 做出 `Issue Credit` 按鈕，點下去就更新 balance。從功能正確性看它成功了；從營運安全看，這是一個沒有角色檢查、沒有 approval、沒有 audit log 的 production write path。
- 「把安全要求寫進 prompt」不是可靠的 enforcement。Prompt 裡的警告和 instruction 仍然和一般需求同處模型 context，屬於 guidance；真正的 boundary 應該落在 runtime 或平台層，讓 code 即使沒有主動實作安全邏輯，也不能繞過 identity、permission、approval 與 logging。
- 文章把 read 和 write 的風險分開：未授權 read 會洩漏資料，未授權 write 會改變 business state。對 billing、credit、CRM、客服、供應商、財務等內部工具來說，write action 的治理應該比 UI polish、component quality 或 mock data 更早被放進 production contract。
- Retool case 的重點不只是 vendor demo，而是 runtime-boundary pattern：同一個 React app 匯入 governed runtime 後，資料呼叫改走 resource layer，SSO resolve 使用者身份，permission group 決定角色權限，mutating query 觸發 approval gate，每次執行進 audit log。控制面不在 agent 寫出的 app code，而在 app 被部署與執行的環境。
- 對工程組織的含義是：當 vibe coding 讓更多人能產生 internal app，工程責任會從「幫每個 app 手寫安全邏輯」上移到「提供預設安全的 production runtime」。否則 shadow AI 不是多了一堆聊天工具，而是一堆帶著資料庫權限、規則各異、無集中治理的內部 app。

## Why It Matters

這篇值得放進 `my-llm-kb`，因為它把 repo 裡幾條線收斂成非常具體的 production failure mode：coding agent 可以把功能做出來，但它不會自然補上 runtime boundary。這和 `Hidden Technical Debt in Agentic Systems` 的 guardrails framing、`Human-Supervised Agent Ops` 的 approval / audit / rollback framing，以及 `Agent Runtime Surfaces` 的 runtime ownership framing 都直接相連。

它也把「vibe coding」從單純生產力問題改成 governance 問題。當內部工具、客服 console、CRM 操作台、billing panel 變得可以快速生成，組織最需要的不是要求每個 prompt 都寫得更完整，而是讓所有 production writes 都自動經過共同的 identity、permission、approval、audit 與 rollback surface。

對 AI systems engineering 來說，這是一個清楚的檢查句：如果 agent-built app 能直接碰真實資料，production readiness 不能只問「功能是否能跑」，還要問「這個 write path 被哪個 runtime enforcement 包住」。

## Relation To Existing Concepts

- [AI Systems Engineering](../concepts/ai-systems-engineering.md): 本文把 AI systems engineering 的責任面落到 internal tools 與 business writes：identity、permissions、approval、audit log 與 scoped credentials 是 decision/action-producing system 的一部分，不是 app code 的 optional enhancement。
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md): Retool resource layer 是一種 governed runtime surface。它讓同一個 agent-built app 在 production 執行時繼承平台邊界，而不是把所有 safety contract 留給 generated React code。
- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md): mutating query 的 approval gate 把人類放回 supervisor role：人不是手動操作所有欄位，而是在高風險 write 前提供可審計的授權。
- [Externalized Agent State](../concepts/externalized-agent-state.md): audit log、approver、caller identity、permission decision 與 resource-level execution record 都是外部化狀態，讓事後 review 和責任歸屬成為可能。
- [Hidden Technical Debt in Agentic Systems](hidden-technical-debt-in-agentic-systems.md): 兩篇共同說明：guardrails 不應只存在 system prompt；irreversible actions 需要 code/runtime-level enforcement 與 human approval path。
- [Collapse Your CRM Pipeline Into One Table](collapse-your-crm-pipeline-into-one-table.md): 兩篇都討論 internal/business workflow runtime，但角度不同。Sim table 強調 row-scoped workflow surface；Retool case 強調 agent-built app 匯入 production runtime 後的 identity / permission / audit boundary。

## Tensions Or Disagreements

- 文章是 Retool partnership framing，因此不應把它當成對 Retool 特定產品能力的獨立評測；更穩定的知識增量是 runtime-boundary pattern，而不是 vendor claim。
- 把安全放到平台層可以降低 app-by-app governance sprawl，但也會讓平台本身成為高權限集中點。平台需要自己的 permission model、resource isolation、audit export、change review 與 rollback，而不是只因為「集中」就自動更安全。
- Agent-built app 匯入 governed runtime 可以補上 production boundary，但不能取代 domain modeling。哪些 action 算 write、哪些 row/column 需遮罩、哪些操作可自動通過、哪些需要二次 approval，仍需要 domain owner 和工程 owner 定義。
- Prompt 裡明確要求 authorization 仍然有價值，因為它能改善 prototype 結構與測試意識；只是它不能被當成唯一 enforcement。比較好的分層是：prompt 產生可接入 runtime 的 clean data seam，runtime 強制身份、權限、approval 與 audit。

## Open Questions

- Agent-generated internal app 進 production 前，最低限度的 runtime checklist 應包含哪些項目：SSO、RBAC、row/column permissions、approval gates、audit logs、resource-scoped credentials、preview mode、rollback path？
- 對不同 write action，approval gate 應如何分級：金額、資料類型、客戶等級、可逆性、操作者角色、異常模式、頻率上限？
- 企業應如何避免「平台治理集中」變成新的 lock-in 或單點風險，同時又避免每個 app 自行實作權限造成 shadow AI sprawl？
- Coding agent 應被 prompt 成產出更乾淨的 `src/api.js` / data seam，還是應直接透過平台 MCP / resource schema 生成 app？兩種方法對 portability、safety 與 review 的 tradeoff 是什麼？
- Audit log 應該保存到什麼粒度才足以 review agent-built apps：caller identity、input diff、query text、resource decision、approval reason、before/after state、linked ticket？

## Merge Candidates

- Agent-built internal tools should be evaluated by runtime enforcement, not only by generated code quality: identity, permissions, approval gates, audit logs, resource-scoped credentials, and rollback path.
- Prompt instructions are guidance; production boundaries must be enforced by the runtime or platform that executes the app.
- Vibe coding shifts engineering responsibility upward: teams need default-safe production runtimes for generated apps, especially when generated UI can perform irreversible business writes.
- A clean data-access seam such as `src/api.js` is useful because it lets a governed runtime intercept resources later, but the seam itself is not a safety boundary.
- Shadow AI risk should include agent-generated internal apps with real data access, not only unsanctioned chatbot use.
