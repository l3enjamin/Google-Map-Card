# 🛠️ Development & CI/CD Guide

[← Back to Main README](../README.md) | [Installation Guide →](installation.md) | [Configuration Reference →](reference.md)

---

## 🏗️ Repository Architecture

* `google-maps-card.js`: The main custom element bundle for `<google-map-card>` and `<google-map-card-editor>`.
* `themes.js`: Built-in map styling presets (40+ dark, light, and themed styles).
* `hacs.json`: HACS repository metadata and category configuration.
* `.github/workflows/`:
  * `validate.yml`: Automated CI workflow validating JavaScript syntax and schemas.
  * `hacs.yaml`: Official HACS validation action.
  * `release.yml`: Release asset packaging and deployment automation.
* `docs/`: Modular documentation directory.

---

## 🧪 Local Testing & Syntax Checking

### JavaScript Syntax Verification
To verify that all JavaScript files parse without syntax errors:

```bash
node --check google-maps-card.js
node --check themes.js
```

### Local Home Assistant Deployment
To test local changes on your Home Assistant instance:

1. Copy the bundles to your Home Assistant `www/` directory:
   ```bash
   cp google-maps-card.js <ha_config>/www/community/Google-Map-Card/
   cp themes.js <ha_config>/www/community/Google-Map-Card/
   ```
2. Gzip compress the files for optimal network loading:
   ```bash
   gzip -kf9 <ha_config>/www/community/Google-Map-Card/google-maps-card.js
   gzip -kf9 <ha_config>/www/community/Google-Map-Card/themes.js
   ```
3. Update the version query string in your Home Assistant Lovelace resource registry (or append `?v=<timestamp>`) to bust browser cache.

---

## 🤖 GitHub Actions Automated CI/CD

The repository includes automated CI/CD workflows:

### 1. `CI Validation` (`.github/workflows/validate.yml`)
Triggers on every `push` and `pull_request` targeting `main`:
* Checks Node.js 20+ syntax validity via `node --check`.
* Validates `hacs.json` JSON schema integrity.

### 2. `HACS Validation` (`.github/workflows/hacs.yaml`)
* Executes `hacs/action@main` to guarantee full compliance with HACS distribution standards.
* Authenticates using `GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}`.

---

## 💡 Testing with `custom:auto-entities`

Because this card integrates seamlessly with dynamic entity filters, you can test it wrapped inside `custom:auto-entities`:

```yaml
type: custom:auto-entities
card:
  type: custom:google-map-card
  api_key: !secret google_maps_api_key
  filter_control: true
  filter_groups:
    - id: transit_live
      label: "Live Transit"
      icon: "mdi:bus-clock"
      checked: true
    - id: deals
      label: "Deals"
      icon: "mdi:tag-outline"
      checked: true
card_param: entities
filter:
  include:
    - entity_id: "geo_location.*bus"
      options:
        filter_group: transit_live
    - entity_id: "sensor.*_deals*"
      options:
        filter_group: deals
        picture_attribute: "deals.0.image_url"
        picture_shape: auto
```

---

## 🤝 Contributing Guidelines

1. Fork the repository and create a feature branch (`feat/my-enhancement`).
2. Verify code syntax locally using `node --check google-maps-card.js`.
3. Test your changes on a real Home Assistant dashboard across both desktop and mobile viewports.
4. Ensure documentation in `docs/` and `README.md` is updated.
5. Submit a Pull Request targeting `main`.
