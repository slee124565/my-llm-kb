# Deep Dive into LLMs like ChatGPT

## Source

- URL: unknown; imported markdown transcript from a workspace course-notes folder
- Author: Andrej Karpathy
- Published: unknown
- Captured: 2026-04-10
- Raw file: `raw/sources/2026/2026-04-10-deep-dive-into-llms-like-chatgpt-andrej-karpathy-transcript.md`
- Imported from workspace path: `/Users/lee/ws/myCS146S/docs/01-introduction-to-coding-llms-and-ai-development/01-deep-dive-into-llms-like-chatgpt-transcript-Andrej-Karpathy.md`
- Source note: filename and body both indicate a Karpathy transcript-style explainer on LLMs, but the imported markdown does not preserve a canonical URL or original publish date

## Main Claims

- 一個可用的 assistant，應理解為三段式產物：pretraining 提供廣泛知識、supervised fine-tuning 提供 assistant behavior、reinforcement learning 則在可驗證任務上讓模型自己發現更有效的解題 token sequence
- 參數中的知識更像 vague recollection，context window 才像 working memory；tool use 的價值在於把外部資訊刷新進 working memory，而不是強迫模型只靠回憶作答
- hallucination mitigation 不能只靠「更會背」，還需要讓模型學會在不確定時拒答，或改用 search / code interpreter 之類的工具
- 模型不是在一個 token 裡完成整個推理，而是需要把計算分散到一串 token 上；因此 prompt 與訓練示範若要求 one-shot 跳答案，往往會教出較差的 reasoning behavior
- LLM 能力具有 jagged intelligence：它可能在高難度任務上表現驚人，卻在 spelling、counting、簡單比較等地方出現局部失真，因此更適合作為需要驗證的工具，而不是可直接託付的權威
- 在 verifiable domain 上，RL 的核心不是模仿人類解法，而是讓模型以 guess-and-check 發現對自己有效的中介步驟；相對地，RLHF 更像有限的 alignment fine-tune，因 reward model 可被 gaming
- 更長的 context window 雖然重要，但不足以單獨支撐真正長時、多模態、持續運行的 agent；之後仍需要新的 memory / test-time learning ideas

## Why It Matters

這篇不是某個單點 agent pattern 的文章，而是一份很強的基礎 framing source。它把 tokenization、working memory、tool use、hallucination、reasoning、RL 與 agent trajectory 放進同一條敘事線，讓 repo 裡很多後續文章在談的「externalized state 為什麼重要」「為什麼 context 不是越長越好就好」「為什麼工具會改變回答品質」都有更清楚的底層解釋。

## Relation To Existing Concepts

- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Agent Knowledge Compilation](../concepts/agent-knowledge-compilation.md)
- [LLM Agents](../maps/llm-agents.md)
- [Long-Running Agents](../maps/long-running-agents.md)

## Tensions Or Disagreements

- 這份來源是長篇 transcript，不是經過收斂的 essay；它的價值更像高質量口頭 framing，而不是逐條可直接引用的穩定 specification
- 文章把許多仍有爭議的研究與產品問題壓成易懂類比，例如 `RLHF is not RL`、context window 不會單獨擴到足夠大，這些更適合當思考起點，而不是直接當成定論
- 其中一些例子和推薦資源明顯受當時產品狀態影響，例如 leaderboard、模型供應商、特定錯題與 tool UX，時效性不高
- 它對 general audience 的講法刻意簡化了很多 implementation nuance，例如 pretraining data engineering、post-training data synthesis、tool protocol design 與 reasoning model internals

## Open Questions

- externalized artifact 應被視為 context window 的延伸、檢索層，還是另一種與 working memory 平行的 state surface
- `models need tokens to think` 這個 framing，在 reasoning model 擁有更多 test-time compute 或隱式 scratchpad 後，哪些部分仍然成立
- tool use 的學習究竟主要依賴少量 schema examples，還是更深層的 environment-model alignment
- 若未來多模態與 computer use 成為基礎能力，repo-based knowledge compilation 應如何和更動態的 runtime memory 分工

## Merge Candidates

- context window functions like working memory; model weights are a vague recollection
- tools improve factuality by refreshing working memory, not only by adding retrieval
- reasoning quality depends on giving models room to unfold computation across multiple tokens
