# Coding 被解掉之後，軟體工作還剩下什麼？Boris Cherny 對 Claude Code 與下一代 Builder 的判斷

- Source: https://www.youtube.com/watch?v=We7BZVKbCVw
- Based on: `youtube_transcript_en.auto.chaptered.md`
- Note: 本文依正版英文 transcript 與 YouTube chapter 結構重寫，保留 Boris Cherny 的核心原意與論證方向，非逐字翻譯。

## 引言：這場訪談真正談的不是寫 code，而是工作單位正在改變

如果只截取最吸睛的一句，這場訪談會被總結成：「Claude Code 負責人 Boris Cherny 已經 100% 用 AI 寫 code，而且從 2025 年 11 月以來沒有手動改過一行。」但那其實不是最重要的部分。

真正更關鍵的是 Boris 對整個軟體工作型態的判斷：**當 coding 逐漸被解掉，真正稀缺的能力會往更高層移動，從手寫程式碼轉向定義問題、吸收回饋、安排優先順序、跨角色協作，以及驅動 agent 持續把事情做成。**

這也是為什麼他不只是把 Claude Code 看成「更強的 coding tool」，而是把它放在一條更長的演進軸線上：從 coding，到 tool use，到 computer use，再到更一般化的 knowledge work。對他來說，這不只是產品演進，也是 AI 能力逐步外溢的自然結果。

## Introduction to Boris and Claude Code：Claude Code 的影響，已經超過寫程式本身

訪談一開始，主持人直接把 Claude Code 定位成過去一年最具代表性的工程工作變化之一。Boris 也沒有回避這種尺度。他承認，當看到類似「Claude Code 已經寫下相當比例 GitHub commits」這類訊號時，自己也覺得非常誇張，但更讓他在意的其實不是當前佔比，而是增長速度還在加快。

這個觀點很重要。因為如果只是已經很大，那還可以當成某個市場份額問題；但如果連成長速度都持續加速，那代表這不是一次性 adoption，而是整個工作方式正在改變。

而這種改變也不只停留在工程師。Boris 多次提到，Claude Code 與後續的 co-work 之所以關鍵，不是因為它們只是新產品，而是因為它們第一次讓更多人感受到 agent 不再是抽象概念，而是能在真實工作裡採取行動的系統。

## Why Boris briefly left Anthropic for Cursor (and what brought him back)：回到 Anthropic，不是因為產品，而是因為 mission

Boris 短暫離開 Anthropic 去 Cursor，又很快回來，主持人把這段拿來當開場提問。這段回答提供了理解他整個 worldview 的一把鑰匙。

他承認自己很喜歡 Cursor，也很欣賞團隊，但他很快發現，真正讓他留在 Anthropic 的不是單純「能做有趣產品」，而是更深一層的 mission。對他來說，AI 的能力已經大到足以改變整個世界，因此自己想待在一個把 safety 當成核心動機的地方。

這個背景會影響他後面對產品與 agent 的很多判斷。因為在他眼裡，Claude Code 並不是一個孤立的 productivity feature，而是更大能力系統的一個可觀察切面。也因此，他談產品時常常會同時談 safety、能力外溢，以及組織與社會要怎麼接住這些變化。

## One year of Claude Code：一年時間，整個 profession 的工作習慣已經變了

當主持人追問過去一年 Claude Code 帶來的變化時，Boris 的重點不是自我表功，而是承認連自己都低估了速度。他提到，公開世界裡看得到的資料已經很驚人，而私有 repo 裡的採用程度只會更高。

他也強調，對 Anthropic 而言，這件事從來不是「做一個 coding 小工具」而已。團隊本來就在沿著一條能力軸推進：先讓模型擅長 coding，再讓它擅長 tool use，接著是更強的 computer use。Claude Code 是這條路線第一次真正讓人看見能力落地的產品。

這也說明為什麼在 Boris 的描述裡，Claude Code 從來不是某個靜態產品，而是能力面向的一個窗口。它讓人第一次真切感受到，模型已經不只是回答問題，而是可以真的「做事」。

## The origin story of Claude Code：它一開始甚至不是一個大家立刻看懂的產品

Boris 回頭講 Claude Code 的起源時，有一個很鮮明的細節：最早他在內部 demo 時，反應其實非常平。因為在當時，多數人對 coding product 的想像還是 IDE 裡的功能，而不是 terminal 裡的一個 agent。

真正改變他判斷的，是模型開始展現出使用工具的能力。當模型拿到工具之後，不只是照指令輸出，而是能自己推理如何用它解問題，這讓 Boris 意識到，事情的本質已經變了。

