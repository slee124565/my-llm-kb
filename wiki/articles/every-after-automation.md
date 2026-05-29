# After Automation

## Source

- URL: https://every.to/p/after-automation
- Author: Dan Shipper
- Publisher: Every
- Published: 2026-05-21
- Captured: 2026-05-27
- Raw file: `raw/sources/2026/2026-05-21-every-after-automation.md`
- Workspace provenance: copied from `refs/my-blog-kb/raw/inbox/every-after-automation.md`

## Main Claims

- 在專家型知識工作中，AI automation 不是單純消除人的工作，而是讓昨天已被框定的能力變得便宜，並提高當下對人類判斷、品味、review 與系統設計的需求。
- 與 agents 協作正在分成兩種模式：可以委派 bounded jobs 的 `agent employees`，以及像 Codex / Claude Code / Claude Cowork 這類更接近複雜工作 operating system 的人機協作介面。
- employee-style agents 仍然需要 ownership、maintenance、calibration 與 team-level stewardship。若沒有人維持其 context、skills、workflows 與 quality loop，個人或團隊 agents 會逐漸失效。
- 稀缺的人類角色轉向 framing：決定什麼重要、設定任務邊界、判斷輸出、把結果轉成真實決策，並建立 review queues、evals、harnesses、repo rules、CI、permissions 與 workflows。
- Benchmarks 衡量的是 frame 內的模型表現。當 benchmark 飽和時，可以改變 frame 來暴露新的 edge，因此 benchmark 進展不應被誤讀為模型取代了人類 framer。
- 便宜的模型能力會刺激需求：如果 codebase rewrites 變得容易，更多人會嘗試 rewrites，反而提高對 scope、invariants、migration、rollback、data 與 review 等資深判斷的需求。
- 即使是很強的 AGI-like always-on agent，仍會在 framer 提供的 goals、reward signals 或 progress definitions 下運作。文章的核心論點是：frame 不是 framer。
- 當前 AI agents 在任務執行上有 autonomy，但不具備人類意義上擁有自身目的的 agency；它們代表人類操作者行動，而不是獨立選擇什麼才重要。

## Why It Matters

這篇文章強化了本 repo 反覆出現的一個 thesis：AI 會把瓶頸往上移。先前來源多從 coding、startup operation 與 self-improving production loops 來談這件事；Shipper 補上更一般化的機制：automation 會讓已被框定的工作變便宜，讓系統充滿 acceptable-but-generic output，並提高下一個邊界上對 expert judgment 的需求。

對 `my-llm-kb` 來說，最可重用的貢獻是 `frame` 與 `framer` 的區分。這能解釋為什麼更好的 agent benchmarks 與更強的任務執行能力，不會消除 human-supervised harness design；相反地，因為更多人能在舊 frame 內行動，framing、evaluation、permissioning、rollback 與 taste 會變得更有價值。

## Relation To Existing Concepts

- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md)：人類角色從 step-by-step operators 轉為 framers、supervisors、reviewers 與 system designers。
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)：更廣泛的 automation 會提高對 review queues、evals、CI、permissions、workflows 與 rollback surfaces 的需求。
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)：文章區分了可委派工作的 `agent employee` surfaces，以及人類和多個 agents 共享 tools 與 context 的 collaborative work OS surfaces。
- [Prompt Migration And Agent Steerability](../concepts/prompt-migration-and-agent-steerability.md)：benchmark 與 prompt performance 取決於 framing；改變 prompt 就會改變被衡量的東西。
- [Codex Workflows](../maps/codex-workflows.md)：Codex 被定位成 work operating system，而不只是 code generator。
- [LLM Agents](../maps/llm-agents.md)：文章補上一個廣義理論，說明為什麼 agent progress 會在當前 edge 創造更多 expert work。

## Tensions Or Disagreements

- 文章很大程度建立在 Every 內部 early-adopter 經驗上，因此對 expert knowledge work 的解釋力最強，但不一定能乾淨地推廣到所有 labor markets。
- `frame is not the framer` 這個 thesis 很有用，但可能低估未來系統在 human goals 之下更好地提出、比較與修訂 frames 的可能性。
- 文章反對簡單的 job-replacement tipping point，但並未證明所有受影響角色都會同等受益；對 experts 的需求增加，可以和 less differentiated work 的 disruption 同時存在。
- 文章對 AGI 的定義 `when it makes economic sense to keep your agent running continuously` 在操作上有用，但比許多 research 或 policy definitions 更窄。

## Open Questions

- 哪些最小 artifacts 能讓人類 framers 領先於 agent execution：problem brief、invariants、evidence threshold、eval target、rollback plan 與 review rubric？
- 什麼情況下，`agent employee` 需要 named owner、maintenance budget、skills repository 或 team-level quality harness？
- Benchmark reports 應如何區分 model capability，以及嵌在 prompt、harness、data selection、verifier 與 scoring frame 裡的 intelligence？
- Expert judgment 的哪些部分可以可靠地 externalize 到 repo rules、evals、workflows 與 supervisor planes，哪些部分必須保留為即時的人類 taste？
- 組織應如何衡量 automation 是否正在產出 differentiated work，而不只是提高 output volume？

## Merge Candidates

- automation 會讓 framed competence 變便宜，接著提高 human framing、taste、review 與 system design 的價值
- agents as employees 與 collaborative agent workspaces 是不同 runtime modes，對 ownership 與 maintenance 有不同需求
- benchmark saturation 應觸發 frame analysis，而不只是 model-capability extrapolation
- 當低成本 agents 讓更多 non-experts 嘗試過去稀缺的工作時，expert review demand 會增加
- frame 不是 framer：agent 在任務內的 autonomy，不等於人類對什麼應該重要的 agency
- review queues、evals、harnesses、repo rules、CI、permissions 與 workflows，是面對大量 AI-generated work 時的 expert response
