# 🧺 Smart Diagnostic Device (SDD) — Integrated ESP32 Wi-Fi Washing Machine Diagnostic System

> **SIH Innovation Project** | In-Cabinet Mounted IoT Diagnostic System with ESP32 Wi-Fi, WebSockets Telemetry & Relay-based Component Auto-Selection

[![Prototype Live](https://img.shields.io/badge/🌐%20Live%20Prototype-smartdiagnostic.netlify.app-blue?style=for-the-badge)](https://smartdiagnostic.netlify.app/)
[![Platform](https://img.shields.io/badge/Platform-ESP32--S3-orange?style=for-the-badge&logo=espressif)](https://www.espressif.com/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Prototype%20Ready-brightgreen?style=for-the-badge)]()

---

## 📌 Overview

The **Smart Diagnostic Device (SDD)** is an embedded IoT module permanently mounted **inside** the washing machine housing. It connects directly to all internal components and uses an **ESP32-S3 Wi-Fi + WebSockets** link to stream live telemetry to any connected laptop, tablet, or smartphone — **without opening the cabinet**.

> 🔗 **Live Prototype Demo:** [https://smartdiagnostic.netlify.app/](https://smartdiagnostic.netlify.app/)

---

## 🚀 Key Features

| Feature | Description |
|---|---|
| 📡 **ESP32-S3 Wi-Fi** | 2.4GHz wireless WebSockets / MQTT telemetry streaming |
| 🔌 **Dual Connectivity** | Wi-Fi Access Point mode + USB wired backup |
| ⚡ **Auto Component Select** | Relay Driver Module auto-switches between components |
| 📊 **Live Oscilloscope** | Real-time voltage, current, resistance & sensor readings |
| 🔒 **Galvanic Isolation** | Optocoupler-based isolation protecting ESP32 from 230V AC |
| 🎯 **99% Accurate Diagnosis** | Root-cause fault isolation to the exact failed component |
| 💰 **Cost Saving** | Prevents unnecessary PCB replacements (saves ₹7,500+) |

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────┐
│              WASHING MACHINE CHASSIS                    │
│                                                         │
│   ┌─────────────────────────────────────────────────┐   │
│   │           SMART DIAGNOSTIC DEVICE (SDD)         │   │
│   │                                                 │   │
│   │  ┌──────────┐   ┌──────────┐   ┌────────────┐  │   │
│   │  │ ESP32-S3 │◄──│  Relay   │──►│  Voltage / │  │   │
│   │  │  Wi-Fi   │   │  Driver  │   │  Current   │  │   │
│   │  │   MCU    │   │  Module  │   │  Module    │  │   │
│   │  └──────────┘   └──────────┘   └────────────┘  │   │
│   │       │              │               │           │   │
│   │  ┌────▼─────┐   ┌────▼─────┐   ┌────▼───────┐  │   │
│   │  │  Power & │   │ Protection│   │  Sensor    │  │   │
│   │  │  Comm    │   │ Isolation │   │  Interface │  │   │
│   │  │  Module  │   │  Circuit  │   │  Module    │  │   │
│   │  └──────────┘   └──────────┘   └────────────┘  │   │
│   └─────────────────────────────────────────────────┘   │
│         │          │         │         │         │       │
│       Motor    Heater    Inlet    Drain     Door        │
│                Elem.     Valve    Pump      Lock        │
└─────────────────────────────────────────────────────────┘
              ↕ Wi-Fi WebSockets / USB
      Laptop / Tablet / Smartphone Dashboard
```

---

## 🔧 Diagnosed Components

- 🔄 **Motor** — Drives drum + Hall/Tacho speed sensor
- 🌡️ **Heating Element** — Heats water + NTC thermistor sensor
- 💧 **Water Inlet Valve** — Controls water fill flow
- 📊 **Water Level / Pressure Sensor** — Detects water volume
- 🚿 **Drain Pump** — Removes water from the drum tub
- 🔐 **Door Lock Mechanism** — Interlock status check
- 🖥️ **Main PCB** — Basic power & signal relay tests
- 🔗 **Wiring / Connectors** — Continuity & harness integrity

---

## 🧩 SDD Internal Modules

### 1. ESP32-S3 Wi-Fi Controller
Main dual-core MCU with integrated 2.4GHz Wi-Fi and Bluetooth LE.
Runs the diagnostic firmware, WebSockets server, and relay control logic.

### 2. Voltage & Current Measurement Module
- **ZMPT101B** — AC Voltage transformer
- **ACS712** — Hall-effect current sensor
- Measures electrical health of each component under load

### 3. Sensor Interface Module
- NTC temperature thermistor (Heating Element)
- Hall / Tacho speed sensor (Motor RPM)
- Water pressure switch (Water Level)
- Door lock interlock status

### 4. Relay Driver Module (Component Auto-Selector)
Automatically switches relays to connect the target component to the measurement circuit — controlled by ESP32 firmware via diagnostic commands received over Wi-Fi.

### 5. Protection & Galvanic Isolation Circuit
- Optocoupler-based isolation
- Overvoltage & surge protection
- Separates hazardous 230V AC from 3.3V ESP32 logic

### 6. Power & Dual Communication Module
- Isolated 5V internal supply
- Wi-Fi WebSockets primary link
- USB backup data link

---

## 📂 Repository Structure

```
SDD-Smart-Diagnostic-System/
├── firmware/              # ESP32 Arduino/IDF firmware source code
│   ├── src/
│   ├── include/
│   └── platformio.ini
├── hardware/              # Schematics, PCB design files, Gerbers
│   ├── schematics/
│   ├── pcb/
│   └── bom/
├── webapp/                # Web dashboard (WebSockets client UI)
│   ├── index.html
│   ├── assets/
│   └── js/
├── docs/                  # Documentation, diagrams, presentations
│   ├── architecture/
│   ├── datasheets/
│   └── sih-presentation/
├── simulation/            # Fault simulation scripts and test cases
├── assets/                # Images, prototype photos, demo videos
├── tests/                 # Unit & integration tests
├── .github/               # GitHub Actions CI workflows
│   └── workflows/
├── LICENSE
├── CONTRIBUTING.md
└── README.md
```

---

## ⚡ Quick Start

### Prerequisites
- [PlatformIO](https://platformio.org/) or Arduino IDE with ESP32 board support
- ESP32-S3 development board
- Required hardware components (see [BOM](hardware/bom/))

### Firmware Upload
```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/SDD-Smart-Diagnostic-System.git
cd SDD-Smart-Diagnostic-System

# Build and flash firmware
cd firmware
pio run --target upload

# Monitor serial output
pio device monitor
```

### Web Dashboard
```bash
cd webapp
# Open index.html in browser or serve locally
python -m http.server 8080
# Visit http://localhost:8080
```

---

## 💡 How It Works

1. **SDD boots up** → ESP32 creates a Wi-Fi Access Point (`SDD_Diagnostic_AP`)
2. **Technician connects** laptop/phone to `SDD_Diagnostic_AP`
3. **Open Web Dashboard** → Live telemetry streams over WebSockets
4. **Select a component** → Relay Driver auto-switches to that component
5. **Run diagnostic** → ESP32 measures voltage, current, resistance, sensor signals
6. **View results** → Exact fault root-cause identified with repair recommendation

---

## 📊 Bill of Materials (BOM) Summary

| Component | Part | Purpose |
|---|---|---|
| MCU | ESP32-S3 | Wi-Fi + BLE + Main controller |
| Voltage Sensor | ZMPT101B | AC Voltage measurement |
| Current Sensor | ACS712 | AC Current measurement |
| Relay Module | 8-ch Relay Board | Component auto-selection |
| Isolation | PC817 Optocoupler | Galvanic isolation |
| Temp Sensor | NTC 10kΩ | Heater element monitoring |
| Power Supply | HLK-5M05 | Isolated 5V AC-DC |

> Full detailed BOM with costs: [hardware/bom/BOM.xlsx](hardware/bom/)

---

## 🛡️ Safety Notes

> ⚠️ **WARNING:** This device interfaces with 230V AC mains voltage.
> All hardware work must be performed by qualified electricians or electronics engineers.
> The galvanic isolation circuit MUST be verified before connecting to mains.

---

## 🏆 Project Context

This project was developed as part of the **Smart India Hackathon (SIH)** innovation challenge. The SDD addresses the problem of inaccurate washing machine fault diagnosis, which frequently leads to unnecessary replacement of expensive main PCBs when only a simple ₹350 component has failed.

---

## 🤝 Contributing

Pull requests are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

## 📄 License

This project is licensed under the **MIT License** — see [LICENSE](LICENSE) for details.

---

## 📞 Contact

> **Project:** Smart Diagnostic Device (SDD)  
> **Live Demo:** [https://smartdiagnostic.netlify.app/](https://smartdiagnostic.netlify.app/)  
> **Year:** 2026

---
*© 2026 Innovation Project — In-Cabinet Mounted SDD with ESP32 Wi-Fi & USB Telemetry*
