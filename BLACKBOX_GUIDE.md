# 💾 Black Box: Local SD Card Logging

The Upgraded PNWC Tracker includes a **Black Box** feature that records GPS data to a MicroSD card. This is essential for when the car is taken into areas with no Cellular or WiFi coverage.

### 🛠️ Hardware Requirements:
1. **MicroSD Card:** Use a high-quality (Class 10) card, formatted to **FAT32**.
2. **Capacity:** 16GB or 32GB is more than enough for years of GPS text logs.

### 📝 How to Retrieve Data:
If your car was moved and you didn't get a live GPS update, the data is saved in `blackbox.log` on the SD card.
1. Remove the SD card from the T-SIM7670G-S3.
2. Plug it into your PC.
3. Open `blackbox.log` in any text editor.
4. The file will contain raw coordinates: `LAT:45.123456, LON:-122.123456`.
5. Copy these coordinates into Google Maps to see where the car was at that moment.

### 🔋 Battery Impact:
The SD card write process uses very little power. The logic is "throttled" to write only once every 30 seconds to prevent unnecessary battery drain and wear on the SD card.
