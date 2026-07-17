# Development Roadmap

This document outlines the milestones for transforming the existing AVR-based USB firmware into a production-quality ESP32-based Bluetooth firmware for the M5StickC Plus 2.

## Milestones

### v0.1: Baseline
- compile (existing AVR codebase)
- documentation (ARCHITECTURE.md, ROADMAP.md)
- cleanup (identify and document what can be reused)

### v0.2: Platform Migration
- M5StickC Plus 2 support (ESP-IDF/PlatformIO setup)
- LCD initialization and basic drawing (ST7789 display)

### v0.3: File System
- LittleFS integration
- Directory structure setup (`/amiibos/`, `/config/`, `/www/`)
- Store/load settings as JSON

### v0.4: Web Server
- Basic web server setup
- Responsive WebUI (Mobile and Desktop)
- Dashboard (controller status, battery, IP)
- Settings page (WiFi, factory reset, etc.)

### v0.5: Amiibo Implementation
- Amiibo page on WebUI (upload, delete, rename, select active dump)
- Implementation of Amiibo logic and spoofing

### v0.6: Controller Implementation
- Bluetooth Classic support for Joy-Con/Pro Controller emulation
- WebSocket controller backend
- Controller page on WebUI (Virtual controls: A, B, X, Y, D-pad, L, R, ZL, ZR, Plus, Minus, Home, Capture, analog sticks)

### v0.7: Over-The-Air (OTA) Updates
- OTA update functionality
- Settings page integration for OTA

### v1.0: Production Release
- Display polish (Booting, Pairing, Waiting, Connected, Disconnected, Sending Amiibo, Error, Battery, IP, Current Amiibo)
- Final testing and bug fixes
- Production release
