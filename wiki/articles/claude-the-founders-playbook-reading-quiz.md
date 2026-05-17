# The Founder's Playbook: Building an AI-Native Startup｜閱讀測驗卷

- 文章檔案：`/Users/lee/ws/myKBs/my-llm-kb/raw/sources/2026/2026-05-06-claude-the-founders-playbook.md`
- 題型：單選題
- 題目總數：6 題
- 使用方式：先完成前半部題目，再看後半部答案與解說。

## 前半部｜選擇題

### 第 1 題

這篇文章對 AI-native startup 最核心的判準轉換是什麼？

A. 只要創辦人能用 AI 寫出產品，就可以跳過傳統 startup lifecycle。
B. AI 把執行速度大幅壓縮，因此創辦人的主要瓶頸轉向判斷、證據與系統設計。
C. AI 讓非技術創辦人不再需要理解產品或市場，只要會下 prompt。
D. AI-native startup 的主要優勢是比傳統公司更早募資與更快擴編。

### 第 2 題

在 Idea stage，文章最反對哪一種常見誤讀？

A. 使用 AI 做競品研究會讓創辦人更容易找到反方證據。
B. 先做 customer discovery 會拖慢速度，所以最好等 MVP 上線後再問用戶。
C. 可運作的 prototype 是驗證工具，不是 problem-solution fit 的證據本身。
D. 非技術創辦人應該先學會完整工程流程，再開始訪談客戶。

### 第 3 題

文章如何區分 Chat、Claude Cowork 與 Claude Code 這三種使用面？

A. 三者本質相同，只是 UI 不同，所以選哪一個不影響工作品質。
B. Chat 適合快問快答，Claude Cowork 適合跨檔案與連接系統的知識工作，Claude Code 適合直接處理 codebase。
C. Chat 只適合非技術創辦人，Claude Code 只適合技術創辦人，Claude Cowork 只適合大公司。
D. Claude Code 應該從 Idea stage 起承接所有工作，避免在不同工具之間切換 context。

### 第 4 題

文章所說的 agentic technical debt，最準確的意思是什麼？

A. AI 生成的程式碼通常語法錯誤很多，需要人工重寫。
B. AI 寫得太快，所以所有 MVP 都應該禁止使用 agentic coding。
C. 若缺少架構、scope、決策與 context 文件，每次 AI session 都可能重推一套不同假設，讓 codebase 漸漸失去一致性。
D. 技術債主要來自使用太多新框架，和 AI 是否參與無關。

### 第 5 題

在 MVP 到 Launch 的轉換中，文章提醒創辦人不要把什麼誤認為 product-market fit？

A. 早期 spike、朋友支持、投資人 portfolio 導流或 Hacker News 熱度。
B. 使用者留存、付費、推薦與多輪 iteration 後仍成立的需求訊號。
C. 預先設定 Day 7、Day 30、activation 與 retention 指標。
D. 請 AI 對 traction data 做 skeptical analysis。

### 第 6 題

到 Scale stage，文章認為最能形成防禦性的東西是什麼？

A. 使用最新模型本身，因為模型越新越難被競爭者取得。
B. 更大的團隊規模，因為 headcount 仍是 AI-native startup 的主要護城河。
C. 累積的 domain context、工作流整合深度、使用者行為資料回饋，以及 institutional knowledge 轉成產品能力。
D. 更快推出更多功能，因為使用者通常不會在意切換成本。

## 後半部｜答案與解說

### 第 1 題：B

- 正解理由：文章不是說 startup lifecycle 消失，而是說 AI 壓縮 execution layer，讓 founder 的稀缺工作上移到 problem selection、orchestration、evidence interpretation 與 system design。
- 錯誤選項分析：
  - A（過度延伸）：AI 確實壓縮流程，但文章仍保留 Idea、MVP、Launch、Scale 與各自 exit criteria。
  - C（反向誤讀）：文章強調非技術創辦人被解鎖，但不代表可以放棄產品、市場與判斷責任。
  - D（指標替換）：文章反而淡化 headcount 與 fundraising 作為進度指標，強調 lean by design 與 evidence。
- 最易誤選：A。因為文章多次說 timeline 被壓縮，容易誤讀成階段可以被跳過。
- 實用含義：看到 AI 加速時，先問「我的判斷與證據有沒有同步加速」，不要只看「我能不能更快做出東西」。

### 第 2 題：C

- 正解理由：文章明確說 prototype 是 pressure-testing prop，真正 validation 來自與潛在使用者的對話、反方證據與 problem-solution fit。
- 錯誤選項分析：
  - A（概念混淆）：AI 可以幫忙找反方證據，這是文章支持的做法，不是它反對的誤讀。
  - B（反向誤讀）：文章強調先驗證再建構，並警告「building for validating」的錯置。
  - D（邊界忽略）：文章不是要求非技術創辦人先變成完整工程師，而是讓 domain expertise 更容易轉成產品探索。
