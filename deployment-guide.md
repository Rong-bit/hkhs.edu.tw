# 疫調系統前後端分離部署指南

## 概述

本指南將協助您將疫調系統分離為：
- **前端**：託管在 GitHub Pages
- **後端**：保留在 Google Apps Script

## 步驟 1：設定 Google Apps Script 後端

### 1.1 部署 Google Apps Script

1. 開啟您的 Google Apps Script 專案
2. 點擊「部署」→「新增部署作業」
3. 選擇類型：「網頁應用程式」
4. 設定：
   - 執行身分：「我」
   - 存取權限：「任何人」
5. 點擊「部署」
6. **重要**：複製部署 URL，格式如：
   ```
   https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec
   ```

### 1.2 驗證 API 端點

測試以下端點是否正常運作：

1. **獲取表單 HTML**：
   ```
   GET https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec?action=getForm
   ```

2. **提交表單資料**：
   ```
   POST https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec
   Content-Type: application/json
   
   {
     "name": "測試姓名",
     "id": "A123456789",
     "class": "一年一班",
     "birthDate": "2000-01-01",
     "onsetMonth": "1",
     "onsetDay": "1"
   }
   ```

## 步驟 2：設定 GitHub 前端

### 2.1 建立 GitHub 儲存庫

1. 在 GitHub 建立新儲存庫，命名為 `epidemic-tracking-frontend`
2. 將 `frontend` 資料夾中的檔案上傳到儲存庫根目錄

### 2.2 更新 API 端點

編輯 `index.html`，找到以下行：
```javascript
const API_URL = 'https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec';
```

將 `YOUR_SCRIPT_ID` 替換為您的實際 Script ID。

### 2.3 啟用 GitHub Pages

1. 進入儲存庫的「Settings」頁面
2. 滾動到「Pages」區段
3. 在「Source」選擇「Deploy from a branch」
4. 選擇「main」分支和「/ (root)」資料夾
5. 點擊「Save」
6. 等待幾分鐘讓 GitHub Pages 部署完成

### 2.4 獲取前端 URL

部署完成後，您的前端 URL 將是：
```
https://YOUR_USERNAME.github.io/epidemic-tracking-frontend/
```

## 步驟 3：測試整合

### 3.1 基本功能測試

1. 開啟前端 URL
2. 填寫測試表單
3. 點擊「送出表單」
4. 檢查是否收到成功訊息
5. 檢查 Google Sheets 是否有新資料
6. 檢查 LINE 通知是否正常發送

### 3.2 錯誤處理測試

1. 測試必填欄位驗證
2. 測試身分證字號格式驗證
3. 測試網路連線中斷情況
4. 測試後端 API 錯誤回應

## 步驟 4：安全性設定

### 4.1 CORS 設定

Google Apps Script 已設定 CORS 標頭：
```javascript
'Access-Control-Allow-Origin': '*'
```

### 4.2 建議的安全改進

1. **限制 CORS 來源**（可選）：
   ```javascript
   'Access-Control-Allow-Origin': 'https://YOUR_USERNAME.github.io'
   ```

2. **API 金鑰驗證**（進階）：
   - 在 Google Apps Script 中新增 API 金鑰驗證
   - 在前端請求中加入金鑰

## 步驟 5：監控和維護

### 5.1 監控工具

1. **Google Apps Script 執行記錄**：
   - 查看「執行」頁面監控 API 呼叫
   - 檢查錯誤日誌

2. **GitHub Pages 分析**：
   - 使用 GitHub 內建分析功能
   - 監控頁面載入時間

### 5.2 定期維護

1. **每月檢查**：
   - 確認 Google Apps Script 配額使用情況
   - 檢查 LINE API 配額

2. **更新部署**：
   - 前端更新：推送到 GitHub 自動部署
   - 後端更新：在 Google Apps Script 中重新部署

## 故障排除

### 常見問題

1. **CORS 錯誤**：
   - 確認 Google Apps Script 已正確設定 CORS 標頭
   - 檢查 API URL 是否正確

2. **API 呼叫失敗**：
   - 檢查 Google Apps Script 部署設定
   - 確認執行權限設定為「任何人」

3. **表單載入失敗**：
   - 檢查網路連線
   - 確認 API 端點可正常存取

### 聯絡支援

如遇到問題，請檢查：
1. Google Apps Script 執行記錄
2. 瀏覽器開發者工具 Console
3. GitHub Pages 部署狀態

## 完成檢查清單

- [ ] Google Apps Script 已部署並可存取
- [ ] API 端點測試通過
- [ ] GitHub 儲存庫已建立
- [ ] 前端檔案已上傳
- [ ] API URL 已更新
- [ ] GitHub Pages 已啟用
- [ ] 前端可正常載入
- [ ] 表單提交功能正常
- [ ] LINE 通知功能正常
- [ ] 錯誤處理正常運作
