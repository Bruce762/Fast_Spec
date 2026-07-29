---
name: spec-plan-accomplish
description: Use when the user invokes `$spec-plan-accomplish` or asks to archive a verified named plan, clean its temporary artifacts, and merge its local feature branch as specified.
---

# Spec plan accomplish

# 目的

將 `@fastplan/pending_test/` 中的計畫檔案移動到 `@fastplan/accomplish/`，並刪除相關暫存檔案。只有經過 implement 的計畫（位於 `pending_test/`）才能歸檔。

# 分支合併規則

若目前位於 feature branch（非 main／master）上開發，歸檔後**自動 merge 回主幹並清理分支，無需詢問使用者**（不再呼叫 `superpowers:finishing-a-development-branch`）：

- merge 前先確認測試通過（跑專案測試套件）；測試失敗則停止、不 merge，回報失敗。
- **預設用 squash merge（`git merge --squash`）**，把整個提案壓成主幹上單一 commit（一個提案＝一個 commit），commit message 以提案簡稱＋重點摘要；使用者明確要求保留任務級歷史時才改用一般 merge（`--no-ff`）。
- squash merge 後 feature branch 未被記為已合併，需用 `git branch -D` 強制刪除；改用 `--no-ff` 時則 `git branch -d`。
- **嚴禁 push 到遠端、嚴禁建立 PR**，只做本地 merge 與分支清理；需要推上遠端時由使用者自行手動 push。

# 作業流程

> **禁止事項**：本指令全程不得建立或修改 `README.md` 與 `CHANGELOG.md`；這兩份文件的同步一律由 `$spec-sync-readme` 指令負責。

1. 檢查 `@fastplan/pending_test/[提案簡稱]_plan.md` 是否存在
   * 若不存在，告知使用者該計畫尚未實作（或不存在），需先執行 `$spec-plan-implement [提案簡稱]`，直接結束
2. 移動計畫檔案到 `@fastplan/accomplish/`
   * 若 `@fastplan/accomplish` 不存在，先建立
   * 若目標已有同名檔案，直接覆蓋
3. 刪除相關暫存檔案：若 `@fastplan/bug/[提案簡稱]_bugs.md` 存在，一併刪除
4. 若目前位於 feature branch，**自動** merge 回主幹並刪除分支（先跑測試，通過才 merge；預設 squash＝一提案一 commit）。**嚴禁 push 到遠端、嚴禁建立 PR**
5. 告知使用者計畫已歸檔至 accomplish、已 merge 的分支與已清理的暫存檔案

# 命名規範

* **提案簡稱** ：使用小寫、連字號，例：`task-refactor`、`onboarding-flow`。

# 使用語言

使用與使用者相同的語言即可
