# MileSpace 網站 - 項目結構詳解

## 📁 完整目錄樹

```
milespace_redesign/
│
├── 📁 client/                          # 前端 React 應用
│   ├── 📁 src/
│   │   ├── 📁 pages/                   # 頁面組件（每個路由一個文件）
│   │   │   ├── Home.tsx                # 首頁 - 8 張輪播背景 + 品牌信息
│   │   │   ├── LiveGigs.tsx            # 現場演出分頁 - Google Calendar 同步
│   │   │   ├── Wedding.tsx             # 婚禮樂團分頁 - 影片 + 服務介紹
│   │   │   ├── Corporate.tsx           # 商演策劃分頁 - 企業活動服務
│   │   │   ├── Team.tsx                # 團隊理念分頁 - 關於團隊
│   │   │   ├── Events.tsx              # 活動頁面
│   │   │   ├── ComponentShowcase.tsx   # UI 組件展示（開發用）
│   │   │   └── NotFound.tsx            # 404 頁面
│   │   │
│   │   ├── 📁 components/              # 可重用組件
│   │   │   ├── Navigation.tsx          # 導航欄（菜單 + 語言切換）
│   │   │   ├── GoogleCalendarEvents.tsx # Google Calendar 事件組件
│   │   │   ├── ErrorBoundary.tsx       # 錯誤邊界
│   │   │   ├── ManusDialog.tsx         # 對話框組件
│   │   │   ├── Map.tsx                 # Google Maps 集成
│   │   │   ├── DashboardLayout.tsx     # 儀表板佈局（可選）
│   │   │   ├── AIChatBox.tsx           # AI 聊天框（可選）
│   │   │   └── 📁 ui/                  # shadcn/ui 組件庫
│   │   │       ├── button.tsx
│   │   │       ├── card.tsx
│   │   │       ├── dialog.tsx
│   │   │       ├── dropdown-menu.tsx
│   │   │       ├── input.tsx
│   │   │       ├── select.tsx
│   │   │       ├── tabs.tsx
│   │   │       └── ... 其他 UI 組件
│   │   │
│   │   ├── 📁 contexts/                # React Context（狀態管理）
│   │   │   ├── LanguageContext.tsx     # 語言狀態
│   │   │   └── ThemeContext.tsx        # 主題狀態
│   │   │
│   │   ├── 📁 hooks/                   # 自訂 React Hooks
│   │   │   ├── useMobile.tsx           # 檢測移動設備
│   │   │   ├── useComposition.ts       # 組合邏輯
│   │   │   └── usePersistFn.ts         # 持久化函數
│   │   │
│   │   ├── 📁 _core/                   # 核心功能
│   │   │   └── 📁 hooks/
│   │   │       └── useAuth.ts          # 認證 Hook
│   │   │
│   │   ├── 📁 locales/                 # 多語言翻譯
│   │   │   └── translations.ts         # 中英文翻譯字典
│   │   │
│   │   ├── 📁 lib/                     # 工具函數庫
│   │   │   ├── trpc.ts                 # tRPC 客戶端配置
│   │   │   └── utils.ts                # 通用工具函數
│   │   │
│   │   ├── App.tsx                     # 主應用組件 - 路由配置
│   │   ├── main.tsx                    # 應用入口點
│   │   ├── const.ts                    # 常數定義
│   │   └── index.css                   # 全局樣式 + Tailwind 配置
│   │
│   ├── 📁 public/                      # 靜態資源（小文件）
│   │   ├── favicon.ico                 # 網站圖標
│   │   ├── robots.txt                  # SEO 機器人配置
│   │   └── 📁 __manus__/               # Manus 平台文件
│   │
│   └── index.html                      # HTML 模板
│
├── 📁 server/                          # 後端 Express 應用
│   ├── index.ts                        # 伺服器入口點
│   ├── routers.ts                      # tRPC 路由定義
│   ├── db.ts                           # 資料庫查詢助手
│   ├── storage.ts                      # S3 存儲集成
│   ├── auth.logout.test.ts             # 認證測試範例
│   │
│   └── 📁 _core/                       # 框架核心（勿修改）
│       ├── index.ts                    # 伺服器啟動
│       ├── context.ts                  # tRPC 上下文
│       ├── oauth.ts                    # OAuth 認證
│       ├── cookies.ts                  # Cookie 管理
│       ├── env.ts                      # 環境變數
│       ├── trpc.ts                     # tRPC 配置
│       ├── llm.ts                      # LLM 集成
│       ├── imageGeneration.ts          # 圖像生成
│       ├── voiceTranscription.ts       # 語音轉文字
│       ├── map.ts                      # Google Maps
│       ├── notification.ts             # 通知系統
│       ├── storageProxy.ts             # 存儲代理
│       ├── dataApi.ts                  # 數據 API
│       ├── heartbeat.ts                # 心跳監控
│       ├── systemRouter.ts             # 系統路由
│       ├── vite.ts                     # Vite 集成
│       ├── sdk.ts                      # SDK 工具
│       └── 📁 types/                   # TypeScript 類型定義
│           ├── cookie.d.ts
│           └── manusTypes.ts
│
├── 📁 drizzle/                         # 資料庫架構（Drizzle ORM）
│   ├── schema.ts                       # 資料表定義
│   ├── relations.ts                    # 表關係定義
│   ├── drizzle.config.ts               # Drizzle 配置
│   ├── 📁 migrations/                  # 資料庫遷移文件
│   │   └── .gitkeep
│   └── 📁 meta/                        # Drizzle 元數據
│       └── _journal.json
│
├── 📁 shared/                          # 前後端共享代碼
│   ├── types.ts                        # 共享類型定義
│   ├── const.ts                        # 共享常數
│   └── 📁 _core/
│       └── errors.ts                   # 錯誤定義
│
├── 📁 references/                      # 參考文檔
│   └── periodic-updates.md             # 定期更新配置
│
├── 📁 .github/                         # GitHub 配置
│   └── 📁 workflows/                   # GitHub Actions
│       └── deploy.yml                  # 自動部署工作流
│
├── 📁 patches/                         # npm 包補丁
│   └── wouter@3.7.1.patch
│
├── 📁 .manus/                          # Manus 平台文件
│   └── 📁 checkpoint_zip/              # 檢查點備份
│
├── 📄 package.json                     # npm 依賴配置
├── 📄 pnpm-lock.yaml                   # pnpm 鎖定文件
├── 📄 tsconfig.json                    # TypeScript 配置
├── 📄 tsconfig.node.json               # TypeScript Node 配置
├── 📄 vite.config.ts                   # Vite 構建配置
├── 📄 vitest.config.ts                 # Vitest 測試配置
├── 📄 drizzle.config.ts                # Drizzle ORM 配置
├── 📄 components.json                  # shadcn/ui 配置
├── 📄 .prettierrc                      # Prettier 代碼格式化配置
├── 📄 .prettierignore                  # Prettier 忽略文件
├── 📄 .gitignore                       # Git 忽略文件
├── 📄 README.md                        # 項目文檔
└── 📄 template.json                    # 模板配置
```

