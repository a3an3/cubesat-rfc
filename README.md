# CubeSat RFC – Radio Communication Board Web Interface

Firmware and web interface for the **radio frequency communication (RFC) board**
of a university microsatellite (CubeSat) project at the I. Physikalisches Institut,
Justus Liebig University Giessen (2020–2022).

An ESP32 on the RFC board hosts a web interface that ground-station operators use to send
telecommands to the satellite's modules, watch telemetry and download logs.

## Features

**Web interface (served directly from the ESP32)**
- Asynchronous web server, reachable at `http://cubesat.local/` via mDNS
- Login-protected access
- Terminal-style command line with history of recent commands, no page reload
- Live graphs for sensor data
- Module configuration in the browser, persisted across restarts
- Download buttons for all log files
- Lightweight fallback page (`index_lite.html`)

**Firmware (C/C++ on ESP32)**
- SPI communication with the satellite's MCU: send and receive functions for every module
- Initialization table per module (connection type), stored in SPIFFS
- Logging of all SPI packets and sensor data with timestamps
- Busy signal pin while the RFC is processing, workload measurement from pin on/off times
- XML endpoint exposing the last command and last initialization

**Hardware**
- Soldered and integrated two ESP32 boards and the MCU; built the flight model and flight spare
- Schematic: `Schematic DS-RFC v2021b.pdf`

## Tech stack

ESP32 (WROOM-32E) · C/C++ · Arduino framework · ESPAsyncWebServer · SPIFFS · SPI · HTML/CSS/JavaScript

## Repository structure

| Path | Purpose |
|---|---|
| `RFC/` | ESP32 firmware and web interface sources |
| `Dokumentation.md` | Detailed technical documentation (German) |
| `Schematic DS-RFC v2021b.pdf` | Board schematic |
| `esp32-wroom-32e_…pdf` | ESP32 datasheet |
| `Wifi_Server.bat` | Helper script for local setup [what it does] |

## Possible improvements

- Module health check after initialization, shown in a "Modules" tab
- Turn modules on/off from the web interface
- Module presets next to the command line for easier command handling
- Remove leftover debug output

---

Built by [Adrian Setka](https://www.linkedin.com/in/…) as part of the RF communication team.
