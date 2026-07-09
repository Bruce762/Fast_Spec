# 目的

依照 `@fastplan/plan/[提案簡稱]_plan.md` 的內容實施程式碼，完成後將計畫移至待測試資料夾。

# Superpowers Skills

- **REQUIRED SUB-SKILL**：實作程式碼時，呼叫 `superpowers:test-driven-development` skill，先寫測試再寫實作。
- **REQUIRED SUB-SKILL**：宣告實作完成前，呼叫 `superpowers:verification-before-completion` skill，實際執行驗證指令並確認輸出後才可宣告完成。
- 若改動涉及多個檔案、安全敏感邏輯或核心資料流，實作完成後、移交待測試前，呼叫 `superpowers:requesting-code-review` skill 派遣乾淨上下文的 reviewer 對照計劃審查 diff。若改動尚未 commit，以 working tree 的 `git diff` 作為審查範圍。
- 若改動範圍大（大規模重構、跨模組改動），開始實作前先呼叫 `superpowers:using-git-worktrees` skill 建立隔離工作區，實作失敗不汙染現有程式。**使用 worktree 時，後續 verify／modify／accomplish 等指令皆須在該 worktree 中執行**，直到 merge 回主幹，程式碼與 fastplan 狀態才會回到主幹。
- 若計劃包含多個可獨立完成的任務，呼叫 `superpowers:subagent-driven-development` skill 平行派發子代理執行，逐任務審查（改動範圍也大時直接用 worktree）。**嚴禁在 main／master 上逐任務 commit**。

# 作業流程

1. 讀取 `@fastplan/plan/[提案簡稱]_plan.md`
   * 若不存在，檢查 `@fastplan/pending_test/[提案簡稱]_plan.md`：若在該處，告知使用者計劃已實作過，可執行 `/spec_plan_verify` 或 `/spec_plan_modify`，直接結束
   * 兩處都不存在 → 告知使用者需先執行 `/spec_plan_proposal [提案簡稱]` 建立計劃，直接結束
2. 建立實作分支：若當前在 main／master，建立並切換到 `feature/[提案簡稱]`（分支已存在則直接切換過去）；若已在其他分支或 worktree 則沿用，不疊套。過程中的 commit 一律落在此分支，**嚴禁直接 commit 到 main／master**；merge 回主幹由 accomplish 階段處理
3. 實作內容（遵循 `superpowers:test-driven-development`）
   * 若改動範圍大，先以 `superpowers:using-git-worktrees` 建立隔離工作區再實作
   * 若計劃含多個可獨立完成的任務，以 `superpowers:subagent-driven-development` 平行派發子代理執行（嚴禁在 main／master 上逐任務 commit）
4. 若發現新問題，記錄於方案的「待解決問題」章節並告知使用者
5. 若改動涉及多個檔案、安全敏感邏輯或核心資料流，呼叫 `superpowers:requesting-code-review` 對照計劃審查 diff，修復 Critical／Important 等級的問題後才繼續
6. 實作完成後，將 `@fastplan/plan/[提案簡稱]_plan.md` 移動到 `@fastplan/pending_test/`
   * 若 `@fastplan/pending_test` 不存在，先建立
   * 若目標已有同名檔案，直接覆蓋
7. 若 `CLAUDE.md` 存在，判斷此次實作是否涉及架構變動（新增/移除模組、改變執行指令、新增目錄、修改關鍵設計決策），有則更新對應段落，維持原有結構與風格
8. 告知使用者實作完成，計畫已移至待測試資料夾

# 輸出後提示

實作完成後，必須在回覆末尾加上以下提示：

> 實作完成，計畫已移至 `fastplan/pending_test/`。可執行 `/spec_plan_verify [提案簡稱]` 驗證改動效果。

# 使用語言

使用與使用者相同的語言即可