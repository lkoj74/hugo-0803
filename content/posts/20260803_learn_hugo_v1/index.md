---
title: "學會建立Hugo個人布落格"
date: 2026-08-03T19:54:00+08:00
draft: false
cover: "cover.jpg"
tags: ["Hugo", "GitHub Actions", "GitHub Pages", "部落格教學", "Git"]
categories: ["技術教學"]
summary: "這是一份專為新手與 Agent 小白設計的 Hugo 個人部落格建置白話教學。從工具安裝、主題選擇、文章撰寫、Git 版本控制到 GitHub Actions 自動化部署，帶你徹底掌握建立個人部落格的全流程。"
---

![Hugo 個人部落格建置教學指南](featured.jpg)

> [!NOTE]
> 本文改編自白話教學指南，用最淺顯易懂的方式，帶完全沒接觸過 Hugo、Git、GitHub Actions 與 Agent 的新手，從零建立並發布專屬於你的 Hugo 個人部落格。

---

## 一、先看全貌：建立部落格到底在做什麼？

把建立 Hugo 部落格的過程想像成「**寫稿 ➔ 試印 ➔ 交給倉庫 ➔ 請機器人出版**」：

```
[你在電腦寫 Markdown 文章] ➔ [Hugo 把文章變成網頁] ➔ [在 localhost 預覽]
                                                               ⬇
[GitHub Pages 公開網站] ⬅ [GitHub Actions 自動編譯] ⬅ [Push 到 GitHub] ⬅ [Git 保存這次修改]
```

### 核心元件角色分工

| 元件名稱 | 白話說明 |
| :--- | :--- |
| **Markdown** | 你真正寫文章的文字檔，語法簡單且乾淨。 |
| **Hugo** | 極速靜態網站產生器，負責把 Markdown、主題與設定檔組合成 HTML 網頁。 |
| **Git** | 版本控制工具，幫你記錄每次修改與建立復原點。 |
| **GitHub** | 雲端程式碼倉庫，儲存你的原始碼並提供自動化運算資源。 |
| **GitHub Actions** | 雲端自動化機器人，收到新程式碼後自動幫你執行 Hugo 編譯。 |
| **GitHub Pages** | 免費的靜態網站託管服務，把編譯好的網頁公開給全世界瀏覽。 |

> [!TIP]
> **觀念建立：** 你平常不是直接修改線上的公開網站，而是在本機修改原始資料；確認預覽無誤後，推送到 GitHub 讓機器人自動發布。

---

## 二、小白必懂的名詞翻譯

在開始動手前，我們先把常見的術語翻譯成白話文：

- **Project (專案)**：整個部落格資料夾（例如 `J:\my-blog`）。
- **Repository / Repo (倉庫)**：使用 Git 管理的專案目錄；上傳到 GitHub 後稱為雲端倉庫。
- **Theme (主題)**：網站的外觀、字體、顏色與版型配置。
- **Content (內容)**：你撰寫的文章與靜態頁面，放在 `content/` 目錄。
- **Layout (佈局)**：控制網頁結構與元件如何渲染顯示。
- **Static / Assets (靜態資源)**：存放圖片、CSS、JavaScript 或圖標等檔案。
- **Commit (提交)**：替目前的修改記錄建立一個附帶說明的歷史存檔點。
- **Push (推送)**：把本機的 Commit 上傳到 GitHub 雲端倉庫。
- **localhost**：只有你本機電腦看得到的測試伺服器（預設為 `http://localhost:1313`）。
- **Agent**：能夠協助你讀取檔案、編寫程式碼、執行命令與除錯的 AI 助理。

---

## 三、第一步：安裝基本工具

在 Windows 環境下，建議使用 `winget` 快速安裝必要的命令列工具：

### 1. 安裝 Hugo Extended
Hugo Extended 版本支援 Sass/SCSS 編譯，能相容絕大多數的現代化主題：
```powershell
winget install Hugo.Hugo.Extended
```

