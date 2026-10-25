# ELO.ELOLearning

ELOLearning 是一個以 Gemini 為核心的 AI 學習助手，任何人註冊後都能用**自己的 Gemini API Key** 來學習。

- 帳號註冊、登入與登出
- 問 AI：依年級、科目產生可編輯的學習筆記，支援智慧鏡頭拍照分析
- 我的重點：富文字編輯、表格、Word / PDF 匯出
- 我的題目：依照已保存重點產生練習、限時快問快答
- 設定：個人資料、頭像、密碼、畫面主題、AI 老師偏好、**Gemini API Key**

## Gemini API Key 怎麼運作

每位使用者在「設定 → Gemini API Key」貼上自己的金鑰：

- 金鑰只存在使用者自己瀏覽器的 localStorage，每個帳號分開保存
- 每次呼叫 AI 時透過 `X-Gemini-Api-Key` 標頭送到伺服器，伺服器只在那次請求中使用，**不會寫入資料庫或 log**
- 儲存前會先向 Gemini 驗證金鑰是否有效（查詢模型資訊，不消耗生成額度）

金鑰申請：<https://aistudio.google.com/apikey>

### 網站預設金鑰（選填）

如果在主機環境變數設定 `GEMINI_API_KEY`，沒填自己金鑰的使用者會改用這把，**額度會算在網站擁有者身上**。要讓大家各自用自己的額度，就不要設定它。

## 本機啟動

```bash
npm install
npm start
```

打開 <http://localhost:3000>。需要時可建立 `.env`（參考 `.env.example`）。

## 部署到 Render

1. New → Web Service → 選這個 repo
2. Runtime：Node，Build Command：`npm install`，Start Command：`npm start`，Instance Type：Free
3. 環境變數全部選填：`GEMINI_MODEL`（預設 `gemini-3.6-flash`）、`GEMINI_API_KEY`（網站預設金鑰）

## 注意

帳號與筆記目前存在 `data/elolearning.json`。Render 免費方案重啟或重新部署時這個檔案會被清空，正式多人使用建議之後改接 PostgreSQL（例如 Supabase）。
