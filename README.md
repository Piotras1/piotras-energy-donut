📸 Visual Presentation

## Piotras Energy Donut
A highly customizable Home Assistant card designed to visualize energy consumption using an interactive donut chart.

The card focuses on clear distribution of values across multiple entities, offering smooth visuals, configurable thresholds, and multiple layout modes optimized for different dashboard styles.

## ✨ Features

- Interactive donut visualization
- Multiple entity support
- Automatic "Others" segment for unmeasured values
- Configurable segment limits
- Dynamic color assignment
- Focus / highlight behavior with auto-dismiss timeout
- Fully responsive SVG rendering
- Visual editor support (no YAML required)
- Consistent design across Piotras Cards Pack

---

## 🧩 Layout 1: Callout Lines Mode
<p align="center">
  <img src="https://github.com/user-attachments/assets/2d844fa6-46ea-4ee9-bce8-7ce154475552" width="32%" />
  <img src="https://github.com/user-attachments/assets/46c9e786-e460-4af1-85c8-5935510bb89e" width="32%" />
  <img src="https://github.com/user-attachments/assets/98d00170-02d0-4b31-83e5-c9f9f45b59d4" width="32%" />
</p>

### Description
A visually rich layout where each segment is connected to its label via a callout line pointing outward from the donut. Designed for dashboards with plenty of space, giving it a modern, technical look.

### Key Characteristics

- Donut chart as the main element
- Callout lines connecting segments to labels
- Dynamic label positioning with anti-overlap correction
- Clicking a segment highlights it and shows detailed value and percentage
- Lines can be hidden with `show_lines: false` (labels remain visible on click)
- Designed for wide screens and large panels

### Configuration
```yaml
type: custom:piotras-energy-donut
entity: sensor.total_power
layout: 1
po_opisie: 'kWh'
po_przecinku: 2
devices:
  - entity: sensor.device1
    name: Device 1
  - entity: sensor.device2
    name: Device 2
```

---

## 🧩 Layout 2: Legend Mode
<p align="center">
  <img src="https://github.com/user-attachments/assets/cb0446a7-cab2-457b-a6c5-52df80db31ce" width="33%" />
  <img src="https://github.com/user-attachments/assets/4ef5071a-a44a-4b57-aa0d-f2dff99637b3" width="33%" />
  <img src="https://github.com/user-attachments/assets/9bcd11ad-8ec3-4a7c-b809-0af23c2b4ba1" width="33%" />
</p>

### Description
A balanced layout combining the donut chart with a two-sided legend — entries are distributed symmetrically to the left and right of the donut. Best suited for mobile devices, narrow sidebar columns, and scenarios with a long list of sensors.

### Key Characteristics

- Donut + two-sided legend combination
- Entries alternate left and right of the chart
- Clear color-coded squares mapping entities to segments
- Stable and predictable positioning
- Better readability for analysis

> **Pro Tip:** Use the `limit` parameter to hide less important devices and keep the legend clean.

### Configuration
```yaml
type: custom:piotras-energy-donut
entity: sensor.total_power
layout: 2
po_opisie: 'kWh'
po_przecinku: 2
limit: 5
devices:
  - entity: sensor.device1
    name: Device 1
  - entity: sensor.device2
    name: Device 2
```

---

## 🧩 Layout 1 and 🧩 Layout 2 Balanced  Power & Current Monitoring
<p align="center">
  <img src="https://github.com/user-attachments/assets/8b7d376a-f037-460e-8788-8bb2e097f633" width="33%" />
  <img src="https://github.com/user-attachments/assets/b78054d9-89c7-4535-b581-a1381778e49b" width="33%" />
  <img src="https://github.com/user-attachments/assets/264c787c-4558-479d-a6b4-22eecff78d1b" width="33%" />
</p>

### Description

This card is not limited to static energy data — it also excels at real-time monitoring of power (W) and current (A).

### Highlights

- **Real-time accuracy** – Track instantaneous spikes in power and current  
- **Flexible units** – Using the `po_opisie` variable, you can display the exact unit provided by your sensor  

### Configuration
```yaml
type: custom:piotras-energy-donut
entity: sensor.total_power
layout: 2
po_opisie: 'W'
po_przecinku: 0
devices:
  - entity: sensor.device_power_1
    name: Device 1
  - entity: sensor.device_power_2
    name: Device 2
```
This makes the card suitable not only for energy distribution, but also for live power monitoring scenarios.

---

## 🧩 Layout 3: Percentage Gauge Mode
<p align="center">
  <img src="https://github.com/user-attachments/assets/602386db-8ef0-4945-93ca-0e5125343f69" width="33%" />
  <img src="https://github.com/user-attachments/assets/e4e8b625-ea88-4e6b-ac42-7c6ee395cf9d" width="33%" />
  <img src="https://github.com/user-attachments/assets/649e6b02-9674-4a3d-aa5b-0fa19fad2f4e" width="33%" />
</p>

### Description
A dedicated layout for single-value percentage-based sensors. Always displays the ring fill — no interaction required to activate it.

The ring fills proportionally between `min_procent` (default: `0`) and `max_procent` (default: `100`). Only `devices[0].entity` is used as the data source in this mode — the top-level `entity` field is not read.

### Key Characteristics

