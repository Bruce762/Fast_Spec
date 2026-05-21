# fast_spec

一套讓 AI 輔助開發流程標準化的指令集。透過 8 個子指令驅動 **計劃 → 審查 → 實作 → 測試 → 歸檔** 的完整工作流，所有計劃文件統一存放在 `fastplan/`，由指令自動建立、移動、歸檔，使用者不需手動命名或維護。

支援三種發布目標：Claude Code 的 **Slash Command**、Claude Code 的 **Skill**、以及 GitHub Copilot Chat 的 **prompt**。三套內容完全一致，擇一安裝即可。

---

## fastplan/ 目錄結構

```
fastplan/
├── plan/          # 進行中的計劃
├── pending_test/  # 實作完成、等待手動測試
├── accomplish/    # 測試通過、已歸檔
├── bug/           # findbug 產出的 bug 報告
└── knowledge/     # check-architecture / find-why 產出的技術說明
```

> 所有 `.md` 文件（含檔名）皆由指令**自動生成與管理**，請勿手動建立或編輯。

---

## 指令總覽

兩種呼叫方式擇一，功能完全相同：

- **Claude Command**（推薦）：`/spec_plan_proposal`、`/spec_plan_implement` …
- **Claude Skill**：`/spec [子指令]`，例如 `/spec proposal`

### 計劃生命週期

| 子指令 | Command 對應 | 功能 |
|--------|-------------|------|
| `proposal` | `/spec_plan_proposal` | 依需求建立 `fastplan/plan/[名稱]_plan.md`，含預期改動 |
| `modify` | `/spec_plan_modify` | 修改現有計劃 |
| `findbug` | `/spec_plan_findbug` | 審查計劃邏輯，找出 bug、矛盾或遺漏（不實作） |
| `implement` | `/spec_plan_implement` | 依計劃實作，完成後將計劃移至 `pending_test/` |
| `accomplish` | `/spec_plan_accomplish` | 測試通過後歸檔至 `accomplish/` |

### 知識與維護

| 子指令 | Command 對應 | 功能 |
|--------|-------------|------|
| `check-architecture` | `/spec_check_code_architecture` | 查詢功能/框架用法，輸出至 `fastplan/knowledge/` |
| `find-why` | `/spec_find_why` | 解釋某段行為「為什麼會這樣」，輸出至 `fastplan/knowledge/` |
| `sync-readme` | `/spec_sync_readme` | 掃描自上次同步以來的 commit，更新 `README.md` 與 `CLAUDE.md`，並在 `CHANGELOG.md` 最上方追加本次改動摘要 |

---

## 標準工作流

```
proposal → (modify) → findbug → implement → 手動測試 → accomplish
```

1. `/spec_plan_proposal` — 描述需求，生成計劃
2. `/spec_plan_modify` — 視需求調整計劃（可選）
3. `/spec_plan_findbug` — 審查計劃，找出風險與遺漏
4. `/spec_plan_implement` — 實作，計劃自動移至 `pending_test/`
5. 手動測試
6. `/spec_plan_accomplish` — 歸檔，計劃移至 `accomplish/`

---

## 範例：新增使用者登入功能

建立計劃：

```
你：/spec_plan_proposal 我想新增 email 登入功能，需要驗證格式、呼叫 API、儲存 token
AI：建立 fastplan/plan/user-login_plan.md
```

審查並修正：

```
你：/spec_plan_findbug user-login
AI：發現未處理 token 過期，建議補上 refresh 邏輯

你：/spec_plan_modify user-login 補上 token refresh 機制
AI：更新 user-login_plan.md
```

實作與歸檔：

```
你：/spec_plan_implement user-login
AI：實作完成，user-login_plan.md 移至 fastplan/pending_test/

你：/spec_plan_accomplish user-login
AI：user-login_plan.md 歸檔至 fastplan/accomplish/
```

---

## 命名規範

計劃簡稱使用 **小寫 + 連字號**，例：`user-auth`、`task-refactor`

同一計劃在生命週期中的路徑：

- `fastplan/plan/[名稱]_plan.md` — 建立後
- `fastplan/pending_test/[名稱]_plan.md` — 實作後
- `fastplan/accomplish/[名稱]_plan.md` — 歸檔後

---

## 安裝

依使用工具，將對應目錄複製到自己的專案，擇一即可：

| 工具 | 來源 | 放入專案 |
|------|------|---------|
| Claude Code Command（推薦） | `commands/` 或 `.claude/commands/` | `.claude/commands/` |
| Claude Code Skill | `.claude/skills/spec/` | `.claude/skills/spec/` |
| GitHub Copilot Chat | `.github/prompts/` | `.github/prompts/` |

三套內容完全一致，由 `sync-readme` 在每次 commit 後負責維持同步。

<!-- last-synced-commit: b4f23d37169923414e33b952484b5eb98b60bd93 -->