他也因此做出一個很關鍵的產品決定：**在模型高速進步的時期，產品不要做得太重。** 早期選擇 terminal，不是因為那是最終理想形態，而是因為它最輕，最能跟得上模型進步速度。若太早綁定某種較重的 form factor，反而會拖慢學習與迭代。

這裡其實已經能看到 Boris 很典型的產品觀：先用最小結構接住能力，再看使用者是否真的把它納進 workflow，而不是一開始就用完整包裝去定義它。

## How fast AI is transforming software development：真正讓人失去直覺的，是變化快到指數化

Boris 提到一個很有代表性的場景：2025 年中他在公開場合預測，到年底工程師可能已經不再需要 IDE 才能寫 code，當時現場有人倒吸一口氣，覺得這太誇張。

但他的意思其實不是在做激進表態，而是說，如果你真的用指數成長去看 adoption 與能力進展，很多看似離譜的結論只是線條自然延伸後的結果。問題不是這些變化會不會發生，而是人的直覺通常跟不上 exponentials。

這種認知框架也解釋了他為什麼對「coding 大致被解掉」這件事講得這麼直接。不是因為他刻意挑釁，而是因為從他的觀察角度來看，對他所做的那類工程工作，這件事其實已經在發生。

## The importance of experimentation in AI innovation：很多突破不是 roadmap 推出來的，而是試出來的

Boris 多次回到同一個母題：很多最重要的 AI 產品創新，不是照 roadmap 推出來的，而是靠大量原型、試驗與對能力邊界的直接碰撞。

他甚至說得很白，innovation 沒有一條清楚 road map。你必須給人足夠的心理安全感，讓他能試很多可能失敗的想法，同時又能在方向錯時迅速止損。早期的 Claude Code 就是在這種條件下長出來的。

這也是他後面談團隊原則時會一直強調 speed、underfunding 與不要太早最佳化的原因。對他來說，AI 產品不是先把流程設計得很完美再執行，而是先高頻地試出一條能成立的路。

## Boris’s current coding workflow (100% AI-written)：人沒有退出，只是從「寫」移到「判斷與驗收」

Boris 對自己當前 workflow 的描述很值得細看。表面上他是 100% 用 Claude Code 寫 code，但這不等於整個流程都不需要人。

他明確提到幾個仍然重要的 human checkpoints：

- 他還是會看 code
- 團隊仍保留 human review
- Claude 也做自動 code review，但不是唯一關卡
- 對會實際執行、會影響他人的程式碼，仍然需要確認 correctness 與 safety

換句話說，最劇烈被抽掉的是「手動輸入程式碼」這個環節；但更高層的判斷、風險意識與最終負責並沒有消失。這是這波轉變很容易被誤解的地方。

## The next frontier：下一個 bottleneck 不是寫 code，而是 deciding what to build

當 coding 被大幅加速後，新的瓶頸自然往上移。Boris 認為接下來最值得注意的是，Claude 已經開始不只寫 code，而是會看 feedback、看 bug reports、看 telemetry，進一步提出該修什麼、該做什麼。

他描述的使用方式其實相當直接：把 Claude 指向一條充滿內部回饋的 Slack thread，讓它先收斂出問題與建議，甚至起草 PR。這代表 agent 開始接手的不只是 implementation，而是初步的產品整理與優先順序形成。

這對傳統產品分工會是很大的變化。因為當 AI 不只做 execution，而開始參與「從混亂訊號中找出方向」，很多角色邊界就會鬆動。

## The downside of rapid innovation：模型進步太快，連老手也會被自己的舊習慣拖住

Boris 提到一個很值得記住的副作用：模型進步得太快，連最早大量使用它的人，也會不小心拿舊能力模型來看待新模型。

他舉的例子是 memory leak debugging。按過去訓練，工程師會自然地打開 heap snapshot、用傳統工具慢慢查；但團隊裡較新的工程師，直接讓 Claude Code 去做，而且做得更快。這件事提醒他，最大的限制有時不是模型能力，而是人類自己對「這種事應該怎麼做」的舊直覺。

這也是為什麼他後面會一直說，要刻意站在 frontier 上，因為一旦你停止重新檢查能力邊界，就會低估 agent 已經能做到什麼。

## Principles for the Claude Code team：速度、低配啟動、讓 agent 成為預設

談到團隊原則時，Boris 有幾個很鮮明的點。

