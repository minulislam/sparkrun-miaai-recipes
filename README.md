# MiaAI-Lab DGX Spark Recipes for sparkrun

Ported from [github.com/MiaAI-Lab](https://github.com/MiaAI-Lab) — inference recipes for NVIDIA DGX Spark clusters using sparkrun.

## Setup

These recipes are stored in `~/.config/sparkrun/recipes/miaai-lab/`. sparkrun auto-discovers recipes in this directory.

If sparkrun is not yet installed:

```bash
uvx sparkrun setup install
sparkrun setup wizard
```

## Recipes (27 total)

### Single-node (TP=1 / 1 GPU)

| Recipe file | Model | Runtime | Quant | Context | Notes |
|---|---|---|---|---|---|
| `qwen3.8-flash-next-nvfp4-tp1.yaml` | drowzeys/keys-Qwen3.8-flash-next-ablit-Mia-Single-Spark-only | vLLM | NVFP4 | 256k | **Abliterated** (gated Keys checkpoint), MTP draft, 256k ctx |
| `deepseek-v4-flash-0731-tp1.yaml` | 0xSero/deepseek-v4-flash-0731-spark | ExllamaV3 | EXL3 | 384k | **Abliterated** (ABLATE=1 refusal projection layers 10-42) |
| `qwen3.6-27b-nvfp4-dflash-tp1.yaml` | nvidia/Qwen3.6-27B-NVFP4 | vLLM | NVFP4 | 256k | DFlash speculative decoding |
| `qwen3.6-27b-nvfp4-tp1.yaml` | nvidia/Qwen3.6-27B-NVFP4 | vLLM | NVFP4 | 256k | vLLM nightly aarch64 |
| `qwen3.6-35b-a3b-nvfp4-tp1.yaml` | unsloth/Qwen3.6-35B-A3B-NVFP4 | vLLM | NVFP4 | 256k | — |
| `qwen3.6-35b-a3b-nvfp4-unofficial-tp1.yaml` | unsloth/Qwen3.6-35B-A3B-NVFP4 | vLLM | NVFP4 | 256k | b12x linear attention recipe |
| `qwen3.6-35b-a3b-ud-q8_k_xl-tp1.yaml` | Local GGUF | llama-cpp | Q8_K_XL | — | **Requires local GGUF weights** |
| `qwen3.8-27b-nvfp4-tp1.yaml` | unsloth/Qwen3.8-27B-NVFP4 | vLLM | NVFP4 | 256k | RTX 6000 PRO variant |
| `qwen3.8-27b-nvfp4-tp1-alt.yaml` | RadixArk/Qwen3.8-27B-NVFP4 | vLLM | NVFP4 | 256k | RTX 5090 variant |
| `ling-3.0-flash-int4-tp1-sglang.yaml` | inclusionAI/Ling-3.0-flash-int4 | SGLang | INT4 | — | DSpark speculative decoding |
| `ornith-1.5-35b-a3b-nvfp4-tp1.yaml` | spark-ai/Ornith-1.5-35B-A3B-NVFP4 | vLLM | NVFP4 | 256k | b12x, in-checkpoint MTP |
| `gemma-4-31b-it-nvfp4-tp1.yaml` | nvidia/Gemma-4-31B-IT-NVFP4 | vLLM | NVFP4 | — | MTP, tool calling, thinking |
| `gemma-4-26b-a4b-nvfp4-tp1.yaml` | nvidia/Gemma-4-26B-A4B-NVFP4 | vLLM | NVFP4 | — | Concurrency testing |
| `nemotron-labs-3-puzzle-75b-nvfp4-tp1.yaml` | nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4 | vLLM | NVFP4 | 256k | Hybrid MoE (Mamba+MoE+Attention) |
| `nemotron-3.5-lightning-30b-a3b-nvfp4-tp1-sglang.yaml` | nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4 | SGLang | NVFP4 | 256k | DSpark, RTX 5090/6000 PRO |
| `muse-glimmer-30b-nvfp4-tp1.yaml` | RedHatAI/Muse-Glimmer-30B-NVFP4 | vLLM | NVFP4 | 256k | W4A4 variant |
| `laguna-s-2.1-nvfp4-tp1.yaml` | poolside/Laguna-S-2.1-NVFP4 | vLLM | NVFP4 | 256k | DFlash speculative decoding |

### Multi-node (TP=N / N GPUs)

| Recipe file | Model | Runtime | Nodes | Quant | Context | Notes |
|---|---|---|---|---|---|---|
| `glm-5.3-flash-exl3-tp2.yaml` | bullerwins/GLM-5.3-Flash-exl3-4bpw-ablit | vLLM | 2 | EXL3 | 850k | **Abliterated** (GLM53_MODEL_PRESET=abliterated, ABLIT=1), Ray TP=2 |
| `glm-5.3-flash-nvfp4-tp2.yaml` | dealignai/GLM-5.3-Flash-UNCENSORED-NVFP4 | vLLM | 2 | NVFP4 | 262k | **Abliterated** (UNCENSORED NVFP4, ABLIT=1), Ray TP=2 |
| `qwen3.8-flash-next-nvfp4-tp2-sglang.yaml` | drowzeys/keys-Qwen3.8-Flash-Next-NVFP4-dual-ablit-house-qsa-L3-47 | SGLang | 2 | NVFP4 | 256k | **Abliterated** (gated Keys checkpoint), SGLang speculative |
| `qwen3.8-27b-nvfp4-tp1-sglang.yaml` | RadixArk/Qwen3.8-27B-NVFP4 | SGLang | 1 | NVFP4 | 256k | DFlash, 8 concurrent |
| `deepseek-v4-flash-vision-exp-tp2.yaml` | drowzeys/keys-DeepSeekV4Flash-Vision-EXP-ablit | vLLM | 2 | NVFP4 | 1M | **Abliterated** (gated Keys checkpoint, ABLITERATED=1), DSpark |
| `deepseek-v4-flash-tp2.yaml` | drowzeys/keys-DeepSeekV4-Flash-GA-0731-Dspark-Abliterated-Anchored-Tensors | vLLM | 2 | FP8 | 1M | **Abliterated** (ABLITERATED=1 MoE), FP8 KV, 1M context |
| `inkling-small-nvfp4-tp2-sglang.yaml` | thinkingmachines/Inkling-Small-NVFP4 | SGLang | 2 | NVFP4 | — | DSpark, fp4_mx_block16 KV |
| `mimo-v2.5-tp2.yaml` | Xiaomi/MiMo-V2.5 | vLLM | 2 | NVFP4-KV | — | Omni MTP1, NVFP4 KV |
| `leanstral-1.5-119b-a6b-tp2.yaml` | mistralai/Leanstral-1.5-119B-A6B | vLLM | 2 | FP8 | 262k | MoE, enforce_eager |
| `hy3-295b-nvfp4-tp2.yaml` | kodelow/Hy3-NVFP4-W4A16 | vLLM | 2 | NVFP4 | — | 295B MoE, tool calling |
| `glm-5.2-nvfp4-aqlm-tp3.yaml` | Mia-AiLab/GLM-5.2-NVFP4-AQLM | vLLM | 3 | AQLM | 380k | Multimodal, 380k ctx |

## Usage

```bash
# List all MiaAI-Lab recipes
sparkrun list miaai

# Show a recipe
sparkrun recipe show qwen3.8-flash-next-nvfp4-tp1

# Validate VRAM requirements
sparkrun recipe vram qwen3.8-flash-next-nvfp4-tp1

# Run on default cluster
sparkrun run qwen3.8-flash-next-nvfp4-tp1 --no-follow

# Run on specific cluster
sparkrun run qwen3.8-flash-next-nvfp4-tp1 --cluster mylab --no-follow

# Multi-node
sparkrun run deepseek-v4-flash-vision-exp-tp2 --cluster mylab --tp 2 --no-follow
sparkrun run glm-5.2-nvfp4-aqlm-tp3 --cluster mylab --tp 3 --no-follow

# Check status
sparkrun cluster status

# View logs
sparkrun logs qwen3.8-flash-next-nvfp4-tp1

# Stop
sparkrun stop qwen3.8-flash-next-nvfp4-tp1
```

## Model Access

Some models (marked 🔐) require HuggingFace authentication:

```bash
export HF_TOKEN=hf_xxxxxxxxxxxxxxxxxxxx
sparkrun run qwen3.8-flash-next-nvfp4-tp1 --no-follow
```

## Source Repositories

These recipes were created by inspecting [github.com/MiaAI-Lab](https://github.com/MiaAI-Lab) and porting their start.sh launch scripts to sparkrun YAML format.
