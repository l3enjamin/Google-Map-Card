# ✨ Feature Deep Dive

[← Back to Main README](../README.md) | [Installation Guide →](installation.md) | [Configuration Reference →](reference.md)

---

## 🚆 1. GTFS2 Transit Integration & Smooth Motion Engine

This card provides dedicated transit visualization designed specifically to integrate with the [GTFS2 (`vingerha/gtfs2`)](https://github.com/vingerha/gtfs2) custom integration and real-time public transit feeds.

### Key Capabilities
* **Decoupled 30 fps Motion**: High-frequency vehicle track interpolation along route polylines runs on an internal 30 fps animation loop decoupled from the 1 Hz backend data polling, producing fluid vehicle motion with minimal CPU/GPU overhead.
* **Dynamic Track Alignment**: Automatically advances vehicles along complex route geometry using distance-based polyline interpolation (`advanceAlongPolylines`).
* **Universal Route Matching**: Matches transit vehicles to route geometries using `route_key`, `route_id`, `name`, or the GeoJSON filename slug.
* **Embedded Offline Vector SVGs**: Standalone inline SVG vector vehicle icons (`GENERIC_SUBWAY_SVG`, `GENERIC_BUS_SVG`) render out-of-the-box without requiring local image assets or triggering 404s.
* **Custom Schedule Ingestion**: Ingests trip schedules via `transit_motion.schedule_url` for live vehicle simulation and arrival tracking.

```yaml
transit_motion:
  enabled: true
  schedule_url: "/local/transit/schedule.json"
  update_interval_ms: 1000

geojson_layers:
  - url: "/local/transit/routes.geojson"
    route_key: "line_1"
    stroke_color: "#0072bc"
    stroke_width: 3
```

---

## 🎛️ 2. Unified Frosted-Glass Layer Filter Control

Instead of cluttering the map with multiple buttons, the card provides a single, unified frosted-glass layer filter control.

* **Native Control Styling**: Styled as a compact $40\times 40\text{ px}$ button consistent with Google Maps controls, featuring an active filter indicator dot when any group is hidden.
* **Checkbox Dropdown Menu**: Clicking opens an accent-colored dropdown menu with MDI icons and custom labels.
* **100% YAML Configurable**: Groups are defined in `filter_groups` (with `id`, `label`, `icon`, `checked`).
* **Dynamic Association**: Entities and GeoJSON layers link to filter groups using the `filter_group` property.

```yaml
filter_control: true
filter_groups:
  - id: transit_live
    label: "Live Transit"
    icon: "mdi:bus-clock"
    checked: true
  - id: stations
    label: "Stations & Stops"
    icon: "mdi:train-car"
    checked: true
  - id: gas
    label: "Gas Stations"
    icon: "mdi:gas-station"
    checked: true
  - id: deals
    label: "Store Deals"
    icon: "mdi:tag-outline"
    checked: false
```

---

## 🏷️ 3. Integration-Agnostic Entity Pictures & Badges

Display photos, brand badges, and flyer images on the map from any Home Assistant integration without distortion or cropping.

* **Configurable Shapes (`picture_shape`)**:
  * `'circle'` (default): Classic circular avatar with border.
  * `'rectangle'`: High-contrast rectangular card with configurable background, border color, and rounded corners.
  * `'auto'`: Dynamically calculates source image aspect ratio to fit rectangular logos and banners without cropping.
  * *(Note: `picture_aspect` is supported as a backwards-compatible alias)*.
* **Nested Attribute Extraction (`picture_attribute`)**: Extract images directly from entity attributes, including nested dot-paths (e.g. `deals.0.image_url` or `brand_logo`).
* **Direct Cross-Origin Image Fallback**: Automatically falls back to direct image rendering for external CDN links lacking cross-origin (CORS) headers.

```yaml
entities:
  # Gas station entity with price badge
  - entity: sensor.shell_gas_price
    picture_shape: rectangle
    picture_height: 24
    filter_group: gas

  # Store entity with flyer deal extracted from nested attribute
  - entity: sensor.local_store_deals
    picture_attribute: "deals.0.image_url"
    picture_shape: auto
    card_background: "#ffffff"
    filter_group: deals
```

---

## 💬 4. Dynamic Popups via `<ha-markdown allow-svg breaks>` & Lovelace Cards (`popup_card`)

Define custom info window popups using either Jinja2 templates or any Lovelace card directly inside Google Maps!

* **Dynamic Jinja2 Popups (`popup_template`)**: Renders HTML/Markdown inside `<ha-markdown allow-svg breaks>` via Home Assistant's WebSocket `render_template` API. Receives `entity`, `state`, and `attributes` in context.
* **Lovelace Cards in Popups (`popup_card`)**: Embed any Lovelace card (e.g. `custom:flex-table-card`, `entities`, `glance`, `tile`) directly inside the marker InfoWindow using Home Assistant's card helpers (`window.loadCardHelpers`). Supports `this.entity_id` dynamic replacement!

```yaml
entities:
  # 1. Lovelace card inside marker popup
  - entity: sensor.departures_from_home_station
    popup_card:
      type: custom:flex-table-card
      entities:
        include:
          - this.entity_id
      clickable: true
      max_rows: 5
      title: 巴士離站時間
      columns:
        - name: 路線
          data: next_departures_lines
          modify: "'<div class=route>' + (x.route || x.route_long || '') + '</div>'"
        - name: 時間
          data: next_departures_lines
          modify: x.departure
        - name: 目的地
          data: next_departures_lines
          modify: "x.headsign"

  # 2. Jinja2 template inside marker popup
  - entity: sensor.local_store_deals
    popup_template: >
      <ha-markdown allow-svg breaks>
      ### {{ attributes.friendly_name | default(entity) }}
      {% if attributes.deals and attributes.deals[0] %}
      **{{ attributes.deals[0].name }}**
      <img src="{{ attributes.deals[0].image_url }}" style="max-width:100%;border-radius:8px;margin-top:6px;" />
      {% else %}
      *No active flyer deals available*
      {% endif %}
      </ha-markdown>
```

---

## 🗺️ 5. Modern Vector Map ID (`map_id`) & Advanced Markers

Google Cloud Vector Maps provide high-performance WebGL rendering, smooth tilt and rotation, and support for modern `AdvancedMarkerElement`.

* **Vector Map ID**: Configure `map_id` with your Google Cloud Map ID.
* **Advanced Markers**: When `map_id` is supplied, the card automatically instantiates `google.maps.marker.AdvancedMarkerElement`. If omitted, the card seamlessly falls back to standard `google.maps.Marker`, ensuring 100% backward compatibility.
* **Viewport Synchronization (`viewport_entity`)**: Automatically updates a Home Assistant `input_text` helper with current bounding coordinates (`southWestLat,southWestLng,northEastLat,northEastLng`) on map pan and zoom, enabling coordinate-based entity filtering.

```yaml
map_id: "YOUR_GOOGLE_CLOUD_MAP_ID"
rendering_type: vector
viewport_entity: "input_text.map_viewport"
```

---

## 🚗 6. Route Search & Travel Time Calculator

Docked travel panel with real-time route calculation, live traffic-colored polylines, address autocomplete, route shortcuts, and multi-modal support (driving, walking, transit, cycling).

* Map-based route info bar with duration and distance.
* Clickable route polylines for route alternatives.
* Predefined route shortcuts with quick one-click calculation.
* Address autocomplete via Places API (New).

```yaml
travel_panel_enabled: true
travel_panel_position: above
show_travel_panel_toggle_button: true
travel_shortcuts:
  - label: "Go to Work"
    icon: "mdi:office-building"
    from_entity: "person.alice"
    to_entity: "zone.office"
  - label: "Go Home"
    icon: "mdi:home"
    from_entity: "person.alice"
    to_entity: "zone.home"
```

---

## ✈️ 7. FlightRadar24 Live Air Traffic

* Dedicated FlightRadar sidebar or docked panel.
* Airport arrivals / departures live tables.
* Flight status chips (Estimated, Landed, Scheduled, Delayed, On Route).
* Interactive right-click actions on map: Add Flight, Remove Flight, Clear Flights.

---

## 🌐 8. Live Data Layers & Overlays

Six opt-in overlays turn the card into a comprehensive data dashboard without extra background overhead when disabled:

1. **🌗 Day/Night Terminator**: Shades the night side of Earth with civil and nautical twilight bands. Computed entirely in-card with astronomy math — zero APIs, zero tokens, works offline.
2. **🌧️ Animated Rain Radar (RainViewer)**: Live animated precipitation radar over the past ~2 hours (free, no API key).
3. **🏭 Air Quality (WAQI)**: Heatmap tiles from the World Air Quality Index project.
4. **🌍 Earthquakes (USGS)**: Live earthquake epicenters scaled by magnitude and colored by depth.
5. **🌡️ Open-Meteo Weather Badges**: Temperature and weather condition badges per marker without needing an API key.
6. **Live Traffic Layer**: Google Maps native real-time traffic overlay.

---

## 📍 9. OpenStreetMap Place Popups & Measurements

* **Free Reverse-Geocoded Popups**: Tapping any map place or transit station displays the exact street address, coordinates, and one-tap directions links. Addresses are reverse-geocoded via keyless OpenStreetMap Nominatim and cached locally.
* **📏 Measurement Tool (`show_measure_button`)**: Measure real-world distance between points or calculate enclosed polygon areas.
* **📐 Crow-Flies Distance Lines (`distance_lines`)**: Live straight-line distance lines dynamically drawn between entities and zones.
* **⏱️ History Playback Timeline**: Interactive bottom playback bar to scrub through loaded entity history trails at 1×–8× speed.
* **🎯 In-Card Zone Management**: Right-click anywhere on the map to create, edit, or delete Home Assistant zones directly.
