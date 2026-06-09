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
必須嚴格對齊 UI 渲染列表，固定為以下七大媒體：
1.  **UDN** (聯合報): 中立/藍
2.  **LTN** (自由時報): 綠/本土
3.  **FTV** (民視新聞): 綠/本土
4.  **CT** (中國時報): 藍/保守
5.  **CTI** (中天新聞): 紅/藍/激進
6.  **SET** (三立新聞): 綠/本土/激進
7.  **ETtoday**: 中立/大眾

## 5. UI 視覺契約 (UI Visual Contract)
為了保持品牌姿態一致性，以下常數不可隨意變更：
*   **背景色**: `slate-50`
*   **Header 背景**: `slate-900`
*   **主色調**: `blue-500` (Bat-Blue)
*   **字體**: 標題 `font-black`, 內文 `font-sans`
*   **Scorecard 指標**: 固定 [Speed, Depth, Neutral, Range, Trust]
*   **Heatmap 顏色**: Green (支持), Yellow (中立/觀望), Red (批判), Red-Video (影音批判), Gray (沈默)


## 5. 版本歷史 (Physical Versions)
*   **v3.1.5**: 基礎架構。
*   **v3.1.6**: 加入 Array 格式自動相容性補丁。
*   **v3.2.0**: (Current) 導入 0508 安全門、物理數據恢復、架構完整性鎖定。
