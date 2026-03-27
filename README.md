# 🚨 ESP32 Security System — Home Assistant Distributed Alarm System

<p align="center">
  <img src="esp32alarm.png" width="800" alt="PNWC Car Alarm Project Collage">
</p>

A professional-grade, distributed vehicle security system. This project bridges a battery-powered mobile sensor unit with a mains-powered house siren using Home Assistant and ESPHome.

---

## 🏗️ System Architecture

1.  **The Sensor (Car Unit):** A **LILYGO T-Display S3** with **LD2410C Human Presence Radar** and an **SW-420 Vibration Sensor**. Automatically charges via a switched USB source; enters deep sleep 30 seconds after the car is parked to preserve LiPo health.
2.  **The Brain (Home Assistant):** Manages global logic, time-of-day scheduling, and **Frigate NVR** camera integration.
3.  **The Alarm (House Unit):** A headless **ESP32-WROOM-32** controlling a **12V DC Siren** via a 5V Relay. Features a high-reliability hardwired "Wall Kill" button.

---

## 🛒 Parts List & Shopping Links

### 🚗 Unit 1: Car Sensor (Presence & Vibration)
* **ESP32 Microcontroller:** [LILYGO T-Display S3](https://a.co/d/0gzxxSAu) (Dual-core ESP32-S3 with 1.9" LCD)
* **Presence Sensor:** [LD2410C mmWave Radar](https://a.co/d/06LWMXAf) 
* **Vibration Sensor:** [SW-420 Motion Sensor](https://a.co/d/02E32HKW)
* **LiPo Battery:** [3.7V 2000mAh LiPo Battery](https://a.co/d/0hEXVDKv) (JST 1.25mm)
* **Car Power Interface:** [12V to USB-C Step-Down Converter (Hardwired)](https://a.co/d/03p8YRCy) OR [Low-Profile Cigarette Lighter USB Adapter](https://a.co/d/03B6qD6h)
* **USB Cable:** [90-Degree Right Angle USB-C Cable](https://a.co/d/06fP6O8w)

### 🏠 Unit 2: House Siren (Relay Controlled)
* **ESP32 Microcontroller:** [ESP32-WROOM-32 DevKit](https://a.co/d/05z59KT6) (Standard 30-pin)
* **5V Relay:** [5V One-Channel Relay Module](https://a.co/d/0aWROudj) (Opto-isolated)
* **12V Siren:** [12V DC Wired Indoor/Outdoor Siren](https://a.co/d/06rncyCy)
* **Siren Power:** [12V 2A DC Power Supply Adapter](https://a.co/d/0imZnCsy)
* **Siren Kill Switch:** [Push Button Switch](https://a.co/d/031p9keo) (For "Wall Kill" extension)

### 🛠️ Tooling & Connectivity
* **Software:** [Home Assistant](https://www.home-assistant.io/) with **ESPHome** add-on.
* **Zigbee Gateway:** [SONOFF Zigbee 3.0 USB Dongle](https://a.co/d/08299SBs) OR [Home Assistant Connect ZB-2](https://a.co/d/0iVhmzxv).
* **Wiring:** [22AWG Hook-up Wire](https://a.co/d/0aoN3zOD).

---

## 🔌 Master Wiring Reference

> ⚠️ **Note:** The House Siren pins have been moved to "Safe Pins" (GPIO 13/14) to prevent the WROOM-32 from entering a boot-loop or strapping pin error.

### 🏠 Unit 2: House Siren (WROOM-32 DevKit)
| Component | ESP32 Pin | Logic / Notes |
| :--- | :--- | :--- |
| **Relay VCC** | **5V / VIN** | Powers the relay coil |
| **Relay GND** | **GND** | Common ground |
| **Relay IN** | **GPIO 13** | Trigger (Safe pin) |
| **Wall Kill Button** | **GPIO 14** | Connect to GND to trigger |
| **Status LED** | **GPIO 2** | Internal Blue LED (Pulses on Alarm) |

### 🚗 Unit 1: Car Sensor (LILYGO T-Display S3)
| Component | ESP32 Pin | Logic / Notes |
| :--- | :--- | :--- |
| **Vibration (SW-420)** | **GPIO 1** | **Hardware Wake-up Pin** |
| **Radar TX (LD2410)** | **GPIO 3** | ESP RX ← Sensor TX |
| **Radar RX (LD2410)** | **GPIO 2** | ESP TX → Sensor RX |
| **Battery Voltage** | **GPIO 4** | 100k/100k Voltage Divider |
| **USB Power Sense** | **GPIO 43** | **Internal** (Auto-Sleep Logic) |
| **LCD Backlight** | **GPIO 38** | **Internal** (Screen Dimming) |

---

## 🤖 Advanced Features

### 📡 Intelligent Power Management
The Car Unit is designed for **Zero-Maintenance Operation**:
* **Ignition Sync:** When the car starts, USB power is detected (GPIO43), deep sleep is disabled, and the battery begins charging.
* **Parked Security:** 30 seconds after the car is turned off, the unit enters Deep Sleep. It remains dormant until the SW-420 vibration sensor triggers a hardware wake-up.

### 🔘 Triple-Layer Kill Switch
1. **Local:** On-board status LED and software logic.
2. **Hardwired:** GPIO14 "Wall Kill" button (WROOM-32 unit).
3. **Mobile:** Actionable notifications via Home Assistant.

---

## 🧪 Testing & Commissioning

### 1. Sensor Calibration
* **Radar (LD2410C):** Tune Gate Sensitivity in ESPHome so movement outside the glass is ignored.
* **Vibration (SW-420):** Adjust the onboard potentiometer clockwise to prevent heavy rain from triggering the alarm.

### 2. Power Logic Verification
* **USB Detect:** Plug in USB-C; verify logs show `USB Power Connected - Disabling Deep Sleep`.
* **Sleep Entry:** Unplug USB-C; screen should turn off after 30 seconds.
* **Wake Trigger:** Shake the device while unplugged; it should boot and connect to WiFi immediately.

### 3. Siren Safety Check
* **Relay Logic:** Listen for the physical *click* of the relay when toggling the switch in HA.
* **Auto-Timeout:** Trigger the siren and verify it shuts off automatically after 60 seconds.

---

## ⚠️ Safety Note
The house unit switches **12V DC only**. Do not attempt to switch mains AC (120V/240V) directly with the relay modules provided in this project. All 12V power should be fused appropriately.
