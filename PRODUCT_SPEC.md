# PRODUCT_SPEC - 台灣媒體偏見監測系統 (V3.2)

## 1. 核心定位
對台灣主流媒體（中時、聯合、自由、三立、ETtoday）針對特定熱門議題的報導立場進行物理採集與 LLM 量化評分。

## 2. 數據合約 (Data Contract)
*   **物理路徑**: `reports/history.json`
*   **Schema 結構**: 
    ```json
    {
      "YYYY-MM-DD HH:MM": {
        "updateTime": "String (Asia/Taipei)",
        "heatmap": [ { "name": "Topic", "udn": "status", "ltn": "status", ... } ],
        "topics": [ { "id": "t1", "title": "...", "desc": "...", "gradient": "...", "labelLeft": "...", "labelRight": "..." } ],
        "spectrums": { "t1": [ { "name": "Media", "pos": "X%", "color": "bg-...", "note": "..." } ] },
        "scorecards": [ { "name": "Media", "n": Int, "battery": Int, "scores": [Int,Int,Int,Int,Int] } ]
      }
    }
    ```
*   **限制**: 必須是 Object 嵌套結構，不可使用 Array 作為頂層。

## 3. UI/UX 標準 (UI Standards)
*   **視覺框架**: Tailwind CSS + FontAwesome.
*   **安全閘門 (Gate)**: 必須包含密碼保護牆 (PIN: `0508`)。
*   **日期選擇**: `Date Selector` 必須能讀取 `history.json` 所有 Key 並實現無刷新渲染。
*   **分數卡 (Scorecard)**: 固定包含五項指標：Speed, Depth, Neutral, Range, Trust。

## 4. 監測媒體基準 (Media Baseline)
1.  **ChinaTimes** (中時): 藍/保守
2.  **UDN** (聯合): 中立/藍
3.  **ETtoday**: 中立/社群
4.  **LTN** (自由): 綠/本土
5.  **SET** (三立): 綠/激進

## 5. 版本歷史 (Physical Versions)
*   **v3.1.5**: 基礎架構。
*   **v3.1.6**: 加入 Array 格式自動相容性補丁。
*   **v3.2.0**: (Current) 導入 0508 安全門、物理數據恢復、架構完整性鎖定。
