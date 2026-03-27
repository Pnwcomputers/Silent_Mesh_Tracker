# 🚨 PNWC Car Security — Pro Edition (Cellular/GPS/BlackBox)

This repository contains the **Ultimate Security Suite** for high-stakes vehicle monitoring. Built on the **LILYGO T-SIM7670G-S3**, this system provides a multi-layered security net using WiFi, 4G LTE, GPS, and local SD logging.

## 🏗️ Core Architecture
The system consists of three primary layers working in sync:

1. **The Sensor (T-SIM7670G-S3):** - **Radar Presence:** Detects movement inside the cabin via LD2410.
   - **Vibration Sensing:** SW-420 triggers on glass break or towing.
   - **GPS Tracking:** Real-time location with windshield-mounted active antenna.
   - **4G LTE Failover:** SMS alerts with Google Maps links if WiFi is unavailable.
   - **Black Box:** Local MicroSD logging for "Dead Zone" tracking.

2. **The Alarm (WROOM-32):**
   - **House Siren:** 12V Relay-controlled unit that triggers a high-decibel siren at your home base when an intruder is confirmed.
   - **Physical Kill-Switch:** Hardware button to manually silence the alarm.

3. **The Intelligence (Home Assistant & Frigate):**
   - **Frigate NVR:** Automatic driveway recording triggered by car sensors.
   - **Geofencing:** Automatic mode switching (Home/Away) based on GPS coordinates.

## 📡 Pro Capabilities
- **Failover Alerts:** If WiFi is jammed or the car leaves your property, the unit automatically switches to **LTE SMS** alerts.
- **Black Box Logging:** Records GPS breadcrumbs to the onboard TF card every 30 seconds—essential for recovery from parking garages or rural areas.
- **Last Gasp Logic:** Bypasses power-save to send one final precise GPS location via SMS if the 18650 battery drops to 3.4V.
- **Stealth Mode:** Software-level "Blackout" of all onboard LEDs and screens to keep the tracker hidden during a theft.
- **Remote Recovery:** Integrated "Restart" command via Home Assistant to re-initialize the modem if it hangs in a low-signal area.

## 📂 File Manifest
| File Name | Description |
| :--- | :--- |
| `car_security_cellular_s3.yaml` | **The Brain:** Full firmware for the S3-SIM sensor unit. |
| `ha_automations.yaml` | **The Logic:** Complete Home Assistant suite (Scheduling, Siren, Geofencing). |
| `house_siren_wroom32.yaml` | **The Noise:** Firmware for the house-side 12V siren controller. |
| `dashboard.md` | **The UI:** Lovelace dashboard code featuring Live Map and controls. |
| `INSTALLATION.md` | **Step-by-Step:** Guide for helpers, SIM provisioning, and flashing. |
| `TROUBLESHOOTING.md` | **Support:** Solutions for GPS locks, LTE APN, and power issues. |
| `antenna_setup.md` | **Hardware:** Critical mounting guide for GPS puck and LTE antennas. |
| `BLACKBOX_GUIDE.md` | **Recovery:** Instructions for retrieving data from the MicroSD card. |
| `zigbee_kill_button.yaml` | **Remote:** Config for physical Zigbee disarm/panic buttons. |
| `frigate_nvr_integrate.md` | **Video:** Integration guide for Frigate NVR recording. |

## 🛠️ Quick Hardware Setup
1. **Flash Sensor:** Use `car_security_cellular_s3.yaml` via ESPHome.
2. **Antennas:** Connect the GPS puck to the IPEX/U.FL port and route to the windshield.
3. **Power:** Insert a high-quality 18650 cell into the integrated holder.
4. **Mesh/SIM:** Ensure your APN is set in the YAML and your SIM PIN is disabled.

---
**Disclaimer:** This project is for personal security and asset recovery assistance. Always contact local law enforcement with GPS data during a theft; do not attempt recovery alone.
