# 3D-Projects

---

# Desk Riser & Smart Lantern Projects

This repository contains two related but independent projects:
- A **completed 3D-printed desk riser**
- A **work-in-progress smart lantern**

Each project focuses on practical, low-cost design with an emphasis on reliability and iteration.

---

# ✅ Desk Riser (Completed)

A minimalist, sturdy desk riser designed for FDM 3D printing.  
Optimized for low material usage while safely supporting a **4–5 kg monitor**.

## Features
- Designed for **PLA / PLA+**
- Lightweight with structural cutouts
- No supports required
- Optimized for **FDM strength** (printed upright)
- Suitable for common desktop monitors

## Recommended Print Settings
These settings balance **cost, print time, and strength**:

- Nozzle: 0.4 mm  
- Layer height: 0.28 mm  
- Walls: 3 wall loops  
- Infill: 15% gyroid  
- Top/Bottom layers: 6 / 6  
- Orientation: Print upright as modeled  
- Supports: Not required  

### Print Estimates
- Material use: ~475–500 g  
- Print time: ~9 hours (Bambu-class printer)

## Load Capacity
Designed to comfortably support:
- Typical desktop monitors
- Static vertical loads in everyday desk use

## Files
- `DeskRiserMain.stl`

## Notes
- Do not scale non-uniformly
- For best strength, avoid printing on its side or upside down
- Rubber feet are recommended to reduce point loading and improve grip

---

# Smart Lantern (Work in Progress)

A portable, battery-powered lantern designed to work reliably **offline**, with optional smart control via **Home Assistant**.

This project is currently under active development and subject to iteration.

## Planned Architecture

### Power System
- **2× 18650 Li-ion cells in parallel (1S2P)**
- **3.7V → 5V boost converter** with:
  - Integrated BMS
  - USB-C charging
  - Power-path (pass-through) support

The lantern operates seamlessly from USB power when plugged in and automatically switches to battery power when unplugged.

### Lighting
- **5V COB LED strip (1 meter)**
- Driven via an **N-channel logic-level MOSFET**
- PWM dimming for efficient brightness control

### Controls
- **Potentiometer** for local, offline brightness control
- **Hard power switch** to fully disable the system while allowing battery charging

### Compute
- **ESP32 DevKit V1**
- Non-critical to basic operation (offline-first design)
- Enhances functionality when enabled

## Smart Integration (Planned)
- Integration with **Home Assistant** via ESPHome
- Web-based on/off and brightness control
- Physical controls remain authoritative

## Project Status
- Electrical architecture defined
- PCB design and layout completed
- Firmware development (X)
- Enclosure design and final assembly (X)
- Home Assistant integration (X)

---

## License
These designs are provided for **personal use**.  
You may print, modify, and experiment with them for your own projects.  
