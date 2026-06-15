# 🍄 Mycelia — Calorie Counter

A bioluminescent-themed calorie and macro tracker. Single-page, no build step, no backend — it runs entirely in the browser and is served straight from GitHub Pages. All data lives privately in your own browser (`localStorage`).

**Live site:** https://agentkush.github.io/Calorie-counter-website/

![theme](https://img.shields.io/badge/theme-bioluminescent%20forest-2ee6c5) ![storage](https://img.shields.io/badge/data-local%20only-a78bfa) ![deps-Chart.js-34d9ff](https://img.shields.io/badge/charts-Chart.js-34d9ff)

## Features

- **Today dashboard** — animated calorie ring (consumed vs. goal, glows red when over) plus protein / carbs / fat macro rings.
- **Meal logging** — Breakfast, Lunch, Dinner and Snacks with per-meal totals; edit/remove entries.
- **Food sources**
  - 🔎 **Search** the [Open Food Facts](https://world.openfoodfacts.org/) database (millions of products, no API key).
  - 🏷️ **Barcode** lookup by number, plus optional **camera scan** (uses the native `BarcodeDetector` where supported).
  - 🥗 **Common foods** — a built-in list of ~50 everyday foods that works fully offline.
  - ✍️ **Manual entry** for anything else.
- **BMR / TDEE calculator** — Mifflin–St Jeor equation with activity multiplier and a goal adjustment; one tap applies the result (calories + macro split) as your daily goals.
- **Trends** — 7 / 14 / 30-day calorie bar chart with a goal line, weight line chart, and summary stats (average intake, day streak, days logged, weight change).
- **Settings** — manual goals, metric/imperial units, animation toggle, and full **export / import / reset** of your data as JSON.
- Mobile-first, responsive, with a glowing animated spore background.

## How it works

Everything is one file: [`index.html`](index.html) (HTML + CSS + JS inline). The only external dependency is [Chart.js](https://www.chartjs.org/) loaded from a CDN for the trend charts.

Data is stored under the `mycelia_v1` key in `localStorage`, so it stays on the device you use and is never uploaded anywhere.

## Running locally

Just open `index.html` in a browser, or serve the folder:

```bash
python -m http.server 8000
# then visit http://localhost:8000
```

(Camera barcode scanning needs `https://` or `localhost`.)

## Deployment

Served by **GitHub Pages** from the `main` branch root. Push `index.html` to the repo, then enable Pages under **Settings → Pages → Source: Deploy from a branch → `main` / `/ (root)`**.

## Notes

- Open Food Facts is a free, crowd-sourced database; some products may have missing or imperfect nutrition data. The app skips products without calorie info and you can always fall back to manual entry.
- Nutrition figures are estimates — not medical advice.
