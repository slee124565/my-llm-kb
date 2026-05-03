# OpenAI Prompt Engineering - GPT-3.5 Era

## Source

- URLs:
  - https://help.openai.com/en/articles/6654000-comprehensive-step-by-step-guide-to-prompt-engineering-with-chatgpt
  - https://cookbook.openai.com/articles/techniques_to_improve_reliability
  - https://developers.openai.com/api/docs/guides/prompt-engineering
- Author: OpenAI
- Published: Mixed; includes 2022 Cookbook reliability guidance and living docs
- Captured: 2026-05-03
- Raw file: `raw/sources/2026/2026-05-03-openai-prompt-engineering-gpt-3-5-era.md`

## Main Claims

- The GPT-3.5-era guidance emphasizes clear, specific instructions, instructions-first formatting, delimiters between task and context, desired output examples, and parameter tuning.
- Reliability is improved by decomposing complex tasks, giving the model room to reason, using few-shot examples where behavior is hard to specify, and constraining output when hallucination risk matters.
- Prompt engineering is treated as a direct control layer over a brittle but general model: if the answer is wrong, first improve wording, examples, decomposition, or output format before moving to fine-tuning or system changes.
- Modern OpenAI docs preserve the foundations but move them into a broader production frame: developer messages, reusable prompt versions, evals, RAG, context-window planning, and structured outputs.

## Why It Matters

This is the baseline for understanding later agent prompting. Early prompt design tried to put more work into the prompt itself: tell, show, delimit, decompose, and ask for reasoning. Later GPT-5-era guidance does not discard these ideas, but relocates many of them into runtime contracts, tool policies, citation rules, eval loops, and repo-local agent instructions.

## Relation To Existing Concepts

- [Prompt Migration And Agent Steerability](../concepts/prompt-migration-and-agent-steerability.md)
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)

## Tensions Or Disagreements

- "Think step by step" and chain-of-thought-style prompts were useful reliability hacks in older guidance, but later reasoning-model guidance warns that explicit chain-of-thought prompting can be unnecessary or harmful.
- Few-shot examples improve format and behavior control, but they can also conflict with written instructions; later prompt migration guidance treats this as an eval and consistency problem.
- Adding more instructions can improve brittle models, but for stronger instruction-following models it can create contradictions, latency, and mechanical behavior.

## Open Questions

- Which old prompt blocks in this repo are true task invariants, and which are older-model scaffolding that should be removed for newer models?
- When should decomposition live in the prompt, and when should it be implemented as a runtime planner, checklist, tool, or workflow artifact?
- Which few-shot examples are still useful, and which should be replaced by stricter output schemas or evals?

## Merge Candidates

- GPT-3.5-era prompting is prompt-as-instruction: clear task wording, delimiters, examples, decomposition, and explicit output format.
- The durable shift since then is not "prompting matters less"; it is that prompt design moves from clever wording into agent system design.
- Model upgrades should trigger prompt audit: remove brittle hacks, keep true constraints, and move production guarantees into tools, evals, and runtime contracts.
