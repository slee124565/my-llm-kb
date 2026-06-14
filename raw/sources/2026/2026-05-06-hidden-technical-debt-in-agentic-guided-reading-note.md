# Hidden Technical Debt in Agentic Systems - Guided Reading Note

Source article: `raw/sources/2026/2026-05-06-hidden-technical-debt-in-agentic.md`
Article title: Hidden Technical Debt in Agentic Systems
Original author: Miguel Otero Pedrido
Original URL: https://theneuralmaze.substack.com/p/hidden-technical-debt-in-agentic
Published: 2026-05-06
Note type: User-provided guided reading note
Captured: 2026-06-13

Markdown Content:

2015 年，Google 發表了一篇影響深遠的論文《Hidden Technical Debt in Machine Learning Systems》。那篇論文提出了一個當時令人震撼、如今看來卻再合理不過的觀察：模型程式碼其實只佔整個機器學習系統很小的一部分，真正複雜、昂貴且容易累積技術債的，是模型周圍的資料管線、特徵工程、部署系統、監控機制與維運流程。那篇論文不只是指出了一個工程問題，更間接催生了後來的 MLOps、生產級機器學習平台，以及 ML Engineer 這個職業角色。

作者認為，2026 年的 Agent 領域正站在同樣的歷史節點上。過去幾年大家把焦點放在模型能力、Prompt 技巧與 Agent Demo，但當 Agent 開始進入企業環境與正式產品之後，人們逐漸發現，真正的挑戰不在模型本身，而在模型周圍那一整套支撐 Agent 運作的基礎設施。Agent 呼叫模型只是整個系統中的一個小盒子，真正會影響成本、穩定性、安全性與維護性的，是模型之外的所有東西。

文章首先指出，目前最被低估的一層是 Markdown Configs，也就是 Prompt、Skill、Sub-Agent 定義、Tool Description、Goal 文件等自然語言設定檔。大多數團隊把它們視為文件，但作者認為它們其實是 Agent 的原始碼。因為真正改變 Agent 行為的，往往不是 Python 或 TypeScript，而是這些 Markdown 檔案中的規則與指示。因此它們應該被視為第一級工程資產，納入版本控制、程式碼審查、差異比較、回滾機制與 Eval 驗證流程。換句話說，Prompt 不應該被當成筆記，而應該被當成程式碼管理。

接著作者談到模型層（Model Layer）。許多團隊在設計 Agent 時最常問的問題是「我們應該用哪個模型？」但作者認為這其實是錯誤的起點。更重要的問題應該是：「我們需要多少種模型？什麼任務應該由哪一種模型處理？」真正成熟的 Agent 系統不會讓所有事情都交給最昂貴的 Frontier Model，而是透過 Router、Model Fleet 與 Fallback Chain 形成一套分工架構。簡單任務交給小模型，複雜任務交給大模型，失敗時還有備援路徑。模型策略的本質不是追求最強模型，而是在成本、品質與穩定性之間取得平衡。

然後作者開始談 Agent Harness，也就是 Agent 的執行框架與編排系統。這是整篇文章最重要的觀念轉折之一。很多人認為 Agent 是 Prompt 加上 LLM，但作者認為 Agent 的本質其實是狀態機（State Machine）。真正的 Agent 不斷在「思考、行動、觀察、再思考」之間循環。無論是 ReAct、Plan-and-Execute 或 Reflexion，最後都會演變成一套狀態轉移系統。當團隊無法畫出 Agent 的狀態圖時，通常代表他們其實還不了解自己的系統。大部分生產環境中的 Agent 災難也不是模型失敗，而是狀態轉移設計錯誤，例如無限迴圈、錯誤重試、遺失轉移條件或無法終止的流程。

接下來作者進入 Tool Layer。這一章提出一個非常重要的觀點：Agent 並不是真的看見工具本身，它看見的是工具描述（Tool Description）。工程師往往花很多時間寫工具程式碼，卻忽略工具描述的重要性。然而對模型而言，工具描述才是它理解工具用途、適用情境與錯誤處理方式的唯一依據。作者甚至指出，重新設計 Tool Description 往往能大幅提升工具選擇準確率。因此 Tool Description 不應該只是註解，而應該被視為工具的 SOP 與契約（Tool Contract）。工具越多不代表系統越強，真正重要的是工具邊界是否清晰、錯誤是否可理解、行為是否可預測。

