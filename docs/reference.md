# ⚙️ Configuration Reference

[← Back to Main README](../README.md) | [Installation Guide →](installation.md) | [Feature Deep Dive →](features.md)

---

## 🧹 General Options

| Key | Type | Default | Description |
|:---|:---|:---|:---|
| `type` | string | **Required** | Must be `custom:google-map-card`. |
| `api_key` | string | **Required** | Your Google Maps JavaScript API key. |
| `map_id` | string | `null` | Google Cloud Vector Map ID. Unlocks `AdvancedMarkerElement` and modern vector rendering. |
| `zoom` | integer / string | `12` | Initial zoom level (1–22) or HA entity ID (`input_number.map_zoom`) for dynamic control. |
| `rendering_type` | string | `raster` | Map rendering engine: `raster` or `vector`. Vector enables 360° rotation and tilt. |
| `color_scheme` | string | `light` | For vector mode: `light`, `dark`, or `follow_system`. |
| `language` | string | `null` | BCP-47 tag for map labels and formats (`zh-HK`, `zh-TW`, `zh-Hant`, `en`, `tr`, `ja`). Leave empty to follow HA user profile. |
| `theme_mode` | string | `null` | Built-in theme name (`Dark_Blueish_Night`, etc.). Raster mode only. |
| `aspect_ratio` | string | `null` | Card aspect ratio (e.g. `16:9`, `4:3`, `400px`). If omitted, fills container height. |
| `map_type` | string | `roadmap` | Map type: `roadmap`, `satellite`, `hybrid`, or `terrain`. |
| `gesture_handling` | string | `auto` | `greedy`, `cooperative` (Ctrl+scroll), or `auto`. |
| `no_world_repeat` | boolean | `true` | Prevents infinite continent repeat on zoom out. |
| `filter_control` | boolean | `false` | Enable unified frosted-glass layer filter control button. |
| `filter_groups` | list | `[]` | Definitions for layer filter groups (`id`, `label`, `icon`, `checked`). |
| `viewport_entity` | string | `null` | `input_text` helper to sync bounding coordinates (`SW_lat,SW_lng,NE_lat,NE_lng`). |
| `transit_motion` | object | `null` | Transit motion engine config: `enabled`, `schedule_url`, `update_interval_ms`. |
| `marker_clustering`| boolean | `false` | Group history dots depending on zoom level for performance. |
| `proximity_clustering` | boolean | `false` | Group nearby markers until zoom >= 17. |
| `proximity_radius` | number | `150` | Proximity clustering radius in meters. |
| `spiderfy` | boolean | `true` | Separates markers with overlapping positions on high zoom. |
| `stale_marker_minutes` | number | `0` | Minutes of inactivity before marker fades out (`0` = disabled). |
| `show_popup_address` | boolean | `true` | Reverse-geocodes street addresses in marker popups via OpenStreetMap. |
| `zone_occupancy_badge` | boolean | `false` | Show counter badge of tracked entities inside each zone. |

---

## 👤 Entities Configuration

Configured under the `entities` list:

| Key | Type | Default | Description |
|:---|:---|:---|:---|
| `entity` | string | **Required** | Entity ID to track (`person.*`, `device_tracker.*`, `sensor.*`, `zone.*`). |
| `name` | string | `null` | Custom display name replacing entity name across the card. |
| `picture` | string | `null` | Custom image URL or local path (`/local/...`) for the marker. |
| `picture_shape` | string | `circle` | Marker shape: `circle`, `rectangle`, or `auto` (aspect-fit without cropping). Legacy alias `picture_aspect` supported. |
| `picture_attribute` | string | `null` | Dot-path to extract image URL from entity attributes (e.g. `deals.0.image_url`). |
| `picture_height` | number | `24` | Height in pixels for rectangular picture badges. |
| `picture_border_radius` | number | `6` | Border radius in pixels for rectangular badges. |
| `card_background` | string | `#ffffff` | Background color for rectangular picture cards. |
| `card_border_color` | string | `null` | Border color for rectangular picture cards. |
| `filter_group` | string | `null` | Associate entity with a defined `filter_groups` ID. |
| `popup_template` | string | `null` | Custom Jinja2 popup template rendered via `<ha-markdown allow-svg breaks>`. Context: `entity`, `state`, `attributes`. |
| `icon_size` | integer | `30` | Size of marker icon in pixels. |
| `icon_color` | string | `null` | Icon color (e.g. `#ffffff`). |
| `background_color` | string | `null` | Background color for the marker pin. |
| `hours_to_show` | integer | `0` | Hours of location history trail to display (`0` = disabled). |
| `polyline_color` | string | `null` | Hex color of history polyline. |
| `polyline_width` | integer | `2` | Stroke width of history polyline. |
| `follow` | boolean | `false` | Centers map on this entity. If multiple, fits bounds to all. |
| `show_history_dots` | boolean | `true` | Render dots along the polyline path. |
| `history_dot_shape` | string | `circle` | Shape: `circle`, `square`, `triangle`, `diamond`, `star`, `pentagon`. |
| `history_dot_filled` | boolean | `true` | Fill dots solid or render as outlines. |
| `use_date_range` | boolean | `false` | Bind to card-level date picker instead of `hours_to_show`. |
| `gps_accuracy_ranges` | list | `[]` | Accuracy thresholds with `min`, `max`, `label`, `color`, `opacity`. |
| `weather_badges` | boolean | `false` | Display Open-Meteo temperature and condition badge on marker. |

