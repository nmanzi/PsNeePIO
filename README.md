# PsNeePIO

A PlayStation modchip implementation using PlatformIO, designed to bypass region locking on PlayStation 1 consoles.

## Overview

PsNeePIO is an open-source implementation of the PS1 modchip that works across multiple PlayStation models and supports various microcontrollers. It injects SCEX data to bypass the region protection, allowing you to play games from any region on your console.

This project is a PlatformIO port of [kalymos' PsNee](https://github.com/kalymos/PsNee), with additions and modifications to support additional microcontrollers.

## Features

- Multi-region support (NTSC-U/C, PAL, and Japanese)
- Supports multiple PlayStation models including SCPH-1000 through SCPH-103
- Compatible with the RP2040 (Raspberry Pi Pico)
- BIOS patching for models that require it
- Hardware switch option for enabling/disabling BIOS patching
- Automatic console generation detection

## Project Goals

- [x] Port the original PsNee to PlatformIO for easier development and cross-platform support
- [x] Support for Arduino-based microcontrollers (ATmega328/168, ATmega32U4/16U4)
- [x] Support for ATtiny microcontrollers (ATtiny85/45/25)
- [x] Complete the port to RP2040 (Raspberry Pi Pico)
- [ ] Improve documentation and add wiring diagrams
- [ ] Add support for more microcontrollers

## Supported PlayStation Models

- SCPH-xxxx (Generic support for NTSC-U/C, PAL FAT models)
- SCPH-xxx1, SCPH-xxx2, SCPH-103 (No BIOS patching needed)
- SCPH-102, SCPH-100, SCPH-7000-9000
- SCPH-5500, SCPH-3500-5000, SCPH-3000, SCPH-1000 (All with BIOS patching)

## Hardware Requirements

### Microcontroller Options
- Arduino Nano & Pro Mini (ATmega328)
- Arduino Micro (ATmega32U4)
- ATtiny85/45/25
- Raspberry Pi Pico (RP2040)
  - Waveshare RP2040-Zero

### Recommended Fuse Settings
- ATmega - H: DF, L: EE, E: FD
- ATtiny - H: DF, L: E2, E: FD

### Pinout for Arduino
- VCC-3.5v
- PinGND-GND
- D2-BIOS AX (Only for BIOS patch)
- D3-BIOS AY (Only for BIOS ver. 1.0j-1.1j)
- D4-BIOS DX (Only for BIOS patch)
- D5-Switch* (Optional for BIOS patch)
- D6-SQCK
- D7-SUBQ
- D8-DATA
- D9-GATE_WFCK
- RST-RESET* (Only for JAP_FAT)

### Pinout for ATtiny
- Pin1-RESET
- Pin2-LED
- Pin3-WFCK
- Pin4-GND
- Pin5-SQCK (MOSI)
- Pin6-SUBQ (MISO)
- Pin7-DATA (SCK)
- Pin8-VCC

### Pinout for RP2040-Zero Board
- GPIO2 - DATA
- GPIO3 - WFCK
- GPIO4 - SQCK
- GPIO5 - SUBQ
- 3.3V - VCC
- GND - GND

For BIOS patching (only needed for certain models):
- GPIO6 - BIOS AX
- GPIO7 - BIOS AY (Only for BIOS ver. 1.0j-1.1j)
- GPIO8 - BIOS DX
- GPIO9 - Switch* (Optional for disabling BIOS patch)

## Installation & Usage

1. Clone this repository
2. Configure your console model and chip type in `src/main.cpp`
3. Build and upload using PlatformIO
4. Install the modchip in your PlayStation console according to the pinout diagrams

## Configuration

Edit the following sections in `src/main.cpp`:

1. Select your console model by uncommenting the appropriate `#define` statement
2. Select your microcontroller by uncommenting the appropriate `#define` statement
3. Optionally enable LED indicators or hardware patching switches

## Building

This project uses PlatformIO for building. Make sure you have PlatformIO installed.

```bash
# Build for Arduino Pro Mini 8MHz
pio run -e pro8MHzatmega328

# Build for Raspberry Pi Pico
pio run -e rp2040

# Upload to Raspberry Pi Pico
pio run -e rp2040 --target upload
```

## License

This project is released under the Unlicense, placing it in the public domain. See the [UNLICENSE](UNLICENSE) file for details.

## Acknowledgements

This project is a PlatformIO port of [kalymos' PsNee](https://github.com/kalymos/PsNee). The original PsNee project provided the foundation for this implementation, and credit goes to kalymos and all contributors to that project.

Additional thanks to the broader PlayStation modding community for their knowledge and insights that have made projects like this possible.