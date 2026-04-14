# Adoption Workflow

**目標**

把高價值文章從「已理解」推進到「會影響你的做法」。這份 workflow 不取代 ingest 或 compile，而是承接 article card 之後的下一層：把知識增量轉成 workflow change、habit change 與可驗證的 adoption。

**核心原則**

- repo 不只編譯知識，也應編譯可重複採用的做法
- adoption 只針對高價值增量，不要求每篇文章都硬轉成行動
- 單篇文章可以提出 adoption 線索，但真正穩定的 adoption 應盡量回寫成 concept、map、checklist、prompt 或其他 repo-local artifact
- adoption 的重點不是宣稱「這很重要」，而是明確說出下次遇到什麼情境時要怎麼做得不同

**三種增量**

每次要做 adoption 判斷時，先把增量拆成三類，不要混在一起：

- knowledge delta
  這篇讓你多知道了什麼新 framing、概念、模式或邊界
- workflow delta
  這篇要求你改變哪個工作流、判斷順序、artifact 設計或工具使用方式
- habit delta
  這篇要求你建立哪個新習慣，或停止哪個舊習慣

不是每篇文章三種增量都會同時存在。

**何時值得做 adoption**

符合以下任一條件，建議在 ingest 後接著做 adoption：

- 它明顯改變你原本的工作方式
- 它提供一個可重複使用的操作模式，而不是只是一個觀點
- 它揭露了你現有 workflow 的低效習慣、盲點或錯誤預設
- 它能被轉成 checklist、rule、prompt、skill、CLI surface 或其他可執行 artifact

若只是一般背景知識、新聞性更新或與現有理解幾乎完全重複，通常不需要做 adoption。

**最小 adoption 問題集**

對值得做 adoption 的文章，至少回答：

1. 這篇最重要的 knowledge delta 是什麼
2. 它要求你改變哪個 workflow
3. 你下次在哪個具體情境要試這個新做法
4. 你要開始做什麼
5. 你要停止做什麼
6. 什麼證據算 adoption 成功

**常見輸出形式**

adoption 不一定要新增新目錄；優先選最薄、最穩定的回寫位置：

- article card 裡補一段 adoption note
- 建立一張 GitHub adoption issue，提醒自己真的回來閱讀與嘗試
- 更新 concept page 的 `Current Framing` 或 `Open Questions`
- 更新 map page，讓新做法成為 topic-level entry point
- 新增或修改 prompt asset
- 新增或修改 repo-local checklist、rule、skill note 或 helper artifact

選擇原則：

- 只對單篇文章成立的，先留在 article level
- 若 adoption note 已有明確 `Next Adoption Experiment` 與 `Success Criteria`，可再建立一張精簡 issue 承接提醒與實驗追蹤
- 可跨 2 篇以上重用的，應提升到 concept 或 map
- 已經影響日常操作的，應再下沉到 prompt、checklist 或其他執行 artifact

**最小 GitHub Issue Flow**

若你希望 adoption follow-up 不只寫回 article card，而是真的回來看，預設採最小 issue flow，不必先引入 GitHub Projects：

- 前提：repository 必須先開啟 GitHub Issues；若 repo 停用 issues，則先保留 article-level adoption note，或改用其他 repo / inbox 承接提醒
- 只有當 adoption note 同時具備 `Next Adoption Experiment` 與 `Success Criteria` 時，才建立 issue
- issue 只放精簡版，不複製整段 article card
- 預設 labels：
  - `adoption`
  - 視情況再補 `experiment`
- 預設 assign 給自己
- issue body 最少包含：
  - source article
  - next adoption experiment
  - stop doing
  - success criteria
  - optional review-by date

**Label Semantics**

- `adoption`
  代表這張 issue 來自 adoption follow-up，表示某個做法值得先採信到足以追蹤
- `experiment`
  代表這張 issue 還需要在真實工作中驗證效果；不是正式定論，而是一次有情境、有判準的試跑

兩者一起出現時，意思是：

- 這個做法值得先納入候選
- 但還沒有被你的工作流正式驗證
- 需要透過一次真實任務來確認作者描述的效果是否對你成立

這樣的分工是：

- article card 保存完整理解與 adoption reasoning
- GitHub issue 承接「記得真的去試」這件事

**Issue 建立門檻**

只有符合以下三點，才值得開 adoption issue：

- 有具體下一次可練習的真實情境
- 有可檢查的 success criteria
- 值得在短期內實際試一次，而不是只是長期觀念提醒

**成功標準**

只有在以下情況，才算 adoption 真正完成，而不只是寫下來：

- 你已指定一個真實情境作為下一次演練場景
- 新做法至少被實際使用一次
- 成功與失敗的判準是可描述的，不只是「感覺比較好」
- 若新做法可重複使用，已回寫成 repo-local artifact，而不是停在單次對話記憶

**反模式**

- 把 adoption 寫成空泛口號，例如「之後要更注意」
- 沒有指定觸發情境，導致知道要改卻永遠不會發生
- 明明是 workflow 規則，卻只留在單篇 article card
- 明明還沒有實際採用，卻提早宣稱已形成習慣

**建議節奏**

- ingest 完高價值文章後，先跑一次 adoption prompt
- 預設使用 `prompts/adoption-follow-up.md` 作為 adoption 的標準執行入口
- 一週內如果該做法真的被使用，再決定是否升成 concept / map / prompt / checklist 層
- 定期 review 時，檢查哪些 adoption note 還沒有真正形成 repo-local artifact
