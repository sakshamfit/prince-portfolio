# PRINCE — a video editor's edit bay

A responsive, six-page portfolio for **Prince, a video editor**, built on the green cutting-mat design language: tactile studio stationery, a scroll-scrubbed three-step process, a familiar edit-bay visual, and motion that stays out of the way. Serve the `dist` directory with any static web server. There is no build step and no runtime dependency. Links use root-relative paths.

The homepage lives in `dist/index.html`; the archive and biography are `dist/work.html` and `dist/about.html`. The Work sections on both pages are a wall of seven real client films embedded from Prince's Google Drive (see [The films](#the-films-google-drive) below). Shared styles and interactions are in `dist/styles.css`, `dist/expanded.css` and `dist/app.js`. Prince's own photography, the reference-guided studio scenes, the stationery artwork and the self-hosted fonts live in `dist/assets`.

Three earlier case studies still sit in `dist/projects/` (FORME, SONAR, Daylight). They are no longer linked from anywhere on the site — the Work sections now show the real client films instead. Keep or delete that folder, whichever you prefer.

## The films (Google Drive)

The Work sections on `/` and `/work.html` show the seven clips from the shared Drive folder [“my video”](https://drive.google.com/drive/folders/11PwkKzJgcLpD9PtuN_kJD4mKw8hPUlHB). Nothing is copied into this repository — the page pulls what it needs straight from Google:

- **Poster still:** `https://drive.google.com/thumbnail?id=FILE_ID&sz=w1600`, with `https://lh3.googleusercontent.com/drive-storage/…=s1600` as the fallback. Both are real frames from the clip, so the wall reads as a film strip rather than a row of identical placeholders. If Drive refuses both (file made private, host blocked, offline) the tile falls back to a titled cutting-mat card instead of a broken image.
- **Playback:** clicking a poster swaps in `https://drive.google.com/file/d/FILE_ID/preview?autoplay=1` in an iframe, right inside the grid. Google's own player means full quality, sound and fullscreen — and it is the only route that works without hosting the files ourselves. One clip plays at a time; `Close ✕`, `Esc` or opening another clip stops it.

Each tile is one `<article class="clip">` block, duplicated in `dist/index.html` and `dist/work.html`. To swap a film, change the `data-drive-id` (and the `href`) on the `.clip-open` link, the `id=` in the two poster URLs, plus the `<h3>` title and date. The first tile carries `clip-feature` for the wide two-column slot — move that class if a different film should lead.

Two things worth knowing about Drive as a video host:

- Every file must stay shared as **Anyone with the link** → Viewer, or the posters and the player both go blank for visitors.
- Drive's preview player tops out at 1080p and Google can throttle a file that suddenly gets heavy traffic. If the reel ever needs guaranteed quality or analytics, upload the MP4s to something like Mux, Cloudflare Stream or a plain object store — the markup only needs the two URLs swapped.

The names on the wall are the client names from the folder (`BTK Curators`, `DAV`, `Naman Sir`, `Narayani Hospital`, `Ramada`). Edit them freely in the HTML.

## Editing the content

Everything is plain HTML — search and replace inside `dist/` and you are done.

- **Name and brand:** the hero name is split into one `<span>` per letter in `dist/index.html` (`<h1 aria-label="Prince">`), and the `p` mark appears in the header, footer, intro overlay and the SVG favicon on every page.
- **Portfolio copy:** the clip titles, dates and the copy around the wall are plain HTML; experience and toolkit entries are illustrative portfolio copy.
- **Contact:** the site uses the illustrative address `hello@princeedits.com` in `dist/index.html`. Replace it with the real address before sharing publicly.
- **Location:** the site says "Remote-first · working worldwide" rather than naming a city — swap that anywhere it appears in `dist/index.html` and `dist/about.html` if you want a real location.

## Prince's image

Every picture of Prince on the site is the same generated studio portrait, `dist/assets/prince-studio.webp` — he is standing on the forest-green backdrop, and the same file is used for the hero print, the about-page cards, the case-study pull quotes and the round contact sticker. (The Work section no longer carries a studio frame: its poster stills come from the Drive clips.) Wise framing (`object-position` in `expanded.css`) keeps his face readable inside the square, wide and circular crops.

`AirBrush_20260317004701.jpg.jpeg` in the repository root is the reference photograph the portrait was generated from. It is deliberately **not** part of the site: the deploy publishes `dist/` only, so no crop of the original photograph ships. Keep the file if you want to generate more scenes against his face; see `asset-prompts.json`.

Two further generated scenes, `prince-edit-bay.webp` and `prince-edit-gear.webp`, show him at the edit desk and in the monitor light — they fill the "Inside the timeline" section.

## Run locally

Serve the static output with Python:

```sh
python3 -m http.server 8080 --directory dist
```

Open `http://localhost:8080`. Use a web server rather than opening HTML files directly, because the pages use root-relative links.

## Deploy

This is a complete static site with no package installation, build step, API keys, or external asset dependencies. Set the host's publish/output directory to `dist`, leave the build command empty, and serve its contents from the domain root. Keep the `projects` and `assets` directories intact.

### Vercel

`vercel.json` in the repository root pins the settings Vercel needs: Framework Preset **Other** (`framework: null`), no install or build command, and **`outputDirectory: "dist"`**. Without an explicit output directory Vercel serves `public/` if it exists and the repository root otherwise — the repository root has no `index.html`, so every URL returns `404: NOT_FOUND` even though the deployment reports success.

If the Vercel project was imported with a **Root Directory** other than the repository root, reset it to the repository root so `vercel.json` is read, then redeploy. Changing the setting in the dashboard (Settings → Build and Deployment → Output Directory → `dist`) or re-running the deployment after this file lands both work; the value in `vercel.json` takes precedence over the dashboard.

## What's included

The clip wall (hover lift, page-in reveals, a slow drift on each still, click-to-play Drive embeds), keyboard-operable experience tabs, pause-motion preference, pointer parallax, draggable stationery, off-screen object entrances, directional card reveals, a scroll-scrubbed three-step editing process (review → assembly → grade and delivery), interactive typography and colour experiments, and reduced-motion support. The process sequence renders as a normal readable stack when motion is paused.

Animation uses native CSS transforms and requestAnimationFrame. The scroll sequence follows ordinary page scroll and does not capture wheel or touch scrolling. Reveal positions are measured before transform effects, so cards entering from outside the viewport can still be triggered reliably.

## Credits

Adapted from the [greenportfolio](https://github.com/gireeshkumarreddy/greenportfolio) template by Gireesh Kumar Reddy — layout, stationery artwork, self-hosted fonts and animation system, re-written for Prince. Font licensing details are in `licenses/`. Asset generation notes are in `asset-prompts.json`.
