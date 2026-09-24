# antigravity-doc-template

[English](README.md) | 繁體中文

一個專為 Google Antigravity（AGY）外掛程式（Plugin）設計的標準化文件模版與自動化雙語文件生成工具。

全面支援 Google Antigravity（AGY）的三大核心平台：Antigravity 命令列介面（Command-Line Interface / CLI）（`agy`）、Antigravity 整合開發環境（Integrated Development Environment / IDE）以及 Antigravity 2.0 桌面應用程式。

## 如何安裝

透過 Antigravity 命令列介面（CLI）進行全域安裝：

```bash
agy plugin install https://github.com/AndyAWD/antigravity-doc-template
```

## 特色亮點

1. **標準化雙語架構**：產出對稱一致且乾淨的 `README.md`（英文）與 `README.zh-TW.md`（繁體中文），並提供頂部雙向無縫跳轉連結。
2. **單行獨立指令一鍵複製**：嚴格將每一行 CLI 與斜線指令（Slash Command）獨立封裝於專屬程式碼區塊中，方便使用者直接點擊 GitHub 右上角複製按鈕。
3. **智慧自動化萃取詮釋資料**：全自動分析任何外掛專案中的 `plugin.json`、`package.json` 與 `skills/` 目錄，無需手動撰寫即可快速產出完整文件。
4. **結構清晰的目錄視覺化**：整合直觀的 ASCII 資料夾樹狀圖與各核心元件逐項用途解說。
5. **全平台無縫相容**：相容於 CLI 終端機、IDE 側邊欄對話框以及 2.0 桌面版的對話畫布（Chat Canvas）。

## 如何管理與切換外掛程式

  • 列出已安裝外掛：
    ```bash
    agy plugin list
    ```

  • 啟用外掛：
    ```bash
    agy plugin enable antigravity-doc-template
    ```

  • 停用外掛：
    ```bash
    agy plugin disable antigravity-doc-template
    ```

  • 移除外掛：
    ```bash
    agy plugin uninstall antigravity-doc-template
    ```

> 在 Antigravity 2.0 左側欄的 **Skills & Customizations** 面板中，亦可即時檢視外掛載入狀態。

## 專案資料夾目錄

```text
antigravity-doc-template/
├── .github/
│   └── PULL_REQUEST_TEMPLATE.md
├── plugin.json
├── package.json
├── LICENSE
├── README.md
├── README.zh-TW.md
├── templates/
│   ├── README.template.md
│   ├── README.zh-TW.template.md
│   ├── RELEASE.template.md
│   ├── PULL_REQUEST_TEMPLATE.md
│   ├── PULL_REQUEST_TEMPLATE.en.md
│   └── PULL_REQUEST_TEMPLATE.bilingual.md
└── skills/
    ├── agy-doc-readme/
    │   └── SKILL.md
    ├── agy-doc-release/
    │   └── SKILL.md
    └── agy-doc-github-pr/
        └── SKILL.md
```

## 指令功能說明

安裝完成後，可在任何 AGY 介面透過語意對話或輸入對應的斜線指令（Slash Command）觸發：

### 1. 雙語說明文件生成器（agy-doc-readme）

```text
/antigravity-doc-template:agy-doc-readme
```

- **使用情境**：建立全新 Antigravity 外掛程式、準備發布至 GitHub，或需要自動同步更新既有外掛 README 文件時。
- **運作流程**：
  1. 檢查目前專案根目錄，解析 `plugin.json`、`package.json` 並偵測 Git 遠端網址。
  2. 掃描 `skills/` 目錄，提取所有註冊技能名稱、觸發時機、工作流程與參數。
  3. 嚴格依照雙語模版標準規格產出或更新 `README.md` 與 `README.zh-TW.md`。

### 2. 雙語 GitHub Release 生成器（agy-doc-release）

```text
/antigravity-doc-template:agy-doc-release
```

- **使用情境**：準備釋出新版號、打標籤（Tag）或建立正式 GitHub Release 發布紀錄時。
- **運作流程**：
  1. 檢查上一個 Git 標籤，計算兩者間的提交區間（`git log <上一個Tag>..HEAD`）。
  2. 依據慣例式提交規範（Conventional Commits）精準歸類變更（新功能、修正、重構、效能、樣式、測試、文件、雜項）。
  3. 產出中英文雙語章節（`English` 與 `繁體中文`）、貢獻者標註與完整比對連結的發布日誌。
  4. 確認後可直接透過 GitHub CLI（`gh release create`）發布至 GitHub。

### 3. GitHub PR 描述生成器（agy-doc-github-pr）

```text
/antigravity-doc-template:agy-doc-github-pr
```

- **使用情境**：準備發起拉取請求（Pull Request）、提交程式碼審查（Code Review）或發布功能分支時。
- **運作流程**：
  1. 檢查分支狀態與遠端追蹤，計算相對於 main 主分支的提交與差異。
  2. **建立 PR 內容前，強制使用 `ask_question` 互動式詢問語言偏好**（1. 繁體中文、2. 英文、3. 中英雙語對照）。
  3. 依據所選語言自動萃取修改目的與變更摘要，並精準勾選對應的變更類型與受影響元件。
  4. 條列結構化測試驗證步驟、結果與提交前檢查清單。
  5. 審核確認後可直接透過 GitHub CLI（`gh pr create`）發布至 GitHub。

## 授權條款

本專案採用 MIT 授權條款釋出，詳情請參閱 [LICENSE](LICENSE) 檔案。
