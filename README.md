![Version](https://img.shields.io/badge/Version-1.0-blue)
![Hardware](https://img.shields.io/badge/Hardware-Cardputer-orange)
![Platform](https://img.shields.io/badge/Platform-M5Stack-red)
![License](https://img.shields.io/badge/License-MIT-green)
[![Boosty](https://img.shields.io/badge/Support-Boosty-orange)](https://boosty.to/zeloksa)

# 🔦 M5Stack Cardputer Flashlight (V1.0)

**Flashlight V1.0** is a highly optimized, state-machine-based illumination utility for the **M5Stack Cardputer**. It repurposes the device's TFT display as a multi-mode light source, featuring standard white light, tactical red light, and a high-frequency strobe.

> [!NOTE]
> **Source Code Status:** Open Source. 
> Written purely in C++ using the `<M5Cardputer.h>` library without third-party button dependencies.

---

## ⚡ Technical Highlights

* **Non-Blocking State Machine:** The core architecture relies entirely on `millis()` for timer management. Zero `delay()` calls ensure instant responsiveness and prevent CPU blocking.
* **Custom Debounce & Click Detection Core:** Features a custom-built event listener that accurately distinguishes between single clicks, double clicks, and prolonged holds using leading-edge and trailing-edge logic.
* **Smart Color Memory:** The system remembers your last active illumination mode (White or Red). Turning the flashlight off and on via a single click will restore the previous state.
* **Deep Power Optimization:** The ESP32-S3 CPU frequency is underclocked from the default 240MHz down to **80MHz** during setup. This guarantees stable I2C/SPI bus operation for the keyboard and display while drastically reducing battery consumption and heat generation.
* **Hardware-Level Display Control:** When turned off, the firmware sets the TFT backlight brightness to `0` and fills the VRAM with `TFT_BLACK` to completely halt power draw from the screen matrix.

---

## 🛠 Installation

1. Clone or download this repository.
2. Open `Main.ino` in the **Arduino IDE**.
3. Ensure you have the [M5Cardputer library](https://github.com/m5stack/M5Cardputer) installed.
4. Select **M5Cardputer** in the board manager.
5. Compile and upload to your device.

---

## 🕹 Controls & Usage

Interaction works by pressing **ANY** key on the Cardputer's matrix keyboard. 

* **[ Single Click ]**: Power Toggle. Turns the flashlight ON (restoring the last used color) or OFF.
* **[ Double Click ]**: Strobe Toggle. Instantly enters or exits a high-frequency (50ms interval) white/black flashing sequence. Exiting returns to the previous color state.
* **[ Hold (>500ms) ]**: Tactical Red Light Toggle. Switches between standard White Light and Red Light modes. Useful for preserving night vision.

---

## ⚙️ Core States Overview

| State | Brightness | Action |
| :--- | :--- | :--- |
| `STATE_WHITE` | 255 | Solid `TFT_WHITE` fill. |
| `STATE_RED` | 255 | Solid `TFT_RED` fill for night vision preservation. |
| `STATE_STROBE` | 255 | Alternating `TFT_WHITE` / `TFT_BLACK` every 50ms. |
| `STATE_OFF` | 0 | Screen brightness killed, VRAM filled with `TFT_BLACK`. |

---

## 💬 Feedback & Suggestions
If you find a bug or have a suggestion for the next version:
1. Go to the **[Issues]** tab at the top of this page.
2. Click **[New Issue]**.
3. Describe your problem or idea in detail.

---

## ☕ Support the Project
If this tool has been useful for your EDC (Everyday Carry) or projects, consider supporting further development:
* **[https://boosty.to/zeloksa](https://boosty.to/zeloksa)**

---
*Created by Zeloksa. Optimized for Cardputer.*
