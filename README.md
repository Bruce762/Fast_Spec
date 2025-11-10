# Fast_Spec

專注於上下文工程以及規格輸入編程之優化指令集，提供完整的開發工作流程管理。

## 簡介

Fast_Spec 是一套結構化的 AI 輔助開發工作流程指令集，幫助開發者從需求調研、方案設計、到程式實作、Bug 修復的完整開發生命週期管理。透過標準化的流程與文件格式，確保開發過程的可追溯性與一致性。

## 安裝與使用方法
把fastplan移動到要編輯的程式資料夾中
並且把commands資料夾放到.claude的.claude/commands
安裝完成後，你的專案結構應該如下：
```
your-project/
├── @fastplan/
│   ├── plan/                      # 功能開發方案
│   ├── architecture&content/      # 功能架構與內容
│   ├── bug/                       # Bug 修復方案
│   └── acomplish/                 # 已完成方案
├── .claude/
│   └── commands/                  # Claude Code 指令
│       ├── spec_plan_proposal.md
│       ├── spec_plan_modify.md
│       └── ...
└── (你的專案檔案)
```
安裝完成後，在 Claude Code 中輸入 `/` 應該可以看到以下指令：
- `/spec_plan_proposal`
- `/spec_plan_modify`
- `/spec_plan_implement`
- `/spec_plan_acomplish`
- `/spec_bugPlan_proposal`
- `/spec_bugPlan_modify`
- `/spec_bugPlan_implement`
- `/spec_merge_bugplan_plan`
- `/spec_find_why`
- `/spec_check_code_architecture`

AI會去看這些指令而動作



## 10 個指令快速導覽

### 📋 功能開發流程

#### 1. `/spec_plan_proposal` - 提案規劃
**用途**：針對新功能需求，進行調研、拆解、輸出方案文件（不實作程式碼）

**範例使用**：
```
使用者：我想新增一個使用者認證功能
AI：[執行 spec_plan_proposal]
→ 產生 @fastplan/plan/user-auth_plan.md
→ 產生 @fastplan/plan/user-auth_plan_summary.md
```

---

#### 2. `/spec_plan_modify` - 修改提案
**用途**：修訂已存在的功能方案（不實作程式碼）

**範例使用**：
```
使用者：user-auth 方案需要加入 OAuth 2.0 支援
AI：[執行 spec_plan_modify]
→ 更新 @fastplan/plan/user-auth_plan.md
→ 產生 @fastplan/plan/user-auth_plan_modify.md
```

---

#### 3. `/spec_plan_implement` - 實施提案
**用途**：依照方案文件進行程式碼開發

**範例使用**：
```
使用者：開始實作 user-auth 功能
AI：[執行 spec_plan_implement]
→ 讀取 @fastplan/plan/user-auth_plan.md
→ 依照里程碑逐步開發並勾選
```

---

#### 4. `/spec_plan_acomplish` - 完成提案
**用途**：歸檔已完成的方案

**範例使用**：
```
使用者：user-auth 功能已完成，進行歸檔
AI：[執行 spec_plan_acomplish]
→ 移動 user-auth_plan.md 到 @fastplan/acomplish/
→ 刪除臨時文件
```

---

### 🐛 Bug 修復流程

#### 5. `/spec_bugPlan_proposal` - Bug 修復提案
**用途**：針對測試發現的 Bug，規劃修復方案（不實作程式碼）

**範例使用**：
```
使用者：user-auth 的登入驗證有問題，token 過期後無法正確處理
AI：[執行 spec_bugPlan_proposal]
→ 產生 @fastplan/bug/user-auth_bug_revise_plan.md
→ 產生 @fastplan/bug/user-auth_bug_revise_plan_summary.md
```

---

#### 6. `/spec_bugPlan_modify` - 修改 Bug 修復方案
**用途**：修訂已存在的 Bug 修復方案（不實作程式碼）

**範例使用**：
```
使用者：Bug 修復方案需要額外處理 refresh token 的情況
AI：[執行 spec_bugPlan_modify]
→ 更新 @fastplan/bug/user-auth_bug_revise_plan.md
```

---

#### 7. `/spec_bugPlan_implement` - 實施 Bug 修復
**用途**：依照 Bug 修復方案進行程式碼修復

**範例使用**：
```
使用者：開始修復 user-auth 的 token 問題
AI：[執行 spec_bugPlan_implement]
→ 讀取 @fastplan/bug/user-auth_bug_revise_plan.md
→ 依照里程碑逐步修復
```

---

#### 8. `/spec_merge_bugplan_plan` - 合併 Bug 修復到主計畫
**用途**：將已完成的 Bug 修復內容合併回主方案文件

