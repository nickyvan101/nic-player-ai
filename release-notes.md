# Nic Player 1.1.8 — 換電腦還原後可接續播放

## 本次更新

- **換電腦還原後可接續播放**：從另一台電腦匯入備份後，播放紀錄裡的網頁影片或相同路徑的本機影片，按「接續播放」或「從頭播放」時，不再被上一支影片留下的結束事件誤判成載入失敗。
- **立即下載開啟安裝檔**：軟體更新視窗右下角「立即下載」只開啟最新版安裝程式，不會開啟版本列表頁。

## 檔案資訊

- 發佈日期：2026-11-04
- 版本：1.1.8（Windows x64，完全免費）
- 安裝檔：[NicPlayer-Setup-1.1.8-x64.exe](https://github.com/nickyvan101/nic-player-ai/releases/download/app-1.1.8/NicPlayer-Setup-1.1.8-x64.exe)
- 大小：276,881,823 bytes
- SHA-256：`76390a8c9420376cde489dd6e50cb7014a1dd8ba77c20f0674defb39a0c5c178`
- 簽章：NotSigned（未簽章；SmartScreen 可能顯示「未知的發行者」，請選「仍要執行」）
- EULA／PRIVACY：1.1.8／2026-11-04

> 請尊重智慧財產權，僅供個人合法影音播放與備份使用。

## 下載

- [NicPlayer-Setup-1.1.8-x64.exe](https://github.com/nickyvan101/nic-player-ai/releases/download/app-1.1.8/NicPlayer-Setup-1.1.8-x64.exe)
- [SHA-256](https://github.com/nickyvan101/nic-player-ai/releases/download/app-1.1.8/NicPlayer-Setup-1.1.8-x64.exe.sha256)
- [第三方授權文件](https://github.com/nickyvan101/nic-player-ai/releases/download/app-1.1.8/NicPlayer-ThirdPartyNotices-1.1.8.zip)

舊版 1.1.7 的下載連結已移除；請使用 1.1.8。

## 系統需求

- Windows 10 22H2／Windows 11 x64
- 首次使用 AI 字幕需下載 AI 引擎與模型（需要網路與足夠磁碟空間）
- 未簽章版本不會自動安裝主程式更新；AI／下載引擎仍驗簽與 SHA-256

## 驗證

- 完整測試：44／44 通過（`node test/run-all.js`，exit 0）
- Installer FileVersion／ProductVersion：1.1.8；app.asar 版本：1.1.8
- Installer `docs/EULA.txt` 與 `build/EULA.txt` SHA-256 一致：`c7ddcc7132f8976b428113378e512d4b5aeb994aefb065ac8b69cd95721cba54`
- Installer 為 NotSigned
- 安裝時顯示的授權協議為 1.1.8／2026-11-04

## 第三方元件

- FFmpeg／FFprobe：`n8.1.3-16-ge0a878dd70-20261009`（BtbN 建置，GPL-3.0）
- mpv：`v0.41.0-1115-gb2c255c13`（shinchiro 建置，GPL-2.0+；內含 FFmpeg `N-127267-gef305e32e`）
- 完整授權、原始碼要約與 Node 子依賴 notices 隨 installer 的 `docs/licenses/` 提供；GPL／LGPL 對應源碼可依 `SOURCE-OFFER.md` 向客服書面索取。

## 已知限制

- 未簽章 installer 可能觸發 Windows SmartScreen。
- 「立即下載」只開啟官方 installer，不會自動安裝。
- 只有 AI／yt-dlp 更新時不會顯示「立即下載」。
- 備份還原後，本機影片與手動字幕路徑必須在 B 電腦存在。
- 網頁需要登入、Cookie 失效、Cloudflare 或地區限制時，重新解析仍可能失敗。
- 同一部影片在兩個 Nic Player 同時播放時，進度採最後寫入者勝。
- 這次修正的是上一支影片留下的結束事件。若影片來源本身已失效，重新解析仍可能失敗。尚未用這支安裝檔在另一台電腦重測匯入後的播放。
