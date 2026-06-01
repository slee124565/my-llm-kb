---
title: "Codex /goal Playbook: 用 Checklist 與 Phase 管理長任務"
source_url: "https://github.com/openai/openai-cookbook/tree/main/examples/codex"
source_kind: "local-markdown-note"
author: "Unknown"
published: "Unknown"
captured: "2026-06-01"
status: "source"
original_path: "/Users/lee230917/Downloads/Codex_Goal_Playbook.md"
official_context_checked: "https://developers.openai.com/codex/prompting#goal-mode"
---

# Codex `/goal` Playbook：用 Checklist 與 Phase 管理長任務

參考連結：
- OpenAI Codex Cookbook examples：
  https://github.com/openai/openai-cookbook/tree/main/examples/codex

---

## Playbook 1：Checklist 分批處理法

適合任務：逆向程式碼、批次分析檔案、整理大量資料。

### 做法

1. 先產生一份任務清單。
2. 每個項目都有狀態，例如 `todo`、`doing`、`done`。
3. 要求 Codex 每次只處理一小批。
4. 每批完成後更新清單。
5. 每批完成後 commit。

### 範例場景：逆向分析 Python 專案

先建立 `analysis_tasks.json`：

```json
[
  {"file": "app/main.py", "status": "todo"},
  {"file": "app/api/user.py", "status": "todo"},
  {"file": "app/services/auth.py", "status": "todo"}
]
```

然後給 Codex：

```text
/goal 請依照 analysis_tasks.json 分批分析程式碼。

規則：
1. 每次只處理 2 個 status=todo 的檔案。
2. 分析完後，把 status 改成 done。
3. 為每個檔案補上 summary。
4. 每批完成後執行測試。
5. 測試通過後 commit。
6. 直到所有項目完成。
```

### 完成後的樣子

```json
[
  {
    "file": "app/main.py",
    "status": "done",
    "summary": "FastAPI 入口，負責註冊 router 與啟動設定"
  },
  {
    "file": "app/api/user.py",
    "status": "done",
    "summary": "User API 層，處理註冊、登入、查詢使用者"
  }
]
```

### 重點

Codex 不是憑感覺一直做，而是照著清單推進。

---

## Playbook 2：Design Doc + Phases 執行法

適合任務：重構、功能開發、資料模型改造、架構調整。

### 做法

1. 先和 Codex 一起寫設計文件。
2. 把任務拆成多個 Phase。
3. 每個 Phase 都要有驗收條件。
4. 一次只執行一個 Phase。
5. 每個 Phase 完成後檢查、測試、commit。
6. 再進入下一個 Phase。

### 範例場景：重構登入系統

先請 Codex 產生 `auth_refactor_plan.md`：

```text
請先不要修改程式碼。

請分析目前 auth 相關程式碼，產生 auth_refactor_plan.md。

文件需要包含：
1. 現況問題
2. 目標設計
3. Phase 拆分
4. 每個 Phase 的驗收條件
5. 風險與回復方式
```

範例：

```markdown
# Auth Refactor Plan

## Phase 1：盤點現有登入流程

驗收條件：
- 找出所有 auth 相關檔案
- 說明目前 login/logout/token 驗證流程
- 不修改正式程式碼
- 產生 auth_current_state.md
- commit

## Phase 2：抽出 AuthService

驗收條件：
- 建立 AuthService
- API layer 不再直接處理 token
- 原有測試通過
- commit

## Phase 3：補測試

驗收條件：
- 補上 login 成功測試
- 補上 login 失敗測試
- 補上 token 過期測試
- 測試全部通過
- commit
```

接著設定：

```text
/goal 請依照 auth_refactor_plan.md 執行。

規則：
1. 一次只執行一個 Phase。
2. 每個 Phase 完成後檢查驗收條件。
3. 驗收條件沒有通過，不准進入下一個 Phase。
4. 每個 Phase 通過後 commit。
5. commit message 使用 Conventional Commits。
```

### 重點

不是叫 Codex 幫我重構，而是先讓它建立施工圖。

---

## 建議進階版（適合 Codex CLI）

### Level 1

```text
Goal
 └── Checklist
      └── Commit
```

### Level 2

```text
Goal
 └── Design Doc
      └── Phases
            └── Acceptance Criteria
                  └── Commit
```

### Level 3

```text
Goal
 └── Design Doc
      └── Phases
            └── Acceptance Criteria
                  └── Test
                        └── Commit
                              └── Update Progress
```

---

## 核心原則

把 Workflow 寫進 Memory：

```text
請幫我完成整個專案重構
```

容易失控。

把 Workflow 寫進可追蹤文件：

```text
Design Doc
Checklist
Task JSON
Acceptance Criteria
```

Codex 才能穩定推進。

一句話總結：

不要讓 Codex 記住流程，
而是讓 Codex 讀取流程。
