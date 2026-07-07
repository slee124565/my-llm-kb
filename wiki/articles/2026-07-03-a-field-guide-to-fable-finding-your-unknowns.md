# A Field Guide to Fable: Finding Your Unknowns

## Source

- URL: https://x.com/i/status/2073100352921215386
- Author: Thariq @trq212
- Published: 2026-07-03
- Captured: 2026-07-07T19:19:04+08:00
- Raw file: `raw/sources/2026/2026-07-03-a-field-guide-to-fable-finding-your-unknowns.md`
- Source note: X.com long-form post / article about using Claude Fable 5 by turning vague task intent into explicit unknowns, prototypes, references, implementation notes, explainers, and review quizzes.

## Main Claims

- 這篇的核心 framing 是「map is not the territory」：prompt、skill、context、plan 都只是地圖；真正的領地是 codebase、使用者需求、既有 constraints、reviewer judgment 和實作中才會浮現的邊界。Agentic coding 的失敗常不是模型完全不會，而是地圖沒有把關鍵 unknowns 表達出來。
- 作者把 agentic coding 的不確定性分成四類：已知已知（known knowns）是 prompt 裡已經寫出的需求；已知未知（known unknowns）是你知道還沒想清楚的問題；未知已知（unknown knowns）是你看到才知道對不對的品味、直覺與隱性標準；未知未知（unknown unknowns）是你根本還不知道該問什麼。越長、越開放的任務，這四類 unknowns 越會主導結果。
- 更強的模型會把 bottleneck 往人類的「澄清 unknowns」能力推。Fable 5 讓作者感覺工作品質不再主要受限於模型能不能執行，而是受限於人能否讓模型看見自己真正要什麼、哪些地方可以自主 pivot、哪些地方必須保守。
- 單純預先 planning 不夠。Unknowns 可能在實作深處才出現，也可能反過來證明原本問題就該換解法；因此更好的 workflow 是 pre-implementation、during implementation、post implementation 都有找 unknowns 的機制，而不是一次性寫完 spec 後就要求 agent 照做到底。
- Pre-implementation 的手法包括 `blindspot pass`、brainstorm / prototype、interview、reference、implementation plan。這些不是形式化文件，而是低成本探索工具：讓 agent 幫你找 unknown unknowns、做多個可反應的 artifact、追問會改變架構的 ambiguity、讀 source-code reference，並把最可能會變的 data model、type interface、UX flow 放到 plan 前面。
- During implementation 的核心是讓 agent 留下 `implementation-notes.md` 或等價 artifact。當 agent 遇到 edge case、偏離原 plan、採取保守選項或做出重要 tradeoff 時，這些決策不應只留在 conversation 裡；它們應成為下一輪修正、review、重做或知識回收的材料。
- Post implementation 的兩個實用 pattern 是 pitch / explainer artifact 與 quiz。前者把 prototype、spec、implementation notes 包成 reviewer 能快速理解的 evidence packet；後者讓人類在 merge 前確認自己真的理解 diff 的行為影響，而不是只看 code diff 的表面。
- 文章對 prompt design 的提醒是：太具體會讓 agent 在應該 pivot 時仍照指令走；太模糊則會讓 agent 用一般 best practices 補空白。好的 steerability 不是把 prompt 寫得無限細，而是讓 agent 知道你的起點、經驗、判斷標準、可變區和不可變 constraints。

## Why It Matters

這篇值得收進 `my-llm-kb`，因為它把 repo 近期幾條線接在一起：Claude Code loops、Codex Goals、skills、long-running harness、externalized state、prompt migration，以及 human-supervised agent ops。前一篇 `Getting Started With Loops` 提供的是 trigger / stop condition / primitive 的 taxonomy；這篇補上的是更前段的問題：在 loop 開始之前，人和 agent 要如何發現「其實還不知道什麼」。

對工程與產品工作最有用的讀法是：agent collaboration 的品質不只由 prompt 清楚度決定，也由 unknown discovery surface 決定。若需求還充滿未知已知和未知未知，直接進入 implementation loop 會讓 agent 在錯的地圖上跑得更快。Blindspot pass、prototype、interview、reference、implementation notes、explainer、quiz 這些 artifact 的價值，是把模糊的 taste、domain gap、review standard 和 implementation deviation 逐步外部化。

這也修正了「更強模型等於更少流程」的簡化想法。更強模型確實能處理更多 ambiguity，但它也會更快產生大量高品質但可能偏離意圖的 work。人類 supervisor 的工作因此不是把所有細節先寫死，而是設計一個能持續找 unknowns、讓 agent 適度 improvisation、並把重要偏差留下證據的 workflow。

