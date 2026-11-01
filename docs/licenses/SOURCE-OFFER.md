# Nic Player — 第三方原始碼取得要約（GPL／LGPL）

本文件只處理 **Nic Player 所隨附的第三方 GPL／LGPL 元件**，不是 Nic Player 自身原始碼的公開授權。Nic Player 自身原始碼仍不公開；本文件也不改變 Nic Player 的 EULA。

## 一、GPL 元件

| 元件 | 本產品使用版本／建置 | 授權 | 上游來源 |
|---|---|---|---|
| FFmpeg／FFprobe | `n8.1.3-16-ge0a878dd70-20261009`，BtbN 建置，`--enable-gpl --enable-version3` | GPL-3.0 | <https://github.com/BtbN/FFmpeg-Builds>、<https://ffmpeg.org> |
| mpv（mpv.exe／mpv.com） | `v0.41.0-1115-gb2c255c13`，shinchiro 建置；內含 FFmpeg `N-127267-gef305e32e` | GPL-2.0+ | <https://github.com/mpv-player/mpv>、<https://github.com/shinchiro/mpv-winbuild-cmake> |

上述 binary 皆為未修改之官方建置。FFmpeg 建置啟用的 libraries 包含（節錄，完整清單以 binary 的 `ffmpeg -buildconf` 為準）：libx264、libx265、libvpx、libdav1d、libaom、libsvtav1、libvvenc、librav1e、libass、libfreetype、libharfbuzz、libfribidi、libplacebo、libopus、libmp3lame、libvorbis、libtheora、libwebp、libzimg、libzvbi、libbluray、libdvdread、libdvdnav、libssh、libzmq、SDL2、OpenSSL/schannel、Vulkan 等。這些 libraries 的授權與著作權屬各自作者；完整 notice 與 build scripts 以其建置來源為準。

## 二、LGPL 元件

| 元件 | 本產品使用方式 | 授權 | 上游來源 |
|---|---|---|---|
| python-zeroconf 0.152.x | 以 PyInstaller 凍結於 AirPlay 輔助程式，未修改 | LGPL-2.1-or-later | <https://github.com/python-zeroconf/python-zeroconf> |

## 三、書面要約

自您取得本軟體之日起 **三年內**，您可以透過 <https://www.101worlds.com/> 客服提出書面請求，索取上述元件對應您所取得之 binary 的 **Corresponding Source**（含建置／安裝 scripts，若該授權要求）。我們會在合理期間內以下載連結或郵寄媒體方式提供；若以郵寄方式，得酌收媒體與運送成本。

請在請求中註明：

- Nic Player 版本（例如 1.1.1）
- 元件名稱（FFmpeg／mpv／python-zeroconf）
- 您的聯絡方式

## 四、重要限制

- 本要約**不包含** Nic Player 自身原始碼、私人金鑰、簽章私鑰或內部管理文件。
- GPL／LGPL 元件的授權全文隨程式提供於 `docs/licenses/`；本文件不取代各該授權條款。
- FFmpeg／mpv 的 binary 另含許多第三方 libraries；其個別授權與 source 取得方式以各上游建置與授權為準。若你需要完整的第三方授權 bundle，請在請求中一併註明。
- 本文件是工程／合規文件，不是法律意見；實際散布前仍應由律師確認 GPLv3 §6（尤其網路下載的 corresponding source）與 LGPL relink 要求。
