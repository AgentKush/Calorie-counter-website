# Security Policy

## Supported versions

Mycelia is a single-page web app served from the `main` branch via GitHub
Pages. Only the currently deployed version (the latest `main`) is supported.
There are no older release branches to patch.

| Version            | Supported          |
| ------------------ | ------------------ |
| Latest (`main`)    | :white_check_mark: |
| Anything older     | :x:                |

## How the app handles your data

Mycelia is a **client-side only** app. There is no backend and no account:

- All of your data (food log, weights, goals, settings) is stored locally in
  your own browser via `localStorage`. It never leaves your device.
- The only outbound network requests are:
  - the [Open Food Facts](https://world.openfoodfacts.org/) API, used when you
    search for or scan a food, and
  - the Chart.js library, loaded from the jsDelivr CDN.
- No analytics, trackers, cookies, or ads.

Because of this, the security surface is small — but reports are still welcome.

## Reporting a vulnerability

If you find a security issue (for example an XSS vector in how logged text or
imported JSON is rendered, or a problem with the service worker), please report
it privately rather than opening a public issue:

- **Preferred:** open a private
  [GitHub Security Advisory](https://github.com/AgentKush/Calorie-counter-website/security/advisories/new).
- **Or email:** finlayhansford66@gmail.com

Please include steps to reproduce and the affected version/commit. I aim to
acknowledge reports within a few days and to fix confirmed issues as soon as is
practical. Please give a reasonable window to address the issue before any
public disclosure.

Thank you for helping keep Mycelia and its users safe.
