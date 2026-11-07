<div align="center">

<a href="https://www.buymeacoffee.com/cataseven" target="_blank">
  <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me a Coffee" style="height: 52px !important; width: 190px !important;" >
</a>

# 🗺️ Ultimate Google Maps Card for Home Assistant

### Turn your Home Assistant into a real-time mission control center: 30 fps GTFS transit animation, live traffic, 360° 3D vector tilt, frosted-glass layer filters, and dynamic Markdown badges.

[![Downloads](https://img.shields.io/github/downloads/cataseven/Google-Map-Card/total?color=41BDF5&logo=home-assistant&label=Downloads&suffix=%20downloads&style=for-the-badge)](https://github.com/cataseven/Google-Map-Card/releases)
[![hacs_badge](https://img.shields.io/badge/HACS-Custom-orange.svg?style=for-the-badge)](https://github.com/hacs/frontend)
[![GitHub Release](https://img.shields.io/github/release/cataseven/Google-Map-Card.svg?style=for-the-badge)](https://github.com/cataseven/Google-Map-Card/releases)
[![License](https://img.shields.io/github/license/cataseven/Google-Map-Card.svg?style=for-the-badge)](LICENSE)
![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2024.1.0%2B-blue.svg?style=for-the-badge)

[Documentation](#-documentation-directory) | [Quick Start](#-quick-start)

---

</div>

<p align="center">
  <img src="images/routenew1.png" width="48%" />
  <img src="images/flight.gif" width="48%" />
</p>
<p align="center">
  <img src="images/tra.png" width="31%" />
  <img src="images/Timeline.gif" width="31%" />
  <img src="images/themes1.png" width="31%" />
</p>

---

## ⚡ What Makes This Card Different?

* **🚆 Real-Time GTFS Transit Engine**: Native compatibility with [GTFS2 (`vingerha/gtfs2`)](https://github.com/vingerha/gtfs2). Decouples 30 fps vehicle track interpolation from 1 Hz polling, rendering smooth vehicle movement along route polylines with zero local 404s.
* **🎛️ Unified Frosted-Glass Filter Control**: A sleek $40\times 40\text{ px}$ Google-styled button opening an accent-colored dropdown menu to toggle marker layers on the fly.
* **🏷️ Universal Aspect-Fit Badges & Pictures**: Integration-agnostic picture markers. Display rectangular store logos, gas price tags, and flyer banners without cropping distortion. Supports nested attribute dot-paths (`deals.0.image_url`).
* **💬 Dynamic Jinja2 + Markdown Popups**: Powered by Home Assistant's WebSocket `render_template` API into native `<ha-markdown allow-svg breaks>` for full styling freedom.
* **🗺️ 360° 3D Vector Maps & Advanced Markers**: Full tilt, rotation, and WebGL rendering with `google.maps.marker.AdvancedMarkerElement` when `map_id` is provided (with seamless legacy fallback).
* **🚗 Route Search & Travel Calculator**: In-card directions, live traffic polylines, address autocomplete, and quick one-tap commute shortcuts.
* **✈️ FlightRadar24 Live Traffic**: Dedicated flight panel, airport arrivals/departures board, and in-map flight tracking.
* **🌐 Six Live Data Overlays**: Day/Night twilight terminator, RainViewer animated radar, WAQI air quality, USGS earthquakes, and Open-Meteo weather badges.
* **📏 Measurement Tools & History Playback**: Scrub through location history at 1×–8× speed, measure real-world distances/areas, or draw live crow-flies distance lines.
* **🌏 Multi-Locale & Traditional Chinese**: Full support for BCP-47 locales including `zh-HK` (香港繁體), `zh-TW` (台灣繁體), and `zh-Hant`.

---

## 🚀 Quick Start

```yaml
type: custom:google-map-card
api_key: !secret google_maps_api_key
zoom: 14
rendering_type: vector
entities:
  - entity: person.alice
    picture_shape: circle

  - entity: sensor.local_gas_price
    picture_shape: rectangle
    popup_template: >
      <ha-markdown allow-svg breaks>
      ### {{ attributes.friendly_name }}
      **Price:** ${{ state }} / L
      </ha-markdown>
```

---

## 📚 Documentation Directory

Explore the modular documentation guides:

| Guide | Description | Link |
|:---|:---|:---:|
| 🚀 **Installation & Setup** | Google Cloud API key requirements, website restrictions, and HACS install. | [Read Guide →](docs/installation.md) |
| ✨ **Feature Deep Dive** | In-depth walkthrough of GTFS2, filters, badges, travel calculator, overlays. | [Read Guide →](docs/features.md) |
| ⚙️ **Configuration Reference** | Exhaustive configuration options, entity parameters, map controls, and YAML examples. | [Read Guide →](docs/reference.md) |
| 📜 **Changelog & History** | Release notes and major upgrade milestones from v1.0 to v6.1. | [Read Guide →](docs/changelog.md) |
| 🛠️ **Development & CI/CD** | Node.js syntax verification, GitHub Actions automated CI, and auto-entities setup. | [Read Guide →](docs/development.md) |

---

## ⭐ Support & Community

If you find this card useful, please give it a ⭐ **star on GitHub** and share it with the Home Assistant community!

<div align="center">

<a href="https://www.buymeacoffee.com/cataseven" target="_blank">
  <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me a Coffee" style="height: 52px !important; width: 190px !important;" >
</a>

### Star History

[![Star History Chart](https://api.star-history.com/svg?repos=cataseven/Google-Map-Card&type=date&legend=top-left)](https://www.star-history.com/#cataseven/Google-Map-Card&type=date&legend=top-left)

</div>
