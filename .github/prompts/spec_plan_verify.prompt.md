# 目的

依照 `@fastplan/pending_test/[提案簡稱]_plan.md` 的內容，實際執行驗證，確認實作符合計劃預期的改動效果，並回報結果（不需歸檔，歸檔由 accomplish 負責）。

# Superpowers Skills

**REQUIRED SUB-SKILL**：執行驗證時，呼叫 `superpowers:verification-before-completion` skill，實際執行驗證指令並確認輸出後才可回報結果，嚴禁未執行就宣稱通過。

# 作業流程

1. 讀取 `@fastplan/pending_test/[提案簡稱]_plan.md`
   * 若不存在，告知使用者需先執行 `/spec_plan_implement [提案簡稱]`，直接結束
2. 根據計劃中的「改動效果」，逐項設計驗證方式（執行測試、實際操作功能、檢查輸出）
3. 實際執行驗證，逐項記錄通過或未通過及其證據
   * 驗證通過的項目，在計劃文件的「改動效果」清單中勾選為 `- [x]`
   * 未通過的項目保持 `- [ ]`，並將問題記錄於「待解決問題」章節
4. 回報驗證結果：
   * 全部通過 → 提示使用者執行 accomplish
   * 有未通過項目 → 告知使用者未通過的項目與原因

# 輸出後提示

驗證全部通過時，必須在回覆末尾加上以下提示：

> 驗證通過。可執行 `/spec_plan_accomplish [提案簡稱]` 歸檔。

有項目未通過時，必須在回覆末尾加上以下提示：

> 驗證未通過，問題已記錄於計劃的「待解決問題」章節。可執行 `/spec_plan_modify [提案簡稱]` 調整方案。

# 命名規範

* **提案簡稱**：使用小寫、連字號，例：`task-refactor`、`onboarding-flow`

# 使用語言

使用與使用者相同的語言即可
