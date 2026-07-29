---
name: spec-sync-readme
description: Use when the user invokes `$spec-sync-readme` or asks to update README, CHANGELOG, and applicable instruction copies from commits since the previous sync.
---

# Spec sync README

# 目的

掃描自上次紀錄以來的 git commit，理解程式實際發生了什麼變化，然後判斷 README.md 哪些地方需要對應更新，直接融入原有內容。若無新 commit 或無變動則不修改，直接結束。

---

# 作業流程

## 步驟 1：讀取上次紀錄的 commit

1. 讀取 `README.md`，尋找標記行：
   ```
   <!-- last-synced-commit: <hash> -->
   ```
2. 若找到 → 將 `<hash>` 作為基準點（`BASE_COMMIT`）
3. 若找不到 → `BASE_COMMIT` 設為空（代表這是第一次執行）

## 步驟 2：檢查是否有新的 commit

```bash
git log --oneline <BASE_COMMIT>..HEAD -- . ':(exclude)CHANGELOG.md' ':(exclude)README.md' ':(exclude)CLAUDE.md' ':(exclude)AGENTS.md'   # 有 BASE_COMMIT 時
git log --oneline -- . ':(exclude)CHANGELOG.md' ':(exclude)README.md' ':(exclude)CLAUDE.md' ':(exclude)AGENTS.md'                        # 無 BASE_COMMIT 時
```

若輸出為空，或 HEAD 與 BASE_COMMIT 相同 → 告知使用者無新 commit，直接結束，不修改任何檔案。

## 步驟 3：理解變動內容

```bash
git diff <BASE_COMMIT>..HEAD -- . ':(exclude)CHANGELOG.md' ':(exclude)README.md' ':(exclude)CLAUDE.md' ':(exclude)AGENTS.md'            # 有 BASE_COMMIT 時
git diff $(git rev-list --max-parents=0 HEAD)..HEAD -- . ':(exclude)CHANGELOG.md' ':(exclude)README.md' ':(exclude)CLAUDE.md' ':(exclude)AGENTS.md'  # 無 BASE_COMMIT 時
```

閱讀 diff 內容，理解這些 commit **實際做了什麼事**，例如：
- 新增了某個功能、指令、設定
- 修改了某段邏輯或說明
- 移除了某些檔案或功能

重點是語意上發生了什麼，不是逐檔列出。

## 步驟 4：更新 `CHANGELOG.md`（追加在最上方）

依據步驟 3 的理解，將本次同步的改動寫入專案根目錄的 `CHANGELOG.md`（與 `README.md` 同層）。

1. 取得本次範圍的 commit 清單（用短 hash）：
   ```bash
   git log --pretty=format:'- %h %s' <BASE_COMMIT>..HEAD -- . ':(exclude)CHANGELOG.md' ':(exclude)README.md' ':(exclude)CLAUDE.md' ':(exclude)AGENTS.md'
   ```
2. 組出本次的新區段，格式如下：
   ```markdown
   ## YYYY-MM-DD｜<base_short>..<head_short>

   **Commits**：
   - <short_hash> <subject>
   - ...

   **改動摘要**：
   <1–3 段語意說明這次到底做了什麼。重點是「做了什麼、為什麼」，不要把 commit message 串起來貼上。>
   ```
   - 日期用今天的日期（YYYY-MM-DD）
   - `<base_short>` 為 BASE_COMMIT 的短 hash；首次執行（無 BASE_COMMIT）時用 `initial`
   - `<head_short>` 為 `git rev-parse --short HEAD` 結果
3. 寫入規則：
   - 若 `CHANGELOG.md` 不存在 → 建立檔案，第一行為 `# Changelog`，空一行後放本次區段。
   - 若 `CHANGELOG.md` 已存在 → 將本次新區段插入在 `# Changelog` 標題之後、所有舊區段之前（最新在最上方）。

**原則：摘要要能讓未來的自己快速回想起這批 commit 主要做了什麼。即使 README/CLAUDE.md/AGENTS.md 不需要更新，CHANGELOG.md 仍要寫入。**

## 步驟 5：判斷 README.md 哪裡需要更新

讀取整份 `README.md`，依據步驟 3 理解的變動，判斷：
- 哪些段落、表格、說明與這次變動有關
- 是否有新功能需要補上、舊描述需要修正、已移除的內容需要刪除

**原則：只改有關聯的地方，維持 README 原本的結構與風格，文字精簡融入，不另開新區塊。**

## 步驟 6：更新 README.md

直接修改 README.md 對應的段落，同時將標記行更新為最新 commit hash：

```
<!-- last-synced-commit: <git rev-parse HEAD 的結果> -->
```

若 README 中原本沒有這行，加在文件最末尾（單獨一行，不加任何說明文字）。

## 步驟 7：同步更新 CLAUDE.md 與 AGENTS.md（若存在）

分別檢查專案根目錄的 `CLAUDE.md` 與 `AGENTS.md`。任一檔案存在時，依據步驟 3 理解的變動，判斷該檔案哪些段落需要對應更新：
- 新增/移除的模組或服務
- 執行指令的變動
- 目錄結構的異動
- 關鍵設計決策的調整

檔案不存在時直接略過，不建立新檔；兩個檔案不必同時存在。

**原則：只改有關聯的地方，維持各檔案原本的結構與風格，不另開新區塊。內容應精簡，不重複 README 的描述性內容。**

---

# 使用語言

使用與使用者相同的語言即可
