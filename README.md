# 🍄 Mycelia — Calorie Counter

A bioluminescent mushroom-forest themed calorie, macro, water and exercise tracker. Single-page, no build step, no backend — it runs entirely in the browser and is served straight from GitHub Pages. All data lives privately in your own browser (`localStorage`).

**Live site:** https://agentkush.github.io/Calorie-counter-website/

![theme](https://img.shields.io/badge/theme-bioluminescent%20forest-2ee6c5) ![storage](https://img.shields.io/badge/data-local%20only-a78bfa) ![charts](https://img.shields.io/badge/charts-Chart.js-34d9ff)

## Features

### Today
- **Calorie ring** — animated progress of food eaten against your budget, where **budget = goal − food + exercise**. The centre shows calories left (or "over"), and the ring glows red when you exceed the budget.
- **Macro rings** — protein, carbs and fat vs. their daily targets.
- **Meal logging** — Breakfast, Lunch, Dinner and Snacks, each with its own running total; edit or remove any entry.
- **💧 Hydration** — a glowing fill-up glass with −250 / +250 ml buttons, a cups read-out, and a goal you set in Settings (default 2000 ml).
- **🔥 Exercise** — log workouts; the calories burned are added back to your daily budget.
- Day switcher (previous / next / tap for today) — every section is per-day.

### Adding food
- ⚡ **Quick** — one-tap re-logging of your **My Foods**, **★ favourites**, and **recent** foods (tap the star on any food to pin it).
- 🔎 **Search** the [Open Food Facts](https://world.openfoodfacts.org/) database (millions of products, no API key).
- 🏷️ **Scan** — barcode lookup by number, plus optional **camera scan** (uses the native `BarcodeDetector` where supported).
- 🥗 **Common** — a built-in list of ~50 everyday foods that works fully offline.
- ✍️ **Manual** entry for anything else, with **Save to My Foods** to keep your own foods/meals for instant re-logging.

A quantity step lets you set grams (database/barcode foods) or servings (common/manual) with a live nutrition preview before adding. **Tap any logged item to edit its quantity**, or the ✕ to remove it.

### Exercise with accurate calories
Pick an activity (Walk, Run, Cycle, Weights, Swim, Yoga) and a **duration** (quick chips for 15 m → 2 h, or any custom minutes). Calories are computed from your body weight using the standard MET method and the number shown is exactly what gets logged. You can always type a calorie value in directly.

### BMR / TDEE calculator
Mifflin–St Jeor BMR with an activity multiplier and a goal preset (−20 % … +20 %). One tap applies the result — calorie target **and** a protein/carb/fat split — as your daily goals. A **Custom target** option lets you enter how much you want to gain or lose and over how many weeks; it works out the daily calories from the energy in body weight (3500 kcal/lb, 7700 kcal/kg), with a 1200-kcal safety floor and a heads-up when the pace is aggressive.

### Recipe ideas
A **Recipes** tab suggests 27 meals matched to your goal — fat loss, maintain, or muscle gain (it defaults to the goal you set in the calculator). You can **search** by name or ingredient, filter by **diet** (vegetarian / high-protein / seafood), mark **favourites** (★ Saved), and hit **🎲 Surprise me** for a random pick. Each card shows a real photo, per-serving calories and macros, ingredients, and a one-tap **Log it**. Photos are hot-linked from TheMealDB and Wikimedia Commons (with an emoji-tile fallback if one ever fails to load), and recipe calories are derived from their macros so logging one keeps your day's totals consistent.

### Trends
7 / 14 / 30-day calorie bar chart with a goal line, a weight line chart, and summary stats: average intake, day streak, days logged, and weight change. An **Achievements** grid awards glowing badges as you build streaks and hit goals (logging, protein/calorie/water goals, workouts, weigh-ins, consistency).

### Settings
Manual calorie + macro goals, water goal, metric/imperial units, background-animation toggle, and full **export / import / reset** of your data as JSON. Switching to **Imperial** shows weight in lb, height in inches, and the water tracker in **US fl oz / cups** (Metric uses kg, cm and ml).

### Look & feel
Layered pine-forest silhouettes, glowing bioluminescent mushrooms, and a drifting spore particle field — mobile-first and responsive, with a reduced-motion fallback.

## How calories are calculated

All figures are estimates (not medical advice), but the math is transparent:

| Quantity | Formula |
|----------|---------|
| Food (database / barcode) | nutrition per 100 g ÷ 100 × grams eaten |
| Food (common / manual) | nutrition per serving × number of servings |
| Energy unit conversion | kcal = kJ ÷ 4.184 (when a product only lists kJ) |
| BMR (Mifflin–St Jeor) | `10 × kg + 6.25 × cm − 5 × age + (male ? +5 : −161)` |
| TDEE | BMR × activity factor (1.2 – 1.9) |
| Daily target | TDEE × (1 + goal adjustment, −20 % … +20 %) |
| Protein | bodyweight × 1.9 g/kg (2.2 g/kg when cutting) |
| Fat | 25 % of target ÷ 9 |
| Carbs | remaining calories ÷ 4 |
| Exercise | **MET × bodyweight (kg) × hours** (Walk 3.5 · Run 9.8 · Cycle 7.5 · Weights 5 · Swim 7 · Yoga 3) |
| Custom target | TDEE ± (weekly rate × 3500 kcal/lb or 7700 kcal/kg ÷ 7); floored at 1200 kcal |
| Water (Imperial) | fl oz = ml ÷ 29.5735; 1 US cup = 8 fl oz |
| Day budget | goal − food + exercise |

Imperial inputs are converted automatically (in → cm × 2.54, lb → kg × 0.453592).

> **Note on activity double-counting:** the calculator's target already includes an activity factor. If you also log exercise (which adds calories back), activity is counted twice. If you plan to log workouts, choose a lower activity level (e.g. Sedentary) in the calculator.

## How it works

Everything is one file: [`index.html`](index.html) (HTML + CSS + JS inline). The only external dependency is [Chart.js](https://www.chartjs.org/), loaded from a CDN for the trend charts.

Data is stored under the `mycelia_v1` key in `localStorage` — profile/goals, per-day food log, exercise, water, weight history, and your recent/favourite foods — so it stays on the device you use and is never uploaded anywhere. New fields merge in over older saves, so updates won't wipe your data.

## Running locally

Open `index.html` in a browser, or serve the folder:

```bash
python -m http.server 8000
# then visit http://localhost:8000
```

(Camera barcode scanning needs `https://` or `localhost`.)

## Deployment

Served by **GitHub Pages** from the `main` branch root. Push `index.html` to the repo, then enable Pages under **Settings → Pages → Source: Deploy from a branch → `main` / `/ (root)`**.

## Notes

- Open Food Facts is a free, crowd-sourced database; some products have missing or imperfect nutrition data. The app skips products without calorie info — fall back to Manual entry when needed.
- Nutrition and calorie-burn figures are estimates, not medical advice.
