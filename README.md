# ComfyUI Z-Image I2L (Image to LoRA)

![License](https://img.shields.io/badge/License-Apache%202.0-green)

ComfyUI custom nodes for Z-Image Image-to-LoRA generation. Generate personalized LoRA weights from reference images using [DiffSynth-Studio](https://github.com/modelscope/DiffSynth-Studio)'s Z-Image pipeline.

## ✨ Features

- **Image to LoRA**: Generate LoRA weights directly from reference images
- **No Training Required**: Instant LoRA generation without traditional fine-tuning
- **ComfyUI Integration**: Seamless workflow integration with standard LoRA nodes

## 🛠️ Installation

1. Clone this repository into your ComfyUI custom nodes folder:

```bash
cd ComfyUI/custom_nodes
git clone https://github.com/HM-RunningHub/ComfyUI_RH_ZImageI2L.git
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

## 📦 Model Downloads

Models will be automatically downloaded from ModelScope on first run and cached locally.

### Required Models

| Model | Description | Files |
|-------|-------------|-------|
| [Tongyi-MAI/Z-Image](https://modelscope.cn/models/Tongyi-MAI/Z-Image) | Base transformer | `transformer/*.safetensors` |
| [Tongyi-MAI/Z-Image-Turbo](https://modelscope.cn/models/Tongyi-MAI/Z-Image-Turbo) | Text encoder, VAE & Tokenizer | `text_encoder/*.safetensors`, `vae/`, `tokenizer/` |
| [DiffSynth-Studio/General-Image-Encoders](https://modelscope.cn/models/DiffSynth-Studio/General-Image-Encoders) | Image encoders | `SigLIP2-G384/`, `DINOv3-7B/` |
| [DiffSynth-Studio/Z-Image-i2L](https://modelscope.cn/models/DiffSynth-Studio/Z-Image-i2L) | Image to LoRA model | `model.safetensors` |

### Model Cache Path

Models are automatically downloaded and cached in the **ModelScope cache directory**:

| OS | Default Cache Path |
|----|-------------------|
| Linux | `~/.cache/modelscope/hub/` |
| Windows | `C:\Users\<username>\.cache\modelscope\hub\` |
| macOS | `~/.cache/modelscope/hub/` |

The directory structure after download:

```
~/.cache/modelscope/hub/
├── Tongyi-MAI/
│   ├── Z-Image/
│   │   └── transformer/*.safetensors
│   └── Z-Image-Turbo/
│       ├── text_encoder/*.safetensors
│       ├── vae/diffusion_pytorch_model.safetensors
│       └── tokenizer/
└── DiffSynth-Studio/
    ├── General-Image-Encoders/
    │   ├── SigLIP2-G384/model.safetensors
    │   └── DINOv3-7B/model.safetensors
    └── Z-Image-i2L/
        └── model.safetensors
```

### Custom Cache Directory

You can customize the cache directory by setting the `MODELSCOPE_CACHE` environment variable:

```bash
# Linux/macOS
export MODELSCOPE_CACHE=/path/to/your/cache

# Windows (PowerShell)
$env:MODELSCOPE_CACHE = "D:\models\modelscope"

# Windows (CMD)
set MODELSCOPE_CACHE=D:\models\modelscope
```

## 🚀 Usage

### Nodes

| Node | Description |
|------|-------------|
| **ZImageI2L Loader** | Load the Z-Image I2L pipeline |
| **ZImageI2L LoRA Generator** | Generate LoRA from input images |
| **ZImageI2L Saver** | Save generated LoRA to output folder |

### Basic Workflow

1. Add **ZImageI2L Loader** to load the pipeline
2. Connect your reference images to **ZImageI2L LoRA Generator**
3. Use **ZImageI2L Saver** to save the generated LoRA
4. Use the generated LoRA with any standard LoRA loader node

## 📝 Parameters

### ZImageI2L LoRA Generator

| Parameter | Type | Description |
|-----------|------|-------------|
| `pipeline` | RH_ZImageI2LPipeline | Pipeline from Loader node |
| `training_images` | IMAGE | Reference images for LoRA generation |
| `seed` | INT | Random seed for reproducibility |

## ⚠️ Requirements

- **VRAM**: 24GB+ recommended (tested on RTX 4090)
- **Python**: 3.10+
- **ComfyUI**: Latest version

## 🙏 Acknowledgments

- [DiffSynth-Studio](https://github.com/modelscope/DiffSynth-Studio) - Core Z-Image pipeline
- [Tongyi-MAI](https://modelscope.cn/organization/Tongyi-MAI) - Z-Image models

## 📄 License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.
