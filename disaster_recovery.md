# 🕵️ Tactical Vehicle Recovery

If the vehicle is stolen and moves beyond your home base station:

1. **Mobile Hunting:** Use a handheld Meshtastic node with a high-gain antenna.
2. **Last Gasp Location:** Check your mesh logs for the `BATT_CRIT` alert. This is the last confirmed location of the car before the tracker entered power-save shutdown.
3. **Signal Punch:** LoRa (915MHz) will penetrate garages and containers better than 4G. If the map stops at a building, the car is likely inside.
