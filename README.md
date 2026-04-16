# 太空指揮中心 (Space Command Dashboard)

[![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white)](https://nodejs.org/)
[![Node-RED](https://img.shields.io/badge/Node--RED-8F0000?style=flat-square&logo=nodered&logoColor=white)](https://nodered.org/)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![AngularJS](https://img.shields.io/badge/AngularJS-E23237?style=flat-square&logo=angularjs&logoColor=white)](https://angularjs.org/)

> **課程名稱**：醫用資訊系統分析與設計
>
> **開發技術**：Node-RED、HTML/CSS/AngularJS、RESTful API 異質系統整合

## 專案簡介

本專案為一個基於 Node-RED 事件驅動架構 (Event-driven Architecture) 所開發的整合型資訊儀表板。系統展示了複雜的異質系統串接、多源 API 通訊、前端 UI 動態渲染以及狀態機邏輯。雖然主題聚焦於「太空探索與指揮中心」，但其底層架構（如即時數據追蹤、影像輪播、API 排程抓取、AI 助理等）完全可平行轉移並應用於醫療健康諮詢、生理數據監測與衛教資訊站等醫資系統領域。

## 系統核心模組與設計亮點

1. **ISS 即時軌道追蹤與遙測 (Live Tracker & Telemetry)**

   * **設計理念**：實作高頻率定時輪詢 (Polling) 抓取衛星遙測數據，結合前端動態地圖渲染。

   * **技術細節**：介接 `WhereTheISS API`，利用 `node-red-contrib-web-worldmap` 即時標記太空站位置。並運用經緯度運算邏輯計算與目標地（台中市）之相對距離，同時實作「日照/陰影區」狀態切換的語音 (Audio) 與推播通知 (Toast) 警報機制。

2. **AI 智能對話助手 (Gemini 2.5 Flash-Lite)**

   * **設計理念**：整合大語言模型 (LLM) API，處理非同步的 JSON 請求與對話歷程渲染。

   * **技術細節**：實作 Switch 節點攔截無效空訊號 (防呆機制)，建立 Change 迴路自動清空前端輸入框以優化 UX。聊天紀錄透過 AngularJS 雙向綁定 (Two-way Data Binding) 保存於前端 Scope 中。

3. **宇宙資料庫與整合影像館 (Deep Space Gallery)**

   * **設計理念**：整合靜態 JSON 資料庫與動態外部 API 媒體資源。

   * **技術細節**：實作狀態機邏輯 (State Machine) 控制「自動輪播」與「手動切換」的影像展示器，資料來源涵蓋韋伯/哈伯望遠鏡圖庫以及 `NASA Mars Rovers API`，並結合 `NASA APOD` 獲取每日天文科普圖文。

4. **多源情報匯流網 (Space Info Hub)**

   * **太空人員追蹤**：介接 `Open-Notify API` 獲取當前在軌太空人名單，並加入 Fallback 容錯機制 (模擬資料)。

   * **太空天氣監測**：實作隨機數模擬器 (Simulation)，即時呈現太陽風、地磁指數 (Kp) 與 X 射線通量。

   * **即時新聞資料流**：介接 `Spaceflight News API`，透過 Function 節點進行資料清洗 (Data Cleansing) 後輸出。

## 系統架構圖 (System Architecture)

本系統採前後端分離的概念，透過 Node-RED 集中管理資料流與路由：

* **前端 (Frontend)**：使用 `node-red-dashboard` 構建深色主題 (Dark Theme) 的響應式 UI。

* **後端邏輯 (Backend Logic)**：負責排程觸發 (Cron/Interval)、API 請求封裝、跨節點狀態儲存 (Flow Context) 與資料正規化。

* **外部 API 整合 (External APIs)**：

  * `Google Gemini API` (AI 分析與對話)

  * `WhereTheISS API` (經緯度與遙測數據)

  * `NASA APOD API` & `NASA Mars Photos API` (天文影像)

  * `Spaceflight News API` (航太新聞)

  * `Open-Notify API` (在軌太空人名單)

## 安裝與執行步驟

如欲在本地端執行本專案，請確保已安裝 [Node.js](https://nodejs.org/) 與 [Node-RED](https://nodered.org/)。

1. 啟動 Node-RED (`node-red` 指令)。

2. **安裝必要模組**：請至 Node-RED 右上角選單 -> 「節點管理 (Manage palette)」中安裝以下套件：

   * `node-red-dashboard` (UI 介面核心)

   * `node-red-contrib-web-worldmap` (即時地圖套件)

3. **匯入流程檔案**：

   * 點擊右上角選單 -> **Import**。

   * 將本專案中的 `flows.json` 內容貼上並匯入。

4. **設定 API Key**：

   * 雙擊名為「準備 API 請求 (Prep)」的 Function 節點。

   * 將 `YOUR_API_KEY_HERE` 替換為有效的 Google Gemini API Key。

   * *(註：NASA API 已預設使用 `DEMO_KEY`，可直接運行)*

5. 點擊右上角 **Deploy** 進行部署。

6. 開啟瀏覽器進入 `http://localhost:1880/ui` 檢視太空儀表板。

## 系統畫面截圖

*(截圖)*

## 授權條款 (License)

本專案採用 [MIT License](LICENSE) 授權。您可以自由使用、修改與散佈此專案內容，但請保留原作者版權聲明。

---

*Developed for the Medical Information System Analysis and Design course.*
