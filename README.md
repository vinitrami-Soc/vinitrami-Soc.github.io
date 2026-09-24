# Vinit Rami · Portfolio

**Live site:** https://vinitrami-soc.github.io

Portfolio of Vinit Rami, cybersecurity analyst: VAPT, digital forensics, and
SOC automation. It is one static page with no build step and no dependencies,
served by GitHub Pages from `main`.

## Projects featured on the site

| Project | What it is | Links |
| --- | --- | --- |
| **IntelPulse** | Threat-intelligence correlation and SOC triage workbench | [Live demo](https://vinitrami-soc.github.io/intelpulse/) · [Source](https://github.com/vinitrami-Soc/intelpulse) |
| **PhishHawk** | Phishing triage engine for reported emails | [Source](https://github.com/vinitrami-Soc/phishhawk) |

## Structure

```
.
├── index.html                 # the whole site: markup, styles and scripts
├── assets/
│   ├── profile.jpg            # original headshot (source for the variants below)
│   ├── profile-800.webp/.jpg  # About-section portrait (WebP with JPEG fallback)
│   ├── profile-400.webp/.jpg  # footer photo and contact avatar
│   ├── Vinit_Rami_CV.pdf      # served by the "Download CV" buttons
│   └── fonts/                 # self-hosted WOFF2 fonts (SIL OFL, see fonts/LICENSE.md)
├── .nojekyll                  # tells GitHub Pages to serve files as-is
└── LICENSE
```

## Run locally

```bash
python3 -m http.server 8123
# open http://localhost:8123
```

Opening `index.html` directly also works.

## Updating content

- **Photo:** replace `assets/profile.jpg`, then regenerate the variants, e.g.
  `npx sharp-cli -i assets/profile.jpg -o assets/profile-800.webp resize 800`
  (repeat for `-800.jpg`, `-400.webp` and `-400.jpg`).
- **CV:** replace `assets/Vinit_Rami_CV.pdf`.
- **Theme:** the first visit follows the visitor's system preference; the
  navbar toggle saves their choice in `localStorage` (`vr-theme`).

## Easter egg

Press `~` (or use the floating button or the "Feeling lucky?" cube) to open an
interactive terminal. Try `help`, `whoami`, `skills`, `certs`, `projects`,
`contact`, `cv`, `theme`, `nmap`, `sudo hire-vinit`, `ls` and `cat flag.txt`.

## Licence

This repository holds two kinds of work, under different terms:

- **Code:** the site's HTML, CSS and JavaScript are MIT. You're welcome to
  build your own site with it.
- **Personal content:** the photographs, `assets/Vinit_Rami_CV.pdf`, the
  biography and the name are all rights reserved. Reuse the code, not the
  identity.
- **Fonts** in `assets/fonts/` are third-party, under the SIL Open Font
  Licence. See `assets/fonts/LICENSE.md`.

Full text in [`LICENSE`](LICENSE).