**範例使用**：
```
使用者：Bug 已修復完成，合併到主計畫
AI：[執行 spec_merge_bugplan_plan]
→ 合併內容到 @fastplan/plan/user-auth_plan.md
→ 刪除 @fastplan/bug/user-auth_bug_revise_plan_summary.md
```

---

### 🔍 知識探索與架構理解

#### 9. `/spec_find_why` - 探索技術原理
**用途**：解釋功能、框架或程式現象的原因與原理

**範例使用**：
```
使用者：為什麼我們的應用會在高併發時出現資料不一致？
AI：[執行 spec_find_why]
→ 分析程式碼中的併發處理機制
→ 解釋資料競爭原理
→ 提供示例說明
→ 產生 @fastplan/plan/architecture&content/[主題]_why.md
```

---

#### 10. `/spec_check_code_architecture` - 檢查代碼架構
**用途**：整理並說明功能、框架的架構與用途

**範例使用**：
```
使用者：解釋一下我們的權限控制系統是如何運作的
AI：[執行 spec_check_code_architecture]
→ 搜尋權限相關程式碼
→ 整理權限系統架構
→ 說明核心概念
→ 產生 @fastplan/plan/architecture&content/permission-system.md
```

---
## 快速參考

| 指令 | 用途 | 輸出位置 |
|------|------|----------|
| `/spec_plan_proposal` | 新功能規劃 | `@fastplan/plan/` |
| `/spec_plan_modify` | 修改功能方案 | `@fastplan/plan/` |
| `/spec_plan_implement` | 實作功能 | 程式碼 |
| `/spec_plan_acomplish` | 歸檔完成方案 | `@fastplan/acomplish/` |
| `/spec_bugPlan_proposal` | Bug 修復規劃 | `@fastplan/bug/` |
| `/spec_bugPlan_modify` | 修改 Bug 方案 | `@fastplan/bug/` |
| `/spec_bugPlan_implement` | 實作 Bug 修復 | 程式碼 |
| `/spec_merge_bugplan_plan` | 合併 Bug 到主計畫 | `@fastplan/plan/` |
| `/spec_find_why` | 探索技術原理 | `@fastplan/plan/architecture&content/` |
| `/spec_check_code_architecture` | 檢查代碼架構 | `@fastplan/plan/architecture&content/` |

## 完整工作流程範例

### 範例 1：新功能開發完整流程

```
階段 1：規劃
使用者：我想新增一個待辦事項（Todo）功能
AI：/spec_plan_proposal
→ 產生 @fastplan/plan/todo-feature_plan.md

階段 2：修改方案（可選）
使用者：Todo 需要支援分類標籤
AI：/spec_plan_modify
→ 更新 @fastplan/plan/todo-feature_plan.md

階段 3：實作
使用者：開始實作 Todo 功能
AI：/spec_plan_implement
→ 依照 plan 進行開發

階段 4：完成歸檔
使用者：Todo 功能開發完成
AI：/spec_plan_acomplish
→ 歸檔到 @fastplan/acomplish/
```

---

### 範例 2：Bug 修復完整流程

```
階段 1：發現 Bug
使用者：Todo 的刪除功能有問題，刪除後資料庫記錄還在
AI：/spec_bugPlan_proposal
→ 產生 @fastplan/bug/todo-feature_bug_revise_plan.md

階段 2：實施修復
使用者：開始修復這個 Bug
AI：/spec_bugPlan_implement
→ 依照 bug plan 進行修復

階段 3：合併到主計畫
使用者：Bug 已修復，合併到主計畫
AI：/spec_merge_bugplan_plan
→ 更新 @fastplan/plan/todo-feature_plan.md
```

---

### 範例 3：技術探索流程

```
情境 1：了解技術原理
使用者：為什麼我們的 Todo 列表在更新時會閃爍？
AI：/spec_find_why
→ 分析渲染機制
→ 產生 @fastplan/plan/architecture&content/todo-flicker-analysis.md

情境 2：了解架構設計
使用者：解釋一下 Todo 的資料流架構
AI：/spec_check_code_architecture
→ 整理資料流說明
→ 產生 @fastplan/plan/architecture&content/todo-data-flow.md
```

---

## 使用建議

1. **循序漸進**：先規劃（proposal）再實作（implement），避免跳過規劃階段
2. **文件先行**：所有 proposal 與 modify 指令都不會實作程式碼，僅產生文件
3. **保持更新**：當需求變更時，使用 modify 指令更新方案文件
4. **適時歸檔**：功能完成後使用 acomplish 進行歸檔，保持工作區整潔
5. **Bug 隔離**：Bug 修復使用獨立的 bug plan，修復完成後再合併回主計畫

---

## 詳細作業流程

### `/spec_plan_proposal` - 提案規劃流程

