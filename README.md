# Cloud Height Card for Home Assistant

<p align="center">
  <a href="https://my.home-assistant.io/redirect/hacs_repository/?owner=dutchsines&repository=cloud-height-card&category=Lovelace" target="_blank" rel="noreferrer noopener">
    <img src="https://my.home-assistant.io/badges/hacs_repository.svg" alt="Open in HACS" />
  </a>
</p>

<p align="center">
  <a href="https://hacs.xyz/"><img src="https://img.shields.io/badge/HACS-Custom-orange.svg?style=for-the-badge" alt="HACS Custom"></a>
  <a href="https://github.com/dutchsines/cloud-height-card/releases/latest"><img src="https://img.shields.io/github/v/release/dutchsines/cloud-height-card?style=for-the-badge&color=blue" alt="Latest Version"></a>
  <a href="https://github.com/dutchsines/cloud-height-card/blob/main/LICENSE"><img src="https://img.shields.io/github/license/dutchsines/cloud-height-card?style=for-the-badge&color=green" alt="License"></a>
  <img src="https://img.shields.io/badge/Home%20Assistant-Lovelace-41BDF5.svg?style=for-the-badge&logo=home-assistant&logoColor=white" alt="Home Assistant Lovelace">
</p>

<p align="center">
  <img src="Preview.png" alt="Cloud Height Card Preview" width="48%">
  <img src="Pannelview.png" alt="Cloud Height Card Preview" width="48%">
</p>

A custom Lovelace card for Home Assistant that visualizes real-time cloud elevation, altitude trends over time, and live sun/moon positions along a parabolic sky arch.

---

## Features
- ☁️ **Dynamic Sky Visualization:** Renders an animated cloud graphic at the real-time altitude reported by your sensor.
- 📈 **Historical Trendline:** Embeds an SVG graph showing altitude changes over a customizable time window (e.g., 24h) with intermediate time markers across the bottom axis.
- 📏 **Responsive Layout & Dynamic Width:** The Y-axis automatically auto-fits its width based on text length to prevent any text or graph overlap, even when using dual height displays.
- 📐 **Flexible Unit System:** Supports automatic Home Assistant native units, forced Imperial (`ft`, `°F`), Metric (`m`, `°C`), or Dual-Unit readouts (`ft (m)` / `°F (°C)`).
- ☀️ **Celestial Tracking:** Tracks real-time Sun and Moon elevation along a parabolic arc with accurate moon phases, sunrise, sunset, moonrise, and moonset time badges.
- 🎨 **Color Thresholds & Blending:** Smoothly transitions or hard-cuts graph colors based on cloud height (e.g., red for fog, yellow for low ceiling, blue for high elevation).
- 🔎 **Dynamic Dynamic Zoom / Auto-Scale:** Automatically scales the graph view ceiling based on historical peaks to eliminate dead space, or can be overridden to a fixed maximum.
- ⚙️ **Dashboard Customization:** Fully configurable via YAML or the built-in visual editor (font sizes, card height, module layout ordering, ground colors, and cloud size).

---

## ☁️ Creating an Estimated Cloud Base Sensor

If you don't already have an entity providing cloud base elevation, you can easily create one in Home Assistant using a **Template Sensor**. The sensor uses the standard Spread Formula:

$$\text{Cloud Base (ft)} = \left( \frac{\text{Temperature} - \text{Dew Point}}{4.4} \right) \times 1000$$

Add one of the following snippets to your `configuration.yaml` (or `templates.yaml`) and replace the sample entity IDs with your local weather sensors.

### Option A: Imperial Units (°F)

```yaml
template:
  - sensor:
      - name: "Estimated Cloud Base"
        unique_id: estimated_cloud_base_ft
        unit_of_measurement: "ft"
        icon: "mdi:cloud-outline"
        state_class: measurement
        state: >
          {% set temp = states('sensor.your_temperature_sensor') | float(none) %}
          {% set dew = states('sensor.your_dew_point_sensor') | float(none) %}
          {% if temp is not none and dew is not none %}
            {{ (((temp - dew) / 4.4) * 1000) | round(0) }}
          {% else %}
            unavailable
          {% endif %}
```
Card Example 
```yaml
type: custom:cloud-height-card
entity: sensor.estimated_cloud_base
title: LOCAL SKY CONDITIONS
moon_rise_entity: sensor.moon_astro_next_rise
temp_entity: sensor.st_00176926_air_temperature
dew_entity: sensor.st_00176926_dew_point
moon_set_entity: sensor.moon_astro_next_set
axis_font_size: 1rem
badge_font_size: 1rem
moon_phase_entity: sensor.moon_astro_phase
bg_gradient: 'linear-gradient(180deg, #0e1726 0%, #ffffff 100%)'
unit_system: dual_m_ft
card_mod:
  style: |
    :host {
      --chc-header-color: #ffffff;        /* Card Header Title Color */
      --chc-axis-color: #000000;          /* Y-Axis & X-Axis Label Color */
      --chc-sensor-label-color: #000000;  /* Temp / Dew Point Labels */
      --chc-sensor-value-color: #000000;  /* Temp / Dew Point Numeric Values */
      --chc-badge-text-color: #fde047;   /* Badge Text Color */
      --chc-badge-bg: rgba(0, 0, 0, 0.8);  /* Badge Background */
    }
