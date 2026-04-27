# Fast_Spec 🚀

專注於上下文工程以及規格輸入編程之優化指令集，提供完整的開發工作流程管理。

## 簡介

Fast_Spec 是一套結構化的 AI 輔助開發工作流程指令集，幫助開發者從需求調研、方案設計、到程式實作、Bug 修復的完整開發生命週期管理。

透過系統化的指令流程，快速將想法轉化為實現方案，並持續追蹤與改進。

---

## 專案結構

```
fast_spec/
├── commands/                      # 所有指令定義
│   ├── spec_plan_proposal.md     # 規劃新方案
│   ├── spec_plan_modify.md       # 修改現有方案
│   ├── spec_plan_implement.md    # 開始實作
│   ├── spec_plan_accomplish.md   # 完成歸檔
│   ├── spec_find_why.md          # 技術解釋
│   └── spec_check_code_architecture.md  # 架構說明
├── fastplan/                      # 工作成果存檔
│   ├── plan/                      # 功能開發方案文件
│   ├── knowledge/                 # 技術知識與架構文件
│   ├── bug/                       # Bug 修復方案文件
│   └── accomplish/                # 已完成方案歸檔
└── README.md
```

---

## 安裝方法

1. 把 `.claude` 或是 `.github `資料夾複製到 `.claude/commands`
2. 重啟 Claude Code或VS Code，輸入 `/` 就能看到所有指令

**安裝後的專案結構：**

```
your-project/
├── @fastplan/ 			   # AI會自動生成
│   ├── plan/                      # 功能開發方案
│   ├── knowledge/                 # 功能架構與內容
│   ├── bug/                       # Bug 修復方案
│   └── accomplish/                # 已完成方案
├── .claude/
│   └── commands/                  # Claude Code 指令
│       ├── spec_plan_proposal.md
│       ├── spec_plan_modify.md
│       └── ...
└── (你的專案檔案)
```

---

## 指令總覽

### 📋 功能開發流程（4個指令）

提供完整的從規劃到實作再到歸檔的開發工作流程。

| 指令                    | 功能       | 說明                           | 產出        |
| ----------------------- | ---------- | ------------------------------ | ----------- |
| `/spec_plan_proposal`   | 規劃新方案 | 根據需求快速規劃開發方案       | 文件 ✏️     |
| `/spec_plan_modify`     | 調整方案   | 修改或優化現有的方案內容       | 文件 ✏️     |
| `/spec_plan_implement`  | 開始實作   | 根據方案開始編寫程式碼         | 程式碼 💻   |
| `/spec_plan_accomplish` | 完成與歸檔 | 將已完成的工作移動到歸檔文件夾 | 文件更新 📁 |

### 🔍 技術探索（2個指令）

快速理解代碼架構、技術原理或功能實現。

| 指令                            | 功能         | 說明                           | 產出        |
| ------------------------------- | ------------ | ------------------------------ | ----------- |
| `/spec_find_why`                | 解釋技術原理 | 説明概念、技術、設計決策的原因 | 技術文件 📖 |
| `/spec_check_code_architecture` | 說明代碼架構 | 分析和說明現有代碼的結構與設計 | 架構文件 🏗️ |

---

## 使用範例

### 情境 1：開發新功能

```bash
# 步驟 1：規劃
/spec_plan_proposal 我想新增使用者登入功能

# 步驟 2：調整（可選）
快速從想法轉化為實現方案。

```

步驟 1：規劃方案
/spec_plan_proposal 我想新增使用者登入功能

步驟 2：調整方案（可選）
/spec_plan_modify 加入 OAuth 2.0 支援

步驟 3：開始寫程式
/spec_plan_implement 開始實作 user-auth

步驟 4：完成歸檔
/spec_plan_accomplish user-auth 完成了

```

生成文件位置：
- 方案文件：`@fastplan/plan/user-auth_plan.md`
- 已完成：`@fastplan/accomplish/user-auth_plan.md`

### 情境 2：理解現有代碼

快速了解代碼架構或技術實現。

```

查看架構設計
/spec_check_code_architecture 請說明 authentication 模塊的架構

了解技術原理
/spec_find_why 為什麼使用 JWT 而不是 Session？

```

生成文件位置：
- 架構文件：`@fastplan/knowledge/architecture-[topic].md`
- 技術知識：`@fastplan/knowledge/why-[topic].md`

### 情境 3：迭代改進

基於反饋持續優化方案。

```

步驟 1：新增改進方案
/spec_plan_proposal 優化登入流程性能

步驟 2：調整細節
/spec_plan_modify 加入緩存機制

步驟 3：實裝改進
/spec_plan_implement 實作性能優化

步驟 4：歸檔完成
/spec_plan_accomplish 性能優化完成

```

---

## 工作成果組織

所有生成的文件自動保存到 `@fastplan/` 文件夾中：

- **`plan/`** — 所有功能開發方案（命名規範：`[簡稱]_plan.md`）
- **`knowledge/`** — 技術知識、架構文件、設計說明
- **`bug/`** — Bug 修復相關方案（保留供未來擴展）
- **`accomplish/`** — 已完成項目的歸檔

---

## 快速上手

1. **開始第一個方案**
```