---

## 🔑 關鍵文件說明

### 前端文件

| 文件 | 用途 | 修改頻率 |
|------|------|---------|
| `client/src/pages/Home.tsx` | 首頁 - 輪播、品牌信息 | ⭐⭐⭐ 高 |
| `client/src/components/Navigation.tsx` | 導航菜單、語言切換 | ⭐⭐ 中 |
| `client/src/locales/translations.ts` | 中英文翻譯 | ⭐⭐⭐ 高 |
| `client/src/pages/LiveGigs.tsx` | 現場演出 - Google Calendar | ⭐ 低 |
| `client/src/pages/Wedding.tsx` | 婚禮樂團 - 影片播放 | ⭐⭐ 中 |
| `client/src/pages/Corporate.tsx` | 商演策劃服務 | ⭐⭐ 中 |
| `client/src/pages/Team.tsx` | 團隊理念介紹 | ⭐⭐ 中 |
| `client/src/App.tsx` | 路由配置 | ⭐ 低 |
| `client/src/index.css` | 全局樣式、顏色主題 | ⭐⭐ 中 |
| `client/index.html` | HTML 模板、SEO 標籤 | ⭐ 低 |

### 後端文件

| 文件 | 用途 | 修改頻率 |
|------|------|---------|
| `server/routers.ts` | tRPC API 路由 | ⭐⭐ 中 |
| `server/db.ts` | 資料庫查詢 | ⭐⭐ 中 |
| `drizzle/schema.ts` | 資料表定義 | ⭐⭐ 中 |

