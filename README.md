# kaivoxa-models

The download source for the AI model files used by **Kaivoxa**, a Windows desktop app with an AI companion called Kai.

The Kaivoxa app downloads files from here in the background, so Kai can hear you better and search its memory. Nothing else lives here.

## Why this repo is public

- The installed app has to download models **without anyone logging in**. Files in a private GitHub repo need a login token.
- The app's code repo is private, and its token can't be put inside the app. Anyone could pull a token out of an installed app and use it to read the private code.
- So the models live here, in a separate public repo that holds **only** model files. The app's code stays private.

## What's inside

| What | Where | Original source | Licence |
|---|---|---|---|
| Whisper speech-to-text models (base, small, large-v3-turbo), GGML format | Release assets `whisper__*.bin` | OpenAI Whisper, converted by whisper.cpp: <https://huggingface.co/ggerganov/whisper.cpp> | MIT ([OpenAI](licenses/openai-whisper-MIT.txt), [whisper.cpp](licenses/whisper.cpp-MIT.txt)) |
| multilingual-e5-small (memory search), ONNX int8 | Release assets `Xenova__multilingual-e5-small__*` | intfloat (Microsoft): <https://huggingface.co/intfloat/multilingual-e5-small>, ONNX by <https://huggingface.co/Xenova/multilingual-e5-small> | [MIT](licenses/multilingual-e5-small-MIT.txt) |
| whisper.cpp GPU build for NVIDIA cards (`whisper-server.exe`, `whisper.dll`, `ggml*.dll`) | Release assets `whisper-cuda__*` | <https://github.com/ggml-org/whisper.cpp> release builds | [MIT](licenses/whisper.cpp-MIT.txt) |
| NVIDIA CUDA runtime + cuBLAS (`cudart64_110.dll`, `cublas64_11.dll`, `cublasLt64_11.dll`) | Release assets `whisper-cuda__*` | NVIDIA CUDA 11.8 / cuBLAS 11.11 | [NVIDIA CUDA EULA](licenses/NVIDIA-CUDA-EULA.txt): listed in its Attachment A as redistributable. Shipped unmodified, for use only by Kaivoxa |
| `manifest.json` + `manifest.json.sig` | Repo root and every release | Made by the Kaivoxa author | — |

**Never in this repo:** app code, secrets (keys, tokens, passwords), or any user data.

## How Kaivoxa checks the files

1. Kaivoxa downloads `manifest.json` and its signature `manifest.json.sig`.
2. The signature is checked with an **Ed25519 public key built into the app**. Only the Kaivoxa author has the matching private key, and it never goes into any repo. A manifest that was changed or faked is rejected.
3. The manifest lists every file with its exact size and **SHA256 hash**. After each download, Kaivoxa hashes the file. If even one byte is different, the file is deleted and not used.

So even if someone swapped a file here or on a mirror, Kai would refuse it and keep using the model it already has.

## Privacy

Downloads go one way only: **your PC ← this repo** (or a listed mirror such as Hugging Face). Kaivoxa uploads nothing about you to get the files: no account, no ID and no usage data. GitHub (or Hugging Face) sees an ordinary download request, as with any download.

## Rule

This repo only ever contains model files, their licences, and the signed manifest. Nothing else.
