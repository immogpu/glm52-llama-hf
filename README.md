# GLM-5.2 llama-server HF Runtime Image

Small RunPod image for serving `unsloth/GLM-5.2-GGUF` UD-IQ1_S with `llama-server`.

The image does not include the model. On first container start it downloads the split GGUF shards from Hugging Face into `/workspace/models/glm-5.2`, then starts `llama-server` directly against shard `00001`. It does not merge shards and does not import anything into Ollama.

Use a persistent RunPod volume mounted at `/workspace` so later starts reuse the downloaded shards.

## Image

```text
ghcr.io/immogpu/glm52-llama-hf:latest
```

## Defaults

```text
LLAMA_PORT=11434
GLM52_CTX_SIZE=8192
GLM52_N_PREDICT=16384
GLM52_ENABLE_THINKING=true
GLM52_REASONING_EFFORT=high
```

## RunPod

- Container disk: `300-350 GB`
- Volume mount path: `/workspace`
- Port: `11434/http`
- Optional secret env: `HF_TOKEN`

The server exposes the llama.cpp server API, including OpenAI-compatible routes.
