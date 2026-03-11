# ESP32-S3 / ESP32-P4 SoundFont (SF2) Sampler Synthesizer

An SF2 (SoundFont 2) based wavetable synth for **ESP32-S3** and **ESP32-P4**. It uses PSRAM / 外部 RAM  to load and play SoundFont samples, with USB MIDI and I2S DAC output. It's cheap and simple, yet powerful.

---

## Overview

The firmware runs on **ESP32-S3** (with PSRAM) or **ESP32-P4** (Arduino-ESP32 3.1+ / ESP-IDF 5.3+). It supports external DACs like the PCM5102, built-in USB MIDI, and optionally SD card and LittleFS. By default, the BOOT button cycles through SF2 files; long press switches between Flash LittleFS and SD.

<img src="./media/prototype.jpg?raw=true">

---

## Features

- **SF2 playback**: Load SoundFont2 banks up to PSRAM size.
- **Filesystem**: Runtime switch between LittleFS and fast 4-bit SD_MMC.
- **USB MIDI**: Plug-and-play MIDI device support.
- **Per-voice filters**: Optional biquad LPF (configurable in `config.h`).
- **Per-channel filters**: Optional CC#74/71-controlled LPF/resonance.
- **Effects**: Reverb (CC#91), Chorus (CC#93), Delay (CC#95).
- **MIDI control**: GM, partially GS/XG-compatible CCs, PC, RPNs, drums on ch.10, GM reset.
- **External DAC**: Works with PCM5102 and similar I2S DACs.
- **ESP32-S3 / ESP32-P4**: Dual-core, PSRAM or internal RAM, minimal wiring.
- **Optional OLED GUI**: Use a rotary encoder and a button to navigate. 

---

## Hardware Requirements

- **ESP32-S3**（带 PSRAM，推荐 OPI）或 **ESP32-P4**（32MB PSRAM，Arduino-ESP32 3.1+）
- **External DAC** (e.g., PCM5102)
- USB connection for MIDI and power

---

## I2S DAC (PCM 5102) Pin Connections

| Signal | GPIO Pin |
|--------|----------|
| BCK    | GPIO5    |
| DTA    | GPIO6    |
| WCK    | GPIO7    |
| CS     | GND      |

These pins can be changed in config.h if needed

---


## SD CARD Pin Connections:

| Signal | GPIO Pin |
|--------|----------|
| CMD     | GPIO38  |
| CLK     | GPIO39  |
| D0     | GPIO10  |
| D1     | GPIO11  |
| D2     | GPIO12  |
| D3     | GPIO13  |
| VCC    | 3V3  |
| GND    | GND  |

These pins can be changed in config.h if needed

---
## GUI:

GUI requires U8g2 library.

| Signal | GPIO Pin |
|------------|---------------|
|   button | 14 |
| encoder pin A | 15 |
| encoder pin B | 16 |
| | |
| display SDA | 8    |
| display SCL | 9    |


These pins can be changed in config.h if needed

---
## Software Setup

### Arduino IDE Configuration

- **Board**: **ESP32-S3** 或 **ESP32-P4**（P4 需 Arduino-ESP32 3.1+）
- **PSRAM** (S3): 选择 **OPI PSRAM**
- **Partition Scheme**: 选可用 SPIFFS/LittleFS 空间较大的方案
- **USB Mode**: **TINY USB**
- **Core Debug Level**: **Info** 或更低（过高可能影响 USB）
- **Upload SF2 to Flash**: Arduino IDE 2.x 可用 https://github.com/earlephilhower/arduino-littlefs-upload
- **ESP32-P4**: 引脚在 `config.h` 中按 `TARGET_ESP32P4` 区分，请根据开发板原理图修改 I2S / SDMMC / GUI 引脚 

---

## Usage

1. 按上表连接 ESP32-S3 或 ESP32-P4 与外部 DAC。
2. 将 SF2 音色文件写入 Flash 或 SD 卡。
3. 用 USB 连接电脑或 MIDI 主机；设备将显示为 USB MIDI 设备（S3 为 "S3 SF2 Synth"，P4 为 "P4 SF2 Synth"）。
4. 通过 MIDI 输入演奏。

---

## Notes

- 支持 **ESP32-S3**（需 PSRAM）和 **ESP32-P4**（32MB PSRAM，需 Arduino-ESP32 3.1+）。P4 无蓝牙，代码已做条件编译。
- 调试级别高于 **Info** 可能影响 USB MIDI。
- 确保外接 DAC 供电与连接正确。

---

## Contributing

Contributions, issues, and feature requests are welcome! Feel free to open a pull request or issue on the GitHub repository.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Links
- [Free SoundFonts](https://github.com/ZmeyKolbasnik/Instruments/tree/master)
- [ESP32-S3](https://www.espressif.com/en/products/socs/esp32-s3) / [ESP32-P4](https://www.espressif.com/en/products/socs/esp32-p4)
- [SoundFont 2 Specification](https://en.wikipedia.org/wiki/SoundFont)
- [ESP Partition calculator](https://github.com/copych/ESP32-S3_SF2_Sampler_Synthesizer/tree/main/partitions)

---

Enjoy your ESP32-S3 / ESP32-P4 sampler!

