# 🚨 PNWC Car Security — Upgraded Cellular/GPS Edition

This is the **Pro Version** of the PNWC Car Alarm. It keeps all original security features (Radar, Vibration, Home Assistant Integration) but upgrades the hardware to the **LILYGO T-SIM7670G-S3**.

## 🚀 Key Upgrades
- **Triple-Mode Connectivity:** Uses Home Assistant (WiFi) as primary, falls back to **LTE SMS** if WiFi is jammed or out of range.
- **Autonomous GPS:** Built-in GPS tracking for real-time recovery.
- **Improved Power:** Integrated 18650 battery management via the AXP2101 PMU.

## 🏗️ Hardware Pinout
- **Vibration (SW-420):** GPIO 1
- **Radar (LD2410):** TX: GPIO 3 | RX: GPIO 2
- **Modem/GPS:** Internal (GPIO 17/18/13)



## 🛠️ Usage
This unit functions exactly like the standard build in Home Assistant, but will "fail-over" to Cellular alerts if the car leaves your property.
