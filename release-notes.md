# Nic Player 1.1.1 — 贊助連結與授權文件

- 發佈日期：2026-11-01
- 版本：1.1.1（Windows x64）
- 安裝檔：`NicPlayer-Setup-1.1.1-x64.exe`
- 大小：276,669,396 bytes
- SHA-256：`f64e28cb605fe9f94e296646aa8aa5a0308fa96e9ec7d6e9de2a8e79cc38523c`
- 簽章：NotSigned（未簽章；SmartScreen 可能顯示「未知的發行者」）
- EULA／PRIVACY：1.1.1／2026-11-01

> 請尊重智慧財產權，僅供個人合法影音播放與備份使用。

## 本次更新

- **贊助連結**：右上角新增「請我喝咖啡」，只以系統瀏覽器開啟 <https://www.101worlds.com/sponsor.html>；不內嵌第三方 SDK。贊助完全自願，不影響任何功能，也不改變 GPL／LGPL 或第三方授權賦予您的權利。
- **授權文件補齊**：installer 內 `docs/licenses/` 現在包含 GPL／LGPL 原始碼要約（`SOURCE-OFFER.md`）與 Node／fast-xml-parser 子依賴 notices（`NODE-SUBDEPS-NOTICES.txt`），修正 1.1.0 installer 文件與 source 不同步的問題。
- **模型授權標示**：Whisper large-v3 統一標示 Apache-2.0（原始 OpenAI weights）；不再以 ggml 轉檔 repo 的 MIT metadata 概括。
- **README／使用說明**：加入智慧財產權聲明與原始碼要約說明；EULA／PRIVACY 版本更新為 1.1.1。
- 播放、投放、AI、下載等行為與 1.1.0 相同，本次沒有功能行為變更（僅新增外部贊助連結）。

## 安裝與升級

- 支援 Windows 10 22H2／Windows 11 x64。
- 可直接下載本版覆蓋安裝；設定、播放紀錄、AI 引擎／模型與下載引擎（yt-dlp）會保留。
- 舊版 `app-1.1.0` 下載連結已移除；請一律使用本 Release 的安裝檔。
- 未簽章版本不自動下載或安裝主程式更新，只會提示新版本並開啟下載頁。
- 下載後請核對上方 SHA-256。

## 驗證

- 完整測試：43／43 全通過（`node test/run-all.js`，exit 0）。
- `npm audit --omit=dev`：0 vulnerabilities。
- Installer FileVersion／ProductVersion：1.1.1；NotSigned。
- Installer 內 `docs/EULA.txt` 與 `build/EULA.txt` SHA-256 一致（`67c60b1937e75f49a97ec591d850d99e1e34d9e552b683898b26dac08d039262`）。
- App 內版本 1.1.1；不含 `license.js`／`quota-integrity.js`，renderer 沒有序號／授權 UI。

## 第三方建置版本

- **FFmpeg／FFprobe**：`n8.1.3-16-ge0a878dd70-20261009`（BtbN 建置，GPL-3.0）
  - 建置庫：<https://github.com/BtbN/FFmpeg-Builds>
- **mpv**：`v0.41.0-1115-gb2c255c13`（shinchiro 建置，GPL-2.0+；內含 FFmpeg `N-127267-gef305e32e`）
  - 建置庫：<https://github.com/shinchiro/mpv-winbuild-cmake>
- **GPL／LGPL 原始碼要約與完整 build 資訊**：`docs/licenses/SOURCE-OFFER.md`（installer 內；repo 亦提供）。

## 授權文件

- EULA：1.1.1（2026-11-01，完全免費）
- 隱私政策：1.1.1（2026-11-01）
- 第三方元件授權：`NicPlayer-ThirdPartyNotices-1.1.1.zip`
- 原始碼：依 GPL／LGPL 要求可透過客服索取，**不公開上傳 Nic Player 原始碼**；完整書面要約與 FFmpeg／mpv build 資訊見 `docs/licenses/SOURCE-OFFER.md`。

## 已知限制

- 未簽章 installer，Windows SmartScreen 可能警示。
- 本次未做 VM 安裝／覆蓋卸載 Gate 與真機 TV／3D 重測。
- AI 引擎／VAD 仍為 [`ai-1.0.0`](https://github.com/nickyvan101/nic-player-ai/releases/tag/ai-1.0.0)；大型 Whisper／Qwen 模型由 Hugging Face 官方來源下載。
- 影音編解碼專利、AirPlay／Google Cast／DLNA 協議與商標、YouTube／Bilibili 條款仍屬法律風險。
