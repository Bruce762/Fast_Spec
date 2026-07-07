# 目的

依照 `@fastplan/plan/[提案簡稱]_plan.md` 的內容實施程式碼，完成後將計畫移至待測試資料夾。

# Superpowers Skills

- **REQUIRED SUB-SKILL**：實作程式碼時，呼叫 `superpowers:test-driven-development` skill，先寫測試再寫實作。
- **REQUIRED SUB-SKILL**：宣告實作完成前，呼叫 `superpowers:verification-before-completion` skill，實際執行驗證指令並確認輸出後才可宣告完成。

# 作業流程

1. 讀取 `@fastplan/plan/[提案簡稱]_plan.md`
2. 實作內容（遵循 `superpowers:test-driven-development`）
3. 若發現新問題，記錄於方案的「待解決問題」章節並告知使用者
4. 實作完成後，將 `@fastplan/plan/[提案簡稱]_plan.md` 移動到 `@fastplan/pending_test/`
   * 若 `@fastplan/pending_test` 不存在，先建立
   * 若目標已有同名檔案，直接覆蓋
5. 若 `CLAUDE.md` 存在，判斷此次實作是否涉及架構變動（新增/移除模組、改變執行指令、新增目錄、修改關鍵設計決策），有則更新對應段落，維持原有結構與風格
6. 告知使用者實作完成，計畫已移至待測試資料夾

# 輸出後提示

實作完成後，必須在回覆末尾加上以下提示：

> 實作完成，計畫已移至 `fastplan/pending_test/`。可執行 `/spec_plan_verify [提案簡稱]` 驗證改動效果。

# 使用語言

使用與使用者相同的語言即可
