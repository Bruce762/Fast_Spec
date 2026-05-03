# 目的

依照 `@fastplan/plan/[提案簡稱]_plan.md` 的內容實施程式碼，完成後將計畫移至待測試資料夾。

# 作業流程

1. 讀取 `@fastplan/plan/[提案簡稱]_plan.md`
2. 實作內容
3. 若發現新問題，記錄於方案的「待解決問題」章節並告知使用者
4. 實作完成後，將 `@fastplan/plan/[提案簡稱]_plan.md` 移動到 `@fastplan/pending_test/`
   * 若 `@fastplan/pending_test` 不存在，先建立
   * 若目標已有同名檔案，直接覆蓋
5. 告知使用者實作完成，計畫已移至待測試資料夾

# 使用語言

使用與使用者相同的語言即可
