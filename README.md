# 腦室鏡手術紀錄 Form (Neuroendoscopy Operative Report)

結構化腦室鏡手術紀錄 — 單檔 HTML form,瀏覽器直接執行。

🔗 **Live demo**: https://cwhuang147852.github.io/neuroendo-form-demo/

> ⚠️ Demo only — 公開網址帶有 `noindex,nofollow` meta + DEMO banner,**請勿輸入真實病人資料**。

---

## 目標

把神經外科腦室鏡手術紀錄從自由文字升級為結構化資料:

1. 手術中即時填寫 + autosave(localStorage)
2. 結構化欄位支援 cohort 分析
3. 匯出 PDF / docx / JSON 用於病歷
4. 累積資料供日後論文(post-op outcome、手術時間、併發症 cohort)

當前版本:**v0.7**

---

## 技術棧

- **單檔 HTML**(無 build,瀏覽器直接開)
- Vanilla JS,無 framework
- CSS variables(主色 `#1a3f6f`,字型 Noto Sans TC + IBM Plex Mono)
- 外部資源:**Google Fonts CDN only**
- 儲存:`localStorage`(不送雲端)
- 部署:GitHub Pages(push 到 `main` 自動上線)

---

## 開發

```bash
git clone https://github.com/CWhuang147852/neuroendo-form-demo.git
cd neuroendo-form-demo

# 方式 A:直接開
open index.html

# 方式 B:起個 local server(建議)
python3 -m http.server 8000
# → http://localhost:8000/
```

無編譯、無依賴、無 package.json。改完存檔重新整理瀏覽器即可。

---

## 規範(請維持)

1. **單檔哲學** — 整份 form 維持單一 `.html` 可獨立執行。**不要引入 build pipeline / npm / framework**。OR 端不可能跑 build,sterile cover 下也不可能 troubleshoot 環境。外部資源只允許 Google Fonts CDN。
2. **病人資料絕不寫死** — 欄位是 schema,不可有真實病例。
3. **autosave 只走 localStorage** — 不要新增雲端 / API 呼叫,除非經過討論。
4. **版本演進** — 改動較大時 bump 版本(v0.7 → v0.8),保留前版於本地工作目錄;但 demo entry point 始終是 `index.html`。
5. **欄位增刪要對齊** — 日後若做 cohort 分析,刪欄位 = 之前資料遺失。新增 OK,刪除前先確認。
6. **DEMO banner 不要動** — `.demo-banner` 與 `<meta name="robots" content="noindex,nofollow">` 是 demo 公開部署的法規護欄,移除前先問。

---

## 結構速覽(`index.html`)

從上到下:

| 區塊 | class | 功能 |
|---|---|---|
| Top bar (sticky) | `.bar` | 標題、版本、autosave indicator、資料夾選擇、列印按鈕 |
| Demo banner | `.demo-banner` | 紅框警告(print 時隱藏) |
| 進度條 | `.prog-wrap` | 完成度 + 已存病例數 |
| Section × N | `.section` / `.sec-head` | 行政資料、Indications、術前/術中/術後 etc. |
| Form table | `.ft` / `.lbl` | 標準兩欄式 label + value |
| Signature | `.sig` | 主刀 / 助手 / 護理簽名欄 |
| Actions | `.actions` | 存檔、列印、匯出 |
| Modal | `.overlay` / `.modal` | 報告預覽、病例列表 |
| JS | inline `<script>` | autosave、欄位驗證、報告生成、匯出 |

CSS 在 `<head>` 內 `<style>` 區塊,JS 在 `</body>` 前 `<script>` 區塊。

---

## 部署

push 到 `main` 即自動部署到 GitHub Pages(60 秒內生效):

```bash
git add index.html
git commit -m "<改了什麼>"
git push
```

Pages 設定:Settings → Pages → Source = `Deploy from a branch` / `main` / `/ (root)`。已啟用,不需再動。

---

## TODO

- [ ] **欄位 JSON schema 明確化** — 在 form 內維護顯式 schema(key、type、enum、required),日後匯出 / 統計 / 串 REDCap 用同一份 source of truth
- [ ] localStorage autosave 邏輯壓測(瀏覽器關閉、quota 滿、跨 tab 同步)
- [ ] 匯出 JSON / PDF / docx 三種格式
- [ ] OR 端實測(平板 / 桌機 / sterile cover 下的可用性)
- [ ] 累積 case → cohort 分析架構(可考慮 REDCap / OpenEHR 對齊)
- [ ] 多人協作版本(若要做,需重新設計儲存層 — 已超出單檔 HTML 範圍)

---

## 聯絡

Repo owner: [@CWhuang147852](https://github.com/CWhuang147852)

任何 PR 或 issue 都歡迎,但**改動前請先 review 上面的「規範」段**,特別是「不要引入 build pipeline」這條。