第一個是 **underfund things a little bit**。這不是為了摳成本，而是為了讓少數工程師在有限資源下自然把 AI 用到極致，逼出新的工作方式。

第二個是 **if you can do it today, do it today**。對他來說，速度不是壓榨，而是產品學習速度的根本來源。Claude Code 早期能在競爭激烈的環境裡站穩，一個核心優勢就是快。

第三個是讓 Claude 成為預設工作方法，而不是額外加分項。當團隊共識變成「任何事情先想能不能讓 Claude 做」，整個組織的 output ceiling 就會被抬高。

## Why you should give engineers unlimited tokens：早期最不該做的，就是太早開始省 token

Boris 對 token 的態度非常清楚：在探索期，不要過早最佳化成本。

他的邏輯是，早期真正稀缺的是找到有效工作模式，而不是省下一點模型花費。只要還在試驗階段，讓工程師能大量使用 tokens，去推到能力邊界、找到新的可行 workflow，價值遠大於提前節省成本。

等到某條路被證明真的可行，而且規模開始放大，再來談換更便宜模型、調整結構、優化成本，那才是對的時點。

這個觀點聽起來像在替模型廠商說話，但 Boris 的論點其實很務實：相對於工程師薪資與整體嘗試成本，早期這些 token 往往不是最大的支出；而太早保守，反而更容易錯過真正有價值的突破。

## Will coding skills still matter in the future?：他不是否定程式設計，而是把它放回手段的位置

當主持人問他會不會懷念手寫 code，Boris 的回答透露出一條很穩定的主線：他一直把 programming 看成做事的方法，而不是目的本身。

他承認語言、型別系統、函數式編程裡有美感，也理解有人就是喜歡手寫 code。但在他的世界觀裡，programming 的形式本來就一直在變。從硬體、打孔卡、虛擬機、現代語言到 agent，每一層都是更高抽象的遷移。

所以他不把這件事看成單純的 skill atrophy，而比較像是抽象層再次上移。短期內懂底層仍然重要，但長期看，很多人未必還需要頻繁親手寫 code。

## The printing press analogy for AI’s impact：如果人人都能 program，真正被改變的是文明分工

Boris 用 printing press 當比喻，不是為了浪漫化 AI，而是想指出：當某種原本只屬於少數人的能力被普及化，後果通常不是「原有工作更快做完」而已，而是整個社會能組織起來的方式都會變。

在他的想像裡，未來如果人人都能用自然語言與 agent 建構軟體，那麼 programming 會像 literacy 一樣成為更普遍的能力。屆時最大的變化，不是工程師更省時，而是原本沒有能力自己動手的人，也能直接把問題轉成可執行系統。

這也是他認為變化會很痛苦、但同時也極具創造性的原因。

## Which roles will AI transform next?：PM、Designer、Engineer 的邊界會越來越模糊

Boris 最直接的一個判斷是：短期內這些角色還存在，但它們之間的重疊會越來越大。

在他現在的團隊裡，幾乎所有人都會寫 code。PM 會寫，EM 會寫，Designer 會寫，其他職能的人也會寫。這不代表專業性不再重要，而是說，當 coding 門檻被降低之後，單靠某個職能的傳統邊界已經不足以描述價值來源。

他甚至認為，到了某個時間點，「software engineer」這個稱呼本身都可能淡化，最後留下來的是更泛化的「builder」。

## Tips for succeeding in the AI era：站上前沿，並且盡量成為 generalist

如果把 Boris 給個人的建議壓縮成兩點，大概就是：

- 不要怕工具，盡可能站在 frontier 上，親手試
- 不要只把自己困在單一職能裡，盡量成為 generalist

他反覆強調，未來被獎勵最多的人，不只是最會用 AI 的人，而是能跨設計、產品、工程、商業與使用者理解一起思考的人。換句話說，AI 讓 execution 成本下降後，整體判斷能力與跨面向整合能力就會更值錢。

## Poll: Which roles are enjoying their jobs more with AI：多數人更喜歡工作了，但不同角色感受不一樣

訪談裡還談到一個有趣觀察：工程師與 PM 多數表示工作變得更有趣，但設計師的感受更分歧。

Boris 對這點的反應不是急著下定論，而是想回到使用情境本身看。因為在 Anthropic 的環境裡，許多設計師本來就相對技術化，也因此更容易直接享受到 agent 帶來的自由度。

這個片段的價值在於提醒我們，AI adoption 並不是抽象平均值，而是非常依賴角色實際 workflow、心理安全感與工具是否貼近日常工作。

## The principle of latent demand in product development：產品不是問出來的，而是被使用者「濫用」出來的

