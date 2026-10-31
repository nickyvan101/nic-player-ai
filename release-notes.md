# Nic Player 1.0.0 — 完全免費

- 發佈日期：2026-11-01
- 版本：1.0.0（Windows x64）
- 安裝檔：`NicPlayer-Setup-1.0.0-x64.exe`
- 大小：276663311 bytes
- SHA-256：`d8a6c313c107b3a055d017638c9c544acd0ccb0c23e7a626e4e6d160f4ca0eb0`
- 簽章：NotSigned（未簽章；SmartScreen 可能顯示「未知的發行者」）

## 完全免費

- 移除序號驗證、每日使用時數、下載次數、付費方案與授權伺服器連線。
- 移除 App 內的序號／方案視窗、額度徽章與限額提示。
- 所有功能免費開放：4K、ABR、字幕、預載、回看緩衝、音量均衡、最高畫質下載。
- 不需要帳號；不會上傳使用量。
- 本程式不使用 `license.json`／`quota.json`。

## 安裝與升級

- 支援 Windows 10 22H2／Windows 11 x64。
- 可直接覆蓋安裝；設定、播放紀錄、AI 模型與下載引擎會保留。
- 未簽章版本不自動安裝主程式更新，只會提示新版本並提供下載頁。
- 主程式 1.0.0；AI 引擎／VAD 見 [`ai-1.0.0`](https://github.com/nickyvan101/nic-player-ai/releases/tag/ai-1.0.0)（AI 元件）。

## 驗證

- 完整測試：43／43 全通過（含投放、HDR／3D、下載、AI、Electron UI 與「完全免費」檢查）。
- `npm audit --omit=dev`：0 vulnerabilities。
- 安裝包內 `docs/EULA.txt` 與 `build/EULA.txt` SHA-256 一致（1.0.0／2026-11-01）。
- App 內版本 1.0.0；已確認不含 `license.js`／`quota-integrity.js`，renderer 沒有序號／授權 UI。

## 授權文件

- EULA：1.0.0（2026-11-01，完全免費）
- 隱私政策：1.0.0（2026-11-01）
- 第三方元件授權：`NicPlayer-ThirdPartyNotices-1.0.0.zip`
- 原始碼：依 GPL／LGPL 要求可透過客服索取，不公開上傳 GitHub Releases。

## 已知限制

- 未簽章 installer，Windows SmartScreen 可能警示。
- 本次未做 VM 安裝／覆蓋卸載 Gate 與真機 TV／3D 重測。
- AI 引擎／VAD 已恢復於 [`ai-1.0.0`](https://github.com/nickyvan101/nic-player-ai/releases/tag/ai-1.0.0)（AI 元件）；大型 Whisper／Qwen 模型仍由 Hugging Face 官方來源下載。
- 影音編解碼專利、AirPlay／Google Cast／DLNA 協議與商標、YouTube／Bilibili 條款仍屬法律風險，與免費與否無關。
