# Electrium Mobility — E-Bike Display + VESC UART Firmware

Firmware for an Electrium Mobility e-bike dashboard/controller that reads telemetry over **VESC UART** and renders ride/battery information on a **TFT display** (ESP32).

Safety note: This repository is for a student design team project. Test on a stand, verify wiring, and use appropriate fusing/current limits before riding.

## What it does
- Connects to a VESC over UART
- Reads key telemetry (speed/RPM, battery voltage, current draw, etc.)
- Displays status on a TFT screen (with Electrium branding/assets)
- Battery indicator / icons

## Hardware (typical)
- Microcontroller: **ESP32 / Arduino-compatible MCU** (depends on your build)
- Display: TFT supported by **TFT_eSPI**
- Motor controller: **VESC** (UART enabled)
- Wiring: UART TX/RX + GND between MCU and VESC (plus display SPI wiring)

## Repository layout (high level)
- `*.ino` — main firmware sketch (entry point)
- `VescUart*.h`, `datatypes.h` — VESC UART communication + types
- `TFT_eSPI.h`, `PNGdec.h` — display + image decoding support
- `battery.h`, `electrium_logo.h` — UI assets

### Software
- **Arduino IDE** (or **PlatformIO**)
- USB drivers for your board (if required)

### Libraries / dependencies
- Install equivalent libraries via **Arduino Library Manager**:

## Build + Upload (Arduino IDE)
1. Open Arduino IDE
2. **File → Open** and select the main `*.ino` sketch
3. Select your **Board** and **Port**
4. If using **TFT_eSPI**:
   - Configure the display driver + pins in `TFT_eSPI`’s `User_Setup.h`
   - Ensure SPI pins match your wiring
5. Click **Verify** (✓), then **Upload** (→)

## Configuration checklist
Before flashing, confirm:
- **VESC UART baud rate** (must match firmware settings)
- **Correct UART pins** on the MCU (TX/RX swapped is a common failure)
- **Display driver + resolution** in TFT configuration
- Any scaling constants (wheel circumference, units, smoothing)

## Troubleshooting
- **Blank screen**: wrong TFT driver or SPI pins; recheck `TFT_eSPI` setup.
- **No VESC data**: wrong UART pins/baud rate; confirm common ground; verify VESC UART is enabled.
- **Garbled UI / wrong colors**: incorrect color order (RGB/BGR) or display init config.

Note: The microcontroller used in this project is an ESP32-105

- Electrium Mobility (UW student design team)
- VESC community / Vedder’s VESC ecosystem
