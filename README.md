# 🚀 我的 Dream 個人部落格 (Hugo + GitHub Actions)

本專案是一個基於 **Hugo Extended** 靜態網站生成器與 **Dream** 炫麗高質感主題打造的個人部落格。支援完整的 **AI Agent 專案規範 (`AGENTS.md`)**、**工作流程手冊 (`SKILLS.md`)** 以及 **GitHub Actions 全自動化雲端部署**。

- 🌐 **雲端公開網址**：[https://lkoj74.github.io/hugo-0803/](https://lkoj74.github.io/hugo-0803/)
- 💻 **本地伺服器**：`http://localhost:1313/`
- 📦 **GitHub 儲存庫**：`https://github.com/lkoj74/hugo-0803.git`

---

## 📌 專案特色與架構

```
your-project/
├── AGENTS.md             ← 給 AI 助理的專案規則書 (AI 自動讀取)
├── SKILLS.md             ← 常用工作流程手冊 (發文/更換主題/發布)
├── hugo.toml             ← Hugo 核心配置檔 (Dream 主題與 Giscus 設定)
├── .github/workflows/    ← GitHub Actions 雲端全自動化部署腳本
├── content/posts/        ← 部落格文章目錄 (Page Bundles 圖片與文章)
├── layouts/              ← 客製化 Layout 覆蓋 (大頭貼/網站計數器/WebP Pipeline)
├── themes/dream/         ← Dream 主題全套範本檔案 (100% 完整追蹤)
└── static/img/           ← 靜態資源目錄
```

---

## ⚡ 實戰宣言語自動化流程

`本地電腦` ➔ `Hugo 網站` ➔ `GitHub` ➔ `GitHub Actions 自動部署` ➔ `公開網址`

每一次您在本地寫完文章並執行 `git push -u origin main`：
1. **GitHub Actions 雲端小幫手** 自動啟動。
2. 在雲端自動執行 `hugo --minify` 編譯產出全套靜態網頁。
3. 自動推送到 `gh-pages` 分支並發表至 GitHub Pages 雲端伺服器！

---

## 🛠️ 給 AI 與開發者的專案文件

本專案遵循最新 AI 輔助開發標準：
- **`AGENTS.md`**：定義語言規範（繁體中文）、主題保護機制與 Git 免費避坑防護。
- **`SKILLS.md`**：提供發布文章、切換主題與本地預覽的 Standard Operating Procedures (SOP)。

---

## 🎨 包含的高級優化

1. **Giscus 留言系統**：整合 GitHub Discussions 免費無廣告留言板。
2. **自動圖片壓縮 Pipeline**：Markdown 中圖片自動轉為 WebP 格式並啟用 85% 品質壓縮與懶加載。
3. **SEO 與 OpenGraph**：包含 Facebook/LINE/Twitter 動態圖文分享卡片。
4. **客製化頂部元件**：包含動態網站訪客計數器與固定比例精緻大頭貼。

---

© 2026 Powered by Hugo with theme Dream.
