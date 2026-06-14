# Mastering Codex (Mobile) for Engineering

Source: https://x.com/i/status/2066082395107758564
Canonical status: https://x.com/i/status/2066082395107758564
Author: Thomas Ricouard @Dimillian
Status ID: 2066082395107758564
Published: 2026-06-14
Captured at: 2026-06-15T06:57:55+08:00
Extraction: myAgentTools/xcom-article-import
Extraction file: `/Users/lee/ws/myKBs/myAgentTools/xcom-article-import/runs/xcom-2066082395107758564.md`
Import mode: X.com browser extraction
Content status: complete

Note: This article is a cleaned KB inbox article based on an X.com browser extraction. Source claims are preserved as source framing unless independently verified.

## 核心觀點

這篇 X.com Article 把 Codex Mobile 的定位從「手機上查看 Codex 任務」改成「手機作為工程工作的控制中心」。作者的主要判準是：手機不需要假裝成迷你 terminal；真正有價值的是讓使用者在離開桌面時，仍能啟動、指揮、審查、轉向與整理實際跑在開發機上的 Codex 工作。

作者指出，Codex Mobile 的能力已經從單純查看任務擴展到更完整的工程控制回路，包括 worktree、goal、side chat、inline code review、queued / steering prompt、附件、skills、plugins、封存 thread，以及一系列讓行動端能參與嚴肅工程工作的細節。

## 主要內容整理

### 1. 手機是控制中心，不是運算主體

作者強調，Codex 任務、程式碼與實際執行環境仍然應該留在 Mac、Windows、devbox 或其他 connected host 上。Codex Mobile 提供的是一個原生控制介面，用來管理那些遠端或本機開發主機上的工作。

這個觀點的反常識處在於：好的 mobile engineering tool 不應該把桌面 IDE 或 terminal 壓縮到手機螢幕，而是找出使用者離開桌面時仍需要做的高價值決策。

相關來源連結：

- Codex remote connections: https://developers.openai.com/codex/remote-connections

### 2. 任務一開始就要設定正確邊界

作者認為，好的 agent work 從正確 scoped environment 開始。Codex Mobile 讓使用者在第一個 prompt 前選擇 connected host 與 workspace；建立新 thread 時，也能選 branch、建立獨立 worktree，並執行對應 environment setup。

這讓手機端可以支援幾個實用模式：

- 用目前 checkout 做快速調查。
- 為需要隔離的修改建立新的 worktree。
- 從正確 base branch 開始，而不是事後補救 Git 狀態。
- 在要求 Codex build 或 test 前，先跑 environment setup。

作者也註記，目前 Codex Mobile 尚不能直接編輯那些 environment scripts。

相關來源連結：

- Codex local environments: https://developers.openai.com/codex/app/local-environments
- Thomas Ricouard related post: https://x.com/Dimillian/status/2064629841496883710

### 3. Side chat 是主工作線旁邊的思考分支

作者把 side chat 視為解決長任務 transcript 汙染的工具。長時間 coding thread 會累積重要 context，如果每個理解問題都插回主線，主 thread 會變得吵雜，也可能把 agent 從目標拉走。

在作者的使用方式裡，主 thread 負責推動工作；side chat 負責理解工作。適合放進 side chat 的問題包括：為什麼 Codex 選這個架構、某個錯誤代表什麼、行為是否和 desktop app 一致、如何把實作細節改寫成 release note、在批准 command 前應該驗證什麼。

相關來源連結：

- Thomas Ricouard related post: https://x.com/Dimillian/status/2064694939087167824

### 4. Plan 決定路徑，Goal 定義結果

作者區分 Plan mode 與 Goal 的用途。Plan mode 適合在任務模糊、風險高或可能跨多個系統時，先讓 Codex 提出 implementation path；Goal 則是更持久的 outcome，讓 Codex 能跨多輪持續追求可驗證的完成狀態。

作者建議的模式是：高風險改動先用 Plan mode 檢查邊界，接受方向後，再把可驗證 outcome 設成 goal，讓 Codex 持續完成 implementation、tests、review feedback 與 cleanup。

同時，作者提醒 goal 不應太寬泛；如果把目標描述成「百分之百像 X 或 Y」，Codex 可能會走得過遠、浪費 token。好的 goal 應該有清楚且可驗證的終態。

### 5. 手機本身的資料與感測能力可以進入工作流

作者提醒，使用者是在手機上工作，因此手機能存取的照片、截圖、檔案、錄音與背景 dictation 都可以成為 Codex task 的輸入。這對 mobile native 或 web app 開發尤其有用。

