# Pisces P100 → Standard LoRa Gateway Conversion

> Whether you’re a developer or hobbyist, this repository provides everything you need to transform your Pisces P100 device into a standard SX1302‑based LoRa gateway—reset pinout may vary by hardware revision.
> For a hassle‑free solution, prebuilt firmware ISO packages (with all pin and configuration settings preconfigured) are also available for purchase.
> **Inquiries & Sales:** [mertzkul@gmail.com](mailto:mertzkul@gmail.com)

---

## 🚀 Project Overview

This **pisces-p100-sx1302-hal** repository adapts Semtech’s SX1302/SX1303 Hardware Abstraction Layer (HAL) library for the Pisces P100 platform. You’ll find modular components for both USB‑ and SPI‑based gateways, utilities for calibration and control, and example applications to get you up and running quickly.

Key components:

* **libloragw/**: Core HAL driver for the SX1302 concentrator chip
* **packet\_forwarder/**: Example forwarder sending uplink packets to a UDP/IP server and handling downlinks
* **mcu\_bin/**: USB–SPI bridge firmware for STM32 microcontrollers
* **util\_**\*/: Tools for reading chip IDs, bootloader utilities, and spectrum scanning
* **tools/**: Shell scripts for pin resets, power control, and gateway management

---

## 📋 Features

* **SPI or USB** connectivity modes for flexible gateway deployment
* Automated reset and power management via `tools/reset_lgw.sh`
* STM32-based DFU bootloader support for USB‑SPI bridge functionality
* Spectrum scan examples and multi‑SF demodulation support
* Easy build and deployment on Linux systems (Raspberry Pi, Ubuntu, etc.)

---

## 🛠️ Requirements

* **Hardware:** Pisces P100 device with SX1302 concentrator
* **OS:** Linux (Debian/Ubuntu/Raspbian recommended)
* **Toolchain & Utilities:**

  * GCC (native or cross‑compile for ARM: `arm-linux-gnueabihf-gcc`)
  * `make`, `git`, `ssh`, `scp`
  * For USB gateway: `dfu-util` or equivalent STM32 programmer

---

## 🚧 Installation & Build

1. **Clone the repository**

   ```bash
   git clone https://github.com/mert-ozkul/pisces-p100-sx1302-hal.git
   cd pisces-p100-sx1302-hal
   ```

2. **Configure your target settings**

   * Edit `target.cfg` to match your gateway’s IP, directory, and user credentials

3. **Clean build & deploy**

   ```bash
   make clean all
   make install         # Deploy binaries via SSH to your gateway device
   make install_conf    # Copy packet_forwarder JSON configs
   ```

4. **Optional: Cross‑compile for ARM**

   ```bash
   export ARCH=arm
   export CROSS_COMPILE=arm-linux-gnueabihf-
   make clean all
   ```

---

## ▶️ Usage

### Packet Forwarder

Run the forwarder with your configuration:

```bash
./bin/packet_forwarder --config global_conf.json
```

* **Uplink:** RF → LoRa concentrator → UDP server
* **Downlink:** UDP server → LoRa concentrator → RF

### USB Gateway Mode

Activate USB–SPI bridge on `/dev/ttyACM0`:

```bash
./util_boot/boot.sh -u -d /dev/ttyACM0
```

This script enters DFU mode on the STM32 and bridges USB to the SX1302 via SPI.

---

## 📞 Contact & Support

* **Firmware ISO Sales & Technical Support:** [mertzkul@gmail.com](mailto:mertzkul@gmail.com)
* Report issues or suggest enhancements via GitHub Issues.

---

## 📝 License

This project is released under the **BSD‑3‑Clause** License. See [LICENSE.TXT](LICENSE.TXT) for details.
