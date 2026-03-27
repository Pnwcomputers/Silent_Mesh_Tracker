# 🛠️ PNWC Car Security: Troubleshooting Guide

### 🛰️ GPS & Tracking Issues
**Issue: GPS coordinates show `0.0, 0.0`.**
* **Cold Start:** The first power-on takes up to 10 minutes for a 3D Lock.
* **Metal Obstruction:** Ensure the GPS puck is in the windshield, not buried under the metal dashboard frame.

### 📶 Cellular & SMS Issues
**Issue: The unit won't connect to LTE.**
* **APN Incorrect:** Verify your carrier's APN in the YAML.
* **SIM PIN Lock:** Disable the SIM PIN using a smartphone before inserting it into the S3.

### 🔄 Remote Recovery & Resets
**Issue: The device is unresponsive.**
* **Soft Reset:** Use the **"Remote Reset Tracker"** button on your Home Assistant Dashboard. This reboots the ESP32 and re-initializes the Modem.
* **Hard Reset:** Disconnect battery and USB for 10 seconds.
