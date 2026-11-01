# 第三方元件與授權清單（隨 Nic Player 散布）

版本：1.1.0（2026-11-01）

本產品包含下列第三方元件。**就著作權授權而言，下列開源元件皆允許商業散布**，不需要向開源作者申請授權或支付權利金；但各授權仍有義務（保留版權標註、附授權全文、GPL／LGPL 之原始碼提供），且**專利授權、平台協議與商標授權不在此列**，需另行評估。NVIDIA／Microsoft 等非開源元件另依其原廠 EULA 辦理。

> 本產品為免費散布之軟體；散布之 GPL 元件係以「獨立執行檔」形式隨附（未修改、未與本產品程式碼連結），本產品自身程式碼不受 GPL 傳染。本清單不構成法律意見。

## 一、GPL 元件（獨立執行檔）

| 元件 | 版本 | 授權 | 用途 | 來源 |
|---|---|---|---|---|
| FFmpeg／FFprobe | n8.1.3（BtbN 建置：`--enable-gpl --enable-version3`，未啟用 `--enable-nonfree`） | GPL-3.0 | 轉碼、抽音、剪輯 | 建置：<https://github.com/BtbN/FFmpeg-Builds>／上游：<https://ffmpeg.org> |
| mpv（mpv.exe／mpv.com） | v0.41.0（shinchiro 建置） | GPL-2.0+ | 內建播放引擎 | 上游：<https://github.com/mpv-player/mpv>／建置：<https://github.com/shinchiro/mpv-winbuild-cmake> |

**對應原始碼取得（書面要約）**：上述皆為未修改之官方建置；完整原始碼與建置腳本可自上方來源取得。另自取得本軟體之日起**三年內**，您可透過 <https://www.101worlds.com/> 客服提出書面請求，我們將提供對應原始碼（以下載連結或郵寄媒體方式，酌收媒體與運送成本）。完整要約、實際 build 版本與已啟用 libraries 見 [`SOURCE-OFFER.md`](SOURCE-OFFER.md)。授權全文：`GPL-3.0.txt`、`GPL-2.0.txt`。

**FFmpeg／mpv 建置資訊**：

- FFmpeg：`n8.1.3-16-ge0a878dd70-20261009`，BtbN 建置，`--enable-gpl --enable-version3`；完整 `ffmpeg -buildconf` 清單包含 libx264、libx265、libvpx、libdav1d、libaom、libsvtav1、libvvenc、librav1e、libass、libfreetype、libharfbuzz、libfribidi、libplacebo、libopus、libmp3lame、libvorbis、libtheora、libwebp、libzimg、libzvbi、libbluray、libdvdread、libdvdnav、libssh、libzmq、SDL2、OpenSSL／schannel、Vulkan 等。
- mpv：`v0.41.0-1115-gb2c255c13`（shinchiro 建置），內含 FFmpeg `N-127267-gef305e32e`。
- 這些 binary 內的第三方 libraries 各有其授權與著作權；本清單不逐一重製其全文。若你需要完整的 third-party license bundle 或對應 source，請依 `SOURCE-OFFER.md` 提出請求。

> 注意：GPL 的專利授權只涵蓋該元件的貢獻者專利，**不包含 H.264／H.265／AAC 等影音專利池**；商業散布前請另行評估專利授權。

## 二、LGPL 元件

| 元件 | 版本 | 授權 | 用途 | 來源 |
|---|---|---|---|---|
| python-zeroconf | 0.152.x（凍結時版本） | LGPL-2.1+ | AirPlay 裝置探索（隨輔助程式散布） | <https://github.com/python-zeroconf/python-zeroconf> |

**對應原始碼取得**：zeroconf 為未修改之官方發行版，原始碼見上方；亦可依上述書面要約向本軟體提供者索取。授權全文：`LGPL-2.1.txt`。

## 三、非開源（原廠可散布元件，免費隨附、無需權利金）

