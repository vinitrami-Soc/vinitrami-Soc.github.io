# Vinit Rami — Portfolio

Single-file portfolio (`index.html`) — no build step, no dependencies, deploys anywhere — plus
**IntelPulse**, a full-stack SOC triage platform served from the same repo.

## Structure
```
vinit-portfolio/
├── index.html               # everything: markup, styles, scripts (minified)
├── assets/
│   ├── profile.jpg          # original headshot (source of the variants below)
│   ├── profile-800.webp/jpg # About-section portrait (WebP + JPEG fallback)
│   ├── profile-400.webp/jpg # footer polaroid + contact avatar
│   └── Vinit_Rami_CV.pdf    # served by the "Download CV" buttons
├── intelpulse/              # IntelPulse — threat intel & triage workbench (see below)
│   ├── web/                 # the live dashboard (GitHub Pages serves this)
│   ├── backend/             # FastAPI + Celery service, tests, Dockerfile
│   ├── docs/                # scoring model, API reference, screenshots
│   └── docker-compose.yml   # api + worker + beat + redis + postgres + nginx
└── README.md
```

## IntelPulse — /intelpulse/

A threat-intelligence correlation and triage workbench: paste an alert, raw syslog or a JSON export,
and it extracts the indicators, queries AbuseIPDB, AlienVault OTX, GreyNoise, ThreatFox and URLhaus
concurrently, scores them into one auditable verdict, graphs how they relate and writes a
Jira-ready SOC ticket.

* **Live demo:** <https://vinitrami-soc.github.io/intelpulse/> — runs a bundled *synthetic* dataset in
  the browser (clearly labelled), so it works with no backend and no API keys.
* **Run the real thing:** `cd intelpulse && cp .env.example .env && docker compose up --build`
  → API on `:8000/docs`, dashboard on `:8080`.
* **Docs:** [project README](intelpulse/README.md) · [scoring model](intelpulse/docs/SCORING.md) ·
  [API reference](intelpulse/docs/API.md) · [security posture](intelpulse/docs/SECURITY.md) ·
  [design system](intelpulse/docs/DESIGN.md)
* **Tests:** `cd intelpulse && make test` (166 backend, incl. the security suite and the
  3,400-line extraction corpus), `make test-web` (56 node tests: engine parity, console model,
  design-system guards), `make test-ui` (260 Chromium checks across the workbench and campaign graph,
  site + console, and phone/tablet/assistant: XSS, hostile URLs, degradation, both graphs, theming,
  accessibility, forced colours, touch targets), `make audit` (pip-audit).
To change the headshot: replace profile.jpg, then regenerate variants:
`npx sharp-cli -i assets/profile.jpg -o assets/profile-800.webp resize 800` (repeat for -800.jpg, -400.webp, -400.jpg)

## Run locally
```
python -m http.server 8123 --directory vinit-portfolio
# open http://localhost:8123
```
(Opening index.html directly also works; fonts/video need internet.)

## Deploy to Netlify
Drag the **whole `vinit-portfolio` folder** onto https://app.netlify.com/drop — done.
Or connect the folder as a repo; no build command, publish directory = `/`.

⚠️ Deploy the FOLDER, never just index.html — the photo, fonts and CV live in
`assets/`. If only index.html is uploaded, the photo and fonts will not show.

## Things you can swap
- **Footer video**: the old Cloudflare Stream URL returns 404 (video was deleted).
  Upload a new video to Cloudflare Stream and replace `HLS_SRC` in index.html —
  the player preflights the URL and auto-falls back to the gradient + photo if it's missing.
- **Photo**: replace `assets/profile.jpg` (used in About, Contact, Footer).
- **CV**: replace `assets/Vinit_Rami_CV.pdf`.
- **Theme default**: first visit follows the visitor's system preference; the
  navbar toggle persists their choice in localStorage (`vr-theme`).

## Easter eggs
- Press `~` (or the floating button / the "Feeling lucky?" cube) → interactive terminal.
- Commands: help, whoami, skills, certs, projects, contact, cv, theme, nmap,
  sudo hire-vinit, ls, cat flag.txt, clear, exit.

## Licence
Two sets of terms, because this repository holds two kinds of work:

- **Code** — everything under `intelpulse/`, and the site's own HTML, CSS and
  JavaScript — is MIT. Build your own site with it.
- **Personal content** — the photographs, `assets/Vinit_Rami_CV.pdf`, the
  biography and the name — is all rights reserved. Reusing the code is welcome;
  reusing the identity is not.
- **Fonts** in `assets/fonts/` are third-party, under the SIL Open Font
  Licence. See `assets/fonts/LICENSE.md`.

Full text in [`LICENSE`](LICENSE).
