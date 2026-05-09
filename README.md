<!-- Badges -->
<p align="center">
  <img src="https://img.shields.io/badge/Python-3.7-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/TensorFlow-1.x-FF6F00?style=flat-square&logo=tensorflow&logoColor=white" alt="TensorFlow" />
  <img src="https://img.shields.io/badge/DeepLabV3-Semantic_Segmentation-4285F4?style=flat-square" alt="DeepLabV3" />
  <img src="https://img.shields.io/badge/OpenCV-4.x-5C3EE8?style=flat-square&logo=opencv&logoColor=white" alt="OpenCV" />
  <img src="https://img.shields.io/badge/Google_Colab-F9AB00?style=flat-square&logo=googlecolab&logoColor=white" alt="Google Colab" />
  <img src="https://img.shields.io/badge/License-MIT-blue?style=flat-square" alt="License" />
</p>

<h1 align="center">Car Speed Detection — DeepLabV3</h1>

<p align="center">
  Computer vision project that estimates vehicle speed from video footage using <strong>DeepLabV3+ semantic segmentation</strong>, <strong>OpenCV</strong>, and <strong>TensorFlow</strong>. Detects cars frame-by-frame, tracks their position over time, and calculates speed in km/h.
</p>

---

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [How It Works](#how-it-works)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Results](#results)
- [Author](#author)
- [License](#license)

---

## Features

- **Semantic segmentation** using DeepLabV3+ MobileNetV2 pre-trained on Pascal VOC
- **Frame extraction** from video input at configurable FPS
- **Car detection** per frame with right-edge position tracking
- **Speed calculation** based on pixel displacement over time, converted to km/h
- **Annotated output** — segmented frames with car position markers saved as images
- **Result video** generated with OpenCV from annotated frames
- Runs entirely in **Google Colab** with GPU acceleration

---

## Tech Stack

| Technology | Version | Purpose |
|---|---|---|
| **Python** | 3.7 | Core programming language |
| **TensorFlow** | 1.x (compat) | DeepLabV3 model inference |
| **DeepLabV3+** | MNv2 Pascal | Pre-trained semantic segmentation model |
| **OpenCV** | 4.x | Video frame extraction and output rendering |
| **NumPy** | — | Numerical array operations |
| **Matplotlib** | — | Visualization and annotated frame export |
| **PIL (Pillow)** | — | Image loading and resizing |
| **Google Colab** | — | Cloud notebook execution with GPU |

---

## How It Works

```
Video Input → Frame Extraction → Car Segmentation (DeepLabV3) → Position Tracking → Speed Calculation
```

1. **Extract frames** from a video at a configurable FPS using OpenCV
2. **Segment each frame** with DeepLabV3+ to isolate pixels belonging to the "car" class (label index 7)
3. **Track right-edge position** of the detected car across consecutive frames
4. **Calculate displacement** between frames and convert pixel delta to meters using a known track length
5. **Compute speed** as `displacement / frame_period`, then convert m/s to km/h
6. **Render annotated output** as images and a result video

---

## Project Structure

```
2021_car-speed-test/
├── rdhT_car_speed_test.ipynb    # Main Colab notebook — all code
├── LICENSE                       # MIT License
└── README.md
```

---

## Prerequisites

| Requirement | Details |
|---|---|
| Google Account | Required for Colab |
| GPU Runtime | Colab → Runtime → Change runtime type → GPU |
| Input Video | MP4 file uploaded to Google Drive |

---

## Getting Started

### 1. Open in Google Colab

Upload `rdhT_car_speed_test.ipynb` to [Google Colab](https://colab.research.google.com/), or open it directly from your Google Drive.

### 2. Enable GPU

```
Runtime → Change runtime type → Hardware accelerator: GPU
```

### 3. Mount Google Drive

The notebook mounts your Drive automatically in the first cell. Upload your test video to Drive before running.

### 4. Configure Parameters

| Parameter | Default | Description |
|---|---|---|
| `video_path` | `/content/drive/MyDrive/_carvideo/50_3.mp4` | Path to input video in Drive |
| `panjang_lintasan` | `11.57` | Track length in meters |
| `fps_input` | `60` | Input video FPS |
| `fps_output` | `60` | Frame extraction FPS |
| `fps_render` | `5` | Output video FPS |
| `code_car` | `7` | Pascal VOC label index for "car" |

### 5. Run All Cells

Click **Runtime → Run all**. The notebook will:
1. Download the DeepLabV3 model (~30 seconds)
2. Extract frames from your video
3. Detect and segment cars in each frame
4. Calculate average speed
5. Generate annotated output images and video

---

## Results

The notebook on a sample 60 FPS video with a 11.57 m track produced:

| Metric | Value |
|---|---|
| **Frames extracted** | 96 |
| **Frames with car detected** | 53 |
| **Average pixel displacement** | 9.52 px/frame |
| **Pixel-to-meter ratio** | 0.0226 m/px |
| **Average speed** | **46.46 km/h** |

Output includes **53 annotated JPEG frames** and a **result MP4 video** showing detection boxes and segmentation masks overlaid on the original footage.

---

## Author

**Ridho Tadjudin**

- 🌐 Website: [ridhotadjudin.id](https://ridhotadjudin.id)
- 💻 GitHub: [@ridhotadjudin](https://github.com/ridhotadjudin)

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

<p align="center">
  Built with 🤖 and <a href="https://www.tensorflow.org/">TensorFlow</a>
</p>
