---
name: spec-check-architecture
description: Use when the user invokes `$spec-check-architecture` or asks to understand a project feature, framework, or code architecture without implementing changes.
---

# Spec check architecture

# 目的

針對使用者想了解的功能、框架或程式開發問題，搜尋整理相關程式碼，提供清晰說明並附上簡單範例，輸出至 `@fastplan/knowledge`。

# 作業流程

1. 讀取使用者問題（若未指定，引導說明想了解的功能）
2. 搜尋相關程式碼與資料
3. 提供核心概念與用途說明，畫出模組的方塊架構相互關係，附上簡單範例（不需實作）
4. 輸出至 `@fastplan/knowledge`

# 使用語言

使用與使用者相同的語言即可
