# OpenClaw Takes Over The Internet

## Source

- URL: unknown; imported transcript from a workspace blog folder named for a different episode title
- Author: Peter Steinberger interview with Harry Stebbings
- Published: 2026-02-24
- Captured: 2026-04-10
- Raw file: `raw/sources/2026/2026-02-24-openclaw-takes-over-the-internet-peter-steinberger.md`
- Imported from workspace path: `blog/2026-02-24-openais-codex-lead-why-coding-as-we-know-it-is-over-20vc-with-harry-stebbings/2026-02-24-openais-codex-lead-why-coding-as-we-know-it-is-over-20vc-with-harry-stebbings.md`
- Source note: workspace path title points to an OpenAI Codex lead / 20VC episode, but the transcript body is an OpenClaw interview titled `OpenClaw takes over the internet`

## Main Claims

- OpenClaw 的核心差異不是更強的雲端模型，而是讓 agent 直接在使用者自己的電腦上運行，因而能接觸本地資料、裝置與現成工具
- 對 personal agent 來說，理想介面不是 command-heavy terminal orchestration，而是 conversation-first 的「像和朋友說話」體驗，把 session、folder、model selection 等複雜度藏起來
- user-owned memory 應該留在使用者可直接控制的資料層，例如本機 markdown files，而不是被鎖在模型公司的 memory silo 裡
- 很多 agent 能力不必靠專屬 protocol；CLI-first tooling 與把 MCP 轉成 CLI 的做法，在本地 agent workflow 中可能比原生 MCP integration 更簡單且更可操作
- coding model 的價值不只在寫 code，而在 creative problem solving；一旦 agent 能操作真實環境，它會開始取代許多只是管理資料與流程的 app
- system prompt、identity files、`soul.md` 這類人格與價值觀 artifact，會直接影響 personal agent 的可用性與長期互動品質

## Why It Matters

這篇重要的不是它是否準確預言「app 將消失」，而是它提供了一個和 OpenAI Codex 幾乎互補的實戰視角。Codex 強調 isolated async coding agent、verifiable evidence 與 repo-local system of record；OpenClaw 這篇則強調 local personal agent、memory ownership、conversation-first steerability，以及 CLI-over-protocol 的極簡主義。兩者放在一起看，能更清楚區分「coding agent 的最佳工作面」和「personal agent 的最佳工作面」未必相同。

## Relation To Existing Concepts

- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [LLM Agents](../maps/llm-agents.md)
- [Codex Workflows](../maps/codex-workflows.md)

## Tensions Or Disagreements

- `80% of apps will go away`、`classical MCP crap` 這類說法帶有強烈個人立場，適合作為設計刺激，不適合直接當成穩定結論
- OpenClaw 所描繪的本地全權限 agent 很有吸引力，但也把安全性、誤操作、資料洩漏與權限治理風險推到最前面
- conversation-first 介面降低了日常摩擦，但也可能把原本顯式可控的 session 邊界、tool routing 與 execution audit 藏起來
- 來源本身是訪談逐字稿而非結構化 essay，因此部分觀點比較像即興 framing，而非經過收斂的設計原則

## Open Questions

- 哪些屬於 Codex workflow 的 repo-local patterns，可以轉譯到 personal agent，而不把互動變得過重
- user-owned markdown memory 要如何同時滿足 portability、privacy 與 machine readability
- CLI-first 何時真的比 MCP 更好，何時只是把結構化能力外包給 shell glue
- personal agent 的人格 artifact，例如 `identity.md`、`soul.md`，是否應視為 externalized state 的一部分

## Merge Candidates

- user-owned markdown memory is a form of externalized agent state, not just app data
- conversation-first local agents can trade explicit session management for lower human friction and higher steerability
- CLI-first tool surfaces can outperform bespoke agent protocols when the real requirement is direct local operability
