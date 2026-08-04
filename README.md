# Jan | AI Product Engineer & Full-Stack Developer

專注於 Flutter 跨平台行動端開發與 Python (FastAPI / GCP) 雲端架構的 AI 全端工程師。具備 0 到 1 完整產品生命週期交付經驗，涵蓋雙平台 App 商業上架、IAP 訂閱金流串接、高併發 LLM 異步任務佇列（Celery + Redis）、自研 AI 安全防衛機制（Guardrails）與離線優先數據救援架構。

注重產品思維，致力於將技術執行與商業價值結合，並善用 AI 輔助工作流提升開發效率與系統穩定度。

---

## 技術棧 (Technical Stack)

| 領域 | 核心技術與工具 | 工程應用範圍 |
| :--- | :--- | :--- |
| **Mobile & Frontend** | Flutter, Dart, Hooks_Riverpod, Rive, Provider | iOS / Android 雙平台開發、60fps 向量狀態機動畫、全域狀態管理、非同步記憶體自動回收 (`autoDispose`) |
| **Backend & Microservices** | Python (FastAPI), Celery, Redis, LINE Messaging API | 高效能 Async API、異步任務佇列解耦、Redis Pub/Sub 即時串流、LINE Webhook 狀態機中台 |
| **AI Systems & Safety** | OpenAI API (GPT-4o / Vision), Ollama, YOLO, Guardrails | 自研三階五因子 AI 風險過濾引擎、多模態圖像分析、邊緣物件辨識、地端 LLM 部署 |
| **Cloud, DB & DevOps** | GCP (Compute Engine, GCS), DigitalOcean, Supabase, Docker, Cloudflare | 雲端基礎設施維運、PostgreSQL 資料庫設計、Firebase Auth / FCM、DNS 資安管理 |
| **Monetization & Ecosystem** | Apple StoreKit, Google Play Billing, Git Flow, App Store Connect | 應用程式內購 (IAP) 串接、後端憑證驗證、企業級開發者帳號維運、CI/CD 分支控制 |

---

## 正式上架專案 (Production Deployments)