1. **理解與需求澄清**
   - 讀取使用者問題
   - 根據使用者的問題，粗略地提出幾個有關於此問題的問題（要提示使用者也可以不回答），但使者可能會針對你提出的問題而提出其他問題。如果已經尋問過了則跳到步驟2

2. **搜集資料**
   - 瀏覽必要的資料夾與文件，蒐集背景與限制及相關程式邏輯

3. **思考與判斷**
   - 綜合調研結果，判斷是否需要將問題拆解為多個子問題
   - 若可拆解：列出子問題清單與其關聯/依賴

4. **擬定可實施的方案（不需實作）**
   - 針對每個子問題，提出至少一個可執行方案（含假設、資源/時程粗估）
   - 彙整成「整體方案」：說明優先順序與協作介面

5. **輸出方案文件**
   - 在 `@fastplan/plan` 建立：`[提案簡稱]_plan.md`
   - 內容包含：背景、目標、拆解、方案、里程碑。且里程碑需依照「整體方案」，將其每個詳細的子任務列出需完成的項目，使得之後可以去勾選

6. **輸出方案摘要**
   - 依第5點的 `[提案簡稱]_plan.md` 撰寫：`[提案簡稱]_plan_summary.md`
   - 內容盡可能簡短簡潔
   - 內容聚焦：方案與目標、關鍵決策

---

### `/spec_plan_modify` - 修改提案流程

1. 針對使用者的問題以及想做的改動進行初步調研
2. 查閱 `@fastplan/plan/[提案簡稱]_plan.md` 與其他相關程式與資料
3. 比較與原本的差異，以及如果有疑問請向使用者提問，然後綜整調研結果，將問題適度拆解為可執行的子問題
4. 依拆解結果修訂方案內容，並將修正後的內容更新至 `@fastplan/plan/[提案簡稱]_plan.md`、`@fastplan/plan/[提案簡稱]_plan_summary.md`，且不需實作此檔案到程式
5. 創建 `@fastplan/plan/[提案簡稱]_plan_modify.md`，並把此次修改用簡單易懂少字的方式告訴使用者

---

### `/spec_plan_implement` - 實施提案流程

- 依照 `@fastplan/plan/[提案簡稱]_plan.md` 的規劃實施程式碼開發
- 以「里程碑 → 子任務」為主軸，逐項勾選、逐步完成

---

### `/spec_plan_acomplish` - 完成提案流程

1. 刪除 `@fastplan/plan/[提案簡稱]_plan_modify.md`、`@fastplan/plan/[提案簡稱]_plan_summary.md`
2. 將 `@fastplan/plan/[提案簡稱]_plan.md` 移動到 `@fastplan/acomplish/`（檔名不變）
3. 若 `@fastplan/acomplish` 不存在，先建立再移動
4. 若目標資料夾已有同名檔案，將欲移動之檔案更名為「`[提案簡稱]_plan_backup_YYYYMMDD_HHMMSS`」後再移動，並回報衝突處理

---

### `/spec_bugPlan_proposal` - Bug 修復提案流程

1. **理解與需求澄清**
   - 讀取使用者問題
   - 根據使用者的問題，粗略地提出幾個有關於此問題的問題（要提示使用者也可以不回答）。如果在本次對話中已經詢問過需求澄清問題，則跳到步驟2

2. **搜集資料**
   - 查看原始程式碼，瀏覽必要的資料夾與文件，蒐集背景與限制及相關程式邏輯
   - 以及查看 `@fastplan/[提案簡稱]_plan.md`

3. **思考與判斷**
   - 依步驟2資料搜集的結果與步驟1使用者提出的問題，綜合歸納差異
   - 綜合調研結果與差異，判斷此改動是否需要將問題拆解為多個子問題
   - 若可拆解：列出子問題清單與其關聯/依賴

4. **擬定可實施的方案（不需實作）**
   - 針對問題（或各子問題，如已拆解），提出至少一個可執行方案（含假設、風險、資源/時程粗估）
   - 彙整成「整體方案」：說明優先順序與協作介面

5. **輸出方案文件**
   - 在 `@fastplan/bug` 建立：`[提案簡稱]_bug_revise_plan.md`
   - 內容包含：背景、目標、拆解、方案、里程碑。且里程碑需依照「整體方案」，將其每個詳細的子任務列出需完成的項目，使得之後可以去勾選

6. **輸出方案摘要**
   - 依第5點的 `[提案簡稱]_bug_revise_plan.md` 撰寫：`[提案簡稱]_bug_revise_plan_summary.md`
   - 內容盡可能簡短簡潔
   - 內容聚焦：方案與目標、關鍵決策

---

### `/spec_bugPlan_modify` - 修改 Bug 修復方案流程

