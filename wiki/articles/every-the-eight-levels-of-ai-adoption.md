# The Eight Levels of AI Adoption

## Source

- URL: https://every.to/guides/the-eight-levels-of-ai-adoption
- Author: Mike Taylor, Laura Entis, Claude / Every
- Publisher: Every Guides
- Published: 2026-06-02
- Captured: 2026-06-13
- Raw file: `raw/sources/2026/2026-06-02-every-the-eight-levels-of-ai-adoption.md`

## Main Claims

- AI adoption 不應被理解成「誰用得最炫」的競賽，而是任務、風險、信任與成本之間的匹配。越高的 level 代表你把更多工作、判斷時機與操作權交給 AI，但也代表你需要更強的驗證、scaffolding 與失敗處理。
- 八個 level 從 `Chatbot`、`Copilot`、`Agent`、`Autopilot`、`Workflows`、`Assistant`、`Multi-agent` 到 `Orchestrator`，本質上是在描述 delegation boundary 的上移：從單次回答，到嵌入文件，再到多步執行、免逐步批准、可重複 workflow、背景主動工作、多 agent 並行，以及由 manager agent 代管協調。
- 高 level 不必然比較好。作者反覆強調，成熟使用者會同時在多個 level 工作，依照任務 stakes、模型能力、輸出品質、人工 review 成本與可接受失敗範圍，選擇當下最合適的 autonomy level。
- 從 Level 1 到 Level 4，主要增量是減少 context setup 與手動操作：Chatbot 需要人貼資料、Copilot 進入工作檔案、Agent 可跨多來源執行並請求批准、Autopilot 則讓 agent 先完成整件事再由人 review。
- Level 5 `Workflows` 是關鍵分水嶺：使用者不再只把任務丟給 agent，而是建立能 professionalize output 的流程，例如 plan、review、confidence check、test、guardrail、CI、repo rule 與 verification loop。這也是從 vibe coding 走向 agentic engineering 的門檻。
- Level 6 到 Level 8 的共同難點不是「多跑幾個 agent」，而是長時間持續性、記憶、權責分工、進度觀測、升級門檻與品質治理。always-on assistant、multi-agent 與 orchestrator 都需要明確的 scope、roles、review thresholds 與人類 judgment loop。
- 角色差異很重要。作者判斷多數 knowledge worker 目前的 sweet spot 大約在 Level 1 到 Level 4；工程師較常能進入 Level 5 到 Level 8，因為他們能建出讓不穩定系統可用的 scaffolding。
- 最後的 takeaway 是：不要在尚未訓練與校準前，把 agent 當成完全可信的 autonomous worker。就像不能吹噓自己讓八個 intern 通宵做關鍵專案卻不檢查結果，agent autonomy 也需要逐步建立信任與審核制度。

## Why It Matters

這篇文章把 AI 導入從「工具清單」整理成一套 delegation maturity model。它對本 repo 的增量不在八個名字本身，而在它把 adoption level 和 trust boundary、approval gate、review cost、harness maturity 綁在一起：每往上一層，人的角色都更像 supervisor、framer 或 orchestrator，而不是逐步 operator。

這也補強 `After Automation` 的 framing。`After Automation` 說 automation 讓 framed competence 變便宜，人的稀缺角色轉向 framing、taste、review 與 system design；本篇則提供一張可操作的階梯，說明什麼時候仍該停在低 autonomy，什麼時候需要投資 workflows / harnesses，什麼時候多 agent 或 orchestrator 仍然只是 frontier experiment。

對組織導入 AI 來說，這篇最有用的地方是降低焦慮：不是每個人都應該追 Level 8。更務實的問題是：這個任務若交給 AI，錯了有多嚴重？我願意投入多少 setup、review、token、工程與維護成本來換取更少介入？如果答案不清楚，留在較低 level 反而是成熟選擇。

## Relation To Existing Concepts

- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md)：八個 level 可讀成 operational-loop ownership 逐步從人轉移到 agent 的 adoption ladder；每一層都需要對應的 supervision surface。
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)：Level 5 以後的重點是 harness，而不是單次 prompt；workflows、assistant、multi-agent、orchestrator 都需要 state、verification、roles、approval 與 recovery contract。
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)：每一層都有不同 runtime surface，從 chat tab、文件內 copilot、repo/local agent、managed workflow，到 always-on assistant 與 orchestrator control plane。
- [LLM Agents](../maps/llm-agents.md)：本篇提供一個高層入口，幫讀者把 agent adoption 放進信任、風險、成本與工程 scaffolding 的座標系。
- [Long-Running Agents](../maps/long-running-agents.md)：Level 6 到 Level 8 直接對應 long-running / multi-agent / orchestrator 的治理問題。

## Tensions Or Disagreements

- 八層模型很適合做導入對話，但它可能把不同維度壓成單一 ladder：runtime surface、permission model、proactivity、multi-agent concurrency、workflow maturity 與 orchestration 其實可以分開演進。
- 作者把 Level 5 以上主要放在工程師領域，這在 2026 年中很合理，但隨著 provider-managed workflows 和 managed agents 成熟，部分 scaffolding 可能會產品化，讓非工程團隊也能使用較高 autonomy 的受管版本。
- `Autopilot` 和 `Workflows` 的邊界不只取決於人是否逐步批准，也取決於輸出的 stakes。低風險原型可以 autopilot，高風險內部流程即使技術上可 one-shot，也仍然需要 workflow gate。
- `Orchestrator` 被放在最高層，但目前仍高度實驗。對許多真實團隊來說，人類自己擔任 orchestrator，加上多個受限 agent worker，可能比 manager agent 更可靠。

## Open Questions

- 對每一個 adoption level，最小可接受的 evidence packet 應該包含什麼：source、reasoning summary、test result、diff、screenshot、audit log、approval record，還是 rollback plan？
- 組織應如何把「任務 stakes」轉成 autonomy policy，而不是讓每個人憑感覺決定何時跳到更高 level？
- Level 5 workflows 若由平台產品化，哪些 guardrails 應該由平台內建，哪些仍必須由 repo、team policy 或 domain owner 持有？
- Multi-agent 和 orchestrator 的可靠性應如何衡量：完成速度、輸出品質、agent-hour 效率、升級精準度、還是 human supervisor 的認知負擔？
- 什麼類型的 non-engineering work 最適合先從 Level 4 升到 Level 5，而不需要完整工程團隊介入？

## Merge Candidates

- AI adoption level 應被視為 delegation boundary / trust boundary，而不是單純功能成熟度
- 高 autonomy 需要對應的 evidence、approval、review、rollback 與 maintenance scaffolding
- Level 5 workflows 是從 one-shot agent use 轉向 agentic engineering 的分水嶺
- knowledge worker 的近期 sweet spot 常在 Level 1-4；engineer 能進 Level 5-8 是因為可建 harness，而不是因為 agent 本身突然可靠
- multi-agent / orchestrator adoption 需要 role isolation、progress observability、review thresholds 與 escalation policy
- 合理的 AI 導入不是追最高 level，而是依 task stakes、failure cost、trust calibration 與 setup / review economics 選擇 level
