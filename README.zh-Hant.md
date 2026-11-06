<div align="center">

<a href="https://www.buymeacoffee.com/cataseven" target="_blank">
  <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me a Coffee" style="height: 52px !important; width: 190px !important;" >
</a>

# 🗺️ Home Assistant 終極 Google Maps 儀表板卡片

### 將您的 Home Assistant 打造為即時指揮中心：30 fps GTFS 公共交通動態模擬、即時路況、360° 3D 向量地圖傾斜、磨砂玻璃圖層篩選器與自定義 Markdown 資訊卡。

[![Downloads](https://img.shields.io/github/downloads/cataseven/Google-Map-Card/total?color=41BDF5&logo=home-assistant&label=Downloads&suffix=%20downloads&style=for-the-badge)](https://github.com/cataseven/Google-Map-Card/releases)
[![hacs_badge](https://img.shields.io/badge/HACS-Custom-orange.svg?style=for-the-badge)](https://github.com/hacs/frontend)
[![GitHub Release](https://img.shields.io/github/release/cataseven/Google-Map-Card.svg?style=for-the-badge)](https://github.com/cataseven/Google-Map-Card/releases)
[![License](https://img.shields.io/github/license/cataseven/Google-Map-Card.svg?style=for-the-badge)](LICENSE)
![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2024.1.0%2B-blue.svg?style=for-the-badge)

[English README](README.md) | [設定文檔](#-完整設定與指南) | [快速上手](#-快速開始-yaml)

---

</div>

<p align="center">
  <img src="images/routenew1.png" width="48%" />
  <img src="images/flight.gif" width="48%" />
</p>

---

## ⚡ 核心特色與優勢

* **🚆 即時 GTFS 交通動態引擎**：完美適配 [GTFS2 (`vingerha/gtfs2`)](https://github.com/vingerha/gtfs2) 整合組件。以 30 fps 獨立動畫幀平滑內插車輛位置，精準沿路線軌跡移動，內建獨立向量 SVG 圖標，離線環境無 404 報錯。
* **🎛️ 磨砂玻璃圖層篩選器**：Google 原生控制按鈕風格（$40\times 40\text{ px}$），點擊展開半透明磨砂選單，隨時切換交通、車站、油站或特價圖層。
* **🏷️ 通用比例自適應實體標誌**：任何實體圖片皆可保持原始長寬比顯示為圓角長方形標誌，不拉伸不裁剪。支援屬性點路徑解析（如 `deals.0.image_url`）。
* **💬 動態 Jinja2 + Markdown 彈出視窗**：透過 Home Assistant WebSocket `render_template` 即時渲染，支援 `<ha-markdown allow-svg breaks>` 與 SVG 自定義樣式。
* **🗺️ 360° 3D 向量地圖與 Advanced Markers**：支援 Google Cloud Vector `map_id`，開啟 360° 自由旋轉、傾斜視角與現代 `AdvancedMarkerElement`。
* **🚗 通勤路線與抵達時間計算**：內建路線搜尋面板、即時交通顏色路徑、地點自動完成與一鍵通勤快捷鍵。
* **✈️ FlightRadar24 航班即時追蹤**：專用航班面板、機場起降時間表與地圖互動航班管理。
* **🌐 六大即時數據圖層**：日夜交替晨昏線、RainViewer 即時降雨雷達、WAQI 空氣質素、USGS 全球地震與 Open-Meteo 免金鑰天氣標籤。
* **🌏 繁體中文在地化支援**：原生支援 `zh-HK`（香港繁體）、`zh-TW`（台灣繁體）與 `zh-Hant`。

---

## 🚀 快速開始 (YAML)

```yaml
type: custom:google-map-card
api_key: !secret google_maps_api_key
language: zh-HK
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
      **即時油價：** ${{ state }} / L
      </ha-markdown>
```

---

## 📚 完整設定與指南

| 主題 | 說明 | 連結 |
|:---|:---|:---:|
| 🚀 **安裝與 Google API 設定** | Google Cloud API 金鑰設定、網址防護限制與 HACS 安裝步驟。 | [閱讀安裝指南 →](docs/installation.md) |
| ✨ **功能深入解析** | GTFS2 動態引擎、圖層篩選、實體標誌、動態彈出卡片深度說明。 | [閱讀功能手冊 →](docs/features.md) |
| ⚙️ **完整參數對照表** | 卡片通用設定、實體選項、地圖控制按鈕與範例 YAML。 | [閱讀設定參考 →](docs/reference.md) |
| 📜 **版本更新記錄** | 各版本重大更新歷程與升級說明。 | [閱讀更新記錄 →](docs/changelog.md) |
| 🛠️ **開發與 CI/CD 測試** | 語法驗證、GitHub Actions 自動化測試與 auto-entities 整合指南。 | [閱讀開發手冊 →](docs/development.md) |

---

## ⭐ 社群與支持

若此卡片對您的智慧家庭有所幫助，歡迎在 GitHub 點擊 ⭐ **Star** 支持，或分享給更多 Home Assistant 使用者！
