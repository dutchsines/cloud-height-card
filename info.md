# Cloud Height Card

An animated, highly customizable Lovelace card for Home Assistant that visualizes estimated cloud base altitude, 24-hour altitude trend graphs, and live celestial movement (Sun & Moon) along a dynamic trajectory.

![Cloud Height Card Preview](https://raw.githubusercontent.com/dutchsines/cloud-height-card/main/preview.png)

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
title: Cloud Elevation
max_altitude: 10000
hours_to_show: 24
blend_colors: true
