# 疫調系統前端

這是高雄市小港高中發病個案疫調系統的前端部分，使用 GitHub Pages 託管。

## 功能特色

- 📱 響應式設計，支援手機和桌面裝置
- 🔄 與 Google Apps Script 後端 API 整合
- ✅ 即時表單驗證
- 📊 資料提交和 LINE 通知功能
- 🎨 現代化 UI 設計

## 部署說明

### 1. 設定 GitHub Pages

1. 將此專案上傳到 GitHub 儲存庫
2. 在儲存庫設定中啟用 GitHub Pages
3. 選擇 `main` 分支作為來源
4. 等待部署完成

### 2. 設定 Google Apps Script API

1. 在 Google Apps Script 中部署為網頁應用程式
2. 設定執行權限為「任何人」
3. 將 API URL 更新到 `index.html` 中的 `API_URL` 變數

### 3. 更新 API 端點

在 `index.html` 中找到以下行：
```javascript
const API_URL = 'https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec';
```

將 `YOUR_SCRIPT_ID` 替換為您的 Google Apps Script 部署 ID。

## 檔案結構

```
frontend/
├── index.html          # 主要 HTML 檔案
├── README.md          # 說明文件
└── assets/            # 靜態資源（如需要）
```

## 技術規格

- 純 HTML/CSS/JavaScript
- 無需建置工具
- 支援所有現代瀏覽器
- 與 Google Apps Script 後端整合

## 使用方式

1. 開啟部署後的 GitHub Pages URL
2. 填寫疫調表單
3. 點擊「送出表單」
4. 系統會自動發送 LINE 通知

## 注意事項

- 確保 Google Apps Script 後端已正確設定 CORS
- 測試時請使用真實的 LINE 通知設定
- 建議在正式環境前進行充分測試
