# fast_spec

一套 Claude Code 自訂指令集與 Skill，讓 AI 輔助開發流程標準化。所有計劃文件統一存放於 `fastplan/` 目錄，透過指令驅動計劃 → 實作 → 歸檔的完整工作流。

> `fastplan/` 下的所有 `.md` 文件皆由指令**自動生成與管理**，包含檔案命名，無需手動建立或編輯。

---

## 目錄結構

```
fastplan/
├── plan/          # 進行中的計劃文件
├── pending_test/  # 實作完成、待測試的計劃
├── accomplish/    # 已完成歸檔的計劃
├── bug/           # bug 回報記錄
└── knowledge/     # 技術說明文件
```

---

## 指令總覽

支援兩種呼叫方式，功能完全相同：
- **Skill**（推薦）：`/spec [子指令]`，例如 `/spec proposal`
- **Command**：`/spec_plan_proposal`、`/spec_plan_implement` …

### 計劃生命週期

| 子指令 | Command 對應 | 功能 |
|--------|-------------|------|
| `proposal` | `/spec_plan_proposal` | 根據需求建立計劃文件 `fastplan/plan/[名稱]_plan.md` |
| `modify` | `/spec_plan_modify` | 修改現有計劃 |
| `findbug` | `/spec_plan_findbug` | 審查計劃邏輯，找出 bug、矛盾或遺漏（不實作）|
| `implement` | `/spec_plan_implement` | 依計劃實作程式，完成後將計劃移至 `pending_test/` |
| `accomplish` | `/spec_plan_accomplish` | 測試通過後，將計劃歸檔至 `accomplish/` |

### 知識與維護

| 子指令 | Command 對應 | 功能 |
|--------|-------------|------|
| `check-architecture` | `/spec_check_code_architecture` | 查詢功能/框架用法，輸出說明文件至 `fastplan/knowledge/` |
| `find-why` | `/spec_find_why` | 解釋某段行為「為什麼會這樣」，輸出至 `fastplan/knowledge/` |
| `sync-readme` | `/spec_sync_readme` | 掃描新 commit，自動同步更新 `README.md` 與 `CLAUDE.md` |

---

## 標準工作流

```
proposal → (modify) → findbug → implement → (測試) → accomplish
```

1. `/spec_plan_proposal` — 描述需求，生成計劃
2. `/spec_plan_modify` — 視需求調整計劃（可選）
3. `/spec_plan_findbug` — 審查計劃找出風險
4. `/spec_plan_implement` — 實作，計劃自動移至 `pending_test/`
5. 手動測試
6. `/spec_plan_accomplish` — 歸檔，計劃移至 `accomplish/`

---

## 範例：新增使用者登入功能

```
你：/spec_plan_proposal 我想新增 email 登入功能，需要驗證格式、呼叫 API、儲存 token
AI：建立 fastplan/plan/user-login_plan.md
```

發現計劃有遺漏，先審查再修正：

```
你：/spec_plan_findbug user-login
AI：發現未處理 token 過期的情境，建議補上 refresh 邏輯

你：/spec_plan_modify user-login 補上 token refresh 機制
AI：更新 user-login_plan.md
```

確認計劃沒問題，開始實作：

```
你：/spec_plan_implement user-login
AI：實作完成，user-login_plan.md 移至 fastplan/pending_test/
```

手動測試通過後歸檔：

```
你：/spec_plan_accomplish user-login
AI：user-login_plan.md 歸檔至 fastplan/accomplish/
```

---

## 命名規範

計劃簡稱使用**小寫 + 連字號**，例：`user-auth`、`task-refactor`

生成檔案路徑：
- `fastplan/plan/[名稱]_plan.md`
- `fastplan/pending_test/[名稱]_plan.md`（實作後）
- `fastplan/accomplish/[名稱]_plan.md`（歸檔後）

---

## 安裝

| 功能 | 來源目錄 | 放入目錄 |
|------|---------|---------|
| Skill `/spec` | `.claude/skills/spec/` | 專案 `.claude/skills/spec/` |
| Command `/spec_*` | `.claude/commands/` 或 `commands/` | 專案 `.claude/commands/` |

擇一安裝即可，推薦使用 Skill。

<!-- last-synced-commit: 1d40a3a4ef0298e2f21971da397ee29c9e980cfd -->
