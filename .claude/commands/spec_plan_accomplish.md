# 目的

將 `@fastplan/pending_test/` 中的計畫檔案移動到 `@fastplan/accomplish/`，並刪除相關暫存檔案。只有經過 implement 的計畫（位於 `pending_test/`）才能歸檔。

# Superpowers Skills

若目前位於 feature branch（非 main／master）上開發，歸檔後呼叫 `superpowers:finishing-a-development-branch` skill，引導完成 merge 或清理分支的決策。**但以下由本指令覆寫之：嚴禁 push 到遠端、嚴禁建立 PR，只允許本地 merge 與分支清理；需要推上遠端時由使用者自行手動 push。** 選擇 merge 時**預設用一般 merge（`--no-ff`）**，保留任務級 commit、並以 merge commit 標記提案邊界；使用者要求主幹精簡「一個提案＝一個 commit」時才用 squash merge。

# 作業流程

1. 檢查 `@fastplan/pending_test/[提案簡稱]_plan.md` 是否存在
   * 若不存在，告知使用者該計畫尚未實作（或不存在），需先執行 `/spec_plan_implement [提案簡稱]`，直接結束
2. 移動計畫檔案到 `@fastplan/accomplish/`
   * 若 `@fastplan/accomplish` 不存在，先建立
   * 若目標已有同名檔案，直接覆蓋
3. 刪除相關暫存檔案：若 `@fastplan/bug/[提案簡稱]_bugs.md` 存在，一併刪除
4. 若目前位於 feature branch，呼叫 `superpowers:finishing-a-development-branch` 引導 merge／清理分支（merge 預設 `--no-ff`）。**嚴禁 push 到遠端、嚴禁建立 PR**
5. 告知使用者計畫已歸檔至 accomplish，並說明已清理的暫存檔案

# 命名規範

* **提案簡稱** ：使用小寫、連字號，例：`task-refactor`、`onboarding-flow`。

# 使用語言

使用與使用者相同的語言即可