1. 針對使用者提出的改動或補充需求進行初步調研
2. 查閱 `@fastplan/bug/[提案簡稱]_bug_revise_plan.md` 與其他相關程式與資料以及 `@fastplan/plan/[提案簡稱]_plan.md`
3. 比較與原本方案的差異，以及如果有疑問請向使用者提問，然後綜整調研結果，將問題適度拆解為可執行的子問題
4. 依拆解結果修訂方案內容，並將修正後的內容更新至 `@fastplan/bug/[提案簡稱]_bug_revise_plan.md`，且不需實作此檔案到程式
5. 創建 `@fastplan/bug/[提案簡稱]_bug_revise_plan_modify.md`，並把此次修改用簡單易懂少字的方式告訴使用者

---

### `/spec_bugPlan_implement` - 實施 Bug 修復流程

- 依照 `@fastplan/bug/[提案簡稱]_bug_revise_plan.md` 的規劃實施 Bug 修復程式碼開發
- 以「里程碑 → 子任務」為主軸，逐項勾選、逐步完成
- 修復過程中若發現新的問題或需要調整方案，應記錄並考慮是否需要更新 `_bug_revise_plan.md`

---

### `/spec_merge_bugplan_plan` - 合併 Bug 修復到主計畫流程

**目標**：將 `@fastplan/bug/[提案簡稱]_bug_revise_plan.md` 的已完成內容，與 `@fastplan/plan/[提案簡稱]_plan.md` 合併，並把整合後的最終版本覆蓋到 `@fastplan/plan/[提案簡稱]_plan.md`。完成後刪除 `@fastplan/bug/[提案簡稱]_bug_revise_plan_summary.md`。

**合併規則**：

1. **保留原有章節結構**
   - `@fastplan/plan/[提案簡稱]_plan.md` 的章節順序（如：目的、作業流程、技術細節、驗證方式…）必須維持不變
   - 若 `bug_revise_plan.md` 含有對應章節，請以「差異更新」方式整併到對應位置，避免整段覆蓋與重複內容

2. **移除暫時性描述**
   - 將「待確認、暫時 workaround、後續再補」等暫時性語句過濾或改為已驗證的正式描述；若尚未驗證，則不要併入主計畫

3. **刪除前進行校驗**
   - 合併完成後檢查：必要修正是否已完整併入對應章節且無重覆、名詞/參數/函式名稱在整份文件中是否一致、連結與引用是否仍有效
   - 僅在校驗通過後才刪除 `@fastplan/bug/[提案簡稱]_bug_revise_plan_summary.md`

**執行步驟**：

1. 解析兩份文件章節對應，建立差異清單
2. 將 bug 修正內容併入對應章節（避免整段覆蓋）
3. 清理暫時性語句，統一名詞/參數/函式名稱
4. 完整性檢查（結構、連結、引用、一致性）
5. 產出最終版 `@fastplan/plan/[提案簡稱]_plan.md` 全文
6. （校驗通過後）刪除 `@fastplan/bug/[提案簡稱]_bug_revise_plan_summary.md`

---

### `/spec_find_why` - 探索技術原理流程

1. 引導使用者描述想了解的問題（若使用者尚未明確說明，請引導其描述想了解的情況或現象）
2. 根據使用者的提問，搜尋並整理相關程式碼與技術資料（可跨範圍搜尋以獲取完整脈絡）
3. 分析該現象「為什麼會這樣」的原因與背後原理
4. 在說明時保持條理清晰、簡潔易懂，先解釋核心原因與邏輯，再視使用者追問補充更深入的技術層面
5. 附上一個簡單的示例（不需實作），幫助使用者更容易理解該現象的成因
6. 將整理結果輸出至 `@fastplan/plan/architecture&content`

---

### `/spec_check_code_architecture` - 檢查代碼架構流程

1. 引導使用者說明想了解的功能或框架（若使用者尚未指定，請引導其說明想了解的功能或框架）
2. 根據使用者的提問，搜尋並整理相關程式碼與資料（可跨範圍搜尋以獲取完整脈絡）
3. 歸納出清晰且可供使用者理解的說明內容
4. 在解釋功能時保持簡潔，僅提供核心概念與用途，若使用者進一步追問，再補充更深入的技術細節
5. 附上一個簡單範例，幫助使用者理解（不需實作）
6. 將整理結果輸出至 `@fastplan/plan/architecture&content`

---

## 多語言支援

所有指令都會自動使用與使用者相同的語言進行回應與文件撰寫。

---

## 注意事項

- 提案簡稱請使用小寫與連字號（kebab-case）
- 所有方案文件都包含：背景、目標、拆解、方案、里程碑
- 里程碑需列出詳細的可勾選子任務清單
- Bug 修復完成後記得執行合併指令，避免資訊分散

---