| 元件 | 授權 | 說明 | 全文／聲明 |
|---|---|---|---|
| NVIDIA CUDA 執行期函式庫（cudart／cuBLAS／cuBLASLt／nvrtc／nvblas） | NVIDIA CUDA Toolkit EULA「可散布軟體」清單 | 隨 AI 引擎（CUDA 版）散布 | `NVIDIA-CUDA-EULA.txt` |
| Microsoft d3dcompiler_43.dll | Microsoft DirectX 可散布元件 | 隨 mpv 引擎散布 | `MICROSOFT-REDISTRIBUTABLES.txt` |
| Microsoft MSVCP140.dll／VCRUNTIME140.dll／VCRUNTIME140_1.dll／VCOMP140.dll | Microsoft Visual C++ 可散布元件 | 隨 AirPlay 輔助程式與 AI 引擎 pack 散布 | `MICROSOFT-REDISTRIBUTABLES.txt` |

上述元件**不是開源軟體**，而是依原廠 EULA 免費隨附；散布時不得修改、不得單獨以原廠名義散布，並應保留原廠著作權標示。若 EULA 要求附上特定聲明，以各檔案內容為準。

## 四、開源元件（MIT／Apache-2.0／BSD-3／MPL-2.0／zlib／Unlicense／PSF／公眾領域）

### 應用程式框架
| 元件 | 授權 | 說明 |
|---|---|---|
| Electron 44（含 Chromium、Node.js 等元件） | MIT | Chromium 完整元件聲明隨程式附上：程式資料夾內 `LICENSES.chromium.html` |
| Google Material Icons（部分介面圖示） | Apache-2.0 | 圖示視覺樣式取自／改作自 Material Icons，依 Apache-2.0 使用 |

### 多媒體與工具（獨立執行檔）
| 元件 | 授權 | 說明 |
|---|---|---|
| yt-dlp 2026.08.19 | Unlicense（公眾領域） | 影片下載引擎；內含 Python 執行期等依其官方發行授權（PSF 等） |
| SDL2（隨 whisper 建置附帶之 SDL2.dll） | zlib | SDL 函式庫 |

### AI 引擎與模型
| 元件 | 授權 |
|---|---|
| whisper.cpp（含 CPU／CUDA 版引擎） | MIT |
| llama.cpp／ggml（含 CPU／CUDA 版引擎） | MIT |
| Whisper large-v3 模型權重（OpenAI 官方 ggml 檔） | **Apache-2.0**（OpenAI 模型頁標示；本產品使用 ggerganov/whisper.cpp 的 ggml 轉檔。該轉檔 repo 的 metadata 標示 MIT，但那只涵蓋轉檔工具／程式；原始 OpenAI weights 仍以 Apache-2.0 為準，不能只用 MIT 概括） |
| Whisper large-v3-turbo 模型權重 | **MIT**（OpenAI 模型頁標示） |
| Qwen3-4B-Instruct-2507（GGUF 量化：Unsloth） | Apache-2.0（依授權保留聲明；GGUF by Unsloth） |
| Silero VAD（模型） | MIT |
| LLVM OpenMP 執行期（libomp.dll） | Apache-2.0 with LLVM Exception（全文：`LLVM-OpenMP-exception.txt`） |

### AirPlay 輔助程式（PyInstaller 凍結；各元件皆為未修改之官方發行版）
| 元件 | 授權 |
|---|---|
| pyatv 0.18.x | MIT |
| Python 3.13 | PSF-2.0 |
| aiohttp、aiosignal、frozenlist、multidict、propcache、yarl、requests | Apache-2.0 |
| cryptography（雙授權） | Apache-2.0 OR BSD-3-Clause |
| OpenSSL（libcrypto-3.dll／libssl-3.dll） | Apache-2.0 |
| certifi | MPL-2.0（source：<https://github.com/certifi/python-certifi>；source 可自上游取得或依 `SOURCE-OFFER.md` 索取） |
| attrs、charset-normalizer、pydantic、pydantic_core、tabulate、tinytag、ifaddr、cffi、urllib3、libffi | MIT |
| protobuf（Google protobuf runtime） | BSD-3-Clause |
| idna、srptools | BSD-3-Clause |
| chacha20poly1305-reuseable | Apache-2.0 OR BSD-3-Clause |
| miniaudio | 公眾領域（Public Domain／MIT-0） |
| PyInstaller（凍結工具 bootloader） | GPL-2.0-or-later WITH Bootloader-exception（全文：`PyInstaller-COPYING.txt`） |

