# Contributing to Mycelia

Thanks for your interest in improving Mycelia 🍄 — a free, private,
bioluminescent calorie & macro tracker. Contributions, bug reports and ideas
are all welcome.

## Reporting bugs & requesting features

Please use the issue forms:

- 🐛 [Report a bug](https://github.com/AgentKush/Calorie-counter-website/issues/new?template=bug_report.yml)
- 💡 [Request a feature](https://github.com/AgentKush/Calorie-counter-website/issues/new?template=feature_request.yml)

Search the [existing issues](https://github.com/AgentKush/Calorie-counter-website/issues)
first in case it's already been raised.

## Project layout

Mycelia is intentionally simple — there is **no build step**:

- `index.html` — the entire app: HTML, CSS and vanilla JavaScript inline. The
  only runtime dependency is Chart.js from a CDN.
- `sw.js` — service worker (offline support / PWA updates). Bump the `CACHE`
  name whenever assets change so installed copies refresh.
- `manifest.json`, `icon*.png`, `icon.svg` — PWA install metadata and icons.
- `robots.txt`, `sitemap.xml`, `og.png` — SEO / link-preview assets.

All user data lives in the browser's `localStorage` (key `mycelia_v1`). There
is no backend.

## Running it locally

Because it's a static site, just open `index.html` in a browser. For the
service worker and PWA features to work you'll want to serve it over HTTP, e.g.:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Making changes

1. Fork the repo and create a branch for your change.
2. Keep changes focused and match the existing code style.
3. If you change calorie/macro/weight math, update the values so calories still
   reconcile to macros (`kcal = protein*4 + carbs*4 + fat*9`).
4. Test in a browser: log food, check the rings, trends, recipes and settings,
   and try it on a narrow mobile viewport.
5. Open a pull request describing **what** changed and **why**.

## Code style

- Vanilla JS, no frameworks or bundlers — please keep it that way.
- Match the surrounding formatting and naming.
- Prefer the minimum change that solves the problem.

By contributing, you agree that your contributions are licensed under the
project's [MIT License](LICENSE).