/spec_plan_proposal 你的新需求或功能想法

```

2. **查看生成的方案**
方案會自動保存在 `fastplan/plan/` 資料夾

3. **開始實作**
```

/spec_plan_implement 開始編寫方案對應的代碼

```

4. **完成並歸檔**
```

/spec_plan_accomplish 工作完成

```

---

## 特色

✨ **快速規劃** — 輸入需求即可得到完整的開發方案
🎯 **系統追蹤** — 所有方案自動組織管理
📚 **知識累積** — 技術決策和設計理由完整記錄
🔄 **持續迭代** — 支持方案修改與優化
🏗️ **架構理解** — 快速查看和理解現有代碼結構
---

## 重點說明

### ✅ 核心概念

1. **先規劃後實作**

- `proposal` 和 `modify` → 只產生文件，不寫程式
- `implement` → 才開始寫程式
2. **命名規則**

- 提案簡稱：小寫 + 連字號
- 例如：`user-auth`、`todo-feature`
3. **文件位置**

- 方案 → `@fastplan/plan/`
- Bug → `@fastplan/bug/`
- 完成 → `@fastplan/accomplish/`

### 📝 方案文件包含

每個方案文件都會包含：

- 背景與目標
- 問題拆解
- 實施方案
- 里程碑（可勾選的子任務清單）

---

## 完整流程範例

### 範例：Todo 功能開發

```

第 1 步：規劃
→ /spec_plan_proposal
→ 產生 todo-feature_plan.md

第 2 步：實作
→ /spec_plan_implement
→ 開始寫程式

第 3 步：發現 Bug
→ /spec_bugPlan_proposal
→ 產生 bug 方案

第 4 步：修復
→ /spec_bugPlan_implement
→ 修復 Bug

第 5 步：合併
→ /spec_merge_bugplan_plan
→ 更新主計畫

第 6 步：歸檔
→ /spec_plan_accomplish
→ 移到 accomplish/

```

---

## AI 執行細節（給 AI 參考）

<details>
<summary>點擊展開詳細流程</summary>

### `/spec_plan_proposal`

1. 提問澄清需求
2. 搜集程式碼與資料
3. 拆解問題
4. 擬定方案
5. 產生 `_plan.md` 與 `_plan_summary.md`

### `/spec_plan_modify`

1. 調研改動
2. 查閱現有 plan
3. 比較差異
4. 更新方案
5. 產生 `_plan_modify.md`

### `/spec_plan_implement`

- 依照里程碑逐步實作
- 勾選完成的子任務

### `/spec_plan_accomplish`

1. 刪除臨時文件
2. 移動到 accomplish/
3. 處理衝突

### `/spec_bugPlan_proposal`

1. 理解 Bug 現象
2. 查看程式碼與原 plan
3. 歸納差異
4. 擬定修復方案
5. 產生 `_bug_revise_plan.md`

### `/spec_bugPlan_modify`

1. 調研補充需求
2. 查閱 bug plan
3. 修訂方案
4. 產生 `_bug_revise_plan_modify.md`

### `/spec_bugPlan_implement`

- 依照 bug plan 修復
- 勾選子任務
- 記錄新問題

### `/spec_merge_bugplan_plan`

1. 解析章節對應
2. 差異更新
3. 清理暫時性語句
4. 完整性檢查
5. 更新主 plan
6. 刪除 bug summary

### `/spec_find_why`

1. 引導描述問題
2. 搜尋程式碼
3. 分析原理
4. 提供說明與示例
5. 輸出到 knowledge/

### `/spec_check_code_architecture`

1. 引導說明功能
2. 搜尋整理程式碼
3. 歸納核心概念
4. 提供簡潔說明
5. 輸出到 knowledge/

</details>

---

## 快速參考

| 指令                              | 用途          | 輸出                      |
| --------------------------------- | ------------- | ------------------------- |
| `/spec_plan_proposal`           | 新功能規劃    | `@fastplan/plan/`       |
| `/spec_plan_modify`             | 修改方案      | `@fastplan/plan/`       |
| `/spec_plan_implement`          | 實作          | 程式碼                    |
| `/spec_plan_accomplish`         | 歸檔          | `@fastplan/accomplish/` |
| `/spec_bugPlan_proposal`        | Bug 規劃      | `@fastplan/bug/`        |
| `/spec_bugPlan_modify`          | 修改 Bug 方案 | `@fastplan/bug/`        |
| `/spec_bugPlan_implement`       | 修復          | 程式碼                    |
| `/spec_merge_bugplan_plan`      | 合併          | `@fastplan/plan/`       |
| `/spec_find_why`                | 探索原理      | `@fastplan/knowledge/`  |
| `/spec_check_code_architecture` | 檢查架構      | `@fastplan/knowledge/`  |

---

## 多語言支援

所有指令都會自動使用與使用者相同的語言進行回應與文件撰寫。
```
