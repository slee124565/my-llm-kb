# How to Fine-Tune LLMs in 2026

## Source

- URL: https://x.com/akshay_pachaar/status/2029212227438518406
- Author: Akshay @akshay_pachaar
- Published: 2026-03-04
- Captured: 2026-06-20
- Raw file: `raw/sources/2026/2026-03-04-how-to-fine-tune-llms-in-2026.md`
- Extraction: `myAgentTools/xcom-article-import`

## Main Claims

- 這篇把 fine-tuning 從「讓模型模仿更好的答案」推到「讓 agent 從嘗試、失敗與回饋中改善」。直覺上，監督式微調（supervised fine-tuning, SFT）像是背標準答案；強化微調（reinforcement fine-tuning, RFT）則像是在真實任務裡做 on-the-job training。對 agent 來說，後者更接近它實際要面對的多步驟工具使用、搜尋與環境互動。
- 作者主張 Group Relative Policy Optimization（GRPO）的重點是相對比較，而不是要求一個完美的絕對分數。它讓同一個 prompt 產生多個 completions 或 trajectories，再根據相對表現強化較好的行為。這對 agent training 很重要，因為很多任務很難說出「這次是 8.3 分」，但比較幾次嘗試哪個更好通常更可行。
- ART（Agent Reinforcement Trainer）被定位成把 GRPO 接到實際 Python agent 的訓練框架。它不是只訓練單輪 chatbot，而是把工具呼叫、多輪對話、環境互動與完整執行軌跡（trajectory）納入訓練資料面，讓 agent 的整段行為可以被記錄、評分、更新。
- RULER（Relative Universal LLM-Elicited Rewards）的主張是：不要讓人為每個 domain 手寫 reward function，也不要只叫 LLM judge 打 0-10 分；改成讓 LLM judge 比較多個 trajectories 哪個更好。這和 GRPO 的相對排序需求相互配合，降低了把真實 agent 任務變成 RFT 訓練資料的門檻。
- 文章最後用「訓練 3B 模型學會使用任意 MCP server」作為例子。這個例子真正值得保留的地方，不是 3B 模型本身，而是它把工具發現、任務生成、trajectory 收集、LLM-as-judge 評分與 LoRA checkpoint 更新串成一個可重複的 agent improvement loop。

## Why It Matters

這篇補上 repo 目前較少的一層：當 agent 的 failure 已經被 eval harness 看見後，下一步不一定只是改 prompt、換模型或加 rule，也可能是把執行軌跡轉成訓練訊號，直接改變較小模型的行為。

它和 `Building Self-Improving Tax Agents With Codex` 的差異也很清楚。Tax AI 那篇的改善路徑是「人類專家 correction -> targeted eval -> Codex 修改產品 / harness」。這篇則描繪另一條路：「agent trajectory -> relative judge reward -> GRPO / LoRA update」。前者改善系統與流程，後者改善模型行為。實務上兩者應該互補，而不是互相取代。

對 AI 產品與工程團隊來說，這意味著 evals 的價值可能不只在 release gate。當 traces、tasks、judges 與 reward pipeline 足夠穩定時，eval infrastructure 也會變成 training infrastructure。這會提高對 trace schema、judge calibration、reward hacking 防護、版本化 checkpoints 與 rollback 的要求。

## Relation To Existing Concepts

- [Agent Evaluations](../concepts/agent-evaluations.md)：這篇把 eval artifacts 往 training loop 推進。trajectory review、LLM-as-judge、relative ranking 與 reward signal 不只是評估品質，也可能成為 fine-tuning 的輸入。
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)：ART 的 client / backend split 顯示 training-time runtime surface 也需要被設計。agent code、trajectory recorder、vLLM inference、Unsloth GRPO trainer、LoRA checkpoint hot-swap 都是不同責任面。
- [AI Systems Engineering](../concepts/ai-systems-engineering.md)：fine-tuning 不再只是 ML notebook，而是決策系統的一部分：任務生成、工具 schema、環境回饋、judge、訓練、部署與監控必須形成一個可治理 loop。
- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md)：即使 RULER 減少人工標註，仍需要人類定義任務分布、審核 judge 是否合理、檢查 reward hacking，並決定何時允許新 checkpoint 進入 production。
- [LLM Agents](../maps/llm-agents.md)：這篇提供 agent training / self-improvement 的另一個入口，和 evals、runtime surface、MCP tooling、small model specialization 相關。

## Tensions Or Disagreements

- 文章把 RULER 描述成「不需要 reward function 或 labeled data」，但這不代表沒有 reward design。選哪些 scenarios、產生哪些 trajectories、judge 看到哪些 evidence、如何校準 judge，仍然是在設計 reward surface。
- LLM-as-judge 的相對比較通常比絕對打分穩定，但它仍可能偏好表面上流暢、過度解釋或迎合 rubric 的 trajectories。若沒有 human spot checks、holdout tasks 與 anti-gaming checks，RFT 可能只是把 judge bias 固化進模型。
- 小模型 fine-tuned 到特定任務後可能帶來成本與 latency 優勢，但也會增加 model operations 負擔：資料版本、checkpoint lineage、eval regression、fallback routing 與安全審核都要進入系統設計。
- 用 MCP server 作為訓練環境很有吸引力，但真實 MCP tools 可能有 side effects、credentials、rate limits 與 non-deterministic state。訓練環境必須先把可重播性與安全邊界設計好。

## Open Questions

- 什麼樣的 agent task 適合用 RFT 改善模型本身，什麼樣的 failure 應該留在 prompt、tool description、harness 或 product workflow 層解決？
- RULER-style relative judging 需要多少 human calibration，才足以支撐 checkpoint update，而不只是 offline experiment？
- 若 trajectory 包含 tool calls、private data 或 production state，training pipeline 應如何保存 provenance、遮罩敏感資訊、重播環境與刪除權？
- 小模型透過 task-specific fine-tuning 變強後，如何避免團隊誤以為它在相鄰任務上也同樣可靠？
- MCP 工具使用的訓練資料應如何避免 reward hacking，例如模型學會觸發容易得分的 tool path，而不是解決使用者真正的任務？

## Merge Candidates

- Agent eval infrastructure can become training infrastructure when tasks, trajectories, judges, rewards, and checkpoint updates are versioned as one loop.
- RFT for agents shifts improvement from answer imitation toward trajectory-level behavior improvement across tool calls, environment interactions, and multi-step attempts.
- Relative judging is useful because many agent tasks are easier to compare than to score absolutely, but the judge, task distribution, and evidence view still define the reward surface.
- Self-improving agent systems should distinguish product / harness improvement loops from model-weight improvement loops; both need traces, evals, governance, and rollback.
- MCP-based training environments need safe replay, side-effect control, credential boundaries, and stable tool schemas before they can become reliable agent training surfaces.
