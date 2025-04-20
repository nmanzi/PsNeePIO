# PsNeePIO

A PlayStation modchip implementation using PlatformIO and the Arduino libraries.

## Overview

PsNeePIO is an open-source implementation of the PS1 modchip that works across multiple PlayStation models and supports various microcontrollers. It injects SCEX data to bypass the region protection, allowing you to play games from any region on your console.

This project is a PlatformIO port of [kalymos' PsNee](https://github.com/kalymos/PsNee), with additions and modifications to support additional microcontrollers.

### My Thoughts

PsNee reminded me of the good old days of working on open-source modchips for the Nintendo Wii and Xbox 360. I was surprised it took so long for someone to create a true open-source mod for the PS1, especially considering the abundance of information out there on the copy-protection functions (like nocash's amazing [PSXSPX specs page](https://problemkaputt.de/psx-spx.htm#cdromprotectionmodchips)). Mad respect to kalymos for getting this done, and to all the other contributors who have worked on the project.

Being bored and having an old SCPH-5002 lying around, as well as a stack of RP2040-Zero boards, I thought it useful to pick up where others have left off and port the code to the RP2040. PlatformIO seemed like a good choice for getting this done, as it allows for easy cross-platform development and supports a wide range of microcontrollers. I'm tossing up whether or not to abandon the Arduino libraries and go with the native RP2040 libraries, but for now, I'm sticking with them for ease of use and cross-compatibility. 

I'll probably end up doing a native RP2040 port at some point, but for now, this is a good start.

## Features

- Multi-region support (NTSC-U/C, PAL, and Japanese)
- Supports multiple PlayStation models including SCPH-1000 through SCPH-103
- Compatible with the RP2040 (Raspberry Pi Pico)
- BIOS patching for models that require it
- Hardware switch option for enabling/disabling BIOS patching
- Automatic console generation detection

## Project Goals

- [x] Port the original PsNee to PlatformIO for easier development and cross-platform support
- [x] Complete the port to RP2040 (Raspberry Pi Pico)
- [ ] Test on various PlayStation models (please feel free to contribute your results)
- [ ] Improve documentation and add wiring diagrams
- [ ] Add support for more microcontrollers

## Supported PlayStation Models

See the [Project Wiki](https://github.com/nmanzi/PsNeePIO/wiki) for a list of supported PlayStation models, requirements for BIOS patching, testing results against each microcontroller, and any additional notes.

## Supported Microcontrollers
This project supports the following microcontrollers:
- Arduino Nano & Pro Mini (ATmega328)
- Arduino Micro (ATmega32U4)
- ATtiny85/45/25
- Raspberry Pi Pico (RP2040)
  - Waveshare RP2040-Zero

## Pinout Diagrams

Check the [Project Wiki](https://github.com/nmanzi/PsNeePIO/wiki) for pinout diagrams for each supported microcontroller and PlayStation model. The diagrams include wiring instructions for the modchip installation.

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

This project uses PlatformIO for building. Ensure you have PlatformIO installed and configured.

### Build Commands

```bash
# Build for Arduino Nano (ATmega328)
pio run -e nanoatmega328

# Build for Arduino Micro (ATmega32U4)
pio run -e micro

# Build for ATtiny85
pio run -e attiny85

# Build for Raspberry Pi Pico (RP2040)
pio run -e rp2040
```

### Upload Commands

```bash
# Upload to Arduino Nano
pio run -e nanoatmega328 --target upload

# Upload to Arduino Micro
pio run -e micro --target upload

# Upload to ATtiny85
pio run -e attiny85 --target upload

# Upload to Raspberry Pi Pico
pio run -e rp2040 --target upload
```

Refer to the `platformio.ini` file for additional environment configurations and options.

## License

This project is released under the Unlicense, placing it in the public domain. See the [UNLICENSE](UNLICENSE) file for details.

## Acknowledgements

This project is a PlatformIO port of [kalymos' PsNee](https://github.com/kalymos/PsNee). The original PsNee project provided the foundation for this implementation, and credit goes to kalymos and all contributors to that project.

Additional thanks to the broader PlayStation modding community for their knowledge and insights that have made projects like this possible.