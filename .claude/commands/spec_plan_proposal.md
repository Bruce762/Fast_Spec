# 目的

針對使用者的問題去計劃要怎麼做，統一存放於 `@fastplan/plan`

# Superpowers Skills

- **REQUIRED SUB-SKILL**：需求確認明確後、撰寫方案文件前，先呼叫 `superpowers:writing-plans` skill，借用其「拆解任務、標註可驗證步驟」的思路撰寫計劃。**但以下三點由本指令控制、覆寫之**：① 文件結構仍由 AI 依提案性質自行組織（只需含下方規定的必含章節），不強制套用其固定 Header／模板；② 存檔路徑以 `@fastplan/plan/[提案簡稱]_plan.md` 為準，不使用其預設的 `docs/superpowers/plans/` 路徑；③ 不執行其結尾的 Execution Handoff（不自動進入實作）。
- 若需求仍模糊且尚未經過 `/spec_plan_discuss` 階段，先呼叫 `superpowers:brainstorming` skill 釐清需求；**同樣只借用其提問釐清，不寫 design doc 檔、不自動轉入 writing-plans**。

# 作業流程

> **禁止事項**：本指令全程不得建立或修改 `README.md` 與 `CHANGELOG.md`；這兩份文件的同步一律由 `/spec_sync_readme` 指令負責。

1. **理解與需求澄清**
   * 讀取使用者問題。
   * 若需求不清楚或有任何疑問，**先向使用者提問**，等收到回覆確認需求明確後再繼續後續步驟。不要假設或自行填補不確定的細節。
2. **搜集資料與思考判斷**
3. **輸出方案文件**
   * 建立前檢查 `@fastplan/plan/` 與 `@fastplan/pending_test/` 是否已有同名的 `[提案簡稱]_plan.md`：**若有，告知使用者該簡稱已有進行中的計劃，詢問要覆蓋還是換名，未收到回覆前不建立檔案**
   * 在 `@fastplan/plan` 建立：`[提案簡稱]_plan.md`
   * 文件結構與內容由 AI 依提案性質自行組織，但必須包含以下兩個章節（後續指令依賴它們）：
     * **改動效果**：逐條列出實施後的預期變化，使用 `- [ ]` 核取方塊格式，供 verify 逐項對照勾選。每一條必須可驗證：寫明「執行／操作什麼 → 會觀察到什麼結果」，不可寫成模糊描述。
       * 壞例：「登入功能更完善」「效能提升」
       * 好例：「同一帳號連續登入失敗 5 次後，第 6 次回傳 429」
     * **待解決問題**：初始為空，implement／verify 過程發現的新問題記錄於此。

# 命名規範
* **提案簡稱** ：使用小寫、連字號，例：`task-refactor`、`onboarding-flow`。
* **路徑固定** ：`@fastplan/plan/[提案簡稱]_plan.md`

# 輸出後提示

方案文件輸出完畢後，必須在回覆末尾加上以下提示：

> 方案已建立。若要開始實作，請執行 `/spec_plan_implement [提案簡稱]`。尚未執行 implement 前，請勿自行修改任何程式碼。

# 使用語言
使用與使用者相同的語言即可
