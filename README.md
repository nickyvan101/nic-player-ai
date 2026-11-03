# Nic Player

Windows 桌面可攜式影片投放工具：把**本地影片檔案**與**網頁影片**穩定投放到電視——支援市面上絕大多數投放方式：**Google Cast（Chromecast 內建）、AirPlay／AirPlay 2（Apple TV 與支援 AirPlay 的電視）、DLNA／UPnP（各大品牌智慧電視）**；並內建**影片下載器**（貼上 YouTube／Bilibili／TikTok／Instagram／Facebook／Twitch 等連結即可存到電腦）。

> 純黑色質感介面 · 緩衝預載 · 自適應碼率（ABR）· 斷線自動續播 · 影片下載

> **1.1.6（2026-11-04，完全免費）**：已移除序號、使用時數、下載次數與付費方案，所有功能免費開放。安裝檔已發佈於 [GitHub Releases](https://github.com/nickyvan101/nic-player-ai/releases/latest)；未簽章，SmartScreen 可能顯示「未知的發行者」。主程式更新只會提示，不會自動安裝；更新視窗可直接按「立即下載」開啟最新官方 installer。AI／下載引擎仍走簽章 manifest 與 SHA-256 驗證。

> **請尊重智慧財產權，僅供個人合法影音播放與備份使用。**

---

## 一、這是什麼

原版 Airflow 類工具採用「即時傳送」方式：電腦端把畫面即時轉換後連續送給電視，只要無線網路短暫不穩，電視就會卡頓、定格或斷線。

本工具採用**新一代穩定播放架構**，讓影片無論是本地檔案或網頁連結，都能從頭到尾完整順暢播完：

| 穩定技術 | 說明 | 對應問題 |
|---|---|---|
| 投放前鏈路偵測 | 開播前先量測電腦→電視的實際連線品質（延遲、抖動、封包遺失）＋歷史紀錄 | 不穩定的網路會在「開播前」就被識別並先做準備 |
| **零中斷預載模式（新）** | 偵測到不穩定時，先在**電視上顯示專屬倒數畫面**（說明原因＋剩餘時間＋進度條）；預設先累積 **30 秒**即開播（最長等 45 秒），背景持續補到 240 秒（本地）／120 秒（網頁）；把「快速開始」設為 0 可改用完整預載（本地 4 分鐘／網頁 2 分鐘目標） | 開頭不卡、整場不中斷；使用者清楚知道「為什麼等、還要等多久」，又不必空等數分鐘 |
| 緩衝預載（Preload Buffer） | 預設先累積 30 秒即開播，背景持續補到 240 秒（本地）／120 秒（網頁）的內容存量 | 無線瞬間抖動時，電視靠存量繼續播 |
| 自適應碼率（ABR） | 同時提供 1080p / 720p / 480p 多種畫質串流，電視依實際網速自動選最順的 | 網速變慢時自動降畫質，而不是卡住 |
| 智慧節流 | 轉碼程序自動「追趕」播放進度、保持安全存量，不是無腦狂轉 | 電腦資源穩定、磁碟用量可控 |
| 斷線自動重連＋續播 | 無線中斷時自動重連，接回原本進度繼續播放；控制通道心跳放寬到 30 秒容錯，短暫延遲不再被誤判成斷線 | 短暫斷線不再需要重新投放 |
| 長緩衝電視端畫面 | 手動緩衝期間電視改播輕量的「手動緩衝中」畫面（本機產生、持續播放），不再長時間停在暫停畫面；停止緩衝一定先載回真正影片 | 避免 Google TV／電視棒因長時間暫停進入待機、省電而斷網 |
| 網頁影片代理＋智慧預讀 | 遠端影片先經過本機代理；**依播放清單順序**＋實測速度自動加深分段預讀（最高 24 段，隨機檔名串流也支援）；來源太慢時自動只挑低碼率版本、或整段下載到本機後再播 | 遠端伺服器突然變慢或抖動也不影響觀看 |
| 網頁 HLS 相容模式 | 代理分段網址縮短、單一變體 master 自動補 CODECS／修正異常 BANDWIDTH；電視若仍連續拒播，自動改用本機 HLS remux（不再無限重載同一個網址） | 老電視或格式不標準的網站也能播 |
| 硬體加速轉碼 | 自動使用 NVIDIA NVENC／Intel Quick Sync，速度可達 10–20 倍即時 | 快轉、跳段幾乎無等待 |

### 零中斷預載模式怎麼運作（用超商比喻）

就像出遠門前先確認天氣與路況：

1. **出發前檢查（鏈路偵測）**：按下投放時，先對電視做 5 次來回測試——就像先打電話確認路況。
2. **路況不好就先備糧（預載畫面）**：偵測到無線不穩（或網頁來源太慢），電視上會出現專屬畫面：
   「因無線傳輸不穩定，為確保完整順暢播完，正在預先載入影片…」＋**即時倒數**（約 X 分 Y 秒後開始播放）＋進度條。
3. **備好糧就出發**：預設先累積 30 秒就開播（最長等 45 秒），背景持續補到 240 秒；可在設定調整「快速開始緩衝／最長等待」。
4. **一路順到底**：播放中程式持續監看網路品質，存量快用完前會提前降畫質，真的卡住也會自動恢復；斷線時自動重連續播。

網頁影片另有兩種「備糧」方式：來源是串流（HLS）時先預先下載多段內容；來源是一般影片檔時，直接**整段下載到本機快取**，電視改成從你的電腦區域網路讀取——等於把慢速來源變成區域網路播放，幾乎無敵順。

設定頁最上方可選**緩衝位置**（**預設智慧混搭＝RAM 優先、滿了續用其他磁碟槽**；另可選自動＝最大空閒磁碟／指定磁碟槽／RAM 記憶體），RAM 上限可自訂（**預設 512MB**；0＝自動，256–8192MB；關閉程式立即釋放），並可調整：預載策略（自動／一律／關閉）、快速開始緩衝／最長等待，以及背景緩衝目標。

---

## 二、支援的投放方式（市場覆蓋）

| 投放方式 | 涵蓋裝置 | 說明 |
|---|---|---|
| **Google Cast** | Chromecast、Android TV、Google TV、內建 Chromecast 的智慧電視、Google TV Streamer | 完整自適應碼率（ABR）＋預載緩衝 |
| **AirPlay／AirPlay 2** | Apple TV、支援 AirPlay 的電視（Samsung／LG／Sony／Vizio 近年機型、AirPlay 顯示器） | 內建 pyatv 引擎（業界最完整的開源 AirPlay 實作）；首次使用於裝置清單按「配對」，輸入電視顯示的 PIN 碼即可，之後自動記住 |
| **DLNA／UPnP AV** | Samsung／LG／Sony／小米等大多數智慧電視、部分擴大機 | 支援直接播放、封裝轉換、即時轉碼三種模式 |
| Miracast／WiDi（螢幕鏡像） | Windows／Android 無線顯示 | 本質為即時螢幕鏡像（非檔案投放），Windows 已內建：按 **Win + K** 即可使用，本工具不另行實作 |

> 裝置清單會自動以 mDNS 同時掃描 Google Cast 與 AirPlay 裝置，並以 SSDP 掃描 DLNA 裝置；找不到時可手動輸入 IP（三種型別皆支援）。

## 三、功能總覽

- **本地影片投放**：幾乎所有格式（MP4／MKV／AVI／MOV／HEVC／HDR…），引擎自動選擇最佳方式：
  - 直接播放（不需轉換，畫質無損）
  - 封裝轉換（不重新編碼，秒速完成）
  - 自適應轉碼（ABR＋預載）
- **網頁影片投放**：貼上網頁連結 → 自動找出頁面中的所有影片 → **列出縮圖、解析度、時長供你選擇** → 一鍵投放
- **影片下載**：貼上影片連結（YouTube／Bilibili／TikTok／Instagram／Facebook／Twitch／一般網頁影片）→ 解析 → 選畫質（最高 4K 或僅音訊 MP3／M4A）→ 下載；有字幕會一併存檔；內建引擎自我更新（`檢查更新`）。**Bilibili 使用內建專用解析**（不依賴 yt-dlp；免登入畫質以網站為準、不含字幕）
- **播放佇列**：多部影片排隊自動續播；**播放中或投放中按「加入影片」、拖放或加入網頁連結都只排入目前項目後方，不會中斷正在看的影片／投放**；清單有前後片時，迷你與全螢幕畫面會出現左右換片箭頭
- **多開**：設定頁最上方可選「只允許開啟一個 Nic Player」（預設）或「不限制」；多開時每個實例有獨立的 Chromium profile、播放清單與快取，**播放紀錄與進度則跨實例共用同步**，可同時播放不同影片，也可直接從檔案總管個別開啟多部影片
- **內建播放器（mpv 引擎，v1.4.0 升級）**：直接觀看電腦上的影片（不必投放）——**全格式免解碼包**（MP4／MKV／AVI／FLV／WMV／HEVC／AV1／VP9；MP3／FLAC／APE／WAV）、**硬體解碼**（DXV A/NVDEC，4K／8K 不卡頓）、**ASS 特效字幕精準呈現**（libass）、熱鍵齊全（快進退／逐格／倍速不變調／滑鼠滾輪音量／字幕延遲·字級·位置快捷鍵）、字幕樣式與顏色、畫面調整（亮度／對比／飽和／色相／伽瑪／比例／旋轉）、無損截圖、自動記憶進度、同資料夾自動接續下一集
- **檔案關聯／預設播放器**：在 Windows「預設應用程式」把 Nic Player 設為影片預設後，檔案總管**雙擊影片**會直接開始播放並**以迷你純影片畫面顯示**（沿用目前視窗大小、不會自動縮小；上方 26px 工具條、置頂／恢復／關閉；滑鼠移動不會恢復介面，按恢復鈕回到完整介面，最右側 X 才真正關閉程式）；程式已在執行時再雙擊其他影片，由同一視窗接手，不新增程序。
- **迷你純影片視窗**：拖曳視窗四角可縮到約 **216×122**（原本 1080×660 的 20%），適合放在角落邊做事邊看；小於 1080×700 時自動隱藏標題列與所有功能選單，只留影片，放大回門檻即恢復（**從檔案總管雙擊影片開啟時也會直接使用這個模式，不受目前視窗大小限制；此情況放大視窗不會恢復，按恢復鈕恢復**）。迷你模式頂部保留 26px 細控制條，右上角有 **置頂、恢復（預設 1320×840 完整介面）與最右側 X（真正關閉程式）** 三顆小按鈕；影片從 26px 以下開始，避免被原生影片視窗蓋住。播放中**按住影片畫面可拖曳整個 App**（完整介面與純影片都支援）；短按畫面仍是暫停／繼續、雙擊仍是全螢幕。迷你模式下片尾按鈕、載入提示、通知與拖放遮罩都會自動縮小，不會被裁切；**滑鼠移到影片下方會顯示與全螢幕相同的控制列（進度、音量、字幕、字幕大小）**，播放清單有前後影片時**滑鼠在影片上會顯示左右換片箭頭**。完整介面控制列的全螢幕鈕左側另新增「**迷你模式**」按鈕，一鍵縮成 640×360 純影片。
- **3D 播放與校準（電腦端）**：支援 **紅藍、Half-SBS／Half-TAB、Full-SBS／Full-TAB**；來源可自動偵測或手動指定 **Half／Full SBS/TAB**，並可交換左右眼。新增 **3D 校正面板**（影片下方，調整時仍看得到畫面）：收斂（水平視差）、右眼垂直對齊、縮放（95–105%），以及 **L/R 校正測試圖**。Full 輸出會保留每眼完整寬/高，適合支援 Full-SBS/TAB 的 AR/VR 播放器或寬螢幕；一般 3D TV 請用 Half。裁切／黑邊可能讓 Half/Full 自動判斷失準，可手動指定來源。文字字幕會依 Half/Full 自動產生每眼版本；PGS／DVD 圖形字幕暫不支援。
- **AI 即時字幕（本地、離線）**：播放器按「AI 字幕」即**邊看邊生成翻譯字幕**（原文＋台灣繁中雙語，可切換僅譯文／僅原文）；AI 字幕直接成為標準字幕軌，延遲／字級／顏色調整全部適用；音訊完全不上傳
  - **首次使用 AI 會下載引擎與模型**：對話框會顯示下載進度、可取消；之後會檢查更新。一般影片播放不觸發下載；下載／驗簽失敗時 AI 字幕停用並顯示原因。
- **更新中心**：啟動後背景檢查主程式、AI 元件與下載引擎；有新版本才提示（可稍後）。本 1.1.6 未簽章版不自動安裝主程式更新，但會主動提示新版本；更新視窗右下角「立即下載」直接開啟最新官方 installer；AI 更新仍會驗簽與 hash（GitHub 有新 AI Release 但清單未更新時只提示下載頁，不安裝未簽章檔案），下載引擎會驗證官方 SHA-256。
- **贊助支持**：右上角「請我喝咖啡」會以系統瀏覽器開啟 <https://www.101worlds.com/sponsor.html>。贊助完全自願，不影響任何功能，也不改變 GPL／LGPL 或第三方授權賦予您的權利。
- **播放紀錄**：**投放與電腦播放合併成同一份**（同一部影片一筆進度），依時間記錄且**不限筆數**；每筆可「**投放**」（電視續播）／「**接續播放**」（電腦續播）／「**從頭播放**」，隨時切換不中斷；自動記憶每片上次的字幕設定。**標籤頁**：可用「**＋**」建立自訂標籤頁（按兩下標籤頁可重新命名或刪除），「**全部**」永遠顯示所有紀錄；每筆左側可勾選，一次**批次刪除**或**存入指定標籤頁**（同一筆可加入多個標籤頁）。**更新紀錄**：一鍵檢查所有紀錄是否失效（檔案不存在／連結 404、410 或連不上），列出清單後可**勾選或全選批次刪除**，或逐筆「**替換**」——本機重新選檔、網頁重新貼連結，**進度與播放設定完整保留**（需要登入或擋機器人的網站不會被誤判）。再次開啟同一部已看過的影片時，會詢問要**開新紀錄**或**使用舊進度**；播放紀錄可按標題搜尋（**繁體／簡體中文互通**）。頂部「置頂」右側提供**完整備份匯出／匯入**（**設定頁所有設定＋全部播放紀錄與進度＋標籤頁**；舊版備份檔亦可匯入；**含網站登入 Cookie 時匯出前會警告**）
- **投放遙控**：播放／暫停／跳轉／**電視音量（即時 %、與電視同步）**／停止、即時緩衝狀態顯示；**投放中主控台下方不顯示播放器畫面**（停止投放後恢復）；**投放中滑鼠停在進度條**會顯示該位置的**縮圖預覽**（即時產生、走本機代理快取）
- **進度條縮圖預覽**：電腦端播放（視窗／全螢幕）與**投放**都能預覽；網頁與 YouTube 影片走本機代理時會**只抓最低碼率變體**產生縮圖，出圖更快；已看過的位置直接快取
- **字幕（全自動）**：自動偵測與影片同名的外掛字幕（`影片.srt`／`影片.zh-TW.srt`／`Subs/影片.srt`，支援 srt/vtt/ass/ssa、語言標記、繁中優先），並自動提供內嵌文字字幕；繁體中文自動設為預設軌；**投放中可即時調整字幕大小（50%–250%，Chromecast 立即生效不中斷；燒錄字幕短暫重新緩衝）**；圖形字幕（PGS／DVD）可燒錄；手動指定可覆蓋自動結果
- **音量均衡**：自動壓縮過大／過小的聲音（可選動態均衡或 EBU R128）
- **裝置探索**：自動掃描 Chromecast 與 DLNA 裝置；找不到時可手動輸入 IP
- **續播點**：記住每部影片的觀看進度
- **診斷紀錄**：一鍵匯出除錯紀錄

---

## 四、快速開始

### 直接使用（可攜版）

1. 解壓縮「NicPlayer-可攜版.zip」到任何資料夾（或 USB 隨身碟）。
2. 執行 `Nic Player.exe`。
3. 主控台左上「**無線投放**」→「加入影片」或「加入網頁連結」（也可直接把影片檔拖進視窗播放）；「影片下載」可把網路影片存到電腦。
4. 選好裝置 → 按「開始投放」。

所有資料（設定、播放紀錄、快取）都保存在程式旁的 `data/` 資料夾，不寫入系統登錄檔，移除即乾淨。

### 開發模式

```bash
npm install
npm start
```

Windows 開發測試也可直接雙擊 `啟動測試.bat`。`NIC_DEV_UNLIMITED` 已不再需要：本軟體所有版本都完全免費，沒有免費時數或下載次數閘門，也不會連線授權伺服器。

### 建置可攜版

```bash
npm run build
# 更新 E:/KanKanVideo/Nic Player-win32-x64/（可直接雙擊 exe 測試；預設不壓縮）
npm run build:zip
# 交付時才產生 E:/KanKanVideo/NicPlayer-可攜版.zip
```

### 執行測試

```bash
node test/make-samples.js   # 首次或清理後：產生測試影片素材（data/test/，可隨時重建）
npm test
# 或單獨執行：
node test/e2e-cast.js          # 投放端到端（模擬 Chromecast + DLNA）
node test/e2e-preload.js       # 零中斷預載模式（倒數畫面／下載快取／不誤判）
node test/e2e-manual-screen.js # 手動緩衝電視端畫面（狀態隔離／重鑄／停止恢復影片）
node test/e2e-cast-heartbeat.js # 投放心跳容錯（PONG 延遲不重連／真斷線仍重連）
node test/e2e-3d-p0.js         # 3D P0（Half/Full 來源・Full 輸出・幾何・每眼字幕・測試圖）
node test/e2e-airplay.js       # AirPlay 投放（模擬接收器 + pyatv 輔助程式）
node test/e2e-subtitle.js      # 字幕自動偵測＋即時字級（含燒錄 filter 檢查）
node test/e2e-download.js      # 影片下載（本機來源＋重試／取消；全程不連外網）
npx electron test/e2e-web.js   # 網頁影片偵測（Electron 環境）
```

> `data/test/`（測試影片樣本）與 `data/cache/`（執行快取）都可安全刪除：
> 前者用 `node test/make-samples.js` 重建；後者程式啟動時會自動清理殘留。

---

## 五、完全免費

Nic Player 現在**完全免費**：不需要序號、不需要付費、沒有每日使用時數或下載次數限制，所有功能（4K、ABR、字幕、預載、回看緩衝、音量均衡、最高畫質下載）全部開放。

- 不需要建立帳號，也不會連線授權伺服器或回傳使用量。
- 本軟體仍受第三方元件授權與相關法律規範約束（見「八、第三方元件授權」）。

---

## 六、技術架構

```
src/main/                 主程序（Node / Electron main）
  core/media-server.js    HTTP 媒體伺服器（Range／CORS／HLS 服務／網頁代理＋預讀＋慢速偏好低碼率）
  core/transcoder.js      HLS 轉碼引擎（分段生產者、ABR 多碼率、預載節流、跳轉重啟）
  core/net-probe.js       投放前鏈路偵測（TCP RTT 探測）＋裝置網路歷史
  core/screen-session.js  電視端預載倒數畫面（ffmpeg 預烘焙 HLS，drawtext 動態倒數）
  core/preload-runner.js  預載階段執行器（畫面投影／緩衝目標／下載快取／HLS 預熱）
  core/capabilities.js    裝置相容性判斷（直接播放／封裝轉換／轉碼策略）
  core/discovery.js       裝置探索（mDNS _googlecast._tcp + SSDP/UPnP）
  core/chromecast.js      CastV2 投放控制（含斷線自動重連續播）
  core/airplay.js         AirPlay 控制（pyatv 輔助程式常駐協定、配對、/rate /scrub 控制）
  core/dlna.js            DLNA AVTransport 控制（SOAP）＋進度輪詢
  core/dlna-stream.js     DLNA 即時 MPEG-TS 串流（背壓節流＋copy 快速模式）
  core/web-resolver.js    網頁影片偵測（隱藏瀏覽器＋網路嗅探＋畫面縮圖）
  core/downloader.js      影片下載引擎（yt-dlp＋ffmpeg 本地管線、佇列、進度、引擎更新）
  core/history.js         播放紀錄（合併最近 30 筆、進度續播）
  core/ai-subtitle.js     AI 即時字幕（whisper-server＋llama-server 常駐、滾動生成排程、雙語輸出）
  core/ai-config.js       AI 下載設定（固定 manifest URL／pinned Ed25519 公鑰／allowHosts）
  core/ai-manifest.js     AI manifest 驗簽、版本／expiry／rollback／快取
  core/ai-downloader.js   AI 引擎／模型下載（續傳、鏡像、SHA-256、ZIP、atomic、取消）
  core/mpv.js             播放引擎控制器（mpv 子行程＋JSON IPC、下一集自然排序偵測）
  core/subs.js            字幕轉換與提取（→ WebVTT）
src/renderer/             純黑質感 UI（無框架，原生 DOM）
test/                     測試套件＋模擬裝置（Mock Chromecast／DLNA／限速來源）
resources/bin/            內附 ffmpeg／ffprobe／yt-dlp／mpv（可攜式）
data/ai/                  開發用 AI 引擎與模型；正式 installer 首次使用 AI 時下載到 %LOCALAPPDATA%\Nic Player\ai
```

### 媒體處理流程

```
本地檔案 → ffprobe 分析 → 相容性判斷 ┬ 直接播放（原始檔案＋Range 串流）
                                     ├ 封裝轉換（-c copy → HLS 分段，秒速）
                                     └ 自適應轉碼（NVENC/QSV/x264 → 4 秒分段 ABR）
                                          ↓ 預載到目標存量後才開始投放
投放前 → TCP 鏈路探測 ─┬ 良好 → 一般節奏開播
                        └ 不穩定 → 零中斷預載模式（電視端倒數畫面＋緩衝達標才開播）
網頁連結 → 隱藏瀏覽器載入 → 影片元素＋網路請求嗅探 → 使用者選擇
        → 本機代理（標頭注入＋分段快取＋自適應預讀）→ 來源速度實測
        → 太慢 → 零中斷預載模式（HLS 預熱 或 整段下載至本機快取）→ 投放
```

---

## 七、已知限制

- **AirPlay 配對**：首次投放至 AirPlay 裝置需輸入電視顯示的 PIN 碼（Apple 的 AirPlay 2 規定，無法略過）；完成一次後永久記住。AirPlay 影片音量需用電視遙控器調整（協定限制）。
- **OpenSubtitles 線上下載**：原版提供線上下載字幕；本版支援本機字幕檔與內嵌字幕，線上字幕庫列為後續版本評估項目。
- **DRM 受保護串流**（Netflix／Disney+ 等）無法投放；YouTube 亦因串流簽章保護無法直接取出，建議使用電視內建 App。工具會在偵測結果中明確標示（**影片下載**功能則不受此限，可正常下載 YouTube 等平台）。
- **影片下載**：網站改版可能造成解析失敗，按「檢查更新」更新下載引擎即可修復；Instagram／Facebook 需登入的內容需在「設定 → 影片下載」開啟「讀取瀏覽器 Cookies」；私人／會員限定／已刪除的影片無法下載。
- **DASH（.mpd）** 串流目前僅支援偵測顯示，不支援投放（Chromecast 預設播放器需 Shaka 才能播放 DASH）。
- **DLNA 轉碼模式**採即時串流，跳轉時電視會重新緩衝數秒；Chromecast 不受此限。
- LDAC／Atmos 等特殊音訊會下混為立體聲 AAC（保持最大相容性）。
- 部分老舊電視的 DLNA 實作不支援字幕軌，屬裝置端限制；本工具在 DLNA 轉碼時會將外掛字幕直接燒錄於畫面（可用「字幕大小」即時調整）。
- 電視休眠時不會回應 mDNS 掃描，請開啟電視或使用「手動新增裝置」。
- **投放斷線不一定是緩衝不足**：緩衝到本機只保證「資料已準備好」，若電視棒本身的 Wi-Fi／待機省電在播放中暫時離線（控制埠 8009 也會一起失聯），任何 App 都無法讓畫面在離線期間繼續。本版已加入 30 秒心跳容錯、TCP keepalive、短暫延遲的主動驗證，以及長手動緩衝時的電視端「手動緩衝中」畫面；若仍頻繁斷線，請優先改用 5GHz／有線網路、以原廠電源供應器供電、關閉電視棒的待機／螢幕保護，並在路由器為電視保留固定 IP。

---

## 八、第三方元件授權

本產品內含之第三方元件，**就著作權授權而言皆允許商業使用**，不需要向開源作者申請授權或支付權利金；但各授權仍有義務（保留版權標註、附授權全文、GPL／LGPL 之原始碼提供）。**專利授權、平台協議與商標授權不在此列**，商業散布前請另行評估（例如 H.264／H.265／AAC 專利、AirPlay／Google Cast 協議與商標）。主要清單、授權全文（含 NVIDIA EULA 與 PyInstaller 例外）與第三方原始碼要約隨附於 `docs/licenses/`，應用程式「設定 → 版權聲明」也可查看。

- **FFmpeg／FFprobe**（GPL-3.0；BtbN 建置，未啟用 nonfree）：以**獨立執行檔**形式呼叫（未修改、未與本產品程式連結）。依 GPL 條款隨附授權全文與原始碼取得方式；自取得本軟體起三年內可透過 <https://www.101worlds.com/> 客服索取對應原始碼（建置來源：<https://github.com/BtbN/FFmpeg-Builds>）。
- **mpv**（GPL-2.0+；獨立執行檔，未修改未連結）：播放引擎。來源：<https://github.com/mpv-player/mpv>（Windows 建置：<https://github.com/shinchiro/mpv-winbuild-cmake>）；原始碼取得方式同上。
- **python-zeroconf**（LGPL-2.1+；隨 AirPlay 輔助程式散布）：隨附授權全文與原始碼取得方式（<https://github.com/python-zeroconf/python-zeroconf>）。
- **第三方原始碼要約**：完整書面要約、FFmpeg／mpv 實際 build 版本與已啟用 libraries 見 `docs/licenses/SOURCE-OFFER.md`（GitHub：<https://github.com/nickyvan101/nic-player-ai/blob/main/docs/licenses/SOURCE-OFFER.md>）。
- **Node.js 子依賴**：`fast-xml-parser` 的 `@nodable/entities`、`anynum`、`fast-xml-builder`、`is-unsafe`、`path-expression-matcher`、`xml-naming` 皆為 MIT；著作權行與全文見 `docs/licenses/NODE-SUBDEPS-NOTICES.txt`。
- **yt-dlp**（Unlicense，公眾領域）：影片下載引擎，獨立執行檔。
- **Whisper large-v3 模型權重**（OpenAI，**Apache-2.0**；本產品使用 ggerganov/whisper.cpp 的 ggml 轉檔；該轉檔 repo 的 MIT metadata 與 OpenAI weights 的 Apache-2.0 有標示差異，為避免衝突以 Apache-2.0 為主）／**Whisper large-v3-turbo**（OpenAI，**MIT**）／**whisper.cpp**（MIT）／**llama.cpp/ggml**（MIT，含 LLVM OpenMP 例外條款授權檔）／**Silero VAD**（MIT）。
- **Qwen3-4B-Instruct-2507**（Alibaba，Apache-2.0）：字幕翻譯模型（依 Apache-2.0 保留授權聲明）。
- **SDL2**（zlib）／**LLVM OpenMP 執行期**（Apache-2.0 with LLVM Exception）／**libffi**（MIT）／**Google Material Icons（部分圖示）**（Apache-2.0）。
- **NVIDIA CUDA 執行期函式庫**（cudart／cuBLAS 等 DLL；**非開源**）：依 NVIDIA CUDA Toolkit EULA「可散布檔案清單」隨應用程式免費散布，**不是開源授權**；EULA 全文見 `docs/licenses/NVIDIA-CUDA-EULA.txt`。
- **Microsoft d3dcompiler_43.dll（DirectX）／VC++ 執行期**：原廠可散布元件，**非開源**；聲明與官方連結見 `docs/licenses/MICROSOFT-REDISTRIBUTABLES.txt`。
- **Electron**（MIT）：含 Chromium 完整元件聲明（程式資料夾 `LICENSES.chromium.html`）。
- **Node.js 執行期套件**：koffi（MIT）、castv2／castv2-client（MIT）、multicast-dns（MIT）、fast-xml-parser（MIT）、protobufjs（BSD-3）、long（Apache-2.0）等。
- **AirPlay 輔助程式（PyInstaller 凍結）**：pyatv（MIT）、Python（PSF-2.0）、aiohttp 等（Apache-2.0）、cryptography／OpenSSL（Apache-2.0）、certifi（MPL-2.0）、protobuf（BSD-3）、miniaudio（公眾領域）等；PyInstaller bootloader 例外全文見 `docs/licenses/PyInstaller-COPYING.txt`，逐項清單見 `docs/licenses/PYTHON-NOTICES.txt`。

---

## 九、版本

v1.1.6 — 更新視窗立即下載：主程式有新版時，右下角由「稍後」改為「立即下載」，直接連到最新版本官方 installer；只有 AI／yt-dlp 更新時仍顯示「稍後」。沿用 1.1.5 迷你模式真正關閉鈕與備份／續播補強。
v1.1.5 — 迷你模式真正關閉鈕：右上角新增最右側 X，會正常結束程式；恢復鈕改用獨立圖示。備份／續播補強：history 保存手動字幕路徑並隨備份還原；網頁開播後 15 秒內失敗仍可 pageUrl 重試；切換影片時舊 session 不覆寫新進度；還原後保留原播放紀錄標題。
v1.1.4 — 多開播放紀錄同步：多個 Nic Player 共用同一份播放紀錄、進度、字幕記憶與標籤頁；舊 instances 歷史首次啟動自動併入 base；history 以檔案鎖＋重載＋watcher 同步；本機續播以共用進度為準；播放進度約每 3 秒同步。
v1.1.3 — 備份還原與播放設定強化：網頁紀錄的直接串流 URL 失效時，會用 pageUrl／Referer 重新解析並接續播放（含長簽章 URL 64 KiB）；每部影片的 AI／YouTube CC／無字幕選擇會自動沿用；從頭播放會重置舊進度；修正上一部 AI 字幕帶到下一部、web AI 設定未回傳與頁面重試進度倒退。
v1.1.2 — 操作與交付強化：播放／投放中加入任何影片或網頁只排入目前項目後方，不中斷、不在播放器自動開片；投放中隱藏播放器區塊；設定頁新增單一／多開播放器；多開實例使用獨立 profile／history／library／cache；修正 JSON 讀取失敗誤搬檔、媒體 token 記錄、隱藏網頁權限與字幕 URL 邊界；hero 圖片移除版本號。
v1.1.1 — 贊助連結與授權文件：右上角新增「請我喝咖啡」外部連結；補齊 GPL／LGPL 原始碼要約、Node 子依賴 notices 與 Whisper large-v3 授權標示；installer 內的 README／授權文件與目前 source 同步。
v1.1.0 — 更新與安裝體驗：可直接覆蓋安裝；解除安裝時詢問保留 AI 引擎／模型與下載引擎；主程式、AI 元件與下載引擎更新集中提示；GitHub AI Release 未進入簽章清單時只提示下載頁；移除公開原始碼快照。
v1.0.0 — 完全免費：移除序號、使用時數、下載次數、付費方案與授權伺服器連線；所有功能免費開放。安裝檔與第三方授權文件隨 GitHub Release 提供。
