# Gemini AI 與太空探索即時儀表板 (Space AI Dashboard)

[![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white)](https://nodejs.org/)
[![Node-RED](https://img.shields.io/badge/Node--RED-8F0000?style=flat-square&logo=nodered&logoColor=white)](https://nodered.org/)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![AngularJS](https://img.shields.io/badge/AngularJS-E23237?style=flat-square&logo=angularjs&logoColor=white)](https://angularjs.org/)

> **課程名稱**：醫用資訊系統分析與設計
>
> **開發技術**：Node-RED、HTML/CSS/AngularJS、RESTful API

## 專案簡介

本專案為一個基於 Node-RED 事件驅動架構 (Event-driven Architecture) 所開發的整合型資訊儀表板。系統主要展示了異質系統串接、API 通訊以及前端 UI 動態渲染的能力。雖然主題聚焦於太空探索，但其底層架構完全可輕易抽換 API，轉換為醫療健康諮詢助手與衛教資訊站。

## 系統功能與設計亮點

1. **AI 智能對話模組 (Gemini 1.5 Flash)**

   * **設計理念**：實作大語言模型 (LLM) 的 API 串接，處理非同步的 JSON 請求與回應。
   * **技術細節**：加入 Switch 節點攔截無效的空訊號 (防呆機制)，並透過 Change 節點建立迴路自動清空前端輸入框，優化使用者體驗 (UX)。

2. **即時新聞資料流 (Spaceflight News API)**

   * **設計理念**：實作排程任務 (Cron-like trigger) 與 RESTful GET 請求，定時抓取並解析 JSON 格式的新聞資料。
   * **技術細節**：透過 Node-RED 的 Function 節點進行資料清洗 (Data Cleansing)，過濾出標題、時間、圖片與連結，並傳遞給前端 Template 進行動態列表渲染。

3. **即時影像串流嵌入**

   * **設計理念**：整合外部媒體資源 (NASA YouTube 直播)，提供 24 小時不間斷的監控/觀賞畫面。

## 系統架構圖 (System Architecture)

本系統採前後端分離的概念，但透過 Node-RED 集中管理資料流：

* **前端 (Frontend)**：使用 `node-red-dashboard` (基於 AngularJS) 構建響應式 UI，包含聊天對話視窗、新聞卡片列表與影片嵌入。
* **後端邏輯 (Backend Logic)**：由 Node-RED 負責路由、資料轉換與錯誤處理。
* **外部 API (External APIs)**：
  * `POST https://generativelanguage.googleapis.com/...` (Gemini AI)
  * `GET https://api.spaceflightnewsapi.net/v4/articles/` (Space News)

## 安裝與執行步驟

如欲在本地端執行本專案，請確保已安裝 [Node.js](https://nodejs.org/) 與 [Node-RED](https://nodered.org/)。

1. 啟動 Node-RED (`node-red` 指令)。
2. 確保已安裝 Dashboard 模組：在節點管理中安裝 `node-red-dashboard`。
3. 匯入流程檔案：
   * 點擊右上角選單 -> **Import**。
   * 將本專案中的 `flows.json` 內容貼上並匯入。
4. **設定 API Key**：
   * 雙擊名為「準備 API」的 Function 節點。
   * 將 `YOUR_API_KEY_HERE` 替換為有效的 Google Gemini API Key。
5. 點擊右上角 **Deploy** 進行部署。
6. 開啟瀏覽器進入 `http://localhost:1880/ui` 檢視儀表板。

## 系統畫面截圖

*(儀表板的實際截圖)*

---
*Developed for the Medical Information System Analysis and Design course.*
