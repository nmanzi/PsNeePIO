# PsNeePIO

A PlayStation modchip implementation using PlatformIO, designed to bypass region locking on PlayStation 1 consoles.

## Overview

PsNeePIO is an open-source implementation of a PS1 modchip that works across multiple PlayStation models and aims to support the RP2040.

This project is a PlatformIO port of [kalymos' PsNee](https://github.com/kalymos/PsNee), with additions and modifications to support additional microcontrollers.

## Features

- Multi-region support (NTSC-U/C, PAL, and Japanese)
- Supports multiple PlayStation models including SCPH-1000 through SCPH-103
- Compatible with the RP2040 (Raspberry Pi Pico) - *Work in progress*
- BIOS patching for models that require it
- Hardware switch option for enabling/disabling BIOS patching
- Automatic console generation detection

## Project Goals

- [x] Port the original PsNee to PlatformIO for easier development and cross-platform support
- [x] Support for Arduino-based microcontrollers (ATmega328/168, ATmega32U4/16U4)
- [x] Support for ATtiny microcontrollers (ATtiny85/45/25)
- [ ] Complete the port to RP2040 (Raspberry Pi Pico)
- [ ] Improve documentation and add wiring diagrams
- [ ] Add support for more microcontrollers

## Supported PlayStation Models

- SCPH-xxxx (Generic support for NTSC-U/C, PAL FAT models)
- SCPH-xxx1, SCPH-xxx2, SCPH-103 (No BIOS patching needed)
- SCPH-102, SCPH-100, SCPH-7000-9000
- SCPH-5500, SCPH-3500-5000, SCPH-3000, SCPH-1000 (All with BIOS patching)

## Hardware Requirements

### Microcontroller Options
- Raspberry Pi Pico (RP2040) - *Support coming soon*

### Pinout
*In development*

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
# Build for Raspberry Pi Pico (not fully implemented yet)
pio run -e rp2040
```

## License

This project is released under the Unlicense, placing it in the public domain. See the [UNLICENSE](UNLICENSE) file for details.

## Acknowledgements

This project is a PlatformIO port of [kalymos' PsNee](https://github.com/kalymos/PsNee). The original PsNee project provided the foundation for this implementation, and credit goes to kalymos and all contributors to that project.

Additional thanks to the broader PlayStation modding community for their knowledge and insights that have made projects like this possible.