# WatchfulAI Frontend

**Live Security Intelligence Dashboard — Johannesburg**

WatchfulAI is a real-time dashboard that visualizes security and safety reports on an interactive map. It ingests incident data from sensors and WhatsApp, classifies it by severity, and surfaces clusters of related reports as alerts — giving operators a live picture of what's happening across the city.

## Features

- **Live heatmap** of incoming reports rendered with [Leaflet](https://leafletjs.com/) and [Leaflet.heat](https://github.com/Leaflet/Leaflet.heat) on a dark CARTO basemap
- **Severity classification** with colour-coded markers and badges:
  - 🔴 `EMERGENCY`
  - 🟠 `SUSPICIOUS`
  - 🟢 `NOISE`
- **Live stats bar** — running totals for emergencies, suspicious activity, noise, and reports by source (sensor vs. WhatsApp)
- **Recent reports panel** — scrollable, clickable list that flies the map to a report's location
- **Cluster alert log** — automatically flags groups of related reports in the same area
- **Auto-refresh** — polls the backend every 30 seconds, no manual reload needed

## Tech Stack

- Plain HTML/CSS/JS — no build step, no framework, no dependencies to install
- [Leaflet.js](https://leafletjs.com/) (via CDN) for mapping
- [Leaflet.heat](https://github.com/Leaflet/Leaflet.heat) (via CDN) for heatmap overlays
- CARTO dark basemap tiles

## Project Structure

```
.
├── index.html      # Entire app: markup, styles, and logic
├── style.css        # Reserved for future extraction of styles (currently unused)
├── app.js         # Reserved for future extraction of app logic (currently unused)
└── README.md
```

> Note: the dashboard is currently self-contained in `index.html` (styles and script are inline). `style.css` and `app.js` exist as placeholders for a future refactor that separates concerns.

## Backend

The dashboard expects a WatchfulAI backend API and currently points to:

```
https://watchfulai-backend-1.onrender.com
```

It consumes two endpoints:

| Endpoint     | Description                                                        |
|--------------|----------------------------------------------------------------------|
| `GET /reports`  | Returns all reports (`lat`, `lng`, `label`, `message`, `location_name`, `source`, `created_at`) |
| `GET /clusters` | Returns groups of related reports used to populate the alert log |

To point the dashboard at a different backend, update the `BACKEND` constant near the top of the `<script>` block in `index.html`.

## Getting Started

No build tools or dependencies required — this is a static site.

1. Clone the repo:
   ```bash
   git clone https://github.com/NjabuloNyawuza/watchfulai-frontend
   cd watchfulai-frontend
   ```
2. Open `index.html` directly in a browser, or serve it locally:
   ```bash
   python3 -m http.server 8000
   ```
3. Visit `http://localhost:8000` in your browser.

The map defaults to Johannesburg (`-26.2041, 28.0473`) and will begin polling the backend for reports immediately.

## Roadmap Ideas

- Extract inline styles/script into `style.css` and `app.js`
- Make the backend URL configurable via environment/config file
- Add filtering by report type or time range
- Add authentication for operator access

## License

No license specified yet.
