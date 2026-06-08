# MileSpace 網站 - 部署完整指南

## 📋 目錄

1. [本地開發](#本地開發)
2. [生產構建](#生產構建)
3. [GitHub Pages 部署](#github-pages-部署)
4. [自訂域名配置](#自訂域名配置)
5. [環境變數設定](#環境變數設定)
6. [故障排除](#故障排除)

---

## 本地開發

### 前置需求

確保您的系統已安裝以下軟體：

| 軟體 | 版本 | 下載 |
|------|------|------|
| Node.js | 18+ | [nodejs.org](https://nodejs.org) |
| pnpm | 8+ | `npm install -g pnpm` |
| Git | 最新版 | [git-scm.com](https://git-scm.com) |

### 安裝步驟

```bash
# 1. 克隆或解壓縮項目
unzip milespace-source-code.zip
cd milespace_redesign

# 2. 安裝依賴
pnpm install

# 3. 建立環境配置文件
cp .env.example .env.local

# 4. 啟動開發伺服器
pnpm dev
```

開啟瀏覽器訪問 `http://localhost:3000`

### 開發工作流程

```bash
# 修改代碼後，Vite 會自動熱更新
# 查看 http://localhost:3000 中的變化

# 運行測試
pnpm test

# 檢查代碼格式
pnpm format

# 檢查 TypeScript 類型
pnpm type-check
```

---

## 生產構建

### 構建靜態版本

```bash
# 構建優化的生產版本
pnpm build

# 生成文件位置：dist/
# 包含：
# - index.html（主頁面）
# - assets/（CSS、JavaScript、圖片）
# - 其他靜態資源
```

### 驗證構建

```bash
# 本地預覽構建結果
pnpm preview

# 訪問 http://localhost:4173
```

---

## GitHub Pages 部署

### 方法 1：使用 GitHub Actions（推薦）

#### 步驟 1：建立 GitHub 倉庫

```bash
# 初始化 Git 倉庫（如果還未初始化）
git init
git add .
git commit -m "Initial commit: MileSpace website"

# 添加遠程倉庫
git remote add origin https://github.com/YOUR_USERNAME/milespace-website.git
git branch -M main
git push -u origin main
```

#### 步驟 2：建立 GitHub Actions 工作流

在項目根目錄建立 `.github/workflows/deploy.yml`：

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '20'
          cache: 'pnpm'
      
      - name: Install pnpm
        run: npm install -g pnpm
      
      - name: Install dependencies
        run: pnpm install
      
      - name: Build
        run: pnpm build
      
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```

#### 步驟 3：啟用 GitHub Pages

1. 進入倉庫設定（Settings）
2. 左側菜單選擇「Pages」
3. 在「Source」選擇 **Deploy from a branch**
4. 選擇 **gh-pages** 分支和 **/ (root)** 目錄
5. 點擊「Save」

#### 步驟 4：推送代碼

```bash
git add .github/workflows/deploy.yml
git commit -m "Add GitHub Pages deployment workflow"
git push
```

GitHub Actions 會自動構建並部署您的網站。

### 方法 2：手動部署

```bash
# 1. 構建項目
pnpm build

# 2. 建立 gh-pages 分支
git checkout --orphan gh-pages

# 3. 清除工作目錄
git rm -rf .

# 4. 複製構建文件
cp -r dist/* .

# 5. 提交並推送
git add .
git commit -m "Deploy to GitHub Pages"
git push origin gh-pages

# 6. 返回主分支
git checkout main
```

---

## 自訂域名配置

### 步驟 1：在 GitHub 中配置域名

1. 進入倉庫設定（Settings）
2. 選擇「Pages」
3. 在「Custom domain」輸入您的域名（例如：`milespace.co`）
4. 點擊「Save」

GitHub 會自動建立 `CNAME` 文件。

### 步驟 2：配置 DNS 記錄

在您的域名提供商（如 GoDaddy、Namecheap 等）中：

#### 選項 A：使用 CNAME 記錄（推薦）

| 類型 | 名稱 | 值 |
|------|------|-----|
| CNAME | @ 或 www | `your-username.github.io` |

#### 選項 B：使用 A 記錄

| 類型 | 名稱 | 值 |
|------|------|-----|
| A | @ | `185.199.108.153` |
| A | @ | `185.199.109.153` |
| A | @ | `185.199.110.153` |
| A | @ | `185.199.111.153` |

### 步驟 3：驗證 DNS 配置

```bash
# 驗證 CNAME 記錄
nslookup milespace.co

# 驗證 A 記錄
dig milespace.co
```

DNS 傳播通常需要 24-48 小時。

### 步驟 4：啟用 HTTPS

1. 在 GitHub Pages 設定中勾選「Enforce HTTPS」
2. 等待 SSL 證書生成（通常需要幾分鐘）

---

## 環境變數設定

### 本地開發環境

建立 `.env.local` 文件：

```env
# 應用配置
VITE_APP_TITLE=MileSpace
VITE_APP_LOGO=https://your-logo-url.png

# Google Calendar API
GOOGLE_CALENDAR_API_KEY=AIzaSyD...your_api_key...
GOOGLE_CALENDAR_ID=your_calendar_id@group.calendar.google.com

# 資料庫（如果使用後端）
DATABASE_URL=mysql://user:password@localhost:3306/milespace

# 認證（如果使用 OAuth）
JWT_SECRET=your_secret_key_here
OAUTH_SERVER_URL=https://oauth.example.com
```

### 生產環境

對於 GitHub Pages（靜態部署），環境變數應在構建時設定：

```bash
# 構建時設定環境變數
VITE_APP_TITLE=MileSpace pnpm build
```

或在 GitHub Actions 中設定 Secrets：

1. 進入倉庫設定（Settings）
2. 選擇「Secrets and variables」→「Actions」
3. 點擊「New repository secret」
4. 添加您的密鑰

然後在 `.github/workflows/deploy.yml` 中使用：

```yaml
- name: Build
  env:
    VITE_APP_TITLE: MileSpace
    GOOGLE_CALENDAR_API_KEY: ${{ secrets.GOOGLE_CALENDAR_API_KEY }}
  run: pnpm build
```

---

## 故障排除

### 部署後頁面顯示 404

**原因**：GitHub Pages 路由配置不正確

**解決方案**：
1. 確保 `dist/` 中有 `index.html`
2. 檢查 `vite.config.ts` 中的 `base` 設定
3. 如果使用子路徑，修改 `vite.config.ts`：
```typescript
export default {
  base: '/milespace-website/',  // 如果倉庫名稱是 milespace-website
  // ...
}
```

### 自訂域名無法訪問

**原因**：DNS 配置未生效或 CNAME 文件丟失

**解決方案**：
1. 等待 DNS 傳播（24-48 小時）
2. 清除瀏覽器 DNS 緩存：`ipconfig /flushdns`（Windows）或 `sudo dscacheutil -flushcache`（macOS）
3. 確保 GitHub 設定中的自訂域名正確
4. 檢查 DNS 記錄是否正確設定

### 樣式或資源無法加載

**原因**：資源路徑不正確

**解決方案**：
1. 檢查瀏覽器開發者工具的「Network」標籤
2. 確保所有資源 URL 都是絕對路徑或相對路徑
3. 檢查 `vite.config.ts` 中的 `base` 設定

### GitHub Actions 構建失敗

**原因**：依賴問題或構建錯誤

**解決方案**：
1. 查看 GitHub Actions 日誌
2. 確保 `pnpm-lock.yaml` 已提交
3. 本地運行 `pnpm build` 驗證構建

```bash
# 清除緩存並重新安裝
rm -rf node_modules pnpm-lock.yaml
pnpm install
pnpm build
```

---

## 監控和維護

### 檢查部署狀態

訪問 `https://github.com/YOUR_USERNAME/milespace-website/actions` 查看部署日誌

### 更新內容

1. 修改代碼
2. 提交並推送到 `main` 分支
3. GitHub Actions 自動部署

```bash
git add .
git commit -m "Update content"
git push origin main
```

### 定期備份

```bash
# 備份本地倉庫
git clone --mirror https://github.com/YOUR_USERNAME/milespace-website.git milespace-backup.git
```

---

## 安全最佳實踐

1. **不要提交敏感信息**：使用環境變數而非硬編碼密鑰
2. **定期更新依賴**：`pnpm update`
3. **使用 HTTPS**：在 GitHub Pages 設定中啟用
4. **設定分支保護**：防止意外推送到主分支

---

## 常見問題

### Q: 如何更新網站內容？
A: 修改代碼並推送到 GitHub。GitHub Actions 會自動重新部署。

### Q: 如何回滾到之前的版本？
A: 使用 `git revert` 或 `git reset`，然後推送。

### Q: 如何添加自訂域名的 SSL 證書？
A: GitHub Pages 自動為自訂域名提供免費的 Let's Encrypt SSL 證書。只需在設定中啟用「Enforce HTTPS」。

### Q: 部署需要多長時間？
A: 通常 1-5 分鐘。查看 GitHub Actions 日誌了解進度。

---

## 下一步

- [快速開始指南](./QUICK_START.md)
- [客製化指南](./MILESPACE_CUSTOMIZATION_GUIDE.md)
- [GitHub Pages 官方文檔](https://docs.github.com/en/pages)

---

**準備好部署了嗎？按照上述步驟進行，您的網站將很快上線！** 🚀
