# 🚨 PNWC Car Security — Pro Edition (Cellular/GPS)

This repository contains the **Ultimate Security Suite** for vehicle monitoring, using the **LILYGO T-SIM7670G-S3**.

## 🏗️ Core Architecture
1. **The Sensor (T-SIM7670G-S3):** Radar presence + Vibration sensing + GPS Tracking + 4G LTE Failover.
2. **The Alarm (WROOM-32):** 12V Relay house siren controller.
3. **The Intelligence:** Home Assistant & Frigate NVR integration.

## 📡 Upgraded Capabilities
- **Failover Alerts:** If WiFi is jammed or the car leaves your property, the unit automatically switches to **LTE SMS** alerts with a Google Maps link.
- **Dynamic Power:** 18650 management with a "Last Gasp" GPS ping before battery depletion.
- **Stealth Mode:** Software-killed LEDs and screen for covert tracking.

## 📂 File List
- `car_security_cellular_s3.yaml`: Pro firmware.
- `ha_automations.yaml`: Full logic suite (Scheduling, Siren, GPS Geofencing).
- `house_siren_wroom32.yaml`: House siren controller firmware.
- `antenna_setup.md`: Critical GPS/LTE mounting guide.
