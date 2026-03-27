# 🚀 PNWC Car Security: First-Time Installation Guide

Follow these steps in order to ensure the **T-SIM7670G-S3** and the **House Siren** sync correctly with Home Assistant and Frigate.

---

### Phase 1: Home Assistant Prep (The Foundation)
Before flashing any hardware, you must create the "Helpers" that the code looks for.
1. Go to **Settings > Devices & Services > Helpers**.
2. Create the following:
   * **Input Boolean:** `car_alarm_armed` (Name: "Car Alarm Armed")
   * **Input Boolean:** `car_alarm_maintenance` (Name: "Car Alarm Maintenance Mode")
3. **(Optional)** Create a **Zone** called `home` in **Settings > Areas & Zones** if you haven't already. This is critical for the "Away" GPS logic.

---

### Phase 2: Cellular SIM Provisioning
Your **T-SIM7670G-S3** won't connect to LTE until the APN is correct.
1. Insert your Nano SIM into the slot on the back of the board.
2. Identify your carrier's **APN** (e.g., `hologram`, `fast.t-mobile.com`, `wholesale`).
3. Open `car_security_cellular_s3.yaml` and update the `apn:` line under the `sim7000:` section.
4. **Important:** Ensure your SIM has the PIN lock disabled (you can do this in any standard smartphone settings).

---

### Phase 3: Flashing the Hardware
1. **The Sensor (Unit 1):** Connect the T-SIM7670G-S3 to your PC via USB-C. Use ESPHome to flash `car_security_cellular_s3.yaml`. 
   * *Note: The first boot takes longer as it initializes the PMU and Modem.*
2. **The Siren (Unit 2):** Connect the ESP32-WROOM-32 and flash `house_siren_wroom32.yaml`.
3. Verify both devices appear as "Online" in your ESPHome dashboard.

---

### Phase 4: Antenna & Physical Install
1. **GPS:** Snap the U.FL connector to the "GPS" port. Route the puck to the windshield.
2. **LTE:** Snap the LTE antenna to the "MAIN" port.
3. **Power:** Insert a high-quality **18650 Lithium Battery** into the holder. 
4. **GPS Cold Start:** The very first time you power it on, the GPS may take **5–10 minutes** to get a lock (it needs to download satellite data). Ensure the car is outside during this process.

---

### Phase 5: Dashboard & Automation Sync
1. Copy the contents of `dashboard.md` into a new **Manual Card** on your Home Assistant Lovelace dashboard.
2. Copy the contents of `ha_automations.yaml` into your Home Assistant `automations.yaml` file.
3. **Test:** Arm the system via the dashboard, then shake the sensor. You should receive a notification and see the **Frigate** recording trigger.
