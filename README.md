# Low-Power Wi-Fi Communication on STM32/ESP32
A C++/C-based embedded system that enables ultra-low-power Wi-Fi communication using RTOS, deep sleep, and secure networking. Ideal for battery-powered, event-driven IoT devices.

## Features
- 🔋 Deep sleep & wake-on-interrupt
- 📶 Wi-Fi communication via MQTT or CoAP
- 🔐 Secure OTA firmware updates
- 📉 Power profiling + real-time diagnostics
- 🛠️ Built with CMake for portability

## Project Structure
```text
stealthlink/
├── .github/
│   ├── workflows/                # CI pipelines for builds/tests
│   └── ISSUE_TEMPLATE.md
├── docs/
│   ├── architecture.md           # Diagrams, state machine, Wi-Fi stack
│   └── power-analysis.md         # Benchmarks on sleep, active power
├── firmware/
│   ├── CMakeLists.txt            # Top-level CMake project
│   ├── src/
│   │   ├── main.c                # RTOS init, main app loop
│   │   ├── sensors.c             # Sensor polling abstraction
│   │   ├── wifi_comm.c           # Wi-Fi (ESP32/HaLow stack)
│   │   └── ota_update.c          # Secure firmware update logic
│   └── include/
│       └── *.h                   # Headers for all modules
├── tools/
│   ├── test_server.py            # Python MQTT/CoAP testing server
│   ├── power_profiler.sh         # Script to log consumption stats
│   └── ota_pusher.py             # Tool to push OTA firmware
├── configs/
│   ├── stm32_nucleo.cfg          # Board-specific settings
│   └── esp32_defconfig           # Optional if using ESP-IDF
├── LICENSE
├── README.md
└── CONTRIBUTING.md
```

## System Architecture
### 1. Hardware Components
| Component | Purpose |
|:-----|:-----|
| MCU: STM32 (e.g., Nucleo-U575ZI-Q) or ESP32 | Main processor running RTOS |
| Wi-Fi Module: ESP8266/ESP32 (if using STM32) | Handles Wi-Fi connectivity |
| Sensors: TMP36 (temperature), phototransistors, tilt sensor | Provides real-world data |
| Battery: 9V or Li-ion (with power regulator) | 	Powers the system for low-power profiling |
| Power Monitoring IC (optional) | Tracks power consumption for optimizations |

### 2. Software Architecture
#### RTOS-Based Multi-Threaded System
  - Task 1: Sensor Data Acquisition (periodic)
  - Task 2: Wi-Fi Communication (MQTT/CoAP over Wi-Fi HaLow)
  - Task 3: Power Management (low-power modes, sleep states)
  - Task 4: OTA Update Handling (firmware updates over Wi-Fi)

#### Software Components
  - Embedded C/C++ with ZephyrOS
  - CMake Build System (cross-compilation for STM32)
  - Wi-Fi Stack (ESP-IDF or LWIP on STM32)
  - Debugging & Logging with GDB, Wireshark, and UART logs

## Getting Started
- STM32 + ESP8266 or ESP32 standalone
- Zephyr OS compatible
- Built with GCC + CMake
