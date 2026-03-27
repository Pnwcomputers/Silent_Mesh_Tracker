# 🛰️ PNWC Car Security — Silent Mesh Tracker Fork

This specialized fork is designed for the **LILYGO T-SIM7670G-S3**. It provides passive, high-stealth vehicle tracking via your existing **Meshtastic** network.

## ✨ Key Features
- **Dynamic Duty Cycling:** High-speed 30s tracking while moving; 15m pulses while parked.
- **Stealth Mode:** Disables all onboard LEDs and screen backlight via software.
- **Last Gasp Logic:** Automatically sends one final precise GPS location to the mesh and enters safety-shutdown if the 18650 battery hits **3.4V**.
- **Meshtastic Native:** No WiFi required; car appears as a standard node on your mesh map.

## 🔌 Quick Wiring
- **Vibration (SW-420):** Pin GPIO 1
- **Mesh Connection:** ESP TX (43) -> Mesh Node RX | ESP RX (44) -> Mesh Node TX
- **Power:** Integrated 18650 Holder (use high-quality protected cells).

[Refer to antenna_setup.md for windshield mounting instructions.]
