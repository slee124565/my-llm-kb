# METR｜Measuring AI Ability to Complete Long Tasks

## Source

- Title: Measuring AI Ability to Complete Long Tasks
- URL: https://metr.org/blog/2025-03-19-measuring-ai-ability-to-complete-long-tasks/
- Publisher: METR
- Author: METR; Thomas Kwa, Ben West, Joel Becker, Amy Deng, Katharyn Garcia, Max Hasin, Sami Jawhar, Megan Kinniment, Nate Rush, Sydney Von Arx, Ryan Bloom, Thomas Broadley, Haoxing Du, Brian Goodrich, Nikola Jurkovic, Luke Harold Miles, Seraphina Nix, Tao Lin, Neev Parikh, David Rein, Lucas Jun Koba Sato, Hjalmar Wijk, Daniel M. Ziegler, Elizabeth Barnes, Lawrence Chan
- Published: 2025-03-19
- Captured: 2026-06-20
- Raw file: `raw/sources/2025/2025-03-19-measuring-ai-ability-to-complete-long-tasks.md`
- Related dashboard: https://metr.org/time-horizons/
- Content type: agent evaluation / time horizon / long-running agents / autonomy forecast / software-task benchmark

## Main Claims

- METR 的 time-horizon evaluation 不是在問「AI 實際跑了多久」，而是在問「這個 agent setup 能以某個成功率，完成一個人類專家通常要花多久的任務」。這讓 benchmark 從抽象分數變成一個比較接近工作委派邊界的刻度。
- 測試設計先用人類專家完成時間標定任務難度，再讓 model + scaffold 的 agent 嘗試同一批任務，最後用 logistic curve 找出 50% 或 80% 成功率對應的人類任務時長。這把模型能力、工具 scaffold、任務 spec、評分方式放進同一個 evaluation harness。
- 這個指標的核心直覺是：agent 常不是缺少單步知識，而是難以長時間串接多個相依動作。任務越長，目標漂移、錯誤累積、工具使用失誤、環境狀態理解錯誤都會放大。
- METR 觀察到 frontier agents 能完成的任務長度在過去幾年快速增加，並用這個趨勢討論未來 week-long / month-long autonomous work 的可能性；但這是 forecast lens，不是現成部署承諾。
- dashboard 特別提醒：這些任務主要是 software engineering、machine learning、cybersecurity，且多半 self-contained、well-specified、可自動評分。它不能直接外推到所有知識工作、所有職業，或高脈絡、高人際、高模糊成功標準的真實工作。

## Why It Matters

這篇對 `my-llm-kb` 的價值，是把 long-running agent 的討論從「能不能跑很久」改成「能不能在一條相依任務鏈上穩定成功」。它和 [Demystifying Evals For AI Agents](demystifying-evals-for-ai-agents.md) 的 vocabulary 接起來：task、trial、scaffold、environment、outcome、grader、transcript 都會影響結果。

對工程人員來說，time horizon 是委派邊界。若一個 agent 只有幾十分鐘的人類任務 horizon，把兩天的模糊需求直接丟給它就是錯誤使用；更合理的是拆成可驗收任務、補 repo context、設測試與 rollback，並用多次 trial 看一致性。

對非工程人員來說，這個 metric 說明了兩件事：第一，AI agent 確實可能跨過部分 coding 門檻；第二，能否成功仍取決於你是否把業務目標、資料、邊界與驗收標準說成 agent 可執行的任務。非工程使用者不需要先變成工程師，但需要變成更好的 task framer。

## Relation To Existing Concepts

- [Agent Evaluations](../concepts/agent-evaluations.md): 補上一個 capability eval 的時間刻度：用人類任務耗時作為難度軸，再看 agent 成功率。
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md): time horizon 把長任務可靠性和 scaffold 設計綁在一起；模型單體能力不能脫離工具、環境和 verifier 解讀。
- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md): time horizon 越長，越需要人類 supervisor 設定任務 frame、審查結果、回收失敗樣本。
- [Long-Running Agents](../maps/long-running-agents.md): 可作為 long-running agent benchmark literacy 的 anchor article。

## Tensions Or Disagreements

- METR 的任務比真實工作乾淨：self-contained、低組織脈絡、評分明確。這會低估或錯估真實工作裡的 tacit knowledge、stakeholder alignment、責任歸屬與 ambiguous success metrics。
- 用人類專家完成時間作為難度刻度很直覺，但不等於職場中的實際工時。熟悉 codebase 的工程師、低脈絡 contractor、AI agent 面對的任務條件不同。
- 50% time horizon 適合看趨勢，不適合直接決定 production 自主性。高風險 workflow 可能需要 95% 或 99% 可靠性、可回滾性、審計線索與人工批准。
- 測到的是 `model + scaffold + task suite + grader` 的組合，不是純模型能力；不同 scaffold 或 tool surface 可能改變結果。

## Open Questions

- 對 repo-local coding agent，應把 50% horizon、80% horizon、pass@k、pass^k、human review burden 哪些指標一起看，才不會把一次成功誤判成可靠委派？
- 真實企業任務如何建立自己的 time-horizon-like eval：人類 baseline、任務切分、成功標準、環境隔離、失敗分類應怎麼設計？
- 當任務很長但可以平行拆成很多獨立短任務時，應該用 time horizon 還是 throughput / cost per successful item 衡量？
- 非工程使用者的 task framing 能否透過 templates、checklists 或 domain-specific scaffolds 轉成可測的能力，而不是只靠個人表達能力？

## Merge Candidates

- 已回寫 [Agent Evaluations](../concepts/agent-evaluations.md)：time horizon 是以人類任務耗時為難度軸的 capability eval，需和 scaffold、task distribution、grader 一起解讀。
- 已回寫 [Long-Running Agents](../maps/long-running-agents.md)：time-horizon benchmark 應作為委派邊界與可靠性討論，而不是當成「AI 能工作幾小時」的字面說法。
- 可後續補進 [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)：若要整理更完整的 long-task eval checklist，再把本文和 Codex / Claude Code 長任務實作頁合併。
