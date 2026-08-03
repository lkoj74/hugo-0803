# 📖 Hugo 專案標準工作流程手冊 (SKILLS.md)

本手冊記錄了本專案最常用的重複性工作流程。當您要求 AI 執行任務時（例如：「幫我發一篇新文章」或「幫我切換主題」），AI 會自動參照本手冊步驟精準執行。

---

## 🛠️ 技能 1：發布一篇全新部落格文章 (Page Bundles)

### 執行步驟：
1. **建立文章目錄**：
   在 `content/posts/` 下建立新資料夾（如 `content/posts/my-new-post/`）。
2. **建立 index.md 檔案**：
   在資料夾中建立 `index.md` 並填入 YAML Frontmatter：
   ```yaml
   ---
   title: "您的文章標題"
   date: 2026-08-03T15:00:00+08:00
   draft: false
   tags: ["Hugo", "技術隨筆"]
   categories: ["技術分享"]
   ---
   ```
3. **圖片 Page Bundles 處置**：
   將文章所需的圖片放入同一目錄（如 `featured.jpg`）。在 Markdown 中直接引用：`![封面圖片](featured.jpg)`。Hugo 會自動轉為 WebP 格式並壓縮。
4. **預覽與提交**：
   本地執行 `hugo server` 驗證後，執行 `git add .` -> `git commit` -> `git push` 發布。

---

## 🛠️ 技能 2：下載與切換全新的 Hugo 主題

### 執行步驟 (避坑防護重點)：
1. **複製主題**：
   在 PowerShell 中執行：`git clone --depth 1 https://github.com/作者/主題 repo.git themes/主題名稱`
2. **CRITICAL: 刪除內置 .git 資料夾**：
   **務必執行**：`Remove-Item -Recurse -Force themes\主題名稱\.git`
   *(徹底防止主題被 Git 判斷為空 Submodule 導致雲端 404)*
3. **更新配置檔**：
   在 `hugo.toml` 中修改 `theme = "主題名稱"`。
4. **測試編譯**：
   執行 `hugo` 驗證編譯通過。

---

## 🛠️ 技能 3：本地開發展覽 (Local Server)

### 執行步驟：
在 PowerShell 執行：
```powershell
# 啟動本地開發伺服器
hugo server --bind 0.0.0.0 --port 1313
```
開啟瀏覽器訪問 `http://localhost:1313/` 查看即時熱重載結果。

---

## 🛠️ 技能 4：一鍵自動化發布至 GitHub Pages

### 執行步驟：
```powershell
cd "J:\【0803】google AntiGravity 2.0-20260606"
git add .
git commit -m "feat: 發布最新內容"
git push -u origin main
```
GitHub Actions 會在雲端自動醒來，30 秒內更新至：
👉 **https://lkoj74.github.io/hugo-0803/**
