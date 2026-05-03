# Prompt Migration And Agent Steerability

## Summary

Prompt migration and agent steerability 指的是：當模型能力、API runtime 或 agent tool surface 改變時，prompt 應如何被重新設計，讓 agent 更可靠地達成 outcome，而不是把舊 prompt stack 無限加厚。

## Why It Matters

模型升級不只是替換 model string。新的模型可能需要更短的 outcome-first instructions、更清楚的 success criteria、更少 process micromanagement，以及更嚴格的 runtime contract。若 prompt migration 只是不斷加規則，agent 會變得機械、昂貴，還可能在 tool use、final answer、citation 或 validation 上出現新的 failure mode。

## Current Framing

- GPT-5.5 guidance pushes prompt migration toward outcome-first contracts: define destination, constraints, evidence, output shape, and stopping conditions, then give the model room to choose the path.
- GPT-5.4 guidance treats output contracts, tool persistence, citation rules, verification loops, coding-tool boundaries, and reasoning effort as production control surfaces.
- GPT-5.3 Codex guidance shows coding-agent prompts as operating contracts: repo reading, `AGENTS.md`, editing discipline, user updates, apply-patch behavior, parallel tool use, validation, and final handoff all belong in the steerability layer.
- GPT-3.5-era prompt engineering treated prompt text itself as the main reliability surface: clear instructions, delimiters, examples, decomposition, output formats, and reasoning scaffolds carried much of the control burden.
- Personality should be separated from collaboration style. Tone controls the user experience; collaboration style controls when the agent asks, assumes, verifies, retries, and stops.
- Preambles and `phase` fields make user-visible progress updates part of runtime correctness, especially when assistant items are replayed across Responses API turns.
- Retrieval budgets, missing-evidence behavior, and citation requirements should be explicit in research or evidence-sensitive workflows.
- Reasoning effort should be workload-specific and eval-backed; higher effort is not automatically the right default.
- Migration should happen one change at a time, with evals or targeted validation proving that the new prompt preserves required behavior.
- Repo-local instruction surfaces such as `AGENTS.md`, `docs/`, prompt assets, and templates prevent global prompts from becoming overloaded with domain workflow detail.
- The six-question GPT-5.5 checklist can also be used as a milestone intake gate for coding-agent collaboration: in the Shopee CS harness case, it turns "design the next plan" into "define the next operational-loop ownership delta, evidence threshold, stop gate, and handoff shape."

## GPT-5.5 Outcome-First Prompt Checklist

設計 GPT-5.5-style agent prompt 前，先問六個問題：

1. 這個 agent 最後要交付什麼？
2. 什麼條件下算成功？
3. 哪些限制不可違反？
4. 哪些資訊或證據是必要的？
5. 什麼情況應該停止、標記 blocked 或問問題？
6. 最終輸出要讓人或系統如何接續使用？

這組問題的目的，是把 prompt 從 step-by-step micromanagement 轉成 outcome contract。若 prompt 裡有大量 `always first...`、`then always...`、`must inspect every...` 這類流程規則，應逐條檢查：它是真正不可違反的 invariant，還是舊模型時代留下的流程補丁。

## Relation To Harness Engineering

GPT-5.5 prompt guidance 和 harness engineering 的深層關係是：兩者都在把更強的模型轉化成可靠、可控、可驗證的工作系統，只是責任分工不同。

Prompt 負責定義 intent、success criteria、constraints、evidence policy、permission boundary、output shape 與 stopping conditions。Harness 負責提供 repo context、tools、state、logs、tests、evals、sandbox、handoff 與 observability。隨模型能力提升，原本塞在 prompt 裡的流程補丁，會被重新分配到 harness、docs、tools、evals 或 runtime protocol。

因此 GPT-5.5-style outcome-first prompt 不是代表 prompt 不重要，而是代表 prompt 更像 harness 的 declarative control layer。它說清楚「什麼算完成、哪些不能違反、缺證據時怎麼停」，但不應把每個搜尋、檢查、重試、格式化步驟都寫成 micromanaged procedure。

這也解釋了 prompt 設計和 harness engineering 的演化：

- GPT-3.5-era prompt 常常在補 harness 的缺口，用文字要求模型拆解、推理、檢查與格式化。
- GPT-5.3 Codex 把 prompt 推向 coding-agent operating contract，明確規定 repo 探查、編輯邊界、工具使用、驗證與 handoff。
- GPT-5.4 把 prompt 推向 production control surface，讓工具持續性、證據、citation、verification loop、phase handling 與完成條件成為可控面。
- GPT-5.5 則把 prompt 收斂成 outcome contract，讓模型自主選路徑，同時把不可違反的邊界和可驗證的交付條件保留下來。

實務上，prompt engineering 正在被 harness engineering 吸收，但不是消失。它從「寫一句神奇指令」升級成「設計模型與執行環境之間的契約」：prompt 描述任務契約，harness 提供可見性、可操作性、可恢復性與驗證證據。

## Signals From Recent Articles

- [OpenAI Prompt Engineering - GPT-3.5 Era](../articles/openai-prompt-engineering-gpt-3-5-era.md)
- [OpenAI Prompt Guidance - GPT-5.5](../articles/openai-prompt-guidance-gpt-5-5.md)
- [OpenAI Prompt Guidance - GPT-5.4](../articles/openai-prompt-guidance-gpt-5-4.md)
- [OpenAI Prompt Guidance - GPT-5.3 Codex](../articles/openai-prompt-guidance-gpt-5-3-codex.md)
- [Using PLANS.md for Multi-Hour Problem Solving](../articles/using-plans-md-for-multi-hour-problem-solving.md)
- [Harness Engineering](../articles/harness-engineering-codex-agent-first-world.md)
- [OpenAI harmony response format](../articles/openai-harmony.md)

## Open Questions

- 哪些 prompt rules 是 true invariants，哪些只是 older-model workaround，應在模型升級時移除
- 舊式 "think step by step"、few-shot、delimiter、persona blocks 哪些仍然是有效控制，哪些應改成 eval、tool contract、schema 或 runtime state
- prompt asset 應如何記錄 target model、reasoning effort、tool assumptions 與 validation evidence
- repo-local `AGENTS.md`、global model prompt、skill prompt、task prompt 之間，哪些規則應放在哪一層
- preamble / phase / final-answer separation 應在 prompt、runtime adapter 還是 product UI 裡負責
- 當模型變得更強，哪些 harness rules 可以收斂成 outcome-first success criteria，哪些必須保持硬性規則

## Related Pages

- [Agent Runtime Surfaces](agent-runtime-surfaces.md)
- [Externalized Agent State](externalized-agent-state.md)
- [Human-Supervised Agent Ops](human-supervised-agent-ops.md)
- [Long-Running Agent Harnesses](long-running-agent-harnesses.md)
- [Repository Knowledge As System Of Record](repository-knowledge-as-system-of-record.md)
- [LLM Agents](../maps/llm-agents.md)
- [Codex Workflows](../maps/codex-workflows.md)
