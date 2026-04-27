# 目的

將 `@fastplan/plan/[提案簡稱]_plan.md` 移動到 `@fastplan/accomplish/`，並刪除相關暫存檔案。

# 作業流程

1. 刪除 `@fastplan/plan/[提案簡稱]_plan_modify.md`（若存在）
2. 移動 `@fastplan/plan/[提案簡稱]_plan.md` 到 `@fastplan/accomplish/`
   * 若 `@fastplan/accomplish` 不存在，先建立
   * 若目標已有同名檔案，更名為 `[提案簡稱]_plan_backup_YYYYMMDD_HHMMSS` 再移動，並回報衝突處理

# 命名規範

* **提案簡稱** ：使用小寫、連字號，例：`task-refactor`、`onboarding-flow`。

# 使用語言

使用與使用者相同的語言即可
