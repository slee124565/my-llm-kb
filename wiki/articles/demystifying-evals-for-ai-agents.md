# Demystifying Evals For AI Agents

## Source

- URL: https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents
- Author: Anthropic Engineering
- Published: 2026-01-09
- Captured: 2026-04-14
- Raw file: `raw/sources/2026/2026-04-14-demystifying-evals-for-ai-agents.md`
- Workspace provenance: copied from `my-blog-kb/raw/sources/2026/2026-04-14-demystifying-evals-for-ai-agents/2026-04-14-demystifying-evals-for-ai-agents.md`

## Main Claims

- Agent evals 比 single-turn LLM evals 更難，因為被評估的不是單一模型輸出，而是 model 加上 agent harness：tools、environment state、intermediate reasoning、transcripts、outcomes 與 grading infrastructure 都會影響結果。
- 有用的 eval suite 需要區分 tasks、trials、graders、transcripts、outcomes、evaluation harnesses、agent harnesses 與 suites，而不是把 eval 簡化成 prompt、answer、score。
- Evals 的價值會在團隊走出早期 dogfooding 後變明顯：它能把 user complaints 與 manual checks 轉成 baselines、regression tests、model-upgrade evidence，以及 product / research 溝通 artifacts。
- Agent evals 需要一組 grader portfolio。Code-based graders 快、便宜、客觀；model-based graders 能處理主觀或開放式判斷；human graders 仍然是 calibration 與 gold-standard review 的必要基準。
- Capability evals 與 regression evals 的任務不同。Capability evals 應該保留可進步空間；regression evals 應接近 100% pass rate，用來捕捉 backsliding。成熟後的 capability evals 可以升級成 regression suites。
- Eval design 應符合 agent 類型：coding agents 偏向 deterministic tests 與 static checks；conversational agents 需要 state checks 加上 interaction rubrics；research agents 需要 groundedness、coverage 與 source-quality checks；computer-use agents 則需要 sandboxed UI environments 與 outcome verification。
- 非決定性的 agent behavior 需要 repeated trials 與符合產品需求的 metrics。`pass@k` 衡量多次嘗試中是否至少有一次成功，`pass^k` 衡量每次嘗試是否都能穩定成功。
- Zero-to-one roadmap 很務實：從 20-50 個真實或 manual-test tasks 開始，寫出不含歧義且有 reference solutions 的 specs，建立 balanced problem sets，隔離 trial environments，選擇 robust graders，閱讀 transcripts，監控 saturation，並為 eval maintenance 指定明確 owner。
- Automated evals 只是其中一層。Production monitoring、A/B tests、user feedback、manual transcript review 與 systematic human studies 是互補 signals，能補上 synthetic evals 漏掉的失敗。

## Why It Matters

This article turns `evals` from a generic quality word into a concrete harness discipline. The strongest contribution for `my-llm-kb` is the separation between the agent being evaluated and the evaluation harness that observes it. A team is not just asking whether a model answered correctly; it is asking whether a task spec, environment, tool surface, transcript, outcome check, grader, and aggregation process jointly measure the behavior that matters.

That bridges several existing repo threads. `A Postmortem of Three Recent Issues` showed that weak production-quality signals can miss real regressions. `Building Self-Improving Tax Agents With Codex` showed how production corrections become targeted evals. `After Automation` framed benchmarks as artifacts inside a chosen frame. This Anthropic article supplies the operating vocabulary for building and maintaining those eval artifacts.

## Relation To Existing Concepts

- [Agent Evaluations](../concepts/agent-evaluations.md)：這篇是 anchor article，用來把 eval suites、graders、transcripts、outcomes 與 trial environments 視為 first-class knowledge objects。
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)：evals 是 harness contract 的一部分，尤其在 state、tool calls 與 environment outcomes 都會影響結果的 multi-turn tasks 中更明顯。
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)：被評估的 runtime 必須足夠接近 production，結果才有意義；但每個 trial 又必須從 isolated state 開始，避免 shared state 污染分數。
- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md)：product teams 與 domain experts 應負責定義 tasks、calibrate LLM judges，並長期維護 eval suites 的健康度。
- [LLM Agents](../maps/llm-agents.md)：這篇補上一個可重用 framework，用來評估 coding、conversational、research 與 computer-use agents。
- [Long-Running Agents](../maps/long-running-agents.md)：任務 horizon 拉長時，multi-turn evals、transcript review、pass-rate consistency 與 environment isolation 都會變得更重要。

## Tensions Or Disagreements

- 文章建議優先 grading outcomes，而不是 rigid tool paths；但某些 production systems 仍然需要針對 tool use 做 policy 或 compliance checks。實務規則不是 `never grade tool calls`，而是除非 path 本身就是 safety 或 business requirement，否則不要用 path checks 拒絕有效解法。
- LLM-as-judge graders 被定位成 scalable 且 flexible，但它們也帶來自己的 calibration burden。若沒有 human spot checks，eval suite 可能變成另一個 failure modes 不透明的 model system。
- 文章主張早期 20-50 個 tasks 可能就足夠。這是有用的 pragmatism，但成熟產品若要偵測很小的 expected deltas，仍然需要更大、更難、分層更好的 suites。
- Evaluation frameworks 是有用的 infrastructure，但 appendix 也提醒：framework choice 不能補償 ambiguous tasks、brittle graders 或不具代表性的 examples。

## Open Questions

- Repo-local agent harness 應保存哪些最小 transcript 與 outcome schema，才能讓未來 evals 從真實 failures 中建立？
- 什麼情況下 task 應明確 grading tool-call path，什麼情況下只應 grading final environment state？
- 團隊應如何針對特定 product surface，決定要優化 `pass@k`、`pass^k`，或其他 reliability metric？
- 最小 calibration loop 應如何設計，才能讓 LLM-as-judge graders 可信，同時不把每次 eval run 都變成 human review project？
- Eval suites 應如何暴露 saturation、ambiguity 與 grader bugs，才不會讓 benchmark reports 誇大 model 或 agent capability？

## Merge Candidates

- agent evals 會同時測量 model、scaffold、task spec、environment、graders 與 aggregation loop。
- 在 agent evaluation work 中，task、trial、grader、transcript、outcome、eval harness、agent harness 與 suite 應成為彼此分離的 vocabulary。
- capability evals 與 regression evals 應以不同方式設計、解讀與維護。
- repeated trials 需要能區分 occasional success 與 reliable success 的 metrics，尤其是 `pass@k` 與 `pass^k` 的差異。
- 好的 eval suites 會從真實 failures 與 manual checks 開始，接著要求 unambiguous specs、reference solutions、balanced cases、isolated environments 與 transcript review。
- 除非 tool-use path 本身就是 requirement，否則應優先採用 outcome grading，而不是 brittle path grading。
- automated evals 應與 production monitoring、A/B tests、user feedback、manual transcript review 與 human studies 結合。
