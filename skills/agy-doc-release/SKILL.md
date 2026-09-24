---
name: agy-doc-release
description: 專為 GitHub Release 設計的雙語發布說明（Release Notes）生成技能。自動比對 Git 提交歷史，依照 antigravity-cli-statusline v1.7.0 標準格式產生中英文雙語變更日誌（Changelog），並支援直接透過 GitHub CLI 建立 Release。當使用者輸入 /antigravity-doc-template:agy-doc-release 或提及「產生 Release Notes」、「建立 Release」時觸發。
---

# agy-doc-release

本技能專門為 Google Antigravity 外掛程式（Plugin）建立標準化、分類嚴謹且美觀的中英文雙語 GitHub 發布說明（Release Notes）。

## 觸發時機

當符合以下任一條件時觸發本技能：
1. 使用者輸入斜線指令（Slash Command）：`/antigravity-doc-template:agy-doc-release`。

## 執行流程

本技能執行時，請依照下列步驟依序進行：

### 步驟 1：確認版本號與目標標籤

1. 檢查目前專案的最新版號：
   - 讀取 `package.json` 或 `plugin.json` 中的 `version` 欄位。
   - 執行 `git describe --tags --abbrev=0` 查詢上一個 Git 標籤（Tag）。
2. 若使用者未明確指定發布版本號，向使用者確認預計發布的版本號（例如 `v1.1.0`）。

### 步驟 2：擷取與分類 Git 提交歷史

1. 確保遠端狀態同步：
   - 執行 `git fetch --all --tags` 確保取得全域最新標籤與節點。
2. 擷取 Commit 紀錄：
   - 執行 `git log <上一個Tag>..HEAD --oneline`（若無任何舊標籤，則取得所有歷史紀錄）。
3. 依據慣例式提交（Conventional Commits）規範分析變更並歸類：
   - `feat:` -> 英文：`**Feat:**` / 繁體中文：`**新功能:**`
   - `fix:` -> 英文：`**Fix:**` / 繁體中文：`**修正:**`
   - `refactor:` -> 英文：`**Refactor:**` / 繁體中文：`**重構:**`
   - `perf:` -> 英文：`**Perf:**` / 繁體中文：`**效能:**`
   - `style:` -> 英文：`**Style:**` / 繁體中文：`**樣式:**`
   - `test:` -> 英文：`**Test:**` / 繁體中文：`**測試:**`
   - `docs:` -> 英文：`**Docs:**` / 繁體中文：`**文件:**`
   - `chore:` -> 英文：`**Chore:**` / 繁體中文：`**雜項:**`
4. 獲取 Commit 作者的 GitHub 帳號名稱（例如 `@AndyAWD`）。

### 步驟 3：產出雙語發布說明內容

**排版規範**：嚴格禁止在發布說明中使用任何 Emoji 表情符號，保持純文字排版的專業性與簡潔風格。

依據 `templates/RELEASE.template.md` 規範產出 Markdown 內容：

```markdown
### What's Changed

#### English

- **Feat:** [英文描述] by @[GitHub 帳號]
- **Fix:** [英文描述] by @[GitHub 帳號]

#### 繁體中文

- **新功能:** [繁體中文描述] by @[GitHub 帳號]
- **修正:** [繁體中文描述] by @[GitHub 帳號]

**Full Changelog**: https://github.com/<owner>/<repo>/compare/<上一個Tag>...<本次版本號>
```

### 步驟 4：發布確認與 GitHub CLI 整合

1. 先將整理好的雙語發布說明呈現給使用者審閱。
2. 檢查 GitHub 命令列介面（GitHub CLI）（`gh`）登入狀態：
   - 執行 `gh auth status`。
3. 若使用者確認內容無誤且 GitHub CLI 已登入，可協助執行指令建立正式 Release：
   ```bash
   gh release create <版本號> --title "<版本號>" --notes "<發布說明內容>"
   ```
4. 若未安裝或未登入 GitHub CLI，提供產出的 Markdown 文本供使用者手動複製至 GitHub 網頁發布。
