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
- **UART-based SCEX injection for RP2040**: Simpler and more efficient than bit-banging on capable MCUs

## Project Goals

- [x] Port the original PsNee to PlatformIO for easier development and cross-platform support
- [x] Complete the port to RP2040 (RP2040-Zero board)
- [x] Implement UART for injection on RP2040 (thanks [Skitchin](https://github.com/johnbaumann/)!)
- [ ] Implement PIO where appropriate to free up the main thread for fun and profit
- [ ] Add [PicoMemcard](https://github.com/dangiu/PicoMemcard/) functionality as a bonus feature (also use littlefs/flash for debug logging?)
- [ ] Test on various PlayStation models (please feel free to contribute your results, especially if you have a hardware model that requires BIOS patching!)
- [ ] Test on other RP2040 boards
- [ ] Improve documentation and add wiring diagrams

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

## UART Injection Mode (RP2040)

For capable microcontrollers like the RP2040, PsNeePIO supports an optional UART-based injection mode. This mode is simpler, more reliable, and frees up CPU cycles compared to the traditional bit-banging approach.

### How It Works

Instead of manually toggling GPIO pins at precise intervals, UART mode leverages the hardware UART peripheral configured at 250 baud. The SCEX region codes are transmitted as ASCII strings ("SCEE", "SCEA", "SCEI"), and when combined with inverted output, the resulting waveform matches the SCEX pattern that PlayStation consoles expect.

The key insight is that the ASCII representation of these region codes, when transmitted via UART with specific timing and polarity, produces the correct signal characteristics for PlayStation's copy protection system.

### Enabling UART Mode

UART injection is enabled by default for the RP2040. To disable it and use the traditional bit-banging method, comment out the `USE_UART_INJECTION` define in `src/main.cpp`:

```cpp
#ifdef rp2040zero
// #define USE_UART_INJECTION  // Comment this out to use the traditional bit-banging method
#endif
```

### Hardware Notes

- The UART TX pin (GPIO 2 by default) should be connected to the DATA line through an inverter
- **Important:** The UART output must be inverted for proper operation. This can be achieved with:
  - A simple transistor inverter circuit (e.g., NPN transistor with base resistor) between the UART TX pin and the DATA line, OR
  - A logic inverter IC (e.g., 74HC04) if you prefer
- Wiring: UART TX (GPIO 2) -> Inverter -> PlayStation DATA line
- The inversion is necessary because UART idle state is HIGH, but the PlayStation expects an inverted signal

### Note on Implementation

This UART-based approach is based on community findings that discovered ASCII strings transmitted at 250 baud with inverted polarity can substitute for the complex bit-banging patterns. While the exact mechanism may seem unconventional, it has been reported to work effectively on RP2040 and similar capable MCUs.

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
