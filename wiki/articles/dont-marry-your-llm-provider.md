# Don't Marry Your LLM Provider

## Source

- URL: https://theneuralmaze.substack.com/p/dont-marry-your-llm-provider
- Author: Miguel Otero Pedrido
- Publisher: The Neural Maze
- Published: 2026-05-19
- Captured: 2026-06-19
- Raw file: `raw/sources/2026/2026-05-19-dont-marry-your-llm-provider.md`
- Subtitle: Issue #03 - Why every production agent ends up behind a reverse proxy
- Source note: Imported with `myAgentTools/neural-maze-ase-journey-import`; Substack metadata marked the post as `only_paid`, and the captured body ends at the `Self-host it in five minutes` heading before the runnable LiteLLM walkthrough.

## Main Claims

- AI gateway 可以被理解成 LLM 時代的 reverse proxy：當多個 app 要呼叫多個模型供應商時，TLS、auth、rate limit、logging 這類 web-era cross-cutting concerns 對應到 model routing、fallback、budget、virtual key、cost attribution、observability 與 tool routing。這些不應散落在每個 agent app 裡，而應集中在每次模型請求都會通過的中介層。
- Provider-agnostic abstraction 的重點不是「未來可以手動換模型」，而是讓 production traffic 可以在 gateway 裡持續做 routing、fallback 與 cost optimization。Application code 只看見一個穩定 API shape；provider-specific request format、錯誤處理、fallback chain 與價格策略則由 gateway 管理。
- LiteLLM 這類 proxy-mode gateway 把模型供應商、API key、fallback、routing strategy 與 MCP server 都收斂到 declarative config。這讓模型選擇從 application logic 變成 runtime policy，也讓同一個 client 可以用 OpenAI-shaped API 呼叫 Anthropic、Gemini、Groq、Bedrock、本地 Ollama 或 MCP-backed tools。
- 真正的 request hot path 應該短而清楚：auth、rate limit、routing、provider call、response。Spend tracking、trace export、observability 與 counter updates 應盡量移到 async path，否則 gateway 會從可靠性邊界變成 latency bottleneck。
- Virtual API keys、team/user-level rate limits、budget enforcement 與 cost attribution 是 agent productionization 的治理面。它們把「誰能用哪個模型、花多少錢、哪個 team 負責哪筆費用」從散落的 raw provider key 變成可撤銷、可審計、可分配的 runtime control surface。
- 文章提出三個 production pattern：用多把 provider key federate rate limit、針對 content policy 或 context window 做特殊 fallback、用 cost-based routing 在多個 cheap-tier deployment 間自動選擇。共同點是把 user-visible error 或成本浪費轉成 gateway policy，而不是要求每個 agent app 自己重寫一套策略。

## Why It Matters

這篇延續 [Hidden Technical Debt in Agentic Systems](hidden-technical-debt-in-agentic-systems.md) 對 model layer 的提醒：production agent 的問題不是「今天選哪個 LLM provider」，而是 team 是否有能力把模型供應商變成可替換、可觀測、可治理的 fleet。

對 `my-llm-kb` 來說，新增價值在於把 provider-agnostic abstraction 從抽象原則落到一個具體 runtime surface：AI gateway。它讓 model choice 不再只是 prompt 或 SDK 層的選項，而是 auth、budget、routing、fallback、trace、MCP/tool discovery 與 cost policy 的集中控制點。

管理含義也很直接：如果 raw provider key 被複製到每個 repo，模型切換、事故 fallback、成本歸因與權限撤銷都會變成逐 app 的手工維運。把模型請求集中到 gateway，不是為了追求架構漂亮，而是為了讓 production agent 的供應商風險、成本風險與 tool routing 風險能被一個明確 owner 管理。

## Relation To Existing Concepts

