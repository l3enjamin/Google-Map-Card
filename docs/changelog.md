# 📜 Changelog & Release History

[← Back to Main README](../README.md) | [Installation Guide →](installation.md) | [Feature Deep Dive →](features.md)

---

## 🚀 Latest Enhancements (v6.1.0)
* **🚆 GTFS2 Transit Integration**: Native compatibility with [GTFS2 (`vingerha/gtfs2`)](https://github.com/vingerha/gtfs2) integration and live GTFS feeds.
* **Smooth 30 fps Transit Motion Engine**: High-frequency vehicle track interpolation decoupled from backend polling loops. Universal route matching and standalone inline SVG vector fallbacks (`GENERIC_SUBWAY_SVG`, `GENERIC_BUS_SVG`).
* **🎛️ Unified Frosted-Glass Layer Filter Control**: Compact $40\times 40\text{ px}$ control button with accent-colored checkbox dropdown menu. 100% YAML configurable via `filter_groups`.
* **🏷️ Integration-Agnostic Entity Pictures**: Configurable shape (`picture_shape: 'rectangle' | 'circle' | 'auto'`), nested dot-path extraction (`picture_attribute`), and direct cross-origin (CORS) image fallback.
* **💬 Dynamic Popups via `<ha-markdown allow-svg breaks>`**: Dynamic template evaluation via Home Assistant WebSocket `render_template` API with Jinja2, HTML, and SVG support.
* **🗺️ Modern Vector Map ID (`map_id`) & Advanced Markers**: Support for Google Cloud Vector Map IDs with `AdvancedMarkerElement` and graceful fallback to `google.maps.Marker`.
* **📐 Safe Viewport Synchronization**: Debounced bounds listener syncs coordinates (`southWestLat,southWestLng,northEastLat,northEastLng`) to a Home Assistant helper (`viewport_entity`).
* **🌏 Traditional Chinese Locale Support**: Built-in support for `zh-HK` (香港繁體), `zh-TW` (台灣繁體), and `zh-Hant` in GUI editor and default UI labels.
* **🧪 Automated CI/CD Validation**: GitHub Actions workflow validating JavaScript syntax (`node --check`) and HACS compliance.

---

## v6.0.2
* **Custom Name & Picture**: Per-entity `picture:` to provide photos for any sensor or tracker; custom `name:` to rename entities card-wide; `show_name: true` prints labels under markers.

## v6.0.1
* **Free Google Tools**: Client-side Measure tool (distance & area), geodesic great-circle trails (`geodesic_polylines`), custom GeoJSON overlays (`geojson_layers`), and live crow-flies distance lines (`distance_lines`).
* **History Playback**: Timeline bar (`show_playback_button`) to scrub and replay loaded history trails (1×–8×).

## v5.16
* **Single-World Zoom Limit (`no_world_repeat`)**: Prevents continent repetitions on zoom-out.
* **Lufop Radar Support**: Dedicated popup layout for European speed cameras.

## v5.15
* **Live Data Layers**: Day/Night terminator shading, WAQI Air Quality heatmap, RainViewer animated radar, USGS earthquakes, and Open-Meteo weather badges.

## v5.2.0
* **Marker Labels & Jitter Filtering**: Per-entity `show_marker_labels`, `stale_marker_minutes` fade, and `min_accuracy` GPS jitter filter inside zones.
* **Zone Occupancy Badges**: Dynamic count of tracked entities inside zones.
* **Keyless Address Popups**: Reverse-geocoded addresses via OpenStreetMap.

## v5.0.0 – v5.0.9
* **Route Search and Travel Time Calculator**: Docked travel panel, traffic-colored polylines, address autocomplete, and shortcuts.
* **External Date Control & Dynamic Zoom**: Integration with `input_datetime` and `input_number` entities.

## v4.0.0
* **FlightRadar24 Integration**: Dedicated FlightRadar panel, arrivals/departures table, and interactive map flight management.
* **GPS Accuracy Circles**: Zoom-aware accuracy rings and customizable distance thresholds.

## v1.0.0 – v3.0.0
* Initial release of Google Maps Card for Home Assistant.
* Multi-entity tracking, custom themes, zone management, POI filtering, and clustering.
