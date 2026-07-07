# fast_spec

一套讓 AI 輔助開發流程標準化的指令集。透過 10 個子指令驅動 **討論 → 計劃 → 審查 → 實作 → 驗證 → 歸檔** 的完整工作流，並整合 [superpowers](https://github.com/obra/superpowers) 流程 skills 強化各階段紀律。所有計劃文件統一存放在 `fastplan/`，由指令自動建立、移動、歸檔，使用者不需手動命名或維護。

支援三種發布目標：Claude Code 的 **Slash Command**、Claude Code 的 **Skill**、以及 GitHub Copilot Chat 的 **prompt**。三套內容一致，擇一安裝即可。

---

## 安裝

### 1. 安裝指令集

依使用工具，將對應目錄複製到自己的專案，擇一即可：

| 工具 | 來源 | 放入專案 | 呼叫方式 |
|------|------|---------|---------|
| Claude Code Command（推薦） | `commands/` 或 `.claude/commands/` | `.claude/commands/` | `/spec_plan_proposal` … |
| Claude Code Skill | `.claude/skills/spec/` | `.claude/skills/spec/` | `/spec proposal` … |
| GitHub Copilot Chat | `.github/prompts/` | `.github/prompts/` | `/spec_plan_proposal` … |

### 2. 安裝 superpowers（建議，Claude Code 限定）

生命週期指令會呼叫 superpowers 的流程 skills（見下方 [Superpowers 整合](#superpowers-整合)）。未安裝時指令仍可正常運作，只是少了對應流程的強制約束。

**方式一：Anthropic 官方 marketplace**

```
/plugin install superpowers@claude-plugins-official
```

**方式二：Superpowers marketplace**

先註冊 marketplace：

```
/plugin marketplace add obra/superpowers-marketplace
```

再從該 marketplace 安裝 plugin：

```
/plugin install superpowers@superpowers-marketplace
```

> 僅 Claude Code 支援 superpowers plugin；GitHub Copilot Chat 沒有 Skill 機制，會自然忽略指令中的 superpowers 指示。

---

## 指令總覽

### 計劃生命週期

| 子指令 | Command 對應 | 功能 |
|--------|-------------|------|
| `discuss` | `/spec_plan_discuss` | 多輪討論釐清需求，**嚴禁實作程式碼**，討論完再執行 proposal |
| `proposal` | `/spec_plan_proposal` | 依需求建立 `fastplan/plan/[名稱]_plan.md`，結構自由，但改動效果須為可驗證的核取清單 |
| `modify` | `/spec_plan_modify` | 修改現有計劃；若計劃已在 `pending_test/`（測試發現問題），更新後自動退回 `plan/` |
| `findbug` | `/spec_plan_findbug` | 審查計劃邏輯，找出 bug、矛盾或遺漏（不實作），發現問題時輸出報告至 `fastplan/bug/` |
| `implement` | `/spec_plan_implement` | 依計劃實作，完成後將計劃移至 `pending_test/` |
| `verify` | `/spec_plan_verify` | 依計劃逐項實際驗證改動效果，通過提示歸檔、未通過記錄問題 |
| `accomplish` | `/spec_plan_accomplish` | 測試通過後歸檔至 `accomplish/`，並清理 `fastplan/bug/` 的對應報告 |

### 知識與維護

| 子指令 | Command 對應 | 功能 |
|--------|-------------|------|
| `check-architecture` | `/spec_check_code_architecture` | 查詢功能/框架用法，輸出至 `fastplan/knowledge/` |
| `find-why` | `/spec_find_why` | 解釋某段行為「為什麼會這樣」，輸出至 `fastplan/knowledge/` |
| `sync-readme` | `/spec_sync_readme` | 掃描自上次同步以來的 commit，更新 `README.md` 與 `CLAUDE.md`、在 `CHANGELOG.md` 追加改動摘要，並同步三套指令副本 |

---

## 標準工作流

```
discuss → proposal → (modify) → findbug → implement → verify → accomplish
```

1. `/spec_plan_discuss` — 與 AI 多輪討論需求（嚴禁實作）
2. `/spec_plan_proposal` — 描述需求，生成計劃
3. `/spec_plan_modify` — 視需求調整計劃（可選）
4. `/spec_plan_findbug` — 審查計劃，找出風險與遺漏
5. `/spec_plan_implement` — 實作，計劃自動移至 `pending_test/`
6. `/spec_plan_verify` — AI 依計劃逐項實際驗證改動效果（可選，也可純手動測試）
7. `/spec_plan_accomplish` — 歸檔，計劃移至 `accomplish/`

> 測試（verify 或手動）發現問題時，直接執行 `/spec_plan_modify`——計劃會自動從 `pending_test/` 退回 `plan/`，修改後重新 implement 即可。

---

## fastplan/ 目錄結構

計劃檔案的**位置即狀態**，由指令自動搬移：

```
fastplan/
├── plan/          # 規劃中（或測試未過退回修改中）
├── pending_test/  # 實作完成，等待驗證（verify 或手動測試）
├── accomplish/    # 測試通過，已歸檔
├── bug/           # findbug 產出的 bug 報告（accomplish 時自動清理）
└── knowledge/     # check-architecture / find-why 產出的技術說明
```

> 所有 `.md` 文件（含檔名）皆由指令**自動生成與管理**，請勿手動建立或編輯。

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
AI：發現未處理 token 過期，報告輸出至 fastplan/bug/user-login_bugs.md

你：/spec_plan_modify user-login 補上 token refresh 機制
AI：更新 user-login_plan.md
```

實作、驗證與歸檔：

```
你：/spec_plan_implement user-login
AI：實作完成，user-login_plan.md 移至 fastplan/pending_test/

你：/spec_plan_verify user-login
AI：逐項驗證通過，可執行 accomplish 歸檔

你：/spec_plan_accomplish user-login
AI：user-login_plan.md 歸檔至 fastplan/accomplish/，並清理 bug 報告
```

---

## Superpowers 整合

生命週期指令內建對 [obra/superpowers](https://github.com/obra/superpowers) 流程 skills 的呼叫，讓討論、規劃、實作、驗證各階段套用對應的紀律流程：

| 子指令 | 使用的 superpowers skill | 時機 |
|--------|------------------------|------|
| `discuss` | `brainstorming` | 開始討論前（必用） |
| `proposal` | `writing-plans`、`brainstorming` | 撰寫方案前（必用）；需求模糊且未經 discuss 時 |
| `implement` | `test-driven-development`、`verification-before-completion` | 實作時、宣告完成前（必用） |
| `verify` | `verification-before-completion` | 執行驗證時（必用） |
| `modify` | `writing-plans` | 修訂方案時（必用） |
| `findbug` | `systematic-debugging` | 涉及實際發生的錯誤時（條件式） |
| `find-why` | `systematic-debugging` | 追查現象根因時（必用） |

`accomplish`、`check-architecture`、`sync-readme` 為純檔案／文件操作，不使用 superpowers。

---

## 命名規範

計劃簡稱使用 **小寫 + 連字號**，例：`user-auth`、`task-refactor`

同一計劃在生命週期中的路徑：

- `fastplan/plan/[名稱]_plan.md` — 建立後（或測試未過退回後）
- `fastplan/pending_test/[名稱]_plan.md` — 實作後
- `fastplan/accomplish/[名稱]_plan.md` — 歸檔後
- `fastplan/bug/[名稱]_bugs.md` — findbug 發現問題時產出，歸檔時清除

---

## 維護：三套副本的同步機制

三套指令內容以 `commands/` 為正本，由 `sync-readme` 的「同步指令副本」步驟維持一致：

- `.claude/commands/`、`.github/prompts/` — 直接複製
- `.claude/skills/spec/` — 自動格式轉換：檔案開頭加 `# [子指令] — [中文名]` 標題、標題層級降一級、指令參照轉為 `/spec [子指令]` 短格式

指令內文提及其他指令時，一律使用完整指令名（`/spec_plan_◯◯`）；`/spec ◯◯` 短格式僅存在於 Skill 版轉換後的檔案中。

<!-- last-synced-commit: b4f23d37169923414e33b952484b5eb98b60bd93 -->
