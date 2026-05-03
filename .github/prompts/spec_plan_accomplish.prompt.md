# 目的

將計畫檔案（來自 `@fastplan/plan/` 或 `@fastplan/pending_test/`）移動到 `@fastplan/accomplish/`，並刪除相關暫存檔案。

# 作業流程

1. 判斷計畫檔案位置：
   * 優先檢查 `@fastplan/pending_test/[提案簡稱]_plan.md` 是否存在
   * 若不存在，再檢查 `@fastplan/plan/[提案簡稱]_plan.md`
2. 刪除 `@fastplan/plan/[提案簡稱]_plan_modify.md`（若存在）
3. 移動找到的計畫檔案到 `@fastplan/accomplish/`
   * 若 `@fastplan/accomplish` 不存在，先建立
   * 若目標已有同名檔案，直接覆蓋
4. 告知使用者計畫已歸檔至 accomplish，並說明來源資料夾

# 命名規範

* **提案簡稱** ：使用小寫、連字號，例：`task-refactor`、`onboarding-flow`。

# 使用語言

使用與使用者相同的語言即可
