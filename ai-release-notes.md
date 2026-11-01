# AI 引擎與必要元件 1.0.0

此 Release **不是主程式 installer**；它是 Nic Player AI 字幕功能所需的引擎與語音活動偵測（VAD）元件。

- 主程式最新版：請下載 [`app-1.1.1`](https://github.com/nickyvan101/nic-player-ai/releases/tag/app-1.1.1)（Latest）。
- 大型 Whisper／Qwen 模型**不在這裡**：維持由 Hugging Face 官方來源下載，manifest 已指向官方固定 commit。
- 這些檔案的 SHA-256 與 Nic Player 的簽章 manifest 一致；App 首次使用 AI 時會自動下載、驗簽、解壓。

> 請尊重智慧財產權，僅供個人合法影音播放與備份使用。

## 內容

- `engine-whisper-cpu-1.0.0.zip`
- `engine-whisper-cuda-1.0.0.zip`
- `engine-llama-cpu-1.0.0.zip`
- `engine-llama-cuda-1.0.0.zip`
- `ggml-silero-v5.1.2.bin`

## 授權文件

- 各引擎 zip 內含 `THIRD-PARTY-NOTICES.txt` 與 `licenses/`（MIT、Apache-2.0、LLVM Exception）。
- CUDA 版另含 NVIDIA CUDA runtime 與 Microsoft VC++ runtime；NVIDIA EULA 與 Microsoft 可散布元件聲明另以下列 assets 提供：
  - `NVIDIA-CUDA-EULA.txt`
  - `MICROSOFT-REDISTRIBUTABLES.txt`
- 完整第三方清單以 Nic Player 安裝後的 `docs/licenses/` 為準。

## 模型授權

- **Whisper large-v3**：Apache-2.0（OpenAI 權重；`ggerganov/whisper.cpp` 的 ggml 轉檔 repo metadata 標示 MIT，與 OpenAI weights 的 Apache-2.0 有標示差異；為避免衝突以 Apache-2.0 為主）。
- **Whisper large-v3-turbo**：MIT（OpenAI）。
- **Qwen3-4B-Instruct-2507（GGUF by Unsloth）**：Apache-2.0。
- **Silero VAD**：MIT。

## 注意

- 這是 AI 元件，不是可獨立執行的應用程式。
- 請使用 Nic Player 1.1.1 的 AI 首次下載流程，不要手動覆蓋安裝目錄。
- 檔案較大（合計約 1.2 GB）；CUDA 版需要相容的 NVIDIA 驅動。
