# 🧺 Smart Laundry Basket

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/)
[![YOLOv8](https://img.shields.io/badge/YOLOv8-Ultralytics-00FFFF.svg)](https://github.com/ultralytics/ultralytics)
[![Raspberry Pi](https://img.shields.io/badge/Raspberry%20Pi-A22846.svg?logo=raspberrypi&logoColor=white)](https://www.raspberrypi.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> An IoT laundry basket that **detects and classifies laundry by washing program** using deep learning, and alerts you when there's enough to start a load.

<p align="center">
  <img src="https://raw.githubusercontent.com/IsabelleDesle/Smart-Laundry-Basket/main/raspberry-pi.gif" width="720" />
</p>

---

## 📖 Overview

A motion-triggered camera mounted on a laundry basket photographs its contents whenever clothes are added. A YOLOv8 model classifies each garment into one of five washing programs, and the running count per program is tracked. When the count reaches a threshold (a typical machine load), the system raises an alert that it's time to start the washing machine.

Inspired by [this Instructables project](https://www.instructables.com/The-Laundry-Basket-Wants-You-to-Start-the-Washing-/).

### Washing programs

| Program | Description |
|---|---|
| 🟦 30°C Color | Colored garments, low temperature |
| ⚪ 30°C White | White garments, low temperature |
| 🟦 60°C Color | Colored garments, hot wash |
| ⚪ 60°C White | White garments, hot wash |
| 🧶 Delicate & Wool | Delicate fabrics and wool |

---

## 🏗️ Architecture

```
┌──────────────────────┐        ┌──────────────────────┐
│  Raspberry Pi        │        │  AI Client (Host)    │
│  • PIR motion sensor │  HTTP  │  • YOLOv8 inference  │
│  • Camera module     │ ─────▶ │  • Per-program count │
│  • LCD display       │ ◀──── │  • Alert logic       │
└──────────────────────┘        └──────────────────────┘
```

- **`RPI/`** — Code that runs on the Raspberry Pi: motion detection, image capture, LCD output, and HTTP communication.
- **`AI/`** — YOLOv8 classifier that receives images, predicts the washing program, and tracks counts.

---

## 🛠️ Tech Stack

- **Deep Learning:** Ultralytics YOLOv8 (`yolov8s.pt`)
- **Hardware:** Raspberry Pi, Pi Camera, PIR motion sensor, I²C LCD
- **Language:** Python 3.10+
- **Comms:** HTTP between Pi and AI client

---

## 🚀 Getting Started

### 1. Clone

```bash
git clone https://github.com/IsabelleDesle/Smart-Laundry-Basket.git
cd Smart-Laundry-Basket
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Run the AI client (on your computer)

```bash
python AI/ai-client.py
```

### 4. Run the Raspberry Pi server (on the Pi)

```bash
python RPI/rpi-server.py
```

---

## 📁 Project Structure

```
Smart-Laundry-Basket/
├── AI/
│   ├── ai-client.py        # YOLOv8 inference + classification
│   └── csv/                # Logged predictions and counts
├── RPI/
│   ├── rpi-server.py       # Pi-side server, camera + sensors
│   └── Class_LCD.py        # LCD output helper
├── runs/                   # Training/inference run outputs
├── yolov8s.pt              # Pretrained YOLOv8 small weights
└── requirements.txt
```

---

## 👤 Author

**Isabelle Deslé** — Bachelor AI & Creative Technologies @ Howest
[GitHub](https://github.com/IsabelleDesle)

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
