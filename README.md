# HKU ROVER Team Prototype

Rudimentary all-in-one Power Distribution Board (PDB) and logic carrier designed for small 6-wheel rovers with a 4-DoF robotic arm.

![PCB View](https://github.com/user-attachments/assets/a0ab9e0c-661f-42ac-b896-66963318b3d0)

## 🚀 Key Specifications
- **Power Input:** 6S LiPo (22.2V nominal, 25.2V max) via XT60.
- **Power Tree:**
  - **12V @ 30A:** High-current rail for BLDC/DC Main Drive motors.
  - **7.5V @ 5A:** Dedicated HV Servo rail (Optimized for 7.4V nominal servos).
  - **5.1V @ 5A:** Stabilized logic power for Pi 5 and peripherals. 3V3 Using Pico's built-in regulator.
- **Processing:**
  - Dual-core architecture: Raspberry Pi 5 (Thinking) + Pi Pico 2 (Doing).
  - High-speed UART communication bridge.
- **Actuation & Sensing:**
  - 6x PWM Encoder inputs.
  - 6x PWM-Controlled DC motor driver headers.
  - 4x High-Torque Servo ports with localized bulk capacitance.
  - Integrated 6S Battery Fuel Gauge (Voltage Divider + ADC).

## 🛡️ Protection Features
- **Reverse Polarity Protection:** High-side MOSFET (SUD50P10) circuit.
- **Logic Firewall:** Schottky isolation and TVS crowbar protection for 5V rails.
- **EMI Suppression:** RC low-pass filters on all encoder inputs and ferrite beads on logic lines.
- **Thermal Design:** Optimized for 2oz copper with solid-pour high-current paths.

## 🛠 Hardware Setup
### Battery Monitor Calibration
The internal voltage divider uses a **100kΩ (Top)** and **13.7kΩ (Bottom)** 1% precision resistor set. 
- **Max Input:** 25.2V
- **ADC Output:** ~3.03V
- **Safety Factor:** 10% headroom to prevent Pico ADC overvoltage.

### Communication
The Pi 5 and Pico 2 communicate via UART.
- **Baud Rate:** 115200 (Default)
- **Pinout:** Pi GPIO 14/15 <-> Pico GPIO 0/1.

## ⚠️ Assembly Warnings
1. **Thermal Reliefs:** High-current pads (XT60, Regulators, Motors) have thermal reliefs **DISABLED**. Use a high-power chisel-tip iron and pre-heat the board to 100°C for assembly.
2. **Capacitors:** Ensure C1 & C2 (2000uF) is rated for 50V minimum.
3. **USB Isolation:** Always use a USB isolator when debugging the Pi/Pico while the main battery is connected to prevent back-powering your PC.

## 📜 License
This project is released under GNU General Public License v3.0. Designed by **Ilo Japar / HKU ROVER Team**.