### 憂隔 Youge – 全方位 AI 心靈療癒與陪伴系統
結合自研 AI 安全防範引擎、異步語音/文字處理與 60fps 向量動畫之 B2C 雙平台行動應用程式。
- **品牌官方網站**: [youge.org](https://www.youge.org/)
- **iOS App Store**: [App Store 下載連結](https://apps.apple.com/tw/app/%E6%86%82%E9%9A%94/id6752664178)
- **Google Play Store**: [Google Play 下載連結](https://play.google.com/store/apps/details?id=com.datzuo.youge.android&pcampaignid=web_share)
- **AI 陪伴 LINE 官方帳號 (厝邊的阿豪)**: [點此加為好友](https://lin.ee/ZKP5Vkn)

### Pestologic – B2B 企業級機動派工與害蟲防治管理系統
整合 GCP 微服務、YOLO AI 視覺辨識與地下室離線數據救援防護之企業營運行動應用程式。
- **iOS App Store**: [App Store 下載連結](https://apps.apple.com/tw/app/pestologic/id6759633666)
- **Google Play Store**: [Google Play 下載連結](https://play.google.com/store/apps/details?id=com.hysia.pestologic&pcampaignid=web_share)

---

## 系統架構圖 (System Architecture)

graph TD
    subgraph Clients [Client Layer]
        App[Flutter Mobile App - iOS / Android]
        LineBot[LINE Official Account Bot]
    end

 subgraph BackendLayer [Backend & Async Pipeline]
        API[FastAPI Async Gateway]
        Guard[AI Risk Guardrails Engine]
        Celery[Celery Distributed Task Queue]
        Redis[(Redis Cache / PubSub Broker)]
    end

subgraph AIEngine [AI & Machine Learning Services]
        OpenAI[OpenAI GPT-4o / Vision API]
        Ollama[Local Ollama LLM Instance]
        YOLO[YOLO Object Detection Pipeline]
    end

subgraph Infrastructure [Cloud Infrastructure & Storage]
        SupaDB[(Supabase / PostgreSQL)]
        GCS[Google Cloud Storage]
        Push[Firebase FCM Push Notifications]
    end

App -- REST API / IAP Receipts --> API
    LineBot -- Webhook Events --> API
    
API --> Guard
    Guard -- Safe Processing --> Celery
    Guard -- Crisis Override --> API
    
Celery <--> Redis
    Celery --> OpenAI
    Celery --> Ollama
    API --> YOLO

Celery -- Save Processed Data --> SupaDB
    API --> GCS
    Redis -. Push Result Notification .-> Push -.-> App

### 【第二部分】實務案例研討、未來演進與聯絡資訊

## 實務案例研討 (Technical Case Studies)

### 1. 高併發 LLM 異步佇列解耦與自研 AI 安全防禦機制
* **問題背景**：B2C LLM 應用在大流量與高併發下，長時間模型推論（文字/語音/圖像）易導致 HTTP 連線超時（Timeout）；同時，心靈療癒場景需要嚴格的自殺防範與危機過濾機制。
* **技術解法**：
  * **自研 Guardrail 引擎**：設計「三階五因子」風險評估 Pipeline，透過正則前置過濾、Moderation API 與語意情境裁決，在識別出高風險輸入時即時觸發安全斷流，引導至緊急救援資源。
  * **任務異步解耦**：將耗時的 LLM 運算派發至 **Celery Task Queue**（搭配 **Redis**），運算完成後透過 **Redis Pub/Sub** 即時推播回前端，解除 HTTP Gateway 的併發瓶頸。

### 2. 離線優先架構與邊緣 AI 物件辨識整合
* **問題背景**：外勤人員於極限環境（如地下室）作業時，網頁式系統常因連線中斷導致數據遺失；傳統人工清點害蟲亦造成巡檢效率低下。
* **技術解法**：
  * **離線數據救援**：於 Flutter 端建立本地 SQLite 與快取策略。當網路斷線時，變更資料寫入本地，待連線恢復後經由 Exponential Backoff Retry 佇列自動同步回 PostgreSQL 伺服器，達成數據零遺失。
  * **邊緣 AI 整合**：將 YOLO 物件辨識模型整合至後端 Pipeline，透過相機拍攝自動計算害蟲密度，提升現場巡檢效率達 40%。

### 3. 向量狀態機渲染與記憶體生命週期優化
* **問題背景**：使用傳統 MP4 或 GIF 動畫容易在低階行動裝置上造成掉幀、發熱及記憶體洩漏（Memory Leak）。
* **技術解法**：
  * **Rive 狀態機**：全面採用向量畫質的 Rive 狀態機取代影片播放，縮減 80% 包體資源並將渲染效能穩定鎖定在 60fps。
  * **自動化記憶體清理**：使用 `Hooks_Riverpod` 搭配 `autoDispose` Provider，在頁面銷毀時自動釋放串流訂閱與控制器，防止記憶體洩漏。

### 4. 跨平台商業化訂閱與伺服器端憑證驗證
* **問題背景**：處理跨 iOS 與 Android 平台的訂閱制金流時，需要處理非同步的計費事件（續訂、退款、寬限期）並防止偽造憑證。
* **技術解法**：
  * 於 Flutter 端整合 iOS StoreKit 與 Google Play Billing 原生金流。
  * 於 FastAPI / Supabase 後端建立 Webhook 監聽與憑證驗證（Receipt Validation）邏輯，自動更新用戶權限並完成訂閱生命週期管理。

---

## 持續演進領域 (Ongoing Technical Focus)

- **AI-Native 工程工作流**：善用 AI Agent 工具（Cursor, Claude Code, MCP）建立自動化重構與測試流程，極大化單人開發產出槓桿。
- **現代化 Web 生態拓展**：將行動端的全棧思維與狀態管理經驗無縫拓展至 React.js 與 Next.js Web 應用開發。

---

## 聯絡方式 (Contact Information)

- **Email**: alex20021009@gmail.com
- **GitHub Profile**: [github.com/lai-jhinyan]([https://github.com/lai-jhinyan](https://github.com/lai-jhinyan/lai-jhinyan))
