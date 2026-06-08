# MileSpace 網站 - 原始碼客製化指南

## 📋 概述

這是 MileSpace 爵士樂酒吧網站的完整原始碼。該網站採用現代技術棧構建，支援多語言、Instagram 整合、Google Calendar 同步等功能。

**技術棧**：
- **前端**：React 19 + Vite + Tailwind CSS 4
- **後端**：Express.js + tRPC 11
- **資料庫**：MySQL (Drizzle ORM)
- **部署**：支援 GitHub Pages（靜態版本）或自託管伺服器

---

## 🗂️ 項目結構

```
milespace_redesign/
├── client/                          # 前端 React 應用
│   ├── src/
│   │   ├── pages/                   # 頁面組件
│   │   │   ├── Home.tsx             # 首頁（8張輪播背景）
│   │   │   ├── LiveGigs.tsx         # 現場演出分頁
│   │   │   ├── Wedding.tsx          # 婚禮樂團分頁（含影片）
│   │   │   ├── Corporate.tsx        # 商演策劃分頁
│   │   │   └── Team.tsx             # 團隊理念分頁
│   │   ├── components/              # 可重用組件
│   │   │   ├── Navigation.tsx       # 導航欄（含語言切換）
│   │   │   ├── GoogleCalendarEvents.tsx  # Google Calendar 組件
│   │   │   └── ui/                  # shadcn/ui 組件庫
│   │   ├── locales/
│   │   │   └── translations.ts      # 中英文翻譯字典
│   │   ├── contexts/
│   │   │   └── LanguageContext.tsx  # 語言狀態管理
│   │   ├── App.tsx                  # 路由配置
│   │   ├── main.tsx                 # 應用入口
│   │   └── index.css                # 全局樣式
│   ├── index.html                   # HTML 模板
│   └── public/                      # 靜態資源
├── server/                          # 後端 Express 應用
│   ├── routers.ts                   # tRPC 路由定義
│   ├── db.ts                        # 資料庫查詢助手
│   ├── storage.ts                   # S3 存儲集成
│   └── _core/                       # 框架核心（OAuth、認證等）
├── drizzle/                         # 資料庫架構
│   ├── schema.ts                    # 資料表定義
│   └── migrations/                  # 資料庫遷移
├── shared/                          # 前後端共享代碼
├── package.json                     # 依賴配置
├── vite.config.ts                   # Vite 配置
├── tsconfig.json                    # TypeScript 配置
└── README.md                        # 完整文檔
```

---

## 🚀 快速開始

### 1. 安裝依賴

```bash
cd milespace_redesign
pnpm install
```

### 2. 設定環境變數

建立 `.env.local` 文件（本地開發）：

```env
# 資料庫
DATABASE_URL=mysql://user:password@localhost:3306/milespace

# OAuth（如果使用 Manus 認證）
VITE_OAUTH_PORTAL_URL=https://oauth.example.com
OAUTH_SERVER_URL=https://api.oauth.example.com

# Google Calendar API（用於演出行程同步）
GOOGLE_CALENDAR_API_KEY=your_api_key_here
GOOGLE_CALENDAR_ID=your_calendar_id@group.calendar.google.com

# 其他配置
JWT_SECRET=your_secret_key
```

### 3. 初始化資料庫

```bash
pnpm db:push
```

### 4. 啟動開發伺服器

```bash
pnpm dev
```

訪問 `http://localhost:3000`

### 5. 構建生產版本

```bash
pnpm build
```

---

## 🎨 主要功能說明

### 1. **首頁輪播背景**

位置：`client/src/pages/Home.tsx`

8 張照片自動循環展示，包含：
- 現場演出照片
- 婚禮樂團表演
- 商演活動

**修改方法**：
```tsx
const carouselImages = [
  'https://your-image-url-1.jpg',
  'https://your-image-url-2.jpg',
  // ... 添加更多圖片 URL
];
```

### 2. **多語言支援**

位置：`client/src/locales/translations.ts`

支援中文和英文切換。

**修改翻譯**：
```typescript
export const translations = {
  en: {
    nav: {
      home: "Home",
      liveGigs: "Live Gigs",
      // ... 其他翻譯
    }
  },
  zh: {
    nav: {
      home: "首頁",
      liveGigs: "現場演出",
      // ... 其他翻譯
    }
  }
};
```

### 3. **Instagram 整合**

位置：`client/src/pages/Home.tsx`

使用 Tagembed 自動顯示 @milespace_jazz 的最新貼文。

**修改 Instagram 帳號**：
```tsx
<div
  className="tagembed-container"
  style={{
    width: "100%",
    height: "500px"
  }}
>
  <p>
    <a href="https://www.instagram.com/your_account/" target="_blank">
      @your_account
    </a>
  </p>
</div>
<script src="//embed.redditmedia.com/widgets/platform.js"></script>
```

### 4. **Google Calendar 同步**

位置：`client/src/components/GoogleCalendarEvents.tsx`

自動從 Google Calendar 獲取演出日程。

