# Downloader Zone TOTP Generator

[![License: GPL-3.0](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://opensource.org/licenses/GPL-3.0) [![Deploy: GitHub Pages](https://img.shields.io/badge/Deploy-GitHub%20Pages-222222)](https://2fa.downloader.zone/)

A small, secure, and privacy-focused browser application for generating Time-Based One-Time Passwords (TOTP). All cryptographic operations run locally in the browser using the Web Crypto API, so secrets never leave your device.

Live demo: https://2fa.downloader.zone/

## Quick links

- Overview: [#overview](#overview)
- Install & Run: [#installation-and-running-locally](#installation-and-running-locally)
- Security & Privacy: [#security--privacy](#security--privacy)
- Development: [#development](#development)
- Contributing: [#contributing](#contributing)
- License: [#license](#license)

## Overview

This project provides a minimal, dependency-free TOTP generator that runs entirely in the browser. It supports common TOTP parameters (digits, period, algorithm) and includes features for exporting/sharing configuration via URL hash without leaking secrets to servers.

Key goals:

- Privacy-first: secrets never leave the client.
- Small and auditable: plain HTML/CSS/JS for easy review.
- Deployable via GitHub Pages or any static host.

## Features

- Offline TOTP generation using the Web Crypto API
- Configurable digits, period, and HMAC algorithm
- Option to fetch UTC time as an alternate time source
- Shareable configuration encoded in the URL hash (does not include secrets)
- Static, dependency-free codebase (no build step required)

## Installation and running locally

Clone the repository and open the project in a browser, or run a small static server.

```bash
git clone https://github.com/DownloaderZone/TOTP-Generator.git
cd TOTP-Generator
# Option A: open index.html in your browser (double-click or file://)
# Option B: serve locally with Python 3 built-in server
python3 -m http.server 8000
# then open http://localhost:8000

# Option C: use node static server (if you have npm)
npm install -g serve
serve -s .
```

Notes:

- Opening `index.html` via `file://` works for most features, but some browsers restrict certain APIs for local files. Using a simple local server avoids those issues.

## Usage

1. Open the app (live site or local server).
2. Enter a Base32 secret (local only).
3. Adjust advanced settings only if needed (digits, period, algorithm).
4. Choose time source: device clock (default) or fetch UTC time.
5. Copy the generated code or use the configuration URL to share settings (the URL hash excludes secrets).

## Security & privacy

- Secrets are never transmitted to a server by the app. The URL hash may store non-secret configuration but does not include the shared secret.
- The app uses the browser's Web Crypto API for HMAC operations; this is considered secure when used properly by modern browsers.
- If you need maximum assurance, audit `script.js` yourself — the entire implementation is contained in a single, human-readable file.

Recommendations:

- Prefer using the live site over third-party deployments only if you trust the hosting and DNS configuration.
- For very high-security use cases, prefer hardware authenticators or platform-backed authenticators.

## Development

This is a static site. Files of interest:

- `index.html` — application UI and metadata
- `script.js` — TOTP implementation and UI logic
- `styles.css` — visual styling

There is no build toolchain. Edit files directly and reload the browser to test changes.

Suggested local test flow:

1. Start local server (`python3 -m http.server 8000`).
2. Open browser devtools (Console) and test entering known secrets.

## Deployment

The site is served from GitHub Pages and uses `CNAME` for the custom domain `2fa.downloader.zone`. To deploy:

1. Push updates to the `main` branch.
2. Ensure `gh-pages` or GitHub Pages is configured to serve from the `main` branch (or repository settings as desired).

## Contributing

Contributions are welcome. Suggested workflow:

1. Fork the repository.
2. Make changes on a feature branch.
3. Open a pull request describing the change and any testing performed.

Please keep changes small and focused. For security-sensitive changes (cryptography, time handling), include rationale and tests or examples demonstrating correctness.

## Troubleshooting

- If TOTPs don't match your server, check clock drift and try the UTC time source.
- Confirm secret encoding (Base32) and correct digit/period settings.

## License

This project is released under the [GPL-3.0 License](LICENSE).

---
 