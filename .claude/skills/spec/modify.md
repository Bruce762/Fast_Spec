# modify — 修改方案

## 目的

對使用者提出的改動，調研並更新 `@fastplan/plan/[提案簡稱]_plan.md`（不需實作）。

## Superpowers Skills

**REQUIRED SUB-SKILL**：更新方案文件時，呼叫 `superpowers:writing-plans` skill，依其結構修訂計劃。

## 作業流程

1. 定位計劃檔案：
   * 優先檢查 `@fastplan/plan/[提案簡稱]_plan.md`
   * 若不存在，再檢查 `@fastplan/pending_test/[提案簡稱]_plan.md`
   * 兩處都不存在 → 告知使用者找不到計劃，直接結束
2. 針對使用者的改動進行調研，查閱計劃檔案與相關程式
3. 比較差異，有疑問向使用者提問，思考後規劃改動內容
4. 將修訂內容更新至計劃檔案
5. 若計劃檔案位於 `@fastplan/pending_test/`，更新後將其移回 `@fastplan/plan/`（代表計劃退回規劃狀態，需重新執行 implement）

## 命名規範
* **提案簡稱** ：使用小寫、連字號，例：`task-refactor`、`onboarding-flow`。

## 輸出後提示

方案更新完畢後，必須在回覆末尾加上以下提示：

> 方案已更新。若要開始實作，請執行 `/spec implement [提案簡稱]`。尚未執行 implement 前，請勿自行修改任何程式碼。

## 使用語言

使用與使用者相同的語言即可
