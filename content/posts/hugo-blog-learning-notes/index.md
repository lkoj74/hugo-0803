---
title: "HUGO個人部落格建置學習筆記"
date: 2026-08-03T15:57:00+08:00
draft: false
cover: "cover.jpg"
tags: ["Hugo", "GitHub-Pages", "GitHub-Actions", "Dream主題", "網頁建置", "學習筆記"]
categories: ["技術隨筆"]
summary: "記錄使用 Hugo Extended 搭配 Dream 主題與 GitHub Actions 實現全自動化雲端發布的完整學習歷程與技術心得。"
---

歡迎來到我的全新個人部落格！這篇文章記錄了我使用 **Hugo Extended** 靜態網站生成器，搭配炫麗的 **Dream** 主題，並結合 **GitHub Actions** 實現全自動化雲端發布的完整學習歷程與技術心得。

---

## 💡 為什麼選擇 Hugo？

在眾多靜態網站生成器（如 Hexo, Jekyll, Gatsby 等）中，Hugo 以 **「全球最快編譯速度」**（Go 語言打造）脫穎而出。

1. **極速靜態編譯**：幾千篇文章能在 1 秒之內完成 HTML 渲染。
2. **無資料庫負擔**：所有文章都是 Markdown 檔案，隨時能轉移備份。
3. **雲端託管免費**：完全不需要租用伺服器，配合 GitHub Pages 即可享受免費、高頻寬且安全的全球 CDN 服務。

---

## 🎨 本站核心特色與架構優化

在搭建過程中，我們不僅完成了基礎的網站佈署，還注入了多項進階功能與客製化細節：

### 1. 視覺極致：Dream 炫麗主題與配色
使用了 Dream 主題，並調配了 **`emerald` (翡翠亮色)** 與 **`forest` (森林暗色)** 的深淺模組切換。

### 2. 導覽列客製化與大頭貼保護
- **48px 大頭貼鎖定**：在大頭貼 CSS 中加上 `48px × 48px` 與 `flex-shrink-0` 限制，防止滿版伸展。
- **動態訪客計數器**：在導覽列即時顯示造訪人次。

### 3. 高級效能 Pipeline (WebP 自動圖片壓縮)
透過 Hugo 的 Resource Hook，文章中的 Markdown 圖片在編譯時會**自動轉換為高壓縮率的 WebP 格式**（85% 品質壓縮），並自動加上 `loading="lazy"` 懶加載，大幅提升手機載入速度。

### 4. Giscus (GitHub Discussions) 無廣告留言板
整合了 Giscus 留言系統，讓讀者能直接使用 GitHub 帳號在文章下方留言討論，無廣告且資料全數儲存於 GitHub Discussions 中。

---

## 🚀 GitHub Actions 自動化部署架構

本站實行了 **「實戰宣言」** 的自動化工作流程：

`本地電腦 (Markdown) ➔ Git Push (main 分支) ➔ GitHub Actions 雲端自動編譯 ➔ GitHub Pages (gh-pages 分支) ➔ 30秒全網上線`

我們使用了 `peaceiris/actions-gh-pages@v4` 工作流程，每次寫完文章只需執行以下三行指令：

```powershell
git add .
git commit -m "feat: 發布最新文章"
git push -u origin main
```

---

## 🛠️ 給 AI 的專案說明書與 SOP

為了讓 AI 助理未來能無縫協助維護本站，我們還在專案中建立了：
- **`AGENTS.md`**：寫給 AI 的專案最高行為規範與避坑原則（如下載新主題必須刪除內置 `.git` 防止空 Submodule 404）。
- **`SKILLS.md`**：發文與主題切換的標準作業程序 (SOP)。

---

## 📝 總結

這次 Hugo 個人部落格的建置不僅讓我擁有了一個完全屬於自己的技術發表舞台，更深刻體驗了現代 AI 輔助開發（Agentic Coding）的強大威力。未來我會在這裡持續分享更多技術隨筆與生活心得，感謝您的閱讀！
