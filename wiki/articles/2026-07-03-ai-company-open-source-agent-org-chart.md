# How to Build Your Own AI Company (0 employees, 100% open-source)

## Source

- URL: https://x.com/akshay_pachaar/status/2073050056299835736
- Author: Akshay @akshay_pachaar
- Published: 2026-07-03
- Captured: 2026-07-04T19:04:10+08:00
- Raw file: `raw/sources/2026/2026-07-03-ai-company-open-source-agent-org-chart.md`
- Source note: X.com long-form post / article about Alook, a self-hosted open-source platform that gives local coding agents roles, inboxes, reporting lines, and persistent runtime sessions.

## Main Claims

- 這篇把「一人公司」的想像具體化成一個 agent 組織架構（agent org chart）：不是讓一個聊天機器人一次處理所有事情，而是把 CEO、PM、工程、Ops 這類角色拆成多個 coding agent，讓它們透過 inbox 與 reporting line 協調。直覺意思是：agent coordination 不應只靠一條長 prompt，而需要接近組織設計的溝通拓樸。
- Alook 的核心 runtime surface 是本機常駐 daemon、local dashboard、Claude Code / OpenCode session、每個 agent 的 `@alook.ai` inbox，以及一套可視化 org chart。這讓 agent 不只是被呼叫的工具，而是有角色、通訊管道、執行環境與可追溯對話紀錄的工作單位。
- 文章的 walkthrough 用競品價格追蹤作為例子：人類只把任務交給 Atlas CEO，Atlas 轉給 Mara PM，Mara 寫 spec 並分派給 Theo 工程 agent 與 Ren Ops agent，最後形成 scraper、排程、變更偵測與通知。這個案例的知識增量不是 scraper 本身，而是「多 agent 工作流如何用角色邊界和 inbox 避免混亂群聊」。
- inbox 被描述為 coordination layer，而不是單純通知功能。Agent 之間用 email 交接 brief、spec、acknowledgement、完成回報與 escalation，讓人類可以回看決策是怎麼形成的。這和 repo 裡一直追蹤的 externalized state、audit log、progress artifact 是同一條線。
- 文章也把工具權限放進角色設計：Theo 需要 scrape competitor site，所以被授予 Bright Data CLI；Ren 負責監看輸出並通知人。這提醒 agent org chart 不能只有角色名稱，還要把工具權限、資料接觸面、可逆性與升級路徑一起設計。
- 作者引用 Dario Amodei 對一人十億美元公司的預測，以及 Medvi revenue 例子來強化敘事；這些應視為來源中的 framing 和未驗證案例，不應直接升級成 KB 的事實主張。比較穩定的可保留觀察是：新一代 agent tool 正在把「公司流程」重構成可由 agent 擁有的 operational loop。

## Why It Matters

這篇值得收進 `my-llm-kb`，因為它把幾個既有概念接在一起：long-running harness、human-supervised agent ops、runtime surface、externalized state，以及 AI-native startup operating system。它不是單純介紹 Alook，而是給出一個可討論的 pattern：用 org chart、inbox、local runtime、角色權限與可追溯 thread，將多個 coding agent 組成一個小型 operation。

對實務設計的啟發是：多 agent 不是「把更多 agent 丟進同一個 chat」。一旦 agent 真的要擁有持續運行的流程，就需要明確的 reporting line、router role、工具邊界、排程、監看責任與人類 supervisor surface。否則 autonomy 增加後，最先壞掉的不是模型能力，而是協調成本、責任歸屬與 reviewability。

這也補強了 AI-native application 的判準：人類不再逐步操作價格頁、手動整理 spreadsheet、每天重跑檢查，而是把一段 operational loop 交給 agent 組織，自己保留 brief、review、授權與例外處理。這是從 assistant/copilot 往 workflow / multi-agent / orchestrator adoption level 前進的具體例子。

## Relation To Existing Concepts

- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md): Alook 展示的是一種 org-chart harness：角色、inbox、reporting line、local coding sessions、calendar schedule 和 audit trail 共同承擔長任務協調，而不是只靠單一 agent session context。
- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md): 人類把 pricing tracker brief 交給 Atlas，agent 組織負責拆解、執行、排程、監看與通知；人類角色轉成 supervisor 和 policy owner，而不是每日手動 operator。
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md): 這篇提供一個 local personal / repo-local 混合 runtime surface：Claude Code 或 OpenCode session 仍在使用者機器上跑，但 Alook 在其上加了 org chart、inbox、dashboard 與持久 agent identity。
- [Externalized Agent State](../concepts/externalized-agent-state.md): email thread、spec、acknowledgement、dashboard 狀態、calendar schedule 與 scraper result 都是外部化狀態，讓人類與下一個 agent 能回看協調過程。
- [Agent Evaluations](../concepts/agent-evaluations.md): 這類多 agent workflow 不應只用「是否有 demo」判斷，而應評估 task handoff 是否正確、router 是否避免錯誤分派、排程是否可靠、通知是否有足夠 evidence、以及重跑時是否穩定。
- [The Eight Levels of AI Adoption](every-the-eight-levels-of-ai-adoption.md): Alook case 落在 workflow / multi-agent / orchestrator 之間；它把多個角色與持久流程接起來，但是否能成為真正 orchestrator，取決於 governance、rollback、eval 與 production boundaries 是否跟上。

## Tensions Or Disagreements

- 文章的語氣偏產品宣傳與 walkthrough，不應把 Alook 或 Bright Data 的能力描述視為獨立驗證結果。尤其 Medvi revenue、一人十億美元公司機率等敘事性 claim，需要 primary source 或外部資料確認後才能升級成 stable concept。
- 用 email 當 agent 協調層有強可讀性與低門檻，但也可能引入 latency、thread sprawl、重複通知與權限治理問題。對高頻或高風險 workflow，email thread 可能需要被更結構化的 state machine、queue 或 event log 補強。
- org chart 可以降低群聊混亂，但也可能把公司政治與 handoff overhead 搬進 agent 系統。角色分離只有在任務真的需要不同 authority、tool access、review surface 或 context boundary 時才有價值；小任務過度拆成多 agent 反而會增加 failure points。
- Agent 自行 provision scraper、設定排程與監看 competitor data，已經接近 live automation。若用在真實 business workflow，應補上 credential scoping、rate limit、terms / compliance review、failure alert、duplicate notification control 與 kill switch。

## Open Questions

- 什麼時候該把一個 workflow 拆成 org chart 多 agent，而不是保留成單一 agent 加 checklist？
- router / PM agent 的可靠性應如何驗證：看 spec 品質、handoff accuracy、blocked escalation，還是 downstream task outcome？
- Agent inbox 應該保存哪些 metadata 才足以 audit：brief version、sender role、receiver role、tool authority、decision reason、linked artifact、approval state、completion evidence？
- Calendar schedule 和 recurring agent work 應如何治理，才不會變成無人負責的 background automation？
- 對競品 scraping 這類外部網站操作，agent runtime 應暴露哪些 compliance、credential、rate-limit 與 kill-switch surface？

## Merge Candidates

- 多 agent workflow 的第一個設計問題不是「要幾個 agent」，而是 coordination topology：誰能直接跟誰說話、誰負責 routing、哪些工具權限跟著角色走、哪些 evidence 必須回報給人。
- Agent org chart 可以視為 long-running harness 的一種型態：角色、inbox、reporting line、persistent sessions、schedule、dashboard 與 audit trail 共同維持跨任務連續性。
- Inbox/email thread 是一種 externalized agent state；它讓決策與交接可回看，但高風險流程仍需要結構化 state machine、approval gate 與 rollback。
- AI-native startup / operation 的核心不是把 AI 放進所有 UI，而是把可重複 operational loop 交給 agent 擁有，同時把 human role 升級成 brief、policy、review、exception handling 與 governance。
- 多 agent autonomy 應由 output value per coordination cost 評估；如果角色分離只增加 handoff、latency 與 debug surface，就不該因為 demo 看起來更 autonomous 而採用。
