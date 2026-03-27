# 🚨 PNWC Car Security — Pro Edition (WiFi/LTE/GPS/SD/BLE)

This repository contains the **Ultimate Security Suite** for high-stakes vehicle monitoring. Built on the **LILYGO T-SIM7670G-S3 (ESP32-S3)** hardware, this system provides a multi-layered security net that remains functional even when WiFi is jammed or the vehicle is hidden in signal-dead zones.

## 🏗️ Core Architecture
The system consists of three primary layers working in sync:

1. **The Sensor (T-SIM7670G-S3):** - **Radar Presence:** Detects movement inside the cabin via **LD2410**.
   - **Vibration Sensing:** **SW-420** triggers on glass break, door slams, or towing.
   - **GPS Tracking:** Real-time location via active antenna.
   - **4G LTE Failover:** Automatic SMS alerts with Google Maps links if WiFi is unavailable.
   - **Black Box:** Local MicroSD logging for "Dead Zone" tracking.
   - **Fox-Hunt Beacon:** Private BLE iBeacon for close-range manual recovery.

2. **The Alarm (WROOM-32):**
   - **House Siren:** 12V Relay-controlled unit that triggers a high-decibel siren at your home base when an intruder is confirmed.
   - **Physical Kill-Switch:** Hardware button to manually silence the alarm locally.

3. **The Intelligence (Home Assistant & Frigate):**
   - **Frigate NVR:** Automatic high-priority driveway recording triggered by car sensors.
   - **Geofencing:** Automatic mode switching (Home/Away) based on GPS coordinates.

## 📡 Pro Capabilities
- **Failover Alerts:** Switches to **LTE SMS** instantly if WiFi is jammed or out of range.
- **Black Box Logging:** Records GPS breadcrumbs to the onboard TF card every 30 seconds—essential for recovery from parking garages or shipping containers.
- **Fox-Hunt Recovery:** Broadcasts a private Bluetooth signal detectable via RSSI "signal sniffing" for manual recovery in buildings.
- **Last Gasp Logic:** Bypasses power-save to send one final precise GPS location via SMS if the 18650 battery hits **3.55V**.
- **Stealth Mode:** Software-level "Blackout" of all onboard LEDs and screens to keep the tracker invisible.
- **Remote Recovery:** Integrated "Restart" command via Home Assistant to re-initialize the modem remotely.

## 📂 File Manifest
| File Name | Description |
| :--- | :--- |
| `car_security_cellular_s3.yaml` | **The Brain:** Complete firmware for the S3-SIM sensor unit. |
| `ha_automations.yaml` | **The Logic:** Full HA suite (Scheduling, Siren, Geofencing, Low Battery). |
| `house_siren_wroom32.yaml` | **The Noise:** Firmware for the house-side 12V siren controller. |
| `dashboard.yaml` | **The UI:** Lovelace code featuring Live Map, Battery Health, and Reset tools. |
| `WIRING_DIAGRAM.md` | **The Build:** Exact GPIO mapping for LD2410 and SW-420 sensors. |
| `INSTALLATION.md` | **Step-by-Step:** Guide for HA Helpers, SIM provisioning, and flashing. |
| `FOX_HUNTING.md` | **Recovery:** How to use BLE RSSI to find the car in a "Dead Zone." |
| `BLACKBOX_GUIDE.md` | **Recovery:** Instructions for retrieving breadcrumb data from the MicroSD. |
| `TROUBLESHOOTING.md` | **Support:** Solutions for GPS locks, LTE APN, and PMU issues. |
| `antenna_setup.md` | **Hardware:** Mounting guide for GPS puck and LTE antennas. |
| `zigbee_kill_button.yaml` | **Remote:** Config for physical Zigbee disarm/panic buttons. |
| `frigate_nvr_integrate.md` | **Video:** Integration guide for Frigate NVR recording. |

## 🛠️ Quick Hardware Setup
1. **Flash Sensor:** Use `car_security_cellular_s3.yaml` via ESPHome.
2. **Antennas:** Connect the GPS puck to the IPEX/U.FL port and route to the windshield glass.
3. **Power:** Insert a high-quality 18650 cell into the integrated holder.
4. **SIM/APN:** Ensure your carrier's APN is set in the YAML and the SIM PIN is disabled.

---
**Disclaimer:** This project is for personal security and asset recovery assistance. Always contact local law enforcement with GPS data during a theft; do not attempt recovery alone.
