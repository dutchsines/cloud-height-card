# Cloud Height Card for Home Assistant

A custom Lovelace card that visualizes real-time cloud elevation, altitude trends over time, and live sun/moon positions along a parabolic sky arch.

![Cloud Height Card Preview](https://raw.githubusercontent.com/YOUR_GITHUB_USERNAME/cloud-height-card/main/preview.png)

## Features
- **Dynamic Sky Visualization:** Renders an animated cloud graphic at the real-time altitude reported by your sensor.
- **Historical Trendline:** Embeds an SVG graph showing altitude changes over a customizable time window (e.g., 24h).
- **Celestial Tracking:** Tracks real-time Sun and Moon elevation along a parabolic arc complete with sunrise and sunset badges.
- **Color Thresholds & Blending:** Smoothly transitions or hard-cuts graph colors based on cloud height (e.g., red for fog, yellow for low ceiling, blue for high elevation).
- **Dashboard Customization:** Fully configurable via YAML or the built-in visual editor (font sizes, card height, ground colors, and cloud size).

---

## Installation

### Method 1: Manual Installation
1. Download `cloud-height-card.js` from the latest release.
2. Copy `cloud-height-card.js` to your Home Assistant configuration directory under `/config/www/cloud-height-card.js`.
3. In Home Assistant, go to **Settings** -> **Dashboards** -> **Resources** (top right three dots).
4. Add a new resource:
   - **URL:** `/local/cloud-height-card.js`
   - **Resource Type:** `JavaScript Module`
5. Refresh your browser (**Ctrl + F5** / **Cmd + Shift + R**).

### Method 2: HACS (Custom Repository)
1. Open **HACS** in Home Assistant.
2. Click the three dots in the top-right corner and select **Custom repositories**.
3. Add repository URL: `https://github.com/YOUR_GITHUB_USERNAME/cloud-height-card`
4. Category: **Lovelace**
5. Click **Add**, then find and install **Cloud Height Card**.

---

## Configuration Example

```yaml
type: custom:cloud-height-card
entity: sensor.estimated_cloud_base
title: Local Sky Conditions
max_altitude: 10000
hours_to_show: 24
card_height: 200px
blend_colors: true

# Font & Sizing Overrides
title_font_size: 1.1rem
axis_font_size: 0.75rem
badge_font_size: 0.85rem
cloud_size: 50px
celestial_size: 1.8rem

# Color Customizations
ground_color: '#4ab561'
arc_color: '#fde047'
bg_gradient: 'linear-gradient(180deg, #0e1726 0%, #162238 100%)'

# Altitude Color Thresholds
color_0: '#8b0000'     # Fog / Ground level
color_500: '#e63946'   # Very low ceiling
color_1000: '#f4a261'  # Low altitude
color_2500: '#e9c46a'  # Mid altitude
color_5000: '#2a9d8f'  # High altitude
color_8000: '#38bdf8'  # Very high ceiling
```

## Options

| Parameter | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `entity` | String | **Required** | Cloud height sensor entity ID |
| `title` | String | `Cloud Elevation` | Card header title |
| `max_altitude` | Number | `10000` | Y-axis ceiling limit |
| `hours_to_show` | Number | `24` | Hours of history to draw on graph |
| `card_height` | String | `200px` | Height of the viewport area |
| `blend_colors` | Boolean | `true` | `true` for smooth gradients, `false` for hard bands |
| `cloud_gif` | String | Default GIF | Custom image/GIF URL or `/local/my_cloud.gif` |
| `title_font_size` | String | `1rem` | Header title font size |
| `axis_font_size` | String | `0.7rem` | X and Y axis labels font size |
| `badge_font_size` | String | `0.8rem` | Altitude badge font size |
| `celestial_size` | String | `1.8rem` | Sun & Moon icon font size |
| `ground_color` | String | `#4ab561` | Ground bar color |
| `arc_color` | String | `#fde047` | Sun trajectory arch color |
| `bg_gradient` | String | CSS Gradient | Background gradient style |

![Cloud Height Card Preview]([https://raw.githubusercontent.com/dutchsines/cloud-height-card/main/preview.png](https://github.com/dutchsines/cloud-height-card/blob/main/Screenshot%202026-09-20%20120430.png)