### 2. 安裝 Git 與 GitHub CLI
```powershell
winget install Git.Git
winget install GitHub.cli
```

### 3. 驗證工具安裝
開啟全新的 PowerShell 視窗，執行以下指令確認版本號：
```powershell
hugo version
git --version
gh --version
```

> [!WARNING]
> 若提示「找不到命令」，請關閉所有 PowerShell 視窗並重新開啟，讓系統重新載入 PATH 環境變數。

---

## 四、第二步：建立 Hugo 網站資料夾

選擇你想放置專案的目錄，執行以下指令：

```powershell
cd "J:\"
hugo new site my-blog
cd my-blog
```

建立完成後，Hugo 會為你生成經典的專案目錄結構：
```
my-blog/
├─ archetypes/      # 文章模板
├─ assets/          # 靜態資源（支援 Hugo Pipes 處理）
├─ content/         # 文章與頁面內容
├─ data/            # 資料檔案 (JSON/YAML/TOML)
├─ layouts/         # 自訂網頁模板
├─ static/          # 直接複製到根目錄的靜態檔案
├─ themes/          # 網站主題
└─ hugo.toml        # 網站全域設定檔
```

---

## 五、第三步：選擇並安裝主題

Hugo 擁有豐富的主題生態（如 Dream、PaperMod、Blowfish、Congo 等）。安裝主題時主要有兩種管理方式：

### 方式 A：使用 Git Submodule (適合與原作者倉庫連動)
```powershell
git init
git submodule add https://github.com/giscus/hugo-giscus.git themes/hugo-giscus
```

### 方式 B：將主題當作一般檔案放入專案 (推薦完全自主控制)
```powershell
git clone --depth 1 https://github.com/giscus/hugo-giscus.git themes/hugo-giscus
Remove-Item -Recurse -Force themes\hugo-giscus\.git
```

> [!IMPORTANT]
> **避坑防護：** 若採用方式 B，**務必移除主題目錄內的 `.git` 隱藏資料夾**，確保主題內的模板能 100% 被主專案的 Git 追蹤與 Commit。

在 `hugo.toml` 中指定主題名稱：
```toml
baseURL = "https://yourname.github.io/"
languageCode = "zh-tw"
title = "我的個人部落格"
theme = "hugo-giscus"
```

---

## 六、第四步：建立第一篇文章 (Page Bundle 模式)

Hugo 推薦使用 **Page Bundle** 結構來管理文章與圖片，保持檔案結構整潔：

```
content/
└─ posts/
   └─ my-first-post/
      ├─ index.md       # 文章主要內容
      └─ featured.jpg   # 該文章專屬圖片
```

執行命令建立文章目錄與 `index.md`：
```powershell
hugo new content posts/my-first-post/index.md
```

開啟 `index.md` 並編輯文章內容：
```markdown
---
title: "我的第一篇 Hugo 文章"
date: 2026-08-03T19:54:00+08:00
draft: false
tags: ["Hugo", "學習紀錄"]
categories: ["技術教學"]
---

大家好，這是我的第一篇 Hugo 文章！

## 🌟 今日學習心得
學會 Hugo 之後，寫文章變得非常純粹與高效。

![展示圖片](featured.jpg)
```

---

## 七、第五步：在本地電腦即時預覽

執行 Hugo 本地開發伺服器：

```powershell
hugo server -D
```

在瀏覽器中開啟：`http://localhost:1313/`

- `-D` 參數表示連同標記為 `draft: true` 的草稿文章一併渲染顯示。
- 當你儲存 `index.md` 檔案時，瀏覽器會自動即時刷新畫面（Live Reload）。

---

## 八、第六步：用 Git 保存網站版本

當本地預覽確認無誤後，使用 Git 保存這個時間點的變更：

### 1. 初始化與建立 `.gitignore`
在專案根目錄建立 `.gitignore` 檔案，忽略編譯產出物：
```gitignore
public/
resources/_gen/
.hugo_build.lock
*.log
```

