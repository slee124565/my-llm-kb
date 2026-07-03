# A Hands-On Guide to Agentic RL

## Source

- URL: https://theneuralmaze.substack.com/p/a-hands-on-guide-to-agentic-rl
- Author: Miguel Otero Pedrido
- Published: 2026-07-01
- Captured: 2026-07-03
- Raw file: `raw/sources/2026/2026-07-01-a-hands-on-guide-to-agentic-rl.md`
- Extraction: `myAgentTools/neural-maze-ase-journey-import`
- Import note: Substack marked the post as `only_paid`; importer required manual review with `--allow-paid-audience --force`. The captured markdown ends at the section heading `Run a real one: Wordle, off the Hub`, so this card compiles only the preserved raw source.

## Main Claims

- 文章用 Wordle failure 說明 agent 的核心問題不是「知道規則」，而是能不能在多步驟互動中持續利用回饋。模型前兩步已經知道答案包含某些字母，第三步卻丟掉已確認資訊，這類錯誤不是單句回答品質問題，而是跨回合行為習慣問題。
- Prompt、tools、memory 都是繞著模型外圍調整的槓桿。它們能改變輸入、可用能力與可召回 context，但不會直接改變模型權重（weights）裡已學到的行為傾向。強化學習（reinforcement learning, RL）被定位成少數能直接改變模型行為習慣的槓桿。
- Agent training 比 chatbot training 難，因為 agent 產生的是軌跡（trajectory），不是單一答案。分數常常只在整段執行結束後出現，真正犯錯的步驟卻可能藏在中間；這就是 credit assignment，會讓 agent RL 比單輪回答評分更難治理。
- Prime Intellect 的重要 framing 是：評估環境（eval environment）和 RL 訓練環境其實共用同一個結構，都需要 task dataset、agent harness、rubric。對 frozen model 使用同一組環境是在測量；對 learning model 把分數回寫到權重，就是在訓練。
- 可驗證獎勵（verifiable reward）是 agentic RL 目前最務實的核心。若任務可以用程式檢查結果，例如 Wordle 是否猜中、測試是否通過，就不必完全依賴模糊的人類偏好或 LLM judge。這也解釋了為什麼 games、math、coding 先成為可行訓練場。
- GRPO 的直覺是讓模型對同一任務嘗試多次，再用同批結果的相對表現當作尺。它不需要額外訓練一個 critic network，而是把高於平均的 trajectories 往上推、低於平均的往下壓。對工程團隊來說，重點不是公式，而是要能大量產生、記錄、評分與回放 attempts。
- `prime-rl` 的 asynchronous design 把 agentic RL 拉回 systems engineering：一組 workers 持續跑 inference 產生 games 或 trajectories，另一側 trainer 持續更新權重。真正困難的部分包含 sandbox、harness、provider abstraction、GPU utilization、任務分發與結果回寫。
- 作者強調 RL 應該是最後一層槓桿。只有當 prompting、tools、memory 已經沒有明顯改善空間，失敗又穩定出現在可驗證的 multi-step trajectory 上，且團隊有足夠 task distribution 與算力時，RL 才可能值得成本。
- Reward function 是整個 pipeline 裡最危險的程式碼。RL 不會最佳化「你心裡真正想要的結果」，只會最佳化被寫進 reward 的訊號；如果分數有漏洞，模型會把漏洞學成能力。

## Why It Matters

這篇把 `How to Fine-Tune LLMs in 2026` 裡較抽象的 GRPO / RFT 觀點，接到更直覺的 agent workflow：一段失敗 transcript 不只是 debug 材料，也可能是訓練資料。對這個 repo 來說，這強化了一個重要方向：agent eval artifacts 若保存得夠好，未來可能從 release gate 升級成 model-improvement substrate。

它也補上 AI Systems Engineer 的實務邊界。Agentic RL 聽起來像研究或訓練算法，但文章反覆指出可用性取決於 systems layer：環境能不能重播、rubric 能不能信任、worker 與 trainer 能不能有效協調、sandbox 能不能隔離 side effects、reward bug 能不能被發現與 rollback。這些不是單純 prompt engineering 能解決的問題。