- [AI Systems Engineering](../concepts/ai-systems-engineering.md): AI gateway 是 model layer 的 production boundary，把 model choice、cost、fallback、auth、observability 與 tool routing 變成可治理 artifact。
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md): Gateway 本身是一個 runtime surface；它暴露 API shape、virtual keys、routing config、budget、trace export、MCP server registration 與 provider adapters。
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md): 長任務 agent 的 retry、fallback、context-window escalation 與 cost circuit breaker 不應只靠 agent loop 自己處理，部分應下沉到 gateway policy。
- [Agent Evaluations](../concepts/agent-evaluations.md): Provider abstraction 不能遮蔽模型差異；fallback 與 routing policy 需要 eval evidence，否則成功率與成本改善可能只是把 failure mode 轉移到另一個供應商。
- [AI Compute Infrastructure](../concepts/ai-compute-infrastructure.md): Gateway 是上層 application 能感受到 compute/provider fragmentation 的抽象邊界；它把不同雲、模型、延遲、價格與可用性差異轉成 routing decision。
- [LLM Agents](../maps/llm-agents.md)
- Related prior sources: [Welcome to The AI Systems Engineer Journey](welcome-to-the-ai-systems-engineer.md), [Hidden Technical Debt in Agentic Systems](hidden-technical-debt-in-agentic-systems.md), [Building a Local Ambient Agent That Never Sleeps](building-a-local-ambient-agent-that-never-sleeps.md), [A Postmortem of Three Recent Issues](a-postmortem-of-three-recent-issues.md)

## Tensions Or Disagreements

- Provider-agnostic abstraction 會降低 lock-in，但也可能把模型差異藏得太乾淨。不同 provider 的 tool semantics、safety policy、context-window behavior、streaming events 與 latency profile 仍然需要被 eval 與 trace 看見；gateway 不應把這些差異全部抹平成一個不可觀測的黑盒。
- Cost-based routing 對大量 routine calls 很有價值，但不能只用單價決定模型。某些 task 的錯誤成本高於 token 成本；gateway policy 應該吃進 task class、risk level、eval score、latency SLO 與 fallback history，而不是只看 cheapest available deployment。
- Content policy fallback 可以把 user-visible refusal 變成成功 response，但也可能繞過 team 原本想維持的 safety boundary。這類 fallback 應被視為 policy decision，需要 logging、review 與明確用途，而不是單純當成可靠性優化。
- 文章用 LiteLLM 示範 gateway pattern，但 captured source 在 code walkthrough 前停止；這張卡只編譯架構與 production pattern，不驗證 Dockerfile、config 或 example client 的可執行性。

## Open Questions

- AI gateway 的最小 production contract 應包含哪些欄位：virtual key、team/user budget、model route、fallback chain、policy fallback、context fallback、trace sink、cost attribution、MCP registry 與 rollback path 是否都要版本化？
- Gateway routing policy 應如何和 agent eval harness 連動，才能知道某個 fallback 或 cheap-tier routing 真的改善 cost per successful task，而不是只降低單次 token cost？
- 哪些 model behavior 差異應暴露給 application 或 evaluator，哪些可以被 gateway adapter 安全地吸收？
- 當 MCP/tool routing 也進入 gateway 後，tool authorization、audit log、schema validation 與 prompt-injection defense 應由 gateway、agent harness 還是 application domain layer 擁有？
- 對早期 team 來說，何時應從 SDK-level provider abstraction 升級到 gateway-level abstraction？觸發條件是多 provider、多 team、多 app、cost attribution、fallback need，還是 credential governance？

## Merge Candidates

- AI gateway 應被視為 LLM/agent runtime 的 reverse proxy：集中處理 model routing、fallback、virtual keys、budgets、cost attribution、observability、MCP/tool routing 與 provider adapters。
- Model choice should be governed as runtime policy, not application code: app calls a stable API shape while gateway config owns provider selection, fallback, rate limits, and cost controls.
- Provider-agnostic abstraction should preserve eval visibility: adapters can normalize API shape, but traces and evals still need model/provider/deployment identity, failure reason, fallback path, latency, and cost.
- Content-policy fallback and context-window fallback are governance decisions, not only reliability optimizations; both should leave auditable traces and be tied to task risk.
