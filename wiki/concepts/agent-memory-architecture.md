# Agent Memory Architecture

## Summary

Agent memory architecture 指的是：長期 agent 系統如何保存、更新、檢索與治理跨 session 的 knowledge、facts、relationships、preferences、procedures 與 task state。它不是單一「記住更多」功能，而是多種 memory surface 的分工。

## Why It Matters

長期 agent 的品質常取決於它怎麼記憶，而不是只取決於模型能力。若系統把 static documents、user facts、session history、procedures、task progress 與 runtime logs 都塞進同一種 store，agent 會很難判斷哪些資訊是現在有效、哪些只是歷史、哪些是可執行流程、哪些只是待查來源。

## Current Framing

- context window 像工作記憶（working memory），可以讓模型暫時操作資訊，但它不是長期 state governance
- repo / vault / wiki 適合保存 source provenance、compiled knowledge、task contracts、decisions、logs 與可審計 artifacts
- markdown memory、USER.md、MEMORY.md、SOUL.md 這類檔案適合保存 compact、穩定、常用的身份、偏好與操作規則，但需要版本控制、更新規則與過期清理
- session transcript / SQLite history 適合保存 episodic memory，但若沒有摘要、檢索與 relevance policy，很快會變成噪音
- skills 是程序記憶（procedural memory）：它們保存如何做事、常見陷阱、驗證流程與可執行 scripts，而不是保存 user facts
- vector RAG 適合大規模、相對靜態的文件搜尋；它找相似文字很強，但本身不理解 identity、relationship、current truth 或 fact lifespan
- temporal knowledge graph 適合 relationship-rich、會變動、需要多跳推理與可解釋 path 的 long-term memory，例如 personal assistant、customer history 或 enterprise knowledge evolution
- Graphiti-style memory 把新 message / document / event 當成 episode，抽取 entities / relationships，和既有 graph reconcile，並用 bi-temporal model 區分事件發生時間與系統得知時間
- hybrid memory 不應被理解成 RAG vs graph 的宗教戰；成熟系統通常讓 static corpus、dynamic graph、procedural skills 與 task artifacts 各自承擔不同責任
- memory backend selection 是 runtime-surface decision：latency、ingest cost、privacy、deletion policy、user ownership、auditability、freshness 與 correction loop 都會改變正確選型

## Signals From Recent Articles

- [Building Agent Memory with Knowledge Graphs](../articles/building-agent-memory-with-knowledge.md)
- [Hermes Agent Masterclass](../articles/hermes-agent-masterclass.md)
- [Getting The Most Out Of Codex](../articles/getting-the-most-out-of-codex.md)
- [Lessons From Building Claude Code: How We Use Skills](../articles/lessons-from-building-claude-code-how-we-use-skills.md)
- [OpenClaw: The Viral AI Agent that Broke the Internet](../articles/openclaw-viral-ai-agent-lex-fridman-peter-steinberger.md)
- [Deep Dive into LLMs like ChatGPT](../articles/deep-dive-into-llms-like-chatgpt.md)
- [LLM Knowledge Bases](../articles/karpathy-llm-knowledge-bases.md)

## Open Questions

- 哪些 memory 應由使用者持有在 repo / vault，哪些可以交給 hosted platform memory，哪些應放在 local personal-agent runtime？
- 對於會影響未來行為的記憶，最小 correction / deletion / audit interface 是什麼？
- Entity resolution 錯誤、過期偏好、錯誤技能與任務狀態 drift 應用同一套治理方式，還是分別處理？
- Long-running agents 應如何決定何時把 transient context 升級成 durable memory？
- Static KB、temporal graph、session transcript、skills 與 tracker state 之間，哪些資料應雙向同步，哪些應保持單一來源？

## Related Pages

- [Externalized Agent State](externalized-agent-state.md)
- [Agent Runtime Surfaces](agent-runtime-surfaces.md)
- [Long-Running Agent Harnesses](long-running-agent-harnesses.md)
- [Repository Knowledge As System Of Record](repository-knowledge-as-system-of-record.md)
- [LLM Agents](../maps/llm-agents.md)
- [Long-Running Agents](../maps/long-running-agents.md)
