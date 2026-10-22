# DAMX - Acer Nitro 16 (AN16-41 Phoenix) Linux Suite

[![Kernel](https://img.shields.io/badge/Linux_Kernel-6.x%20%7C%207.x%20Ready-brightgreen.svg)](#)
[![Distro](https://img.shields.io/badge/Tested%20On-CachyOS%20%7C%20Arch%20Linux-blue.svg)](#)
[![Hardware](https://img.shields.io/badge/Hardware-Acer%20Nitro%2016%20(AN16--41)-red.svg)](#)
[![Version](https://img.shields.io/badge/DAMX%20Suite-v1.0.2-orange.svg)](#)

A complete fan control, thermal management, RGB keyboard, and hardware utility suite for **Acer Nitro 16 (AN16-41 "Phoenix")** and Acer Predator/Nitro gaming laptops on Linux.

---

## 🌟 Features

- 🌀 **Custom Fan Control**: Independent control for CPU and GPU fans (Auto, Custom RPM/percentage, Max/Turbo).
- ⚡ **Thermal & Performance Profiles**: Quick switching between *Eco*, *Balanced*, *Performance*, and *Turbo* modes.
- 🌈 **4-Zone RGB Keyboard Backlight**: Control modes, speeds, brightness, and colors per zone.
- 🔋 **Battery Health**: Built-in 80% battery charge limiter and battery calibration support.
- 🔘 **Hardware Nitro Button Hook**: Automatically launches DAMX when pressing the physical **NitroSense** button on the keyboard.
- 🖥️ **Modern GUI**: Clean desktop interface built with Avalonia UI (.NET 9.0).

---

## 🛠️ Fixes & Improvements in This Fork

This repository contains critical compatibility fixes over the original DAMX 1.0.2 release:

1. **Linux Kernel 7.x & 6.14+ Compatibility**:
   - Modern Linux kernels removed deprecated string functions (`strncpy`).
   - Patched `Linuwu-Sense/src/linuwu_sense.c` to use safe, bounds-checked `memcpy` and proper null-termination.
   - Fixed bitwise boolean operations for cleaner Clang/LLVM compilation.
2. **Kbuild Whitespace / Special Character Path Fix**:
   - Linux kernel's Kbuild system fails when source paths contain spaces or parentheses (e.g. `DAMX-1.0.2 (2)`).
   - `setup.sh` now builds the driver module in a clean temporary directory (`/tmp/damx_linuwu_sense_build`) before installing.
3. **Enhanced Setup Script**:
   - Added CLI arguments support (e.g., `sudo ./setup.sh 1` for direct full installation).
   - Added TTY detection for `pause` to prevent non-interactive hangs.

---

## 🚀 Installation

### 1. Requirements

Make sure you have basic build tools and kernel headers installed:

- **Arch Linux / CachyOS**:
  ```bash
  sudo pacman -S --needed base-devel linux-headers clang llvm lld evtest
  ```
- **Ubuntu / Debian**:
  ```bash
  sudo apt update && sudo apt install -y build-essential linux-headers-$(uname -r) evtest
  ```
- **Fedora**:
  ```bash
  sudo dnf install -y gcc make kernel-devel evtest
  ```

### 2. Install DAMX Suite

Clone this repository and run the setup script:

```bash
git clone https://github.com/namsoaica/damx-nito-sense-to-acer-nito-16-phoenix.git
cd damx-nito-sense-to-acer-nito-16-phoenix
sudo ./setup.sh
```

Follow the interactive menu:
1. Select **`1`** for **Complete Installation** (installs `Linuwu-Sense` driver, background daemon, and GUI).
2. When prompted:
   ```text
   Do you want to setup your Nitro/PredatorSense Key? (y/N)
   ```
   Press **`y`**, then press the physical **Nitro** key on your laptop keyboard within 30 seconds.

---

## 🎮 How to Use

- **Launch GUI**: Run `DAMX` in terminal, open **DAMX** from your Application Menu, or press the physical **Nitro** key.
- **Check Service Status**:
  ```bash
  systemctl status damx-daemon.service
  ```
- **Check Nitro Button Service**:
  ```bash
  systemctl status nitro-key-detection.service
  ```

---

## 🗑️ Uninstallation

If you ever want to remove DAMX Suite:

```bash
sudo ./setup.sh 3
```

---

## 🤝 Credits & Acknowledgements

- **DAMX (Div Acer Manager Max)** by [PXDiv](https://github.com/PXDiv/Div-Acer-Manager-Max)
- **Linuwu-Sense Driver** by [0x7375646F](https://github.com/0x7375646F/Linuwu-Sense)
- Inspired by [acer-predator-turbo](https://github.com/JafarAkhondali/acer-predator-turbo-and-rgb-keyboard-linux-module) and the Linux `acer-wmi` kernel driver.