## Relation To Existing Concepts

- [Prompt Migration And Agent Steerability](../concepts/prompt-migration-and-agent-steerability.md): 本文補上一個比 outcome-first prompt 更細的 steering layer：當人還不知道完整 outcome 或 success criteria 時，應先用 blindspot pass、interview、prototype 和 reference 把 unknowns 轉成可討論的 prompt contract。
- [Externalized Agent State](../concepts/externalized-agent-state.md): `implementation-notes.md`、prototype、spec、pitch / explainer、quiz 都是 state artifact。它們把「為什麼改變 plan」、「哪些地方仍不確定」、「reviewer 需要理解什麼」從一次性 conversation 搬到可回看、可交接、可審計的文件。
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md): 對長任務而言，unknown discovery 本身應該被視為 harness phase。若 initializer、planner 或 coding session 沒有留下 blindspot、deviation、prototype validation 和 reviewer comprehension 的證據，長時間執行很容易忠實完成錯誤 spec。
- [Codex Workflows](../maps/codex-workflows.md): 雖然文章以 Claude Fable / Claude Code 為主，但對 Codex 也直接可用：在進入 `/goal`、long-horizon delegation 或 multi-file refactor 前，先讓 agent 做 blindspot pass、提出 architecture-changing questions、做 throwaway prototype 或讀 reference，比單純要求「implement this」更能降低返工。
- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md): 人類 supervisor 不只是批准輸出，也要揭露自己的隱性 judgment。Quiz pattern 特別有價值，因為它把 human approval 從「看起來可以」提升成「我理解這個 change 的行為和風險」。
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md): 若 unknowns、implementation deviations、review explanations 和 post-merge lessons 會影響未來 agent 行為，就應該回寫 repo-local docs、plans、skills 或 article cards，而不是只留在聊天記錄裡。

## Tensions Or Disagreements

- 文章稱 Fable 是第一個讓作者感覺瓶頸轉到 unknown clarification 的模型，這是作者工作流中的主觀觀察，不應直接升級成穩定模型比較結論。可保留的是 workflow pattern，而不是對特定模型的普遍評價。
- Prototype 和 HTML artifact 很適合找 visual / UX unknown knowns，但若沒有明確標示 throwaway 或 spike boundary，很容易被誤認為正式架構方向。Prototype artifact 應該帶有「要驗證什麼、不驗證什麼」的 scope。
- Quiz 能提高 reviewer comprehension，但也可能被 agent 設計得太容易或太迎合 reviewer。對高風險 change，quiz 應搭配測試、diff review、evidence packet 或第二 reviewer，而不是取代正式 verification。
- Implementation notes 有助於 externalized state，但若沒有 owner 和整理節奏，也可能變成過期 decision dump。真正應回收的是會影響下一次實作、review 或 skill / docs 更新的 deviation。

## Open Questions

- 在 Codex / Claude Code workflow 裡，哪些任務應先做 blindspot pass，哪些可以直接進 implementation？
- Unknowns artifact 的最小 contract 應包含哪些欄位：assumption、risk、decision needed、prototype evidence、owner、resolution status？
- `implementation-notes.md` 應該是每個長任務的暫存 artifact，還是只在 plan deviation、domain uncertainty 或 multi-session work 時啟用？
- Post-implementation quiz 應如何設計才不會只是 agent 自問自答，而能真的測出 reviewer 是否理解 behavior、rollback path 和 residual risk？
- 對 visual / product / architecture 這類 unknown knowns 很多的工作，prototype、reference、interview 和 plan review 的最佳順序是什麼？

## Merge Candidates

- Agentic coding 的核心能力之一，是把 known knowns、known unknowns、unknown knowns 和 unknown unknowns 逐步轉成可驗證的 task contract。
- 更強模型會把 bottleneck 往 human judgment externalization 推；人類需要說明起點、隱性標準、可變區、不可變 constraints，以及允許 agent pivot 的條件。
- Pre-implementation 應把 blindspot pass、brainstorm / prototype、interview、reference 和 implementation plan 視為降低返工的 cheap discovery loop。
- During implementation 應把 plan deviation、edge case、保守選項和重要 tradeoff 寫進 implementation notes，讓下一輪 agent 或 reviewer 能接手。
- Post implementation 的 explainer 和 quiz 是 human-supervised review artifact；它們補足 code diff 無法直接呈現的行為理解、approval context 和 residual risk。
- Prototype artifact 應明確標示 scope：它要幫人類發現 taste / UX / architecture unknowns，不應自動變成正式 implementation commitment。
