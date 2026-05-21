---
name: spec
description: 統一規劃與開發工作流程入口。子指令：proposal（規劃方案）、implement（實施）、modify（修改方案）、findbug（找 bug）、accomplish（歸檔）、check-architecture（了解架構）、find-why（解釋原因）、sync-readme（同步 README 並維護 CHANGELOG.md）。呼叫格式：/spec [子指令] [提案簡稱]
disable-model-invocation: false
---

# 使用方式

`/spec [子指令] [提案簡稱（若適用）]`

根據子指令讀取對應流程檔案並執行：

| 子指令 | 流程檔案 |
|--------|---------|
| proposal | .claude/skills/spec/proposal.md |
| implement | .claude/skills/spec/implement.md |
| modify | .claude/skills/spec/modify.md |
| findbug | .claude/skills/spec/findbug.md |
| accomplish | .claude/skills/spec/accomplish.md |
| check-architecture | .claude/skills/spec/check-architecture.md |
| find-why | .claude/skills/spec/find-why.md |
| sync-readme | .claude/skills/spec/sync-readme.md |

讀取對應流程檔案後，依照其中的作業流程執行。

若未指定子指令，列出上表供使用者選擇。
