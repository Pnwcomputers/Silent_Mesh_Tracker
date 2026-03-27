# 🛠️ PNWC Car Security: Troubleshooting Guide

If your upgraded system is not behaving as expected, use this guide to diagnose the most common issues with the **T-SIM7670G-S3** hardware and Home Assistant integration.

---

### 🛰️ GPS & Tracking Issues

**Issue: GPS coordinates show `0.0, 0.0` or `Unknown`.**
* **Cold Start:** The first time the unit powers on, it can take up to 10 minutes to download the "Almanac" (satellite data). Leave the car in an open area during this time.
* **Antenna Connection:** The U.FL connector is fragile. Ensure it is snapped firmly onto the "GPS" port (not the LTE port).
* **Active Antenna Power:** Ensure your antenna is "Active." If you are using a passive sticker antenna, it may not work inside a vehicle.
* **Metal Obstruction:** If the GPS puck is under the metal roof or a heavy dashboard support beam, it will fail. Move it to the corner of the windshield glass.

---

### 📶 Cellular & SMS Issues

**Issue: The unit won't connect to LTE or send SMS.**
* **APN Incorrect:** This is the #1 cause of failure. Check your SIM provider's documentation. Common APNs: `hologram`, `fast.t-mobile.com`, `wholesale`, `h2g2`. 
* **SIM PIN Lock:** If your SIM card requires a PIN to unlock, the modem will fail to register. Put the SIM in a phone first and disable the PIN lock in settings.
* **Power Spikes:** If the modem resets when trying to send a text, the battery is likely low or poor quality. Ensure you are using a high-discharge 18650 cell.
* **Signal Strength:** Check the `sensor.car_security_upgraded_gps_signal` in Home Assistant. If it is below -100dBm, you may need a better LTE antenna.

---

### 🤖 Home Assistant & Automation Issues

**Issue: The House Siren doesn't trigger when the car is shaken.**
* **API Check:** Ensure both the Car S3 and the House WROOM-32 show as "Online" in the ESPHome Dashboard.
* **Helper State:** Check if `input_boolean.car_alarm_armed` is actually **ON**. The automations will not run if it is off.
* **Maintenance Mode:** Ensure `input_boolean.car_alarm_maintenance` is **OFF**.
* **Entity Names:** If you changed the name of your ESPHome nodes during flashing, the automation YAML may be looking for the old entity names. Check your entities under **Settings > Devices**.

---

### 🔋 Power & Battery Issues

**Issue: The device keeps rebooting or "Brownout" occurs.**
* **AXP2101 Limits:** The S3-SIM board uses a PMU. If you are powering via USB, ensure the port provides at least 1.5A. 
* **Battery Polarity:** Double-check that the 18650 is inserted correctly. Most LILYGO boards have polarity markings on the PCB; reversing it can destroy the PMU.
* **Deep Sleep Loop:** If the device is stuck in sleep, plug it into USB power. The `on_boot` logic is designed to stay awake while charging.

---

### 📹 Frigate & Camera Issues

**Issue: No video recording or snapshot in the notification.**
* **MQTT:** Frigate relies on MQTT. Ensure your Home Assistant and Frigate are communicating via your MQTT broker.
* **Snapshot Path:** If you get the text alert but the image is broken, check the `frigate_notify_automate.yaml` path. It must match your Frigate camera's name (e.g., `camera.driveway`).

---

### 📝 Checking Logs
To see exactly what the device is doing in real-time:
1. Open the **ESPHome Dashboard**.
2. Click **LOGS** on your `car-security-upgraded` device.
3. Look for lines starting with `[sim7000]`. If you see `AT+CREG?` returning `0,2`, it means it is still searching for a cell tower.