- Single-value gauge visualization
- Percentage-based scale with configurable min and max
- Always-on display (no click required)
- Smooth proportional ring fill
- Clear central value indication

### Comfort Zone Ring
An optional outer ring that visualizes threshold-based zones.
It is divided into three configurable ranges:

- below range (color 2)
- within comfort zone (color 3)
- above range (color 4)

Activated by setting `min_temp` and `max_temp`. This makes it especially useful for environmental monitoring such as temperature or humidity.

### Best For

- Battery monitoring
- Humidity sensors
- Tank / reservoir levels
- Temperature (range-based)
- Any percentage-based sensor

### Configuration
```yaml
type: custom:piotras-energy-donut
entity: ""
layout: 3
title: Lenovo Battery
po_opisie: '%'
max_procent: 100
min_procent: 0
po_przecinku: 1
devices:
  - entity: sensor.battery
    name: Lenovo Battery
```

---

### 🧠 Notes

- Layouts are independent display modes — functionality remains the same
- Layout 3 is intended for single-value sensors only — percentage mode is always active
- Comfort zone ring is optional and requires `min_temp` and `max_temp` to be set
- All layouts are configurable via the visual editor
- The card uses SVG rendering for smooth and responsive visuals

---

## ⚙️ Configuration Reference

### Card-level options

| Option | Type | Default | Layouts | Description |
|---|---|---|---|---|
| `entity` | string | — | 1, 2 | Main entity for total value (sum of all devices) |
| `layout` | number | `1` | all | Layout mode: `1` = Callout Lines, `2` = Legend, `3` = Percentage Gauge |
| `title` | string | `'ENERGY STRUCTURE'` | all | Title text displayed at the top of the card |
| `show_title` | boolean | `true` | all | Show or hide the title |
| `show_line` | boolean | `true` | all | Show or hide the separator line below the title |
| `show_lines` | boolean | `true` | 1 | Show or hide callout lines (labels remain on click) |
| `limit` | number | `9` | 1, 2 | Maximum number of devices shown; the rest are grouped into "Others" |
| `detail_timeout` | number | `15` | 1, 2 | Seconds before an active (highlighted) segment auto-deselects. Set to `0` to disable |
| `po_opisie` | string | `'kWh'` | all | Unit label displayed next to values |
| `po_przecinku` | number | `2` | all | Number of decimal places for displayed values |
| `max_procent` | number | `100` | 3 | Maximum value of the percentage scale (top of the ring) |
| `min_procent` | number | `0` | 3 | Minimum value of the percentage scale (bottom of the ring) |
| `center_label` | string | `'kWh TODAY'` | 1, 2 | Label shown below the total value in the center of the donut |

### Chart geometry

| Option | Type | Default | Description |
|---|---|---|---|
| `svg_width` | number | `480` | Base SVG width in logical units (scales with container) |
| `aspect_ratio` | number | layout-dependent | Height-to-width ratio of the SVG canvas |
| `radius` | number | auto | Donut ring radius in px (overrides `radius_ratio`) |
| `radius_ratio` | number | `0.167` | Donut radius as a fraction of `svg_width` |
| `stroke_width` | number | auto | Ring stroke thickness in px (overrides `stroke_ratio`) |
| `stroke_ratio` | number | `0.079` | Ring thickness as a fraction of `svg_width` |
| `center_y_ratio` | number | `0.55` | Vertical center of the donut as a fraction of SVG height |
| `margin_from_chart` | number | `30` | Distance between the donut edge and callout line endpoints (Layout 1) |
| `odleg_okreg` | number | `40` | Distance between the donut edge and the legend columns (Layout 2, 3) |

### Typography

| Option | Type | Default | Description |
|---|---|---|---|
| `title_color` | string | `var(--primary-text-color)` | Title and center text color |
| `label_color` | string | `var(--primary-text-color)` | Label and legend text color |
| `title_font_size` | number | auto | Title font size (px) |
| `center_font_size` | number | auto | Center value font size (px) |
| `label_font_size` | number | auto | Label/legend font size (px) |
| `font_style` | number | `1` | Font style: `1` = default, `2` = small-caps, `3` = monospace, `4` = uppercase with letter spacing |

### Card appearance

| Option | Type | Default | Description |
|---|---|---|---|
| `background_color` | string | HA default | Card background color |
| `border_radius` | number | HA default | Card corner radius (px) |
| `border_width` | number | HA default | Card border width (px) |
| `border_color` | string | HA default | Card border color |
| `box_shadow` | string | HA default | Card box shadow |

### Colors

| Option | Type | Default | Description |
|---|---|---|---|
| `c1` – `c20` | string | palette | Custom colors for segments 1–20. `c20` is always used for the "Others" segment |

### Comfort Zone Ring (Layout 3 only)

| Option | Type | Default | Description |
|---|---|---|---|
| `min_temp` | number | — | Start of the comfort zone (activates the outer ring) |
| `max_temp` | number | — | End of the comfort zone |
| `kom_gr` | number | `5` | Outer ring stroke width (px) |
| `ile_od_okregu` | number | `8` | Distance between the main ring and the comfort zone ring (px) |
| `kom_opti` | number | `0.75` | Opacity of the comfort zone ring |

### Per-device options (under `devices:`)

| Option | Type | Description |
|---|---|---|
| `entity` | string | Entity ID of the sensor |
| `name` | string | Display name for the segment and legend |
