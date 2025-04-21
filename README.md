# PsNeePIO

A PlayStation modchip implementation using PlatformIO and the Arduino libraries.

## Overview

PsNeePIO is an open-source implementation of the PS1 modchip that works across multiple PlayStation models and supports various microcontrollers. It injects SCEX data to bypass the region protection, allowing you to play games from any region on your console.

This project is a PlatformIO port of [kalymos' PsNee](https://github.com/kalymos/PsNee), with additions and modifications to support additional microcontrollers.

### Rationale

PsNee reminded me of the good old days of working on open-source modchips for the Nintendo Wii and Xbox 360. I was surprised it took so long for someone to create a true open-source mod for the PS1, especially considering the abundance of information out there on the copy-protection functions (like nocash's amazing [PSXSPX specs page](https://problemkaputt.de/psx-spx.htm#cdromprotectionmodchips)). Mad respect to kalymos for getting this done, and to all the other contributors who have worked on the project.

Being bored and having an old SCPH-7502 lying around, as well as a stack of RP2040-Zero boards, I thought it useful to pick up where others have left off and port the code to the RP2040. PlatformIO seemed like a good choice for getting this done, as it allows for easy cross-platform development and supports a wide range of microcontrollers. I'm tossing up whether or not to abandon the Arduino libraries and go with the native RP2040 libraries, but for now, I'm sticking with them for ease of use and cross-compatibility. 

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
- [x] Complete the port to RP2040
- [ ] Implement UART for injection on RP2040 (thanks [Skitchin](https://github.com/johnbaumann/)!)
- [ ] Test on various PlayStation models (please feel free to contribute your results, especially if you have a hardware model that requires BIOS patching!)
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

### Pinout and installation instructions

Check the [Project Wiki](https://github.com/nmanzi/PsNeePIO/wiki) for pinout diagrams for each supported microcontroller and PlayStation model. The diagrams include wiring instructions for the modchip installation.

## Building

1. Clone this repository
2. Configure your console model and chip type in `src/main.cpp`
3. Build and upload using PlatformIO
4. Install the modchip in your PlayStation console according to the [pinout diagrams](https://github.com/nmanzi/PsNeePIO/wiki)

### Build Commands

Check the `platformio.ini` file for the available environments. You can build for your desired microcontroller by running the following commands in the terminal as an example:

```bash
# Build for Raspberry Pi Pico (RP2040)
pio run -e rp2040

# Upload to Raspberry Pi Pico (RP2040)
pio run -e rp2040 --target upload
```

## License

This project is released under the Unlicense, placing it in the public domain. See the [UNLICENSE](UNLICENSE) file for details.

## Acknowledgements

This project is a PlatformIO port of [kalymos' PsNee](https://github.com/kalymos/PsNee). The original PsNee project provided the foundation for this implementation, and credit goes to kalymos and all contributors to that project.

Additional thanks to the broader PlayStation modding community for their knowledge and insights that have made projects like this possible.
