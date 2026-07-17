# Architecture Document

## Project Structure

The current codebase is an AVR-based USB firmware project (EasyMCU/EasyCon) designed to emulate a Nintendo Switch controller using a wired USB connection.

Key directories and files:
- `Joystick.c` / `Joystick.h`: Main entry point, interrupt handlers, and core application loop.
- `HID.c` / `HID.h`: USB HID handling.
- `EasyCon.c`, `EasyCon_API.c`: Core controller and macro/scripting logic.
- `LUFADescriptors.c`, `HORI_Descriptors`: USB descriptors for controller emulation.
- `lufa/`: Lightweight USB Framework for AVRs submodule.
- `makefile`, `makefile.core.mk`: AVR build system configuration.

## Build System

The current build system uses `make` with `avr-gcc`, relying heavily on LUFA's build scripts (`lufa_core.mk`, `lufa_sources.mk`, `lufa_build.mk`, etc.).
It targets 8-bit AVR microcontrollers (atmega16u2, atmega32u4, at90usb1286).

## Bluetooth Implementation

**MISSING.**
The current codebase relies entirely on wired USB via the LUFA stack. There is no Bluetooth implementation present in the repository.

## Controller Implementation

The controller implementation emulates a HORI Pokken Tournament Pro Pad.
It uses AVR interrupts (`TIMER0_OVF_vect`, `USART1_RX_vect`, `PCINT0_vect`) to manage timings and receive commands.
While the core logic is present, it is tightly coupled to the AVR architecture and LUFA USB HID APIs.

## Amiibo Implementation

**MISSING.**
There is no Amiibo support, NFC handling, or related data structures in the current repository.

## Dependencies

- **LUFA:** Used for USB communication.
- **AVR-GCC / WinAVR:** Required for compilation.

## Risks

1. **Hardware Mismatch:** The target hardware is the ESP32-based M5StickC Plus 2, but the codebase is written for 8-bit AVRs.
2. **Protocol Mismatch:** The target requires Bluetooth Classic and WebSockets, but the existing code only supports wired USB.
3. **Interrupt Coupling:** The existing logic relies on specific AVR hardware interrupts which do not exist on the ESP32.
4. **Missing Components:** Critical features required by the project goals (Amiibo, Bluetooth, LittleFS, WebUI) are not present.

## Assumptions

- The existing core controller logic (`EasyCon` / macros) is what needs to be preserved, while the transport layer (USB -> Bluetooth) and hardware layer (AVR -> ESP32) will need to be adapted or wrapped.
- The project will eventually need a new build system (e.g., ESP-IDF or PlatformIO) to support the ESP32 and its Bluetooth/WiFi capabilities.

## Missing Source Code

The following required source code is missing from the repository:
1. **Bluetooth Classic Stack / Implementation:** For Joy-Con / Pro Controller emulation over wireless.
2. **Amiibo Implementation:** NFC/Amiibo data handling and transmission over Bluetooth.
3. **ESP32 Port / HAL:** Abstraction layer for ESP32 timers, GPIO, and peripherals, including physical button mappings (e.g., BTN A for pairing, BTN B for controller type switching).
4. **LittleFS & WebUI:** Web server, REST API, filesystem code, and a Switch-themed responsive WebUI framework.
5. **Display Drivers:** ST7789 LCD support for the M5StickC Plus 2 to show system statuses (Booting, Standby, Pairing, Connected, etc.).