### 配置文件

| 文件 | 用途 | 修改頻率 |
|------|------|---------|
| `package.json` | 依賴配置 | ⭐ 低 |
| `vite.config.ts` | Vite 構建配置 | ⭐ 低 |
| `tsconfig.json` | TypeScript 配置 | ⭐ 低 |
| `.env.local` | 環境變數（本地） | ⭐⭐⭐ 高 |

---

## 🔄 數據流

### 前端到後端

```
React Component
    ↓
useQuery/useMutation (tRPC Hook)
    ↓
/api/trpc (HTTP 請求)
    ↓
server/routers.ts (tRPC 路由)
    ↓
server/db.ts (資料庫查詢)
    ↓
drizzle/schema.ts (資料表)
    ↓
MySQL 資料庫
```

### 多語言流程

```
Navigation.tsx (語言切換)
    ↓
LanguageContext.tsx (全局狀態)
    ↓
translations.ts (翻譯字典)
    ↓
各頁面組件 (使用 t() 函數)
```

---

## 📦 主要依賴

| 包名 | 版本 | 用途 |
|------|------|------|
| React | 19 | 前端框架 |
| Vite | 7+ | 構建工具 |
| Tailwind CSS | 4 | 樣式框架 |
| tRPC | 11 | API 通信 |
| Express | 4 | 後端框架 |
| Drizzle ORM | 最新 | 資料庫 ORM |
| TypeScript | 5+ | 類型檢查 |
| Framer Motion | 最新 | 動畫庫 |
| Wouter | 3+ | 路由庫 |

---

## 🔐 環境變數

### 必需變數

```env
# 應用配置
VITE_APP_TITLE=MileSpace

# Google Calendar
GOOGLE_CALENDAR_API_KEY=your_api_key
GOOGLE_CALENDAR_ID=your_calendar_id@group.calendar.google.com
```

### 可選變數

```env
# 資料庫
DATABASE_URL=mysql://user:pass@localhost/db

# OAuth
JWT_SECRET=your_secret
OAUTH_SERVER_URL=https://oauth.example.com

# S3 存儲
AWS_ACCESS_KEY_ID=your_key
AWS_SECRET_ACCESS_KEY=your_secret
```

---

## 🚀 常見修改位置

| 需求 | 修改位置 |
|------|---------|
| 修改首頁文字 | `client/src/pages/Home.tsx` |
| 修改菜單項目 | `client/src/components/Navigation.tsx` |
| 修改翻譯 | `client/src/locales/translations.ts` |
| 修改顏色主題 | `client/src/index.css` |
| 修改聯絡資訊 | `client/src/pages/Home.tsx` |
| 添加新頁面 | 在 `client/src/pages/` 建立新文件 |
| 添加新 API | 在 `server/routers.ts` 添加新路由 |
| 修改資料表 | `drizzle/schema.ts` + `pnpm db:push` |

---

## 📚 文件命名約定

- **頁面組件**：PascalCase，例如 `Home.tsx`、`LiveGigs.tsx`
- **可重用組件**：PascalCase，例如 `Navigation.tsx`
- **工具函數**：camelCase，例如 `utils.ts`
- **類型定義**：PascalCase，例如 `User.ts`
- **常數**：UPPER_SNAKE_CASE，例如 `API_URL`

---

## 🔗 文件關係圖

```
App.tsx (主路由)
├── Navigation.tsx (全局導航)
├── Home.tsx (首頁)
│   ├── GoogleCalendarEvents.tsx
│   └── translations.ts
├── LiveGigs.tsx
│   └── GoogleCalendarEvents.tsx
├── Wedding.tsx
├── Corporate.tsx
└── Team.tsx

server/routers.ts (後端 API)
├── server/db.ts (資料庫查詢)
└── drizzle/schema.ts (資料表)
```

---

## 💡 最佳實踐

1. **不要修改 `server/_core/`**：這是框架核心，修改可能破壞應用
2. **使用 TypeScript**：享受完整的類型檢查
3. **組件化設計**：將 UI 分解為小的、可重用的組件
4. **集中管理翻譯**：所有文本都應在 `translations.ts` 中
5. **環境變數**：不要硬編碼敏感信息
6. **測試覆蓋**：為關鍵功能編寫測試

---

**準備好探索代碼了嗎？從 `Home.tsx` 開始吧！** 🚀
