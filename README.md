# PRINCE — a video editor's edit bay

A responsive, six-page portfolio for **Prince, a video editor**, built on the green cutting-mat design language: tactile studio stationery, a scroll-scrubbed three-step process, and motion that stays out of the way. Serve the `dist` directory with any static web server. There is no build step and no runtime dependency. Links use root-relative paths.

The homepage lives in `dist/index.html`; the archive and biography are `dist/work.html` and `dist/about.html`. Three complete case studies live in `dist/projects/`: FORME (fashion campaign film), SONAR (brand film with sound and motion) and Daylight (product launch film). Shared styles and interactions are in `dist/styles.css`, `dist/expanded.css` and `dist/app.js`. Optimized original imagery and self-hosted fonts live in `dist/assets`.

## Editing the content

Everything is plain HTML — search and replace inside `dist/` and you are done.

- **Name and brand:** the hero name is split into one `<span>` per letter in `dist/index.html` (`<h1 aria-label="Prince">`), and the `p` mark appears in the header, footer, intro overlay and the SVG favicon on every page.
- **Portfolio copy:** project descriptions, experience and toolkit entries are illustrative portfolio copy. Case studies are framed as independent concepts, not commissioned work.
- **Contact:** the site uses the illustrative address `hello@princeedits.com` in `dist/index.html`. Replace it with the real address before sharing publicly.
- **Location:** the site says "Remote-first · working worldwide" rather than naming a city — swap that anywhere it appears in `dist/index.html` and `dist/about.html` if you want a real location.

## Run locally

Serve the static output with Python:

```sh
python3 -m http.server 8080 --directory dist
```

Open `http://localhost:8080`. Use a web server rather than opening HTML files directly, because the pages use root-relative links.

## Deploy

This is a complete static site with no package installation, build step, API keys, or external asset dependencies. Set the host's publish/output directory to `dist`, leave the build command empty, and serve its contents from the domain root. Keep the `projects` and `assets` directories intact.

## What's included

Full project navigation, archive filters, keyboard-operable experience tabs, pause-motion preference, pointer parallax, draggable stationery, off-screen object entrances, directional card reveals, a scroll-scrubbed three-step editing process (review → assembly → grade and delivery), interactive typography and colour experiments, and reduced-motion support. The process sequence renders as a normal readable stack when motion is paused.

Animation uses native CSS transforms and requestAnimationFrame. The scroll sequence follows ordinary page scroll and does not capture wheel or touch scrolling. Reveal positions are measured before transform effects, so cards entering from outside the viewport can still be triggered reliably.

## Credits

Adapted from the [greenportfolio](https://github.com/gireeshkumarreddy/greenportfolio) template by Gireesh Kumar Reddy — layout, stationery artwork, self-hosted fonts and animation system, re-written for Prince. Font licensing details are in `licenses/`. Asset generation notes are in `asset-prompts.json`.
