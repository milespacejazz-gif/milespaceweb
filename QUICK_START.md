# MileSpace 網站 - 快速開始指南

## 📥 安裝和運行

### 1. 解壓縮原始碼

```bash
unzip milespace-source-code.zip
cd milespace_redesign
```

### 2. 安裝依賴

```bash
pnpm install
```

如果您還沒有安裝 pnpm，請先安裝：
```bash
npm install -g pnpm
```

### 3. 啟動開發伺服器

```bash
pnpm dev
```

開啟瀏覽器訪問 `http://localhost:3000`

---

## 🎯 主要文件位置

| 文件 | 位置 | 說明 |
|------|------|------|
| 首頁 | `client/src/pages/Home.tsx` | 8 張輪播背景 + 品牌信息 |
| 導航欄 | `client/src/components/Navigation.tsx` | 菜單 + 語言切換 |
| 翻譯 | `client/src/locales/translations.ts` | 中英文內容 |
| 現場演出 | `client/src/pages/LiveGigs.tsx` | Google Calendar 同步 |
| 婚禮樂團 | `client/src/pages/Wedding.tsx` | 影片 + 服務介紹 |
| 商演策劃 | `client/src/pages/Corporate.tsx` | 企業活動服務 |
| 團隊理念 | `client/src/pages/Team.tsx` | 關於團隊 |

---

## ✏️ 快速修改

### 修改首頁文字

打開 `client/src/pages/Home.tsx`，找到：
```tsx
const heroContent = {
  title: "TAICHUNG LIVE JAZZ · WEDDING · EVENTS",
  brand: "MileSpace",
  subtitle: "爵士現場策劃與活動音樂整合",
  // ... 修改文字
};
```

### 修改聯絡資訊

打開 `client/src/pages/Home.tsx`，找到聯絡區塊：
```tsx
<p>Email: your-email@milespace.co</p>
<p>Phone: +886-4-XXXX-XXXX</p>
<p>Address: 台中市西區...</p>
```

### 修改菜單項目

打開 `client/src/components/Navigation.tsx`，修改 `menuItems` 陣列

### 修改顏色主題

打開 `client/src/index.css`，修改 CSS 變數：
```css
:root {
  --primary: #d4af37;      /* 香檳金色 */
  --secondary: #1e293b;    /* 深色背景 */
}
```

---

## 🔗 集成外部服務

### Google Calendar

1. 獲取 Google Calendar API 金鑰
2. 在 `.env.local` 中設定：
```env
GOOGLE_CALENDAR_API_KEY=your_api_key
GOOGLE_CALENDAR_ID=your_calendar_id@group.calendar.google.com
```

### Instagram（Tagembed）

已自動集成 @milespace_jazz。要修改帳號，編輯 `client/src/pages/Home.tsx`

---

## 📦 構建和部署

### 構建生產版本

```bash
pnpm build
```

生成的文件在 `dist/` 目錄中

### 部署到 GitHub Pages

1. 將 `dist/` 中的文件上傳到 GitHub 倉庫
2. 在 GitHub Settings 中啟用 Pages
3. 選擇部署來源為 `main` 分支的 `/` 根目錄

### 部署到自訂伺服器

```bash
# 構建
pnpm build

# 上傳 dist 文件夾到伺服器
# 配置 Web 伺服器（Nginx/Apache）指向 dist 目錄
```

---

## 🧪 開發提示

### 添加新頁面

1. 在 `client/src/pages/` 中建立新文件，例如 `NewPage.tsx`
2. 在 `client/src/App.tsx` 中添加路由
3. 在 `client/src/components/Navigation.tsx` 中添加菜單項

### 修改樣式

- 使用 Tailwind CSS 類名
- 全局樣式在 `client/src/index.css`
- 組件樣式在各自的 `.tsx` 文件中

### 使用 TypeScript

所有代碼都是 TypeScript，享受完整的類型檢查

---

## 🐛 故障排除

### 開發伺服器無法啟動

```bash
# 清除 node_modules 和重新安裝
rm -rf node_modules
pnpm install
pnpm dev
```

### 頁面無法加載

- 檢查瀏覽器控制台是否有錯誤
- 確保所有環境變數都已設定
- 檢查 `client/src/App.tsx` 中的路由配置

### 樣式不正確

- 確保 Tailwind CSS 已正確配置
- 清除瀏覽器緩存
- 重新啟動開發伺服器

---

## 📚 更多資源

- [完整客製化指南](./MILESPACE_CUSTOMIZATION_GUIDE.md)
- [React 文檔](https://react.dev)
- [Tailwind CSS 文檔](https://tailwindcss.com)
- [Vite 文檔](https://vitejs.dev)

---

**準備好開始了嗎？執行 `pnpm dev` 吧！** 🚀