- 最易誤選：B。因為 AI 讓 build 變便宜，創辦人很容易把「先上線再說」包裝成速度優勢。
- 實用含義：prototype 的任務是讓對話更真實，不是替代訪談、反證與需求判斷。

### 第 3 題：B

- 正解理由：文章把三個 Claude surface 對應到不同工作：Chat 做快速交換，Claude Cowork 做跨來源知識工作與 operational workflow，Claude Code 做 codebase 層的建構、測試與修改。
- 錯誤選項分析：
  - A（指標替換）：三者共享底層模型不代表工作面相同；workspace、工具、檔案與持久 context 都會改變效果。
  - C（過度分類）：文章沒有用創辦人背景或公司規模硬切工具，而是按任務型態選 surface。
  - D（行動誤用）：Idea stage 需要 research、validation、訪談設計與反方推理，不應把所有工作都壓到 coding surface。
- 最易誤選：A。因為同一模型容易讓人忽略 runtime surface 的差異。
- 實用含義：選工具時不要只問「哪個模型比較強」，要問「這個任務需要哪種 context、工具、權限與驗證面」。

### 第 4 題：C

- 正解理由：文章把 AI technical debt 描述為缺少 persistent context 造成的結構漂移：沒有 specs、architecture constraints、CLAUDE.md 與 scope 文件時，每次 session 都會重新推論並可能偏離原本設計。
- 錯誤選項分析：
  - A（表面化）：文章不是聚焦語法錯誤，而是聚焦可運作但結構不一致的 codebase。
  - B（過度延伸）：文章支持用 Claude Code 建 MVP，但要求用 guardrails 約束。
  - D（概念混淆）：傳統技術債仍存在，但文章特別指出 agentic coding 讓缺少 context 的漂移更容易累積。
- 最易誤選：D。因為「技術債」常被理解成一般工程問題，容易忽略 AI session memory 與外部化文件的作用。
- 實用含義：每次讓 coding agent 動手前，先確認 architecture、scope、tradeoffs、session log 與 measurement criteria 是否能被它讀到。

### 第 5 題：A

- 正解理由：文章提醒 early traction 常來自短暫外力，例如朋友、投資人關係或社群曝光，這些不等於長期 retention、revenue、referral 或 repeatable growth。
- 錯誤選項分析：
  - B（反向誤讀）：這些才是文章用來判斷 PMF 的高品質訊號。
  - C（行動誤用）：文章鼓勵在 launch 前建立 measurement framework，而不是事後挑好看的數字。
  - D（反向誤讀）：文章建議讓 Claude 對 traction data 做反方分析，以避免自我確認。
- 最易誤選：A 之外最容易混淆的是 B，因為早期數字都可能看起來像 traction，但文章要求看訊號是否跨時間與多輪 iteration 成立。
- 實用含義：PMF 不看單次熱度，要看用戶是否回來、付費、推薦，且 founder 不再需要一直用人工推力維持使用。

### 第 6 題：C

- 正解理由：文章在 Scale stage 把 moat 放在累積深度：domain expertise、workflow lock-in、user interaction data、institutional knowledge、integration depth 與可審計的成熟 operation。
- 錯誤選項分析：
  - A（指標替換）：最新模型是可用基礎設施，不是長期防禦本身；競爭者也可能取得相近能力。
  - B（反向誤讀）：文章強調 lean startup 可以像更大組織運作，不把 headcount 當主要 moat。
  - D（邊界忽略）：功能速度有價值，但 Scale stage 更重視是否嵌入使用者 workflow、資料回饋與 switching cost。
- 最易誤選：A。因為 AI-native startup 很容易把模型能力誤認為公司自己的防禦性。
- 實用含義：建立 moat 時，優先問「我們累積了哪些競爭者買不到、補不回、也難以從外部觀察的 context 與 workflow depth」。

## 味覺訓練提示

- 比較能力：練習分辨「AI 讓執行變快」和「AI 讓判斷變好」是兩件事；前者可能放大錯誤，後者需要 evidence gate。
- 延伸能力：把文章的 stage gate 套到自己的 agent workflow：每擴大一段 agent 權限前，先定義 evidence、scope、rollback、security 與 human escalation。

## Writeback Pointers

- 留在單篇層：Anthropic 產品線的具體命名、Claude Startups Program、Founder stories 與資源清單。
- 可上升到 theme / playbook / map / series：AI-native startup 的 stage gates、agentic technical debt as state debt、runtime surface selection、founder-from-operator-to-orchestrator、domain context plus workflow lock-in as moat。