---

## 🕹️ Map Controls & Buttons

| Key | Type | Default | Description |
|:---|:---|:---|:---|
| `cameraControl` | boolean | `false` | Raster mode: pan control. Vector mode: rotate & tilt grid. |
| `cameraControl_position` | string | `RIGHT_BOTTOM` | Position on map. |
| `zoomControl` | boolean | `true` | Native zoom in/out buttons. |
| `zoomControl_position` | string | `RIGHT_BOTTOM` | Position on map. |
| `streetViewControl` | boolean | `true` | Pegman Street View control. |
| `mapTypeControl` | boolean | `true` | Map type toggle (Roadmap, Satellite, Terrain). |
| `rotateControl` | boolean | `false` | Rotate & 45° tilt button. |
| `fullscreenControl` | boolean | `false` | Fullscreen toggle button. |
| `showScale` | boolean | `false` | Map distance scale bar. |
| `keyboardShortcuts` | boolean | `false` | Keyboard navigation shortcuts. |
| `show_traffic_button` | boolean | `false` | Real-time traffic overlay toggle button. |
| `show_weather_button` | boolean | `false` | Weather layer menu button. |
| `show_datepicker_button`| boolean | `false` | Calendar history date range picker button. |
| `show_recenter_button` | boolean | `false` | Reset view to center on tracked entities. |
| `show_daynight_button` | boolean | `false` | Toggle Day/Night terminator shading overlay. |
| `show_waqi_button` | boolean | `false` | Toggle WAQI Air Quality heatmap overlay. |
| `show_rainviewer_button`| boolean | `false` | Toggle animated precipitation radar overlay. |
| `show_usgs_button` | boolean | `false` | Toggle USGS Earthquakes live overlay. |
| `show_measure_button` | boolean | `false` | Toggle distance and area measurement tool. |
| `show_playback_button` | boolean | `false` | Toggle timeline history playback bar. |
| `buttons_opacity` | float | `1.0` | Button opacity (hover becomes solid). |

Supported positions: `TOP_LEFT`, `TOP_CENTER`, `TOP_RIGHT`, `LEFT_TOP`, `LEFT_CENTER`, `LEFT_BOTTOM`, `RIGHT_TOP`, `RIGHT_CENTER`, `RIGHT_BOTTOM`, `BOTTOM_LEFT`, `BOTTOM_CENTER`, `BOTTOM_RIGHT`.

---

## 🚗 Travel Panel & Shortcuts

```yaml
travel_panel_enabled: true
travel_panel_position: above          # above | below
show_travel_panel_toggle_button: true
show_travel_panel_toggle_button_position: LEFT_BOTTOM
travel_shortcuts:
  - label: "Work"
    icon: "mdi:briefcase"
    from_entity: "person.alice"
    to_entity: "zone.office"
```

---

## 🎯 Zones Configuration

```yaml
zones:
  zone.home:
    show: true
    color: "#3498db"
    zone_opacity: 0.3
    label_color: "#ffffff"
    zone_label_opacity: 0.9
    follow: false
```

---

## 📑 Full YAML Configuration Example

```yaml
type: custom:google-map-card
api_key: !secret google_maps_api_key
map_id: YOUR_VECTOR_MAP_ID
rendering_type: vector
color_scheme: follow_system
language: zh-HK
zoom: 15
filter_control: true
viewport_entity: input_text.map_viewport

filter_groups:
  - id: transit_live
    label: "實時交通"
    icon: "mdi:bus-clock"
    checked: true
  - id: stations
    label: "車站月台"
    icon: "mdi:train-car"
    checked: true
  - id: gas
    label: "油站油價"
    icon: "mdi:gas-station"
    checked: true
  - id: deals
    label: "特價優惠"
    icon: "mdi:tag-outline"
    checked: false

transit_motion:
  enabled: true
  schedule_url: "/local/transit/schedule.json"
  update_interval_ms: 1000

entities:
  - entity: person.alice
    picture_shape: circle

  - entity: sensor.shell_gas_price
    filter_group: gas
    picture_shape: rectangle
    popup_template: >
      <ha-markdown allow-svg breaks>
      ### {{ attributes.friendly_name }}
      **Regular Fuel:** ${{ state }} / L
      *Updated: {{ attributes.updated }}*
      </ha-markdown>

  - entity: sensor.local_deals
    filter_group: deals
    picture_attribute: "deals.0.image_url"
    picture_shape: auto
    popup_template: >
      <ha-markdown allow-svg breaks>
      ### {{ attributes.friendly_name }}
      {% if attributes.deals and attributes.deals[0] %}
      **{{ attributes.deals[0].name }}**
      <img src="{{ attributes.deals[0].image_url }}" style="max-width:100%;border-radius:6px;margin-top:6px;" />
      {% endif %}
      </ha-markdown>
```
