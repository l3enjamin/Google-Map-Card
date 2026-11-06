# 🚀 Installation & Setup Guide

[← Back to Main README](../README.md) | [Feature Deep Dive →](features.md) | [Configuration Reference →](reference.md)

---

## 📋 Prerequisites

Before installing the card, you need a **Google Maps JavaScript API Key** from the Google Cloud Platform (GCP) Console.

### 1. Create a Google Cloud Project & Enable APIs
1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. Create a new project (e.g. `Home Assistant Maps`).
3. Navigate to **APIs & Services → Library** and enable the following APIs:

| API | Required For | Free Tier Limit |
|:---|:---|:---|
| **Maps JavaScript API** | Core map rendering (Mandatory) | Included in \$200/mo credit (~28,000 loads) |
| **Directions API** | Route Search and Travel Time Calculator | Optional |
| **Places API (New)** | Address Autocomplete in Travel Panel | Optional |
| **Routes API** | Real-time traffic segment polyline colors | Optional |

> [!TIP]
> Google provides **\$200 free credit every month** for Google Maps Platform, which is more than enough for personal Home Assistant dashboards.

### 2. Restrict Your API Key (Security Best Practice)
To prevent unauthorized use of your API key:
1. Navigate to **APIs & Services → Credentials**.
2. Click your API key to edit.
3. Under **Application restrictions**, choose **Websites**.
4. Add your Home Assistant domain referrers (include trailing `/*`):
   * `https://your-ha-domain.example.com/*`
   * `https://homeassistant.local:8123/*`
   * `http://192.168.*.*:*/*` (if accessing via local IP)
5. Under **API restrictions**, choose **Restrict key** and select only the APIs you enabled above.

---

## 📦 Installation Methods

### Method 1: Via HACS (Recommended)

1. Open **HACS** in your Home Assistant sidebar.
2. Click the three dots in the top-right corner and select **Custom repositories**.
3. Add the repository URL:
   * **Repository**: `https://github.com/cataseven/Google-Map-Card` (or your fork)
   * **Category**: `Dashboard` (or `Lovelace`)
4. Search for **Google Map Card** and click **Download**.
5. Restart Home Assistant or reload your Lovelace dashboard resources.

---

### Method 2: Manual Installation

1. Download `google-maps-card.js` and `themes.js` from the [Releases](https://github.com/cataseven/Google-Map-Card/releases) page.
2. Copy the files into your Home Assistant directory:
   ```text
   <config directory>/www/community/Google-Map-Card/google-maps-card.js
   <config directory>/www/community/Google-Map-Card/themes.js
   ```
3. Add the resource reference in Home Assistant:
   * Go to **Settings → Dashboards → Resources** (click the three dots in the top right).
   * Click **Add Resource**:
     * **URL**: `/local/community/Google-Map-Card/google-maps-card.js`
     * **Resource type**: `JavaScript Module`

---

## ⚙️ Quick Start Lovelace YAML

Add a card to your dashboard using the visual editor or YAML mode:

```yaml
type: custom:google-map-card
api_key: !secret google_maps_api_key
zoom: 14
rendering_type: vector
entities:
  - entity: person.alice
  - entity: device_tracker.family_car
```

For advanced features and full configuration options, see the [Configuration Reference](reference.md).
