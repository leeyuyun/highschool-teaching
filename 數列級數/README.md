# 高中「數列級數」教學專案（v1）

本目錄為獨立教學專案，提供高中《數列與級數》題型練習與考試模式，使用純前端實作，可直接在瀏覽器開啟。

## 1. 專案目錄結構

- `sequence-series-demo.html`  
  主程式頁面，包含題目渲染、作答檢查、考試流程、結果彙整、提示/解析。
- `sequence-series-bank.json`  
  外部題庫資料，放置大量題目（含題型與難度資訊）。
- `README.md`  
  本檔，紀錄專案使用方式與維護規則。

## 2. 快速啟動

### 2.1 使用本機靜態伺服器（建議）

```bash
cd d:/leeyuyun_data/project/20260223
python -m http.server 8080
```

開啟：

```text
http://localhost:8080/數列級數/sequence-series-demo.html
```

> 為避免瀏覽器對 `fetch` 本地檔案的限制，請不要直接用 `file://` 開啟。

## 3. 主要功能

- 練習模式（Practice）
  - 題目連續生成
  - 立即判斷正誤
  - 顯示提示與詳細解析
- 考試模式（Exam）
  - 預設 10 題
  - 倒數計時器
  - 完成後彙總作答結果與題目回顧
- 題目來源
  - 內建題庫：內嵌在 `sequence-series-demo.html` 的 `QUESTION_TEMPLATES`
  - 外部題庫：從 `sequence-series-bank.json` 載入
- 題庫設定
  - 練習模式與考試模式可設定不同外部題庫使用機率
  - 支援依 `topic` 權重進行加權抽題

## 4. 外部題庫格式（`sequence-series-bank.json`）

檔案是 JSON，核心欄位在 `items` 陣列，常見欄位如下：

- `kind`：`fill` 或 `choice`
- `scope`：`both` / `practice` / `exam`
- `topic`：主題分類（如等差數列、等比級數…）
- `title`：題目敘述類型
- `prompt`：題目文字
- `answer`：填空題答案；`choice` 用 answer index 或可對應答案索引
- `options`：選擇題選項（僅 `choice`）
- `hint`：提示
- `explain`：解析
- `formula`：公式
- `terms`：題列預覽值（可選）

## 5. 常用維護規則

- 新增外部題目時，先填好 `topic` 與 `title`，並指定 `scope`。
- 若要調整各主題抽題傾向，修改 `sequence-series-demo.html` 中：
  - `BANK_CONFIG.externalTopicWeights`
- 問題修正以此順序進行：
  1. 檢查題目資料欄位是否完整  
  2. 確認 `parseAnswer` 能解析輸入格式（數字、分數）  
  3. 測試一次練習模式與考試模式各 1-2 輪

## 6. 目前版本紀錄

- 2026-02-26：建立「數列級數」教學專案，包含主頁面與外部題庫
- 2026-02-26：建立題目類型統計、外部題庫權重抽題、Git tag 與上傳至 repo
- 2026-02-27：整合內建與外部題庫為單一出題池，固定題型選單可直接涵蓋全部主題
- 2026-02-27：新增「看完整解題過程」按鈕；Hint 與完整解法分離，且考試模式禁用提示/解法
- 2026-02-27：補齊遞迴數列與幾何加權級數題型（含 `a_n=2a_{n-1}+7`、`a_n=4a_{n-1}+3n+6`、`Σ4^k(3k^2+4k+5)`）
- 2026-02-27：修正 LaTeX/MathJax 顯示與 fallback 轉換（下標、上標、求和上/下限、分數與遞迴表達式）

## 7. 注意事項

- `.codex/skills/*` 是 Codex 使用檔，不參與前端運行。
- 若 `sequence-series-bank.json` 無法載入，系統仍可使用內建題目繼續運作。
