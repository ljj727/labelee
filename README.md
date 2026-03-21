# Labelee

Desktop image annotation and labeling tool for computer vision.

![License](https://img.shields.io/badge/License-MIT-green)

---

## Features

### Annotation Tools
- **Bounding Box** — Click and drag to draw, resize handles, arrow key fine-tuning
- **Polygon** — Click to place vertices, right-click to delete, click edge to insert point
- **Keypoint** — Template-based with skeleton connections, multi-select drag
- **SAM Interactive** — Click to segment with SAM model (GPU required)

### Labeling Workflow
- **Class Management** — Create, edit, delete with color picker
- **Keypoint Templates** — Define per-class keypoint names with auto-skeleton
- **Label Lock** — Prevent accidental edits (L key)
- **Image Tags** — Notion-style multi-select tags with auto-complete
- **Undo/Redo** — Ctrl+Z / Ctrl+Y
- **Copy/Paste** — Ctrl+C/V with offset duplication
- **Multi-select** — Ctrl+click, Shift+click range select

### Data Management
- **Project / Dataset** structure
- **Dataset Roles** — train / val / test badges
- **Import** — COCO, CVAT XML, YOLO formats
- **Export** — COCO, CVAT XML, YOLO (to `annotations/` folder)
- **Video Frame Extraction** — ffmpeg-based, drag & drop support
- **Image Move** — Move images between datasets with labels
- **Sync** — Detect filesystem changes automatically

### Auto Labeling (Docker)
- SAM3 text-prompt based object detection
- Docker container execution with real-time log streaming
- Setup via Settings page

### UI
- **Dark / Light / System** theme
- **Customizable keyboard shortcuts**
- **Statistics dashboard** — Class distribution, tag usage, labeling progress
- **Tag-based image filtering**

---

## Downloads

Download the latest release from the [Releases](https://github.com/ljj727/labelee/releases) page.

| Platform | File |
|----------|------|
| **Linux** | `.AppImage` (portable) or `.deb` (Ubuntu/Debian) |
| **Windows** | `.exe` installer |

---

## Requirements

| Feature | Requirement |
|---------|-------------|
| Basic labeling | None |
| SAM Interactive | NVIDIA GPU + CUDA driver + ONNX model |
| Auto Labeling | Docker |
| Video extraction | ffmpeg |

---

## SAM Interactive Setup

SAM Interactive uses ONNX models for point-click segmentation. You need to prepare a zip file containing the model files.

### 1. Download models

Download SAM ONNX models from HuggingFace (e.g., [SAM2 ONNX](https://huggingface.co/models?search=sam2+onnx) or your own exported models).

Required files:
```
vision_encoder_fp16.onnx
vision_encoder_fp16.onnx_data
prompt_encoder_mask_decoder_fp16.onnx
prompt_encoder_mask_decoder_fp16.onnx_data
```

### 2. Create zip

Bundle the 4 files into a single zip:
```bash
zip sam_models.zip \
  vision_encoder_fp16.onnx \
  vision_encoder_fp16.onnx_data \
  prompt_encoder_mask_decoder_fp16.onnx \
  prompt_encoder_mask_decoder_fp16.onnx_data
```

### 3. Load in Labelee

1. Open **Settings** (gear icon in sidebar)
2. Under **SAM Interactive**, click **"모델 업로드 (.zip)"**
3. Select the zip file
4. Wait for loading (first time may take ~30 seconds)

Once loaded, use the **C** key in the labeling view to activate SAM mode. Click on an object to get a bounding box / polygon.

> **Note**: SAM requires an NVIDIA GPU with CUDA. It will not work on CPU-only or Mac environments.

---

## Keyboard Shortcuts

All shortcuts are customizable in Settings.

| Shortcut | Action |
|----------|--------|
| `V` | Select tool |
| `B` | BBox / Polygon tool |
| `K` | Keypoint tool |
| `C` | SAM tool (if loaded) |
| `H` | Toggle label visibility |
| `T` | Toggle class name display |
| `L` | Toggle label lock |
| `F` | Fit to screen |
| `G` | Toggle image list |
| `Ctrl+Z` | Undo |
| `Ctrl+Y` | Redo |
| `Ctrl+C/V` | Copy / Paste labels |
| `Ctrl+A` | Select all |
| `Arrow keys` | Move label 1px (Shift: 10px) |
| `Delete` | Delete selected |
| `Space+Drag` | Pan canvas |
| `Scroll` | Zoom |

---

## Supported Formats

### Import
| Format | Source |
|--------|--------|
| COCO | `coco.json` + images |
| CVAT | `annotations.xml` + images |
| YOLO | `data.yaml` + images/labels |
| Images | jpg, png, bmp, webp |
| Video | mp4, avi, mov, mkv, webm (frame extraction) |

### Export
| Format | Output |
|--------|--------|
| COCO | `annotations/coco.json` |
| CVAT | `annotations/annotations.xml` |
| YOLO | `annotations/labels/*.txt` + `data.yaml` |

All exports include keypoint data where applicable.

---

## License

[MIT License](LICENSE) - Free to use.
