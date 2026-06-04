# 🏟️ SporTrips — The Sports Road Trip Machine

Tell it your dates, how far you're willing to drive each day, and which sports you care about — SporTrips cross-references real game schedules against real drive times and hands you several itinerary options you can actually pull off.

It's the thing that's surprisingly painful to do by hand: there are too many schedules, drive times, and league combinations to juggle in your head.

## ✨ Features

- **Start from anywhere** — type any street address, landmark, or city (or tap 📍 for your current location). Geocoded via [Photon](https://photon.komoot.io) with [Nominatim](https://nominatim.openstreetmap.org) as a fallback.
- **Live schedules** — pulls real games from ESPN's public scoreboard API for MLB, NBA, NHL, and NFL. Falls back to a built-in season-aware sample schedule if it can't reach the network (and tells you so).
- **Real drive math (metric)** — distances from a built-in table of all 124 MLB/NBA/NHL/NFL venue coordinates (great-circle × 1.25 road-detour factor at ~100 km/h). A trip only links two games if you can cover the distance within your rest days at your daily driving limit. All distances are in kilometres.
- **Multiple itinerary strategies** — every search returns up to four distinct options:
  - **Max Games** — cram in everything you can make
  - **Least Driving** — tightest cluster, minimal windshield time
  - **Sampler Platter** — most different sports & teams
  - **Scenic Cruise** — a rest day between games
- **Interactive maps** — each itinerary is drawn on a real [Leaflet](https://leafletjs.com) map (dark [CARTO](https://carto.com/attributions) / [OpenStreetMap](https://openstreetmap.org/copyright) tiles, full North America coverage) with the route line, numbered league-colored pins, and clickable popups for each game.

## 🚀 Usage

It's a single self-contained file with no build step. The only runtime dependency is [Leaflet](https://leafletjs.com), loaded from a CDN for the maps. Just open it:

```sh
open index.html
```

Or serve it locally:

```sh
python3 -m http.server 8000   # then visit http://localhost:8000
```

> Live schedules and geocoding need an internet connection. ESPN reliably posts schedules for the current and upcoming weeks; far-future dates or out-of-season leagues may come back empty.

## 🔧 How it's built

Plain HTML + CSS + JavaScript in one file — no frameworks, no API keys (Leaflet via CDN for maps).

- `generateSchedule()` — the offline sample-schedule generator (the swappable seam).
- `fetchLiveSchedule()` / `parseEvent()` — ESPN integration, matching home teams to venue coordinates.
- `geocode()` — address → lat/lon (Photon, Nominatim fallback).
- `buildTrip()` / `planFromPool()` — the routing & itinerary engine (metric).
- `buildLeaflet()` — renders each itinerary on a Leaflet map.

## 📝 License

MIT
