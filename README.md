# 🍄 Mycelia — Calorie Counter

A bioluminescent mushroom-forest themed calorie, macro, water and exercise tracker. Single-page, no build step, no backend — it runs entirely in the browser and is served straight from GitHub Pages. All data lives privately in your own browser (`localStorage`, plus IndexedDB for progress photos) and is never uploaded.

**Live site:** https://agentkush.github.io/Calorie-counter-website/

![theme](https://img.shields.io/badge/theme-bioluminescent%20forest-2ee6c5) ![storage](https://img.shields.io/badge/data-local%20only-a78bfa) ![charts](https://img.shields.io/badge/charts-Chart.js-34d9ff) ![pwa](https://img.shields.io/badge/PWA-installable%20%26%20offline-5ef08a)

## First run

A skippable **setup wizard** walks new users through units (height/water + weight), sex/age/height/weight, activity and goal in a few taps, then computes their calorie and macro targets. You can re-open it any time from **Settings → Preferences → Run setup wizard**.

## Features

### Today
- **Calorie ring** — animated progress of food eaten against your budget, where **budget = goal − food + exercise**. The centre shows calories left (or "over") and the ring glows red when you exceed it.
- **Macro rings** — protein, carbs and fat vs. their daily targets, with net carbs, fibre, sugar, saturated fat and sodium chips, plus a collapsible **micronutrient panel** (iron, calcium, potassium, magnesium, zinc, vitamin C/A/D, cholesterol) for foods that carry the data, shown as % of a daily target.
- **🥗 Food-quality score** — an A–E grade for the day from protein, fibre, sugar, saturated fat and calorie adherence.
- **Meal logging** — Breakfast, Lunch, Dinner and Snacks; edit or remove any entry (with **Undo**), and **💾 save a meal** to re-log the whole thing later in one tap.
- **⚡ Quick-add calories** and **⧉ copy yesterday** for fast entry; a gentle **low-calorie warning** if your target is very low.
- **💧 Hydration**, **🔥 Exercise** (calories added back to your budget), and an **⏱️ intermittent-fasting timer** (14:10 / 16:8 / 18:6 / 20:4, with a first-timer explainer).
- **🎯 Goal-weight card** with current → goal, ETA, target calories and **BMI**.
- **🌙 Daily check-in** — log energy, mood, hunger and sleep.
- Day switcher (previous / next / tap for today); a chip flags **high days** (calorie cycling) and **diet breaks**.

### Adding food
- ⚡ **Quick** — one-tap re-logging of **saved meals**, **My Foods**, **★ favourites** and **recent** foods, plus a **Quick-add calories** button.
- 🔎 **Search** the [Open Food Facts](https://world.openfoodfacts.org/) database, with **🎤 voice dictation** into the search box.
- 🏷️ **Scan** — barcode lookup by number or **camera scan** (native `BarcodeDetector`).
- 🥗 **Common** — a built-in offline list of ~50 everyday foods.
- ✍️ **Manual** entry, with **Save to My Foods**.

Tap any logged item to edit its quantity, or ✕ to remove (with Undo).

### Calculator, BMI & adaptive coach
- **BMR / TDEE calculator** (Mifflin–St Jeor + activity factor + goal preset, or a **Custom target** by amount and weeks). One tap applies calories + a protein/carb/fat split.
- **BMI** with a healthy/under/over category on the Calc page and the goal card.
- **Goal weight + "reach it in (weeks)"** back-calculates your daily target — you pick the timeframe.
- **🧭 Adaptive coach** (Trends) estimates your *real* daily burn from logged intake vs. your weight trend and suggests an updated target, with optional **weekly auto-adjust** (MacroFactor-style).

### Diet phases & calorie cycling
Set **higher-calorie days** (e.g. training days or weekends) and Mycelia switches that day's goal automatically; start a maintenance **diet break** for a rest from a deficit. (Settings → Plan & cycling.)

### Recipes
**45 recipes** (15 each for fat loss / maintain / muscle gain) with real photos and step-by-step methods. **Search**, filter by **diet** (veg / high-protein / seafood / ★ saved) and by **meal type** (breakfast / lunch / dinner / snack), **🎲 surprise me**, a per-recipe **servings scaler** that scales calories, macros and what gets logged, and **🍳 build your own recipe** — type macros or **total them from ingredients** automatically. A **📅 weekly planner** slots recipes into Mon–Sun and generates a **🛒 grocery list** of whole, shoppable items (copy to clipboard or download as plain text).

### Trends
- 7 / 14 / 30-day **calorie** bar chart with a goal line, a **macros-over-time** line chart, and a **weight** line chart with trend.
- A **13-week logging-streak heatmap** and summary stats.
- **📏 Body measurements** (waist / hips / chest / arms / body-fat %) with change over time, and **📸 progress photos** stored privately on-device (IndexedDB — never uploaded).
- A **📅 weekly review**, **🔬 smart insights** (adaptive TDEE), and the adaptive coach.
- **🏅 38 achievements** — streaks (3 → 100 days), logging volume and variety, protein/calorie/water goal runs, clean-eating days, workouts, weigh-ins, measurements, fasts and fasting streaks, daily check-ins, creating recipes, saving meals and using the planner.

### Reminders
Optional notifications (while the app is open/installed): **water** every 2 h, **meal** nudges (breakfast/lunch/dinner), and a **weekly check-in**.

### Settings
Calorie + macro goals (grams or %), goal weight + weeks, water goal, a **weight-unit picker (kg / stone / lb)** independent of the height & water **Metric/Imperial** toggle, **theme (Dark / Light / Auto)**, a **text-size** option, background-animation toggle, reminders, plan & cycling, the setup wizard, feedback links, a Buy-me-a-coffee link, and **data tools**: export / import JSON, **export & import food log as CSV** (bring data over from other apps), **share a progress card** (PNG), **print / save a PDF report**, and reset.

### Installable & offline (PWA)
A web-app manifest + service worker mean you can **install** Mycelia to your home screen / desktop and use it **offline** (app shell + Chart.js cached). It includes **home-screen shortcuts** (Add food / Log weight), and installed copies auto-update on next online launch.

### Look, feel & accessibility
Layered pine-forest silhouettes, glowing mushrooms and a drifting spore field; light/dark/auto themes; keyboard focus outlines, a larger-text option, and respect for the OS **reduced-motion** setting.

## How calories are calculated

All figures are estimates (not medical advice), but the math is transparent:

| Quantity | Formula |
|----------|---------|
| Food (database / barcode) | nutrition per 100 g ÷ 100 × grams eaten |
| Food (common / manual / recipe) | nutrition per serving × number of servings |
| Energy unit conversion | kcal = kJ ÷ 4.184 (when a product only lists kJ) |
| BMR (Mifflin–St Jeor) | `10 × kg + 6.25 × cm − 5 × age + (male ? +5 : −161)` |
| TDEE | BMR × activity factor (1.2 – 1.9) |
| Daily target | TDEE × (1 + goal adjustment, −20 % … +20 %) |
| BMI | `kg ÷ (m)²` (Underweight < 18.5 · Healthy < 25 · Overweight < 30 · Obese ≥ 30) |
| Adaptive burn (coach) | average logged intake − (weight change × 7700 kcal/kg) ÷ days |
| Protein | bodyweight × 1.9 g/kg (2.2 g/kg when cutting) |
| Fat | 25 % of target ÷ 9 |
| Carbs | remaining calories ÷ 4 |
| Exercise | **MET × bodyweight (kg) × hours** (Walk 3.5 · Run 9.8 · Cycle 7.5 · Weights 5 · Swim 7 · Yoga 3) |
| Custom / goal-weight target | TDEE ± (Δweight in kg × 7700 ÷ (weeks × 7)); floored at 1200 kcal |
| Water (Imperial) | fl oz = ml ÷ 29.5735; 1 US cup = 8 fl oz |
| Day budget | effective goal − food + exercise |

Weight is stored internally in **kilograms** and shown in your chosen unit — **kg**, **stone** (decimal) or **pounds** (1 st = 6.35029 kg = 14 lb). Height and water follow the separate Metric/Imperial toggle.

> **Activity double-counting:** the calculator target already includes an activity factor. If you also log exercise (which adds calories back), choose a lower activity level (e.g. Sedentary) to avoid counting activity twice. The adaptive coach sidesteps this by learning your real burn from results.

## How it works

Everything is one file: [`index.html`](index.html) (HTML + CSS + JS inline). The only external dependency is [Chart.js](https://www.chartjs.org/) from a CDN for the charts. A `sw.js` service worker and `manifest.json` provide the PWA.

Data is stored under the `mycelia_v1` key in `localStorage` — profile/goals, per-day food log, exercise, water, weight history, body measurements, daily check-ins, fasting history, recent/favourite/own foods, saved meals, custom recipes and the weekly plan. **Progress photos** live in a separate IndexedDB store (so they never bloat or risk your main data). New fields merge in over older saves, so updates won't wipe your data, and nothing ever leaves your device.

## Running locally

Open `index.html` in a browser, or serve the folder:

```bash
python -m http.server 8000
# then visit http://localhost:8000
```

(Camera barcode scanning and the service worker need `https://` or `localhost`.)

## Deployment

Served by **GitHub Pages** from the `main` branch root. Push `index.html` (and `sw.js` / `manifest.json` when they change), then enable Pages under **Settings → Pages → Source: Deploy from a branch → `main` / `/ (root)`**. Bump the `CACHE` name in `sw.js` on each release so installed copies pick up the new build.

## Contributing

Bug reports and feature requests are welcome via the in-app **Settings → Feedback** links or the repo's [issue templates](.github/ISSUE_TEMPLATE). See [CONTRIBUTING.md](CONTRIBUTING.md). Licensed under the [MIT License](LICENSE).

## Notes

- Open Food Facts is a free, crowd-sourced database; some products have missing nutrition data. The app skips products without calorie info — use Manual entry when needed.
- Nutrition and calorie-burn figures are estimates, not medical advice.