Boris 談 latent demand 的部分，是整場訪談裡很有產品含金量的一段。

他的核心意思是：很多需求不是使用者一開始就能清楚說出的，而是當你把一個能力放進真實工作環境後，使用者開始以你沒預期的方式使用它，這些「偏離原始設計」的行為反而揭示了更真實的需求。

對 Claude Code 是如此，對 co-work 也是如此。當大家開始把它用在原本不屬於「工程工具」範圍的工作上，團隊反而更能看到下一步產品該往哪裡長。

## How Cowork was built in just 10 days：這不是 miracle，而是模型能力成熟後的自然結果

co-work 被做出來的速度很快，但 Boris 並不把它講成傳奇故事。他的重點比較像是：一旦底層能力到了，很多過去不成立的東西就會突然成立。

團隊的價值不只是執行力，而是能在能力成熟到某個點時，快速辨認出「現在該把它包成什麼產品」。

這再次呼應了他對產品工作的理解：不是從零設計一個完全獨立的新世界，而是持續觀察模型與使用者互動，等到兩者交會出清晰訊號時，迅速把它具體化。

## The three layers of AI safety at Anthropic：安全不是附加條件，而是能力外溢後必須一起升級的東西

當產品從 coding 走向更一般化的 agent work，Boris 很自然地把話題帶回 safety。

在他的框架裡，模型變得更會使用工具、能採取更多行動，本質上既是產品進步，也是風險升高。因此安全不能被視為事後補件，而必須與產品、模型、feedback loop 一起被設計。

這也是為什麼他談 co-work 時會強調它仍然是 research preview。不是因為它沒用，而是因為這類 agent 一旦進入更廣泛的工作流，就必須連 observability、sandbox、權限與失誤模式一起考慮。

## Advice for building AI products：先把工具給模型，不要試圖替模型預先寫死一切

訪談後段，Boris 給了很多做 AI product 的建議，裡面有一條很值得記住：**不要太早嘗試把一切 hardcode 進流程裡，先給模型工具，再看它怎麼完成任務。**

他的邏輯是，很多產品團隊太想控制模型，所以會預先把 interaction path 寫得很死。但如果模型其實已經能靠工具自己找到完成任務的方法，過度限制反而會損失能力。

這與他前面對 Claude Code 的 origin story 完全一致。真正的突破，往往來自你願意先把能力放出去，觀察它會長成什麼樣。

## Pro tips for using Claude Code effectively：把 agent 當成多工系統，不要只把它當聊天室

談到實作層面的使用方式，Boris 最實際的建議之一是：不要把 agent 當成單執行緒對話框。

他自己工作時常常同時開著多個 agents，讓它們平行處理不同任務。這種工作法背後的假設已經不同於傳統 IDE 輔助工具了。它不再是你寫到卡住時叫它補一段，而是你把多條工作線同時交給它跑，再自己切回更高層的監督與決策。

這其實很接近他對未來 builder 的想像：不是更快地自己做完每件事，而是更像在 orchestrate 一群可用的執行者。

## Thoughts on Codex：他不迷戀競品比較，而更關心自己產品與使用者的真實回路

當主持人問到對 Codex 的看法時，Boris 的態度相對節制。他沒有把重點放在競品比較，而是回到一個很 Anthropic / 很 Boris 的位置：真正重要的不是別家做了什麼，而是自己的產品能否持續從使用者回饋裡變好。

這個反應其實很一致。他前面大部分回答都不是在談「贏過誰」，而是在談「如何讓回路更短、讓能力更快進入工作現場、讓團隊更快學到真實需求」。

## 結語：Boris 所說的 Builder，不是新稱呼，而是新工作單位

整場訪談聽下來，Boris 最重要的判斷其實可以濃縮成一句話：**當 coding 逐漸成為已解問題，真正有價值的人會是那些能定義方向、整合跨職能訊號、有效驅動 agent 與組織一起前進的人。**

這也是他為什麼會認為「software engineer」這個稱呼本身都可能慢慢淡化。因為未來最關鍵的工作單位，不再只是「會寫 code 的人」，而是能把：

- 問題定義
- 用戶回饋
- 工具能力
- 產品判斷
- 風險意識
- 執行節奏

組裝成一條可持續推進路徑的人。

如果要給這個角色一個名字，Boris 用的是 **builder**。這不是比較潮的新 title，而是他對下一代知識工作者的工作模型：不是手上做每一件事的人，而是最懂得如何讓人與 agent 一起把事情做成的人。