### 2. 進行日常 Commit
```powershell
git status
git add .
git commit -m "feat: 新增『學會建之Hugo個人布落格』文章"
```

### 3. 綁定 GitHub 雲端倉庫
在 GitHub 上建立一個新的公開 Repository，並將本地專案推送到遠端：
```powershell
git remote add origin https://github.com/你的帳號/你的倉庫名稱.git
git branch -M main
git push -u origin main
```

---

## 九、第七步：讓 GitHub Actions 自動發布網站

為了實現「**只需 `git push`，網站就自動發布**」，我們需要在專案中新增 GitHub Actions 工作流程。

建立 `.github/workflows/deploy.yml` 檔案：

```yaml
name: Deploy Hugo Site to GitHub Pages

on:
  push:
    branches:
      - main

permissions:
  contents: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4
        with:
          submodules: true
          fetch-depth: 0

      - name: Setup Hugo
        uses: actions/configure-hugo@v1
        with:
          hugo-version: 'latest'
          extended: true

      - name: Build Site
        run: hugo --gc --minify

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

在 GitHub 專案設定中：
1. 前往 **Settings ➔ Pages**。
2. 將 **Source** 改為 `Deploy from a branch`。
3. Branch 選擇 `gh-pages` / `/ (root)` 並儲存。

以後只要將最新修改 Push 到 `main` 分支，GitHub Actions 就會自動編譯並推送到 `gh-pages` 分支上線！

---

## 十、Agent 小白要怎麼請 AI 幫忙？

如果你正在使用 AI 助理（如 Antigravity, Claude, ChatGPT）協助維護部落格，請給予明確且可驗證的 Prompt 結構：

### 💡 推薦的 Agent 任務 Prompt
```text
請先檢查目前所在目錄與 Git 狀態。
確認這是一個 Hugo 專案後，再執行以下工作：

1. 檢查目前使用的主題名稱。
2. 新增文章 content/posts/20260803_learn_hugo_v1/index.md。
3. 建立完成後執行 `hugo --gc --minify` 驗證編譯是否正常。
4. 顯示 git status 與變更檔案，確認無誤後協助進行 git add、commit 與 push。
5. 簡報告知變更檔案完整路徑與執行結果。
```

---

## 十一、小白常遇到的常見錯誤與排查指南

| 錯誤症狀 | 可能原因 | 排除步驟 |
| :--- | :--- | :--- |
| **`localhost:1313` 拒絕連線** | Hugo server 未啟動或已關閉。 | 重新開啟 PowerShell 並執行 `hugo server -D`。 |
| **`fatal: not a git repository`** | 當前 PowerShell 不在 Git 專案目錄內。 | 使用 `cd` 指令切換至包含 `hugo.toml` 的資料夾。 |
| **本地正常，GitHub Pages 呈現 404** | `baseURL` 未設定為正式網址、Actions 部署失敗或 Pages Source 設定錯誤。 | 檢查 `hugo.toml` 的 `baseURL` 與 GitHub Actions 的部署 Log。 |
| **圖片顯示破圖** | 檔名大小寫不符合，或圖片未放入 Page Bundle 目錄。 | 確認圖片檔名與 `index.md` 中的引用路徑完全相同。 |

---

## 十二、日常寫作與更新 SOP 快速清單

每當你想要寫一篇新文章時，只需遵循這 8 個步驟：

1. **進入專案**：`cd "J:\你的Hugo專案"`
2. **拉取最新版**：`git pull origin main`
3. **啟動本地預覽**：`hugo server -D`
4. **建立新文章**：`hugo new content posts/文章名稱/index.md`
5. **撰寫 Markdown 與放置圖片**
6. **編譯測試**：`hugo --gc --minify`
7. **Git 提交存檔**：
   ```powershell
   git add .
   git commit -m "feat: 新增文章標題"
   ```
8. **推送發布**：`git push origin main`

祝你順利建置出屬於自己的個人部落格，享受純粹且高質感的寫作體驗！ 🚀