接著文章來到 Memory。作者直接挑戰一個流行觀念：向量資料庫不等於記憶系統。真正的 Agent Memory 其實是一個多層次架構。短期記憶負責目前任務的上下文與工作區；會話記憶負責維持同一段對話中的連續性；長期記憶則負責跨 Session 的知識與經驗保存。此外還可以進一步區分語意記憶、事件記憶與程序記憶。作者特別指出，許多團隊過度關注長期記憶與 Vector DB，卻忽略了真正最容易出錯的 Session Memory。許多 Agent 出現「剛剛才說過卻又忘記」的問題，往往不是長期記憶失敗，而是摘要系統與原始對話產生偏差。

之後作者進入 Agent Serving Infrastructure。這一章提出一個非常重要的觀念：Web 的工作單位是 Request，而 Agent 的工作單位是 Session。傳統 Web Request 通常短暫、無狀態且快速完成；Agent Session 則可能持續數分鐘、數小時甚至數天。Agent 大部分時間其實不是在推理，而是在等待工具、等待人類批准、等待 Webhook 或等待外部系統。因此 Agent Runtime 的核心問題不是 CPU，而是 Session Persistence，也就是如何在中斷後恢復狀態。作者進一步提出五個關鍵設計問題：任務如何進入系統、狀態存在哪裡、如何擴展、如何觀測，以及成本模型如何運作。這些問題共同構成了 Agent Runtime 的基礎。

接下來是 Observability 與 Tracing。作者認為，當 Agent 給出錯誤答案時，答案本身只是症狀，真正的錯誤通常發生在前面十幾個步驟之中的某一個環節。因此 Agent 系統必須具備完整的 Trace Tree，而不只是最終輸出紀錄。模型呼叫、工具呼叫、狀態轉移、重試行為、人工介入與成本累積都應該被完整追蹤。作者特別區分 Tracing 與 Monitoring。Tracing 是為了理解單次任務發生了什麼，而 Monitoring 則是觀察整體系統健康狀況。沒有 Replay 能力的 Agent 幾乎無法除錯，因此可觀測性是生產環境中的必要條件，而非附加功能。

在 Evaluation Harness 章節中，作者提出另一個非常強烈的觀點：如果沒有 Eval，你沒有產品，你只有 Demo。許多團隊修改 Prompt 後憑感覺判斷效果是否提升，但作者認為這種做法無法長期維持品質。成熟的 Agent 系統必須建立 Eval Framework，讓每次 Prompt、Model、Tool 或 Memory 的修改都能被驗證。作者介紹了四種評估方式：Reference-Based Eval、LLM-as-Judge、Trajectory Eval 與 Online Eval。尤其是 Trajectory Eval，它不只評估答案是否正確，更評估 Agent 是否走了正確的路徑。這與近年流行的 Verifier 與 Self-Healing Agent 概念高度一致，因為所有自我修正能力都必須建立在可驗證的基礎之上。

之後文章進入 Guardrails 與 Safety。作者提醒讀者，Prompt Injection 只是 Agent 安全問題中的冰山一角。除了使用者輸入的攻擊之外，Tool Output Injection、Memory Leakage、Cost Attack 與 Off-Policy Assistance 都是實際存在的風險。作者提出整篇文章最值得記住的一句話之一：寫在 Prompt 裡的規則只是願望，寫在程式裡的規則才是真的。企業不應依賴模型自律，而應透過權限控制、輸出過濾、人類批准機制與稽核紀錄來保證安全性。寄送 Email、刪除檔案、執行交易或部署程式等不可逆操作，都應該納入 Human-in-the-Loop 的治理架構。

最後，作者回到 AI Systems Engineer 這個角色本身。他認為 2015 年那篇 ML 技術債論文催生了 MLOps 與 ML Engineer，而今天 Agent 領域也正在經歷同樣的過程。未來最有價值的人才，不是最會寫 Prompt 的人，而是能夠理解並整合整張系統圖的人。從 Prompt、Model、Harness、Tool、Memory、Serving、Tracing、Eval 到 Guardrails，每一層都會影響最終系統品質。AI Systems Engineer 的價值不在於模型本身，而在於能夠將模型周圍的整個系統設計、治理、維運與持續改善。

如果把整篇文章濃縮成一句話，那就是：

**2015 年大家發現模型不是機器學習系統；2026 年大家再次發現，模型呼叫也不是 Agent 系統。真正的競爭力來自於模型之外那整套可觀測、可驗證、可恢復、可治理的工程體系。**
