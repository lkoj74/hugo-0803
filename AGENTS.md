# 🤖 給 AI 助理的 Hugo 專案規則書 (AGENTS.md)

本檔案為本 Hugo 個人部落格專案的權威規範。任何 AI 助理（如 Antigravity, Claude, ChatGPT 等）在進入本專案工作時，必須自動讀取並嚴格遵守以下規則。

---

## 1. 語言與溝通規範
- **語言偏好**：所有對話、思考過程、程式碼註解與文檔說明一律使用 **繁體中文 (Traditional Chinese, Taiwan)**。
- **態度與對話**：保持專業、親切與高效，主動提供最佳實踐建議。

## 2. 專案結構與路徑慣例
- **專案根目錄**：`J:\【0803】google AntiGravity 2.0-20260606`
- **當前主題**：`Dream` (`themes/dream`)
- **文章目錄**：`content/posts/` (採用 Page Bundles 結構，如 `content/posts/my-post/index.md` + 圖片)
- **大頭貼資產**：`static/img/author.png` 與 `assets/img/author.png`
- **公開網址**：`https://lkoj74.github.io/hugo-0803/`

## 3. 主題與 Git 避坑防護 (CRITICAL)
- **禁止 Submodule 陷阱**：下載或新增主題時，**必須立即移除主題目錄內的 `.git` 隱藏資料夾**（例如 `Remove-Item -Recurse -Force themes/xxx/.git`），確保主題內所有 `layouts/` 模板能 100% 被主專案 Git 追蹤並 Commit。
- **大頭貼保護**：Dream 主題導覽列中的大頭貼必須嚴格固定 `48px × 48px` 並加上 `flex-shrink-0` 與遮罩，防止滿版伸展。
- **首頁渲染保護**：`hugo.toml` 中 `[outputs]` 設定 `home = ["HTML"]`，確保直接輸出 `index.html` 避免 RSS `index.xml` 快取誤載。

## 4. Git & GitHub Actions 發布規範
- **部署方式**：使用 `peaceiris/actions-gh-pages` 工作流程自動編譯並推送到 `gh-pages` 分支。
- **Commit 訊息格式**：遵循 Conventional Commits（例如 `feat: ...`, `fix: ...`, `style: ...`, `docs: ...`）。
- **完成變更後**：主動自動執行 `git add .` -> `git commit` -> `git push -u origin main`。