逐項套件、版本、授權與專案位址另見 `PYTHON-NOTICES.txt`。

### AI 引擎與模型下載包
AI 引擎 zip（`engine-whisper-*`、`engine-llama-*`）內含 `THIRD-PARTY-NOTICES.txt` 與 `licenses/`（MIT、Apache-2.0、LLVM Exception）。CUDA 版另含 NVIDIA CUDA runtime 與 Microsoft VC++ runtime；NVIDIA EULA／Microsoft 聲明全文隨 Nic Player 安裝於 `docs/licenses/`，並另以 `ai-1.0.0` Release 的 `NVIDIA-CUDA-EULA.txt`／`MICROSOFT-REDISTRIBUTABLES.txt` assets 提供。若直接下載引擎 zip，請一併閱讀 zip 內的 third-party notices 與上述 assets；完整授權清單以安裝後的 `docs/licenses/` 為準。

### Node.js 執行期套件（含巢狀依賴）
| 元件 | 授權 |
|---|---|
| koffi、@koromix/koffi-win32-x64 | MIT |
| castv2-client、castv2 | MIT |
| debug、ms、strnum、dns-packet、@leichtgewicht/ip-codec、thunky | MIT |
| fast-xml-parser | MIT |
| @nodable/entities（fast-xml-parser 子依賴） | MIT（© 2026 Nodable；npm 套件未附 LICENSE，notice 見 `NODE-SUBDEPS-NOTICES.txt`） |
| anynum、fast-xml-builder、is-unsafe、xml-naming（fast-xml-parser 子依賴） | MIT（© 2026 Natural Intelligence） |
| path-expression-matcher（fast-xml-builder 子依賴） | MIT（© 2024；上游 LICENSE 未列著作權人姓名） |
| multicast-dns | MIT |
| @types/long、@types/node、undici-types | MIT |
| protobufjs、@protobufjs/*（aspromise、base64、codegen、eventemitter、fetch、float、inquire、path、pool、utf8） | BSD-3-Clause |
| long | Apache-2.0 |
| opencc-js（簡→繁台灣用語轉換） | MIT AND Apache-2.0（雙授權二選一） |

## 五、授權全文索引

| 檔案 | 適用元件 |
|---|---|
| `MIT.txt` | MIT 類全部元件（含 libffi、Material Icons 以外之 UI 元件） |
| `Apache-2.0.txt` | Apache-2.0 類全部元件（含 OpenSSL、Qwen、Whisper large-v3、Material Icons） |
| `BSD-3-Clause.txt` | protobufjs／protobuf runtime／idna／srptools |
| `MPL-2.0.txt` | certifi |
| `zlib.txt` | SDL2 |
| `Unlicense.txt` | yt-dlp |
| `PSF-2.0.txt` | Python |
| `GPL-3.0.txt` | FFmpeg／FFprobe |
| `GPL-2.0.txt` | mpv |
| `LGPL-2.1.txt` | python-zeroconf |
| `LLVM-OpenMP-exception.txt` | LLVM OpenMP 執行期（含 Apache-2.0 全文與 LLVM 例外條款） |
| `PyInstaller-COPYING.txt` | PyInstaller（GPL-2.0-or-later WITH Bootloader-exception 全文） |
| `NVIDIA-CUDA-EULA.txt` | NVIDIA CUDA 執行期（非開源） |
| `MICROSOFT-REDISTRIBUTABLES.txt` | Microsoft DirectX／VC++ 可散布元件（非開源） |
| `PYTHON-NOTICES.txt` | AirPlay 輔助程式之 Python 套件逐項清單 |
| `NODE-SUBDEPS-NOTICES.txt` | `fast-xml-parser` 子依賴的 MIT 著作權行與全文 |
| `SOURCE-OFFER.md` | FFmpeg／mpv／python-zeroconf 的 GPL／LGPL 原始碼要約與 build 資訊 |

各元件之完整著作權行（版權標註）另見應用程式「設定 → 版權聲明」清單與上述檔案；Node.js 套件之 LICENSE 檔隨 app.asar 一併散布。
