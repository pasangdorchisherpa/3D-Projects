# Lantern (HomeAssistant / ESP-32 / Complete PCB + Schematics)

This document describes the current architecture and design direction of the **Smart Lantern** project.

The goal of this build is a **portable, battery-powered lantern** that works reliably as a standalone device, while optionally integrating with **Home Assistant** when connected to the network.

---

## Design Goals

- Fully functional **offline** (no Wi-Fi required)
- **Battery powered**, rechargeable via USB-C
- Simple **physical controls** for everyday use
- Optional **smart control** via Home Assistant
- Low-cost, modular, and easy to iterate

The lantern is designed so that **core lighting functionality does not depend on the ESP32**. The microcontroller enhances the experience but is not required for basic operation.

---

## Power Architecture

### Battery System
  - **2× 18650 Li-ion cells in parallel (1S2P)**
  - Nominal voltage: 3.7 V

### Power Management Module
  - **Portable 3.7V → 5V boost converter**

  - Integrated:
  - Battery Management System (BMS)
  - Over-charge / over-discharge protection
  - Short-circuit protection
  - USB-C charging interface
  - Power-path (pass-through) support

#### Behavior
- When USB-C is plugged in:
  - Lantern runs from USB power
  - Batteries charge simultaneously
- When USB-C is unplugged:
  - Lantern seamlessly switches to battery power
- A physical power switch disconnects the lantern load while allowing charging to continue

The lantern electronics always see a **stable 5V rail**, regardless of power source.

---

## Lighting System

- **5V COB LED strip (1 meter)**
  - High efficiency
  - Even, diffuse light output
  - Powered directly from the 5V system rail

### Dimming
- LED brightness is controlled via:
  - **N-channel logic-level MOSFET**
  - PWM signal from the ESP32
- A **100Ω gate resistor** and **100kΩ pulldown** ensure:
  - Clean switching
  - LED remains off during ESP32 boot/reset

---

## Physical Controls (Offline-First)

### Potentiometer
- 10k potentiometer connected to:
  - ESP32 ADC input
  - 3.3V and GND reference
- Allows:
  - Manual brightness control
  - Full functionality even when Wi-Fi is unavailable

### Power Switch
- Hard on/off switch placed **after the power module**
- Cuts power to:
  - ESP32
  - LED system
- Does **not** interfere with battery charging

---

## Control & Compute

### Microcontroller
- **ESP32 DevKit V1**
  - Powered from 5V system rail
  - Uses onboard 3.3V regulator
  - Provides PWM, ADC, and Wi-Fi

The ESP32 is intentionally **non-critical**:
- If it crashes or is powered off:
  - The lantern can still operate manually
- This improves reliability and user trust

---

## Smart Integration (Planned)

### Home Assistant
The lantern will integrate with **Home Assistant** using ESPHome.

Planned features:
- On/off control from the web UI
- Brightness control
- State synchronization with the physical potentiometer
- Optional automations (time-based, scenes, etc.)

Key principle:
> **Physical control always works first. Smart control mirrors it.**

The potentiometer remains authoritative, ensuring:
- No lock-out
- No dependency on network availability

---

## Design Philosophy Summary

- **Offline-first, smart-enhanced**
- Simple power path
- Easy to repair or upgrade

This architecture prioritizes reliability, safety, and usability over unnecessary complexity.

---

## Next Steps
- Finalize enclosure and internal mounting
- ESPHome firmware implementation
- Home Assistant entity mapping
- Runtime and thermal testing

  
![fda737fc-9e3a-4ccf-86c7-231cff46beaa](https://github.com/user-attachments/assets/42cc87c5-7644-4d1e-bc90-df04cd24d75d)

<img width="1373" height="852" alt="Screenshot 2026-01-18 214510" src="https://github.com/user-attachments/assets/8ab49a2e-16d8-458f-82b9-6cd735c169cd" />

<img width="848" height="840" alt="123333" src="https://github.com/user-attachments/assets/dd2f99fa-3f82-4b20-88ea-64ee83bfc2b3" />

