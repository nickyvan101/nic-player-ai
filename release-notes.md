# Nic Player 1.1.0 — 更新與安裝體驗

- 發佈日期：2026-11-01
- 版本：1.1.0（Windows x64）
- 安裝檔：`NicPlayer-Setup-1.1.0-x64.exe`
- 大小：276,664,690 bytes
- SHA-256：`5e0882c9e790718868b43b5da1a9c6c31ba2c9bca4ac24132d3dae6e895c68b2`
- 簽章：NotSigned（未簽章；SmartScreen 可能顯示「未知的發行者」）
- EULA／PRIVACY：1.1.0／2026-11-01

## 本次更新

- **可直接覆蓋安裝**：不必先移除舊版；設定、播放紀錄、AI 引擎／模型與下載引擎（yt-dlp）會保留。
- **解除安裝詢問**：移除程式時先詢問是否保留 AI 引擎／模型與下載引擎；選「是」保留，選「否」才刪除。覆蓋安裝的更新流程不會詢問，也不會刪除資料。
- **更新中心**：主程式啟動時主動檢查 GitHub `app-*`；AI 啟動時刷新簽章 manifest。主程式未簽章時只提示並提供官方下載頁；AI 有可下載版本時可一鍵下載。
- **AI Release 提示**：GitHub 先出現 `ai-*` Release、但簽章 manifest 尚未更新時，只提示並提供下載頁，不會直接安裝未經簽章驗證的 GitHub 檔案。
- **安全性**：GitHub Release 不再提供原始碼壓縮檔；repo 與 Release 都不含主程式原始碼，原始碼依 GPL／LGPL 由客服索取。
- **授權協議**：EULA／PRIVACY 更新為 1.1.0，新增更新、AI 驗簽與解除安裝保留條款。

## 安裝與升級

- 支援 Windows 10 22H2／Windows 11 x64。
- 可直接下載本版覆蓋安裝；舊版 1.0.0 下載連結已移除。
- 未簽章版本不自動下載或安裝主程式更新，只會提示新版本並開啟下載頁。
- 下載後請核對上方 SHA-256。

## 驗證

- 完整測試：43／43 全通過。
- `npm audit --omit=dev`：0 vulnerabilities。
- Installer FileVersion／ProductVersion：1.1.0；NotSigned。
- Installer 內 `docs/EULA.txt` 與 `build/EULA.txt` SHA-256 一致（`c4e0aebc498821e43fd2a09249a2cb0c3b4e25293e785f2ae3430be881de4c2b`）。
- App 內版本 1.1.0；不含 `license.js`／`quota-integrity.js`，renderer 沒有序號／授權 UI。

## 授權文件

- EULA：1.1.0（2026-11-01，完全免費）
- 隱私政策：1.1.0（2026-11-01）
- 第三方元件授權：`NicPlayer-ThirdPartyNotices-1.1.0.zip`
- 原始碼：依 GPL／LGPL 要求可透過客服索取，**不公開上傳 Nic Player 原始碼**；完整書面要約與 FFmpeg／mpv build 資訊見 `docs/licenses/SOURCE-OFFER.md`。

## 已知限制

- 未簽章 installer，Windows SmartScreen 可能警示。
- 本次未做 VM 安裝／覆蓋卸載 Gate 與真機 TV／3D 重測。
- AI 引擎／VAD 仍為 [`ai-1.0.0`](https://github.com/nickyvan101/nic-player-ai/releases/tag/ai-1.0.0)；大型 Whisper／Qwen 模型由 Hugging Face 官方來源下載。
- 影音編解碼專利、AirPlay／Google Cast／DLNA 協議與商標、YouTube／Bilibili 條款仍屬法律風險。
