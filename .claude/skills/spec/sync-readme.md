# sync-readme — 同步 README

## 目的

掃描自上次紀錄以來的 git commit，理解程式實際發生了什麼變化，然後判斷 README.md 哪些地方需要對應更新，直接融入原有內容。若無新 commit 或無變動則不修改，直接結束。

---

## 作業流程

### 步驟 1：讀取上次紀錄的 commit

1. 讀取 `README.md`，尋找標記行：
   ```
   <!-- last-synced-commit: <hash> -->
   ```
2. 若找到 → 將 `<hash>` 作為基準點（`BASE_COMMIT`）
3. 若找不到 → `BASE_COMMIT` 設為空（代表這是第一次執行）

### 步驟 2：檢查是否有新的 commit

```bash
git log --oneline <BASE_COMMIT>..HEAD -- . ':(exclude)CHANGELOG.md' ':(exclude)README.md' ':(exclude)CLAUDE.md'   # 有 BASE_COMMIT 時
git log --oneline -- . ':(exclude)CHANGELOG.md' ':(exclude)README.md' ':(exclude)CLAUDE.md'                        # 無 BASE_COMMIT 時
```

若輸出為空，或 HEAD 與 BASE_COMMIT 相同 → 告知使用者無新 commit，直接結束，不修改任何檔案。

### 步驟 3：理解變動內容

```bash
git diff <BASE_COMMIT>..HEAD -- . ':(exclude)CHANGELOG.md' ':(exclude)README.md' ':(exclude)CLAUDE.md'            # 有 BASE_COMMIT 時
git diff $(git rev-list --max-parents=0 HEAD)..HEAD -- . ':(exclude)CHANGELOG.md' ':(exclude)README.md' ':(exclude)CLAUDE.md'  # 無 BASE_COMMIT 時
```

閱讀 diff 內容，理解這些 commit **實際做了什麼事**，例如：
- 新增了某個功能、指令、設定
- 修改了某段邏輯或說明
- 移除了某些檔案或功能

重點是語意上發生了什麼，不是逐檔列出。

### 步驟 4：更新 `CHANGELOG.md`（追加在最上方）

依據步驟 3 的理解，將本次同步的改動寫入專案根目錄的 `CHANGELOG.md`（與 `README.md` 同層）。

1. 取得本次範圍的 commit 清單（用短 hash）：
   ```bash
   git log --pretty=format:'- %h %s' <BASE_COMMIT>..HEAD -- . ':(exclude)CHANGELOG.md' ':(exclude)README.md' ':(exclude)CLAUDE.md'
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

**原則：摘要要能讓未來的自己快速回想起這批 commit 主要做了什麼。即使 README/CLAUDE.md 不需要更新，CHANGELOG.md 仍要寫入。**

### 步驟 5：判斷 README.md 哪裡需要更新

讀取整份 `README.md`，依據步驟 3 理解的變動，判斷：
- 哪些段落、表格、說明與這次變動有關
- 是否有新功能需要補上、舊描述需要修正、已移除的內容需要刪除

**原則：只改有關聯的地方，維持 README 原本的結構與風格，文字精簡融入，不另開新區塊。**

### 步驟 6：更新 README.md

直接修改 README.md 對應的段落，同時將標記行更新為最新 commit hash：

```
<!-- last-synced-commit: <git rev-parse HEAD 的結果> -->
```

若 README 中原本沒有這行，加在文件最末尾（單獨一行，不加任何說明文字）。

### 步驟 7：同步更新 CLAUDE.md（若存在）

若 `CLAUDE.md` 存在，依據步驟 3 理解的變動，判斷哪些段落需要對應更新：
- 新增/移除的模組或服務
- 執行指令的變動
- 目錄結構的異動
- 關鍵設計決策的調整

**原則：只改有關聯的地方，維持 CLAUDE.md 原本的結構與風格，不另開新區塊。CLAUDE.md 內容應精簡，不重複 README 的描述性內容。**

### 步驟 8：同步指令副本（僅適用於指令集原始 repo）

**觸發條件**：專案根目錄同時存在 `commands/` 與 `.claude/skills/spec/`（代表這是 fast_spec 指令集本身的 repo）。不符合條件則跳過此步驟。

以 `commands/` 為準，逐一檢查並同步以下三份副本：

1. `.claude/commands/[同名].md` — 內容需與 `commands/` 完全一致，不一致則直接覆蓋
2. `.github/prompts/[同名].prompt.md` — 內容需與 `commands/` 完全一致，不一致則直接覆蓋
3. `.claude/skills/spec/[子指令名].md` — 內容相同，但格式轉換：
   * 檔案開頭為 `# [子指令] — [中文名]` 標題行，其餘標題層級降一級（`#` → `##`）
   * 指令參照轉為 skill 呼叫格式：`/spec_plan_◯◯` → `/spec ◯◯`

**指令參照格式原則**：`commands/`（及其直接複製的兩份副本）內文中提及其他指令時，一律使用完整指令名（`/spec_plan_◯◯`）；`/spec ◯◯` 短格式僅存在於 skill 版轉換後的檔案中。

若 `commands/` 有新增或刪除指令，同步更新 `.claude/skills/spec/SKILL.md` 的子指令對照表與 frontmatter description。

---

## 使用語言

使用與使用者相同的語言即可
