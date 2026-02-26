# 數列與級數互動題庫專案

這是一個純前端靜態網頁應用，用來進行高中數列/級數的「練習模式」與「考試模式」題目互動。

- 前端：`sequence-series-demo.html`
- 外部題庫：`sequence-series-bank.json`

---

## 專案目標

- 以高中數列與級數為主題，提供互動題目與即時判斷
- 支援兩種模式
  - 練習模式：即時作答與回饋
  - 考試模式：10 題計時測驗與結果回顧
- 內建題庫 + 外部 JSON 題庫混合抽題
- 可依題型分類（topic / title）擴充題庫

---

## 快速開始

### 1) 下載/切換到專案目錄

```bash
cd d:/leeyuyun_data/project/20260223
```

### 2) 開啟本機靜態伺服器（建議）

```bash
# 使用 Python
python -m http.server 8080
```

然後開啟：

```text
http://localhost:8080/sequence-series-demo.html
```

> 不建議直接用 `file://` 打開 HTML，因為題庫是透過 `fetch` 載入 `sequence-series-bank.json`，容易受瀏覽器檔案協定限制。

---

## 專案檔案

- `sequence-series-demo.html`
  - 主要應用程式，包含：
    - 題目生成（內建題目 + 外部題庫）
    - 練習/考試流程
    - 計分、回饋、錯題重練
    - 題型對照表與題庫權重設定
- `sequence-series-bank.json`
  - 外部題庫檔案（`items` 陣列）
- `README.md`
  - 專案說明文件
- `.codex/skills/*/SKILL.md`
  - 僅為 Codex 規則/輔助文件，不影響瀏覽器執行

---

## 題庫格式（`sequence-series-bank.json`)

JSON 需有 `items` 陣列，項目欄位如下：

- `kind`: `fill` 或 `choice`
- `topic`: 題目主題（用於主題權重與篩選）
- `title`: 題型敘述（更細分類）
- `prompt`: 題目文字
- `answer`: 答案（`fill` 用可解析數值或文字；`choice` 指向正確選項）
- `options`: `choice` 類型必填
- `hint`: 提示文字
- `explain`: 解釋文字
- `formula`: 公式資訊
- `terms`: 預覽項目序列（可選）
- `scope`: `both` / `practice` / `exam`
- `scope` 可以控制題目只出現在某個模式；預設為 `both`

---

## 抽題設定

在 `sequence-series-demo.html` 的 `BANK_CONFIG` 可調整：

- `useExternalRateByMode.practice`
- `useExternalRateByMode.exam`
- `externalTopicWeights.practice`
- `externalTopicWeights.exam`

目前設定為：
- 練習：優先使用外部題庫比約 `0.65`
- 考試：優先使用外部題庫比約 `0.9`

---

## 開發注意事項

- 所有題目由前端即時生成或從 JSON 載入，無後端依賴
- 啟動時會先載入外部題庫（`sequence-series-bank.json`）
- 若題庫載入失敗，仍可使用內建題庫繼續使用

---

## 簡單擴充流程

1. 新增一筆題目到 `sequence-series-bank.json` 的 `items`
2. 確認有 `topic`、`title`、`scope`
3. 需要新題型比例可在 `BANK_CONFIG.externalTopicWeights` 補上 `topic` 權重
4. 重新整理頁面即可生效

## 專案異動紀錄

- 2026-02-26：將 `sequence-series-demo.html`、`sequence-series-bank.json` 與 `README.md` 整理到子目錄 `數列級數/`，並推送到 GitHub 倉庫 `https://github.com/leeyuyun/highschool-teaching`。
- 對應 Commit：`7889003`
- 指派 Git tag：`sequence-series-demo-2026-02-26`