實務上，這篇不應被讀成「大家都該開始做 RL」。更好的讀法是：當 agent failure 已經被清楚分類、反覆重現、可用程式評分，而且外圍槓桿已經用盡時，團隊才有理由把 trajectories 轉成權重更新。否則 RL 只是用更高成本把錯誤規格固定進模型。

## Relation To Existing Concepts

- [Agent Evaluations](../concepts/agent-evaluations.md)：這篇把 eval suite 和 RL environment 合併成同一個 artifact frame。task dataset、harness、rubric 在 frozen model 上是 eval；在 learning model 上接到 reward update 就是 RL。
- [AI Systems Engineering](../concepts/ai-systems-engineering.md)：agentic RL 不是 isolated training trick，而是包含 inference workers、trainer、sandbox、provider abstraction、reward design、GPU utilization、checkpoint governance 的系統閉環。
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)：RL environment 本身也是 runtime surface。它需要可控 state、可重播 trajectories、安全工具邊界、可觀測執行紀錄與可靠 scoring。
- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md)：即使 reward 可由程式計算，人類仍要定義任務分布、審核 rubric 是否對齊真實目標、檢查 reward hacking，並決定 checkpoint 是否能進 production。
- [LLM Agents](../maps/llm-agents.md)：這篇提供 agentic RL 的入口，連到 evals、fine-tuning、AI systems engineering、agent harness 和 model-weight improvement loop。

## Tensions Or Disagreements

- 文章說 Wordle 例子不是 prompt 能可靠修好的問題，這個方向合理，但實務上仍需要先分清楚 failure 來源。若問題其實是 task framing、state rendering、tool feedback 或 harness bug，直接做 RL 可能只是把外圍設計缺陷寫進權重。
- 可驗證 reward 很有吸引力，但只適合結果能被清楚檢查的任務。客服、策略、設計、研究這類 open-ended workflow 可能仍需要 human review、LLM judge calibration 或多層 evidence，而不是單一程式分數。
- 把 eval environment 直接變成 training environment 會提高 reward hacking 風險。原本只會造成錯誤報表的 grader bug，一旦進入 RL loop，就可能變成模型學到的行為。
- Prime Intellect Environments Hub 的規模很有價值，但 environment quality、task representativeness、sandbox isolation、license / provenance、grader loopholes 都會影響訓練結果。environment registry 不等於可信訓練資料。
- 本次 preserved raw source 只到 hands-on section heading，缺少後續實作細節。因此此 article card 主要保存概念 framing 與 systems implication，不應被當作完整 Prime Intellect / Wordle 操作教學。

## Open Questions

- 什麼 failure pattern 足以證明「prompt / tool / memory 已經到頂，需要 RL」？
- 一個 eval suite 要升級成 RL environment 前，最低 evidence bundle 應包含哪些：task distribution、trajectory schema、grader tests、anti-gaming checks、sandbox policy、checkpoint rollback？
- 對 agentic RL 來說，reward function 的 code review 應該比一般 product code 多哪些檢查？
- 當 training environment 來自 public hub 時，團隊應如何驗證 task quality、license、grader loopholes 與 domain representativeness？
- `pass@k`、`pass^k`、trajectory reward 和 GRPO group-relative score 應如何共同解讀，避免把偶然成功誤當成可靠能力？

## Merge Candidates

- Agent eval environments and RL environments share the same core artifact shape: task dataset, harness, and rubric; frozen-model use measures behavior, learning-model use updates behavior.
- Agentic RL is justified only when failures are repeated across trajectories, success is verifiable, lower-cost levers are saturated, and enough varied tasks plus compute are available.
- Reward functions should be treated as high-risk behavioral artifacts because grader bugs can become learned model behavior once they feed weight updates.
- Agentic RL turns systems engineering into the bottleneck: trajectory generation, async training, sandboxing, provider abstraction, environment registries, GPU utilization, checkpoint governance, and rollback matter as much as the algorithm.
- Transcript preservation has a second use beyond debugging and evals: it can become training substrate when paired with reliable scoring and governance.
