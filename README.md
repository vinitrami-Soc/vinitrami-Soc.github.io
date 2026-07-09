# Vinit Rami — Portfolio

Single-file portfolio (`index.html`) — no build step, no dependencies, deploys anywhere.

## Structure
```
vinit-portfolio/
├── index.html               # everything: markup, styles, scripts (minified)
├── assets/
│   ├── profile.jpg          # original headshot (source of the variants below)
│   ├── profile-800.webp/jpg # About-section portrait (WebP + JPEG fallback)
│   ├── profile-400.webp/jpg # footer polaroid + contact avatar
│   └── Vinit_Rami_CV.pdf    # served by the "Download CV" buttons
└── README.md
```
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
