---
name: spec-plan-discuss
description: Use when the user invokes `$spec-plan-discuss` or wants to discuss and clarify a proposed project change before creating a plan. Do not implement code in this workflow.
---

# Spec plan discuss

# 目的

與使用者進行多輪討論與提問，釐清需求與方向，為後續 proposal 做準備。

# Superpowers Skills

**REQUIRED SUB-SKILL**：開始討論前，先呼叫 `superpowers:brainstorming` skill，借用其「多輪提問、探索使用者意圖與需求方向」的流程。

**覆寫 brainstorming 的收尾**：本階段**不寫任何 design doc 檔、不 commit、也不進入 writing-plans**。討論結論只以對話呈現，實際計劃檔留給 `$spec-plan-proposal` 建立。

# 規則

**此階段嚴禁實作任何程式碼。**

AI 的職責僅限於：
- 提問釐清需求
- 分析與討論方向
- 回答使用者的疑問

討論可進行多輪，直到使用者認為需求已明確為止。

# 作業流程

1. 讀取使用者描述的問題或想法
2. 若需求模糊，主動提問釐清
3. 分析可能的方向與取捨，與使用者來回討論
4. 討論完畢後，提示使用者執行 proposal

# 結束提示

每輪討論回覆末尾，若判斷需求已趨於明確，加上以下提示：

> 若需求已討論清楚，可執行 `$spec-plan-proposal [提案簡稱]` 開始建立計劃。

# 使用語言

使用與使用者相同的語言即可