作者舉例：在 ChatGPT iOS 工作時，若看到問題，可以直接截圖並送進 task，讓 Codex 修正；在同一 Wi-Fi 下，還可以把 app build 到自己的裝置上，直接測試 Codex thread 的成果。

文章也引用 Nick Dobos 的使用例：在 iOS app 中切換到其他 app 操作時，Codex iOS 的 dictation 仍可在背景持續錄音，讓使用者邊使用待開發 app 邊描述要修正的問題。

相關來源連結：

- Nick Dobos related post: https://x.com/NickADobos/status/2063327344304271852

### 6. Code review 不必等回到桌面

作者指出，Codex Mobile 可以在 completed turn 後顯示 changed files summary，使用者可以開 diff、檢查個別檔案、展開或收合區塊、wrap long lines，並用 syntax highlighting 開 source file。

更重要的是，使用者可以對相關行加 inline comment，再把 review context 送回 Codex。作者的判準不是「手機能不能取代大螢幕深度 code reading」，而是許多 review 卡住的其實只是一兩個決策，這些決策不必等回到桌面才做。

相關來源連結：

- Thomas Ricouard related post: https://x.com/Dimillian/status/2064562932638269903

### 7. Mobile app 的 plugins、skills 與 changelog

作者提到 Codex Mobile 持續更新，並連到 Codex Mobile changelog。文章也引用另一則作者貼文，說 mobile composer 現在能像 desktop app 一樣 inline 顯示 plugins 和 skills，使使用者更自然地串接工具與 prompt。

相關來源連結：

- Codex Mobile changelog: https://developers.openai.com/codex/changelog?type=codex-mobile
- Thomas Ricouard related post: https://x.com/Dimillian/status/2064668608362324376

## 可遷移判準

- 如果一個 mobile tool 只是縮小桌面介面，通常不會產生好的行動工作流；應該問它讓哪些「離開桌面時仍重要的決策」變快、清楚且可控。
- Agent workflow 的主線應該保留給執行與目標推進；理解、詢問、摘要與局部判斷可以放到 side channel，避免污染主 transcript。
- Worktree、branch、environment setup 不是工程細節而已，它們是 agent 任務邊界的一部分，應該在第一個 prompt 前就設好。
- Plan 適合降低動手前的不確定性；Goal 適合維持跨回合的完成條件。兩者不是同一種控制工具。
- 手機的價值不只在隨時輸入文字，而是能把截圖、相機、檔案、錄音與真機測試帶進 agent loop。
- 行動端 code review 的核心價值不是完整替代桌面 review，而是移除「只差一兩個決策」造成的等待。

## Media And Referenced Posts

- Main article image: https://pbs.twimg.com/media/HKwbuf_WcAATS9y?format=jpg&name=medium
- Article media link: https://x.com/Dimillian/article/2066082395107758564/media/2066056814731358208
- Mobile attachment image: https://pbs.twimg.com/media/HKwyfUYWoAAHk9u?format=jpg&name=large
- Mobile attachment media link: https://x.com/Dimillian/article/2066082395107758564/media/2066081842684403712
- Worktree / branch related post: https://x.com/Dimillian/status/2064629841496883710
- Side chat related post: https://x.com/Dimillian/status/2064694939087167824
- Dictation related post: https://x.com/NickADobos/status/2063327344304271852
- Code review related post: https://x.com/Dimillian/status/2064562932638269903
- Plugins / skills related post: https://x.com/Dimillian/status/2064668608362324376

## 邊界與注意事項

- 本文是作者對 Codex Mobile 的產品使用指南與個人工作流整理，不是獨立第三方評測。
- 文章中的功能可用性與 UI 細節可能隨 Codex Mobile 更新改變；若要做產品決策或教學文件，應再查 Codex changelog 與官方文件。
- X.com extraction 原始檔包含 X.com 頁面 UI、Premium 提示與推薦貼文區塊；本 inbox article 已移除那些不屬於主文章內容的噪音。

## Source Notes

- Source URL: https://x.com/i/status/2066082395107758564
- Author: Thomas Ricouard @Dimillian
- Status ID: 2066082395107758564
- Published: 2026-06-14
- Captured at: 2026-06-15T06:57:55+08:00
- Extraction file: `/Users/lee/ws/myKBs/myAgentTools/xcom-article-import/runs/xcom-2066082395107758564.md`
- Content status: complete
