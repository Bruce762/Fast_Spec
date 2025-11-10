# 目標：

刪除@`@fastplan/plan/[提案簡稱]_plan_modify.md`、`@fastplan/plan/[提案簡稱]_plan_summary.md`，並將 `@fastplan/plan/[提案簡稱]_plan.md` 移動到 `@fastplan/acomplish/（檔名不變）`。

# 規則：

1) 若 @fastplan/acomplish 不存在，先建立再移動到 @fastplan/acomplish/（檔名不變）。
2) 若目標資料夾已有同名檔案，將欲移動之檔案更名為「`[提案簡稱]_plan_backup_YYYYMMDD_HHMMSS`」後再移動，並回報衝突處理。
3) 請輸出「動作摘要」：刪除清單、移動前後路徑、是否發生衝突與結果、成功/失敗狀態。

# 使用語言

使用與使用者相同的語言即可