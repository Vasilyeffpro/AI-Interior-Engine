# 🏛️ Leonards AI Interior Engine

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![ComfyUI](https://img.shields.io/badge/engine-ComfyUI-orange.svg)
![VRAM](https://img.shields.io/badge/VRAM-12GB%20Optimized-green.svg)
![Status](https://img.shields.io/badge/Status-Production--Ready-brightgreen.svg)

**Advanced SDXL Workflow for High-End Architectural Visualization & Interior Design.**

![Workflow Preview](assets/workflow-preview.jpg)

---

## ✨ Features

- **SDXL Base Model** — High-quality generation powered by Stable Diffusion XL
- **Dual ControlNet Integration** — Depth + Canny for precise architectural line preservation
- **Two-Stage Upscale Pipeline** — 4x-UltraSharp model for crisp, detailed outputs
- **VRAM Optimized** — Runs smoothly on 12GB GPUs with Tiled VAE and FreeU
- **Artifact-Free Backgrounds** — Fixed "brush stroke" artifacts on distant elements (e.g., outdoor scenery)

## 🖼️ Results

| Input Sketch | Output |
|--------------|--------|
| ![Input](assets/input-example.png) | ![Output](assets/output-example.png) |

## 📋 Requirements

| Component | Specification |
|-----------|---------------|
| **GPU** | NVIDIA with 12GB+ VRAM |
| **Base Model** | SDXL 1.0 |
| **ComfyUI** | Latest version |
| **Custom Nodes** | See [requirements](#custom-nodes) |

## 🚀 Quick Start

### 1. Install Dependencies

```bash
# Clone ComfyUI custom nodes
cd ComfyUI/custom_nodes

# Install ControlNet
git clone https://github.com/Fannovel16/ComfyUI-ControlNet.git

# Install FreeU
git clone https://github.com/AInseven/ComfyUI-FreeU.git
```

### 2. Download Models

Place the following models in your `ComfyUI/models/` directory:

```
models/
├── checkpoints/
│   └── sd_xl_base_1.0.safetensors
├── controlnet/
│   ├── control-lora-canny-rank128.safetensors
│   └── control-lora-depth-rank128.safetensors
├── upscale/
│   └── 4x-UltraSharp.pth
└── vae/
    └── sdxl_vae.safetensors
```

### 3. Load Workflow

1. Open ComfyUI
2. Drag & drop `workflows/premium_interior_workflow.json` into the interface
3. Load your input image (depth/canny maps auto-generated)
4. Click **Queue Prompt**

## ⚙️ Workflow Architecture

```
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│   Input Image   │────▶│  ControlNet      │────▶│   SDXL Base     │
│   (Reference)   │     │  Depth + Canny   │     │   Generation    │
└─────────────────┘     └──────────────────┘     └────────┬────────┘
                                                          │
                                                          ▼
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│   Final Output  │◀────│   4x-UltraSharp  │◀────│   FreeU +       │
│   (4K Ready)    │     │   2-Stage Upscale│     │   Tiled VAE     │
└─────────────────┘     └──────────────────┘     └─────────────────┘
```

## 🎛️ Configuration

### Recommended Settings

| Parameter | Value |
|-----------|-------|
| **Resolution** | 1024×1024 (base), 4096×4096 (upscaled) |
| **Steps** | 30–40 |
| **CFG Scale** | 5.0–7.0 |
| **Sampler** | DPM++ 2M Karras |
| **ControlNet Strength** | 0.6–0.8 |

### VRAM Optimization

For 12GB GPUs, ensure the following nodes are enabled:

- ✅ **Tiled VAE** — Prevents OOM during decode
- ✅ **FreeU** — Enhances details without extra VRAM cost

## 🐛 Known Issues & Fixes

### Background Artifacts

**Problem:** Brush stroke patterns on distant backgrounds (e.g., windows, outdoor scenery)

**Solution:** This workflow includes a dedicated fix using:
- Adjusted denoise scheduling
- Depth-aware masking
- Refined ControlNet weighting

## 📁 Repository Structure

```
.
├── workflows/
│   ├── premium_interior_workflow.json    # Main workflow file
│   └── advanced_settings.json            # Optional advanced config
├── assets/
│   ├── workflow-preview.jpg              # Full workflow graph screenshot
│   ├── workflow-diagram.png              # Architecture diagram
│   ├── input-example.png                 # Sample input
│   └── output-example.png                # Sample output
├── examples/
│   ├── interior_modern_marble.json       # Modern marble interior preset
│   ├── interior_night_lighting.json      # Night lighting scenario
│   ├── living-room/
│   ├── bedroom/
│   └── kitchen/
├── custom_nodes/                         # Optional: custom extensions
├── LICENSE                               # MIT License
└── README.md
```

## 🧪 Examples

See the [`examples/`](examples/) directory for ready-to-use presets:

| Preset | Description |
|--------|-------------|
| **interior_modern_marble.json** | Modern luxury with marble textures and natural lighting |
| **interior_night_lighting.json** | Atmospheric night scenes with artificial lighting |
| **living-room/** | Modern luxury with natural lighting |
| **bedroom/** | Cozy premium interior |
| **kitchen/** | Minimalist high-end design |

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [ComfyUI](https://github.com/comfyanonymous/ComfyUI) — Amazing UI framework
- [ControlNet](https://github.com/lllyasviel/ControlNet) — Architectural control
- [4x-UltraSharp](https://github.com/kim2091/UltraSharp) — Upscaling model
- [FreeU](https://github.com/ChenyangSi/FreeU) — Detail enhancement

## 📬 Contact

For questions and support, please open an [Issue](https://github.com/Vasilyeffpro/AI-Interior-Engine/issues).

---

<div align="center">

**Made with ❤️ for AI Interior Design Community**

⭐ Star this repo if you find it useful!

</div>