**配置 Google Calendar**：
1. 建立 Google Calendar API 金鑰
2. 在 `.env.local` 中設定 `GOOGLE_CALENDAR_ID`
3. 確保日曆是公開的

### 5. **婚禮樂團影片**

位置：`client/src/pages/Wedding.tsx`

自動循環播放的婚禮樂團表演影片。

**修改影片 URL**：
```tsx
<video
  autoPlay
  loop
  muted
  className="w-full h-auto rounded-lg"
  src="https://your-video-url.mp4"
/>
```

---

## 🔧 常見修改

### 修改網站標題和描述

位置：`client/index.html`

```html
<title>MileSpace - 台中爵士樂酒吧</title>
<meta name="description" content="台中必訪的爵士音樂地標。現場演出、婚禮樂團、商演策劃。" />
```

### 修改導航菜單

位置：`client/src/components/Navigation.tsx`

```tsx
const menuItems = [
  { label: "首頁", href: "/" },
  { label: "現場演出", href: "/live-gigs" },
  { label: "婚禮樂團", href: "/wedding" },
  { label: "商演策劃", href: "/corporate" },
  { label: "團隊理念", href: "/team" },
];
```

### 修改聯絡資訊

位置：`client/src/pages/Home.tsx`（聯絡區塊）

```tsx
const contactInfo = {
  email: "your-email@milespace.co",
  phone: "+886-4-XXXX-XXXX",
  address: "台中市西區...",
  lineId: "your-line-id"
};
```

### 修改顏色主題

位置：`client/src/index.css`

```css
:root {
  --primary: #d4af37;      /* 香檳金色 */
  --secondary: #1e293b;    /* 深色背景 */
  --accent: #f5f5f0;       /* 奶油色 */
}
```

---

## 📱 響應式設計

網站已針對所有設備進行優化：
- **桌面**：1920px 及以上
- **平板**：768px - 1024px
- **手機**：320px - 767px

使用 Tailwind CSS 的響應式類名：
```tsx
<div className="text-sm md:text-base lg:text-lg">
  響應式文本大小
</div>
```

---

## 🗄️ 資料庫架構

位置：`drizzle/schema.ts`

預設包含 `users` 表（用於認證）。根據需要擴展：

```typescript
export const events = sqliteTable('events', {
  id: text('id').primaryKey(),
  title: text('title').notNull(),
  date: integer('date').notNull(),
  location: text('location'),
  createdAt: integer('created_at').notNull(),
});
```

推送遷移：
```bash
pnpm db:push
```

---

## 🔐 環境變數清單

| 變數名 | 說明 | 示例 |
|--------|------|------|
| `DATABASE_URL` | MySQL 連接字符串 | `mysql://user:pass@localhost/db` |
| `JWT_SECRET` | Session 簽名密鑰 | `your-secret-key-123` |
| `GOOGLE_CALENDAR_API_KEY` | Google Calendar API 金鑰 | `AIzaSyD...` |
| `GOOGLE_CALENDAR_ID` | Google Calendar ID | `abc123@group.calendar.google.com` |
| `VITE_APP_TITLE` | 網站標題 | `MileSpace` |

---

## 🧪 測試

運行測試：
```bash
pnpm test
```

查看測試範例：`server/auth.logout.test.ts`

---

## 📦 部署選項

### 選項 1：GitHub Pages（靜態版本）

1. 構建靜態版本：
```bash
pnpm build
```

2. 上傳 `dist/` 文件夾到 GitHub Pages

### 選項 2：自託管伺服器

1. 構建應用：
```bash
pnpm build
```

2. 上傳到伺服器並運行：
```bash
node dist/index.js
```

### 選項 3：Docker 部署

建立 `Dockerfile`：
```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY . .
RUN pnpm install
RUN pnpm build
EXPOSE 3000
CMD ["node", "dist/index.js"]
```

---

## 🐛 常見問題

### Q: 如何修改 Logo？
A: 在 `client/src/components/Navigation.tsx` 中修改 `logoUrl`：
```tsx
const logoUrl = "https://your-logo-url.png";
```

### Q: 如何添加新頁面？
A: 
1. 在 `client/src/pages/` 中建立新組件
2. 在 `client/src/App.tsx` 中添加路由
3. 在 `client/src/components/Navigation.tsx` 中添加菜單項

### Q: 如何修改聯絡表單？
A: 位置：`client/src/pages/Home.tsx`
修改表單字段和提交邏輯

### Q: 如何集成支付系統？
A: 使用 Stripe 或 PayPal
1. 安裝相應的 npm 包
2. 在 `server/routers.ts` 中添加支付路由
3. 在前端調用支付 API

---

## 📞 支援

如有問題，請參考：
- [React 文檔](https://react.dev)
- [Tailwind CSS 文檔](https://tailwindcss.com)
- [tRPC 文檔](https://trpc.io)
- [Drizzle ORM 文檔](https://orm.drizzle.team)

---

## 📄 許可證

此項目為 MileSpace 爵士樂酒吧專用。

---

**最後更新**：2026 年 6 月 8 日
