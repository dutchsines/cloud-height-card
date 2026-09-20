# Cloud Height Card

An animated, highly customizable Lovelace card for Home Assistant that visualizes estimated cloud base altitude, 24-hour altitude trend graphs, and live celestial movement (Sun & Moon) along a dynamic trajectory.

![Cloud Height Card Preview]([https://raw.githubusercontent.com/dutchsines/cloud-height-card/main/preview.png](https://raw.githubusercontent.com/dutchsines/cloud-height-card/refs/heads/main/Screenshot%202026-09-20%20120430.png)

## Key Features

- ☁️ **Dynamic Cloud Graphics:** Animated cloud GIF placed at the exact real-time cloud base elevation.
- 📈 **Altitude History Graph:** Visualizes cloud base trends over a customizable timeframe with multi-stop SVG gradients.
- ☀️ **Real-time Sun & Moon Tracking:** Displays sun and moon altitude along a parabolic arc with exact sunrise and sunset time badges.
- 🎨 **Custom Color Thresholds:** Set altitude-based color thresholds (e.g., fog, low ceiling, mid, high) with optional smooth color blending.
- ⚙️ **Visual Card Editor:** Adjust font sizes, card height, cloud icon sizes, and threshold colors directly from the Home Assistant dashboard UI.

---

## Quick Setup

Add the card to your dashboard YAML:

```yaml
type: custom:cloud-height-card
entity: sensor.estimated_cloud_base
temp_entity: sensor.st_00176926_air_temperature
dew_entity: sensor.st_00176926_dew_point
title: LOCAL SKY CONDITIONS
max_altitude: 10000
hours_to_show: 24
progress_bar_order: 3
sensors_order: 1
analysis_order: 1
show_celestial: true
show_progress_bar: true
show_sensors: true
show_analysis: true
