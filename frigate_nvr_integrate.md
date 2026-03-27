# 📹 Frigate NVR Integration — Upgraded Edition

This document covers how to link the **T-SIM7670G-S3** sensors to Frigate to ensure intruders are captured on video immediately.

### 1. Frigate Configuration (`config.yml`)
Add the car's presence sensor as a trigger for your driveway camera.

```yaml
cameras:
  driveway:
    enabled: True
    ffmpeg:
      inputs:
        - path: rtsp://your_camera_stream
          roles:
            - detect
            - record
    record:
      enabled: True
      events:
        pre_capture: 5
        post_capture: 15
        retain:
          default: 10
          mode: active_objects
    # Trigger recording via Home Assistant API when Radar is tripped
    ui:
      dashboard: True
