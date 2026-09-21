# Drosophil·AI

## Meta
| Field | Value |
| --- | --- |
| Last Active | 2026-09-21 |
| Status | shipping |
| Repo | jimmyardis/drosophilai (public) |
| Live | https://www.drosophilai.com |
| Local | /home/wner/drosophilai |

## Current State
Landing page for Drosophil·AI — an experimental lab framing around the
*Drosophila* connectome ("biological hardware, alien problems"). A single
self-contained `index.html` (858 KB, two hero PNGs embedded as base64, Google
Fonts the only external dependency), live on GitHub Pages at
**www.drosophilai.com**. The mobile layout has been reworked: the hero stacks
the two plates as uncropped bands, horizontal overflow is gone from 320px up,
and hero text sits on a scrim so it reads over both the light and dark halves.

## Next Action
Decide what Experiment 001 actually is — the page ships with the question
deliberately unlocked, and it is the only section with no real content.

## Blockers
- None. (HTTPS enforcement was never explicitly set via the API; the site
  serves over HTTPS, so confirm `https_enforced` if the padlock ever lapses.)

## Open Questions
- What is Experiment 001? The page deliberately ships with the first question
  unlocked ("What should we ask first?").
- Does the lab stay a static page, or does it eventually need a backend to run
  and display actual connectome simulations?
- The anatomical plate PNG is cropped at its right edge *in the source asset*
  (wing tip and the end of the legend are cut). Re-export it if the full plate
  matters; CSS can only fade the edge, which is what it now does.

## Session Log

### 2026-09-21
- Fixed the mobile rendering reported from an iPhone. Three separate defects,
  each reproduced in headless Chromium at phone viewports before changing
  anything:
  1. **Hero cropping.** Both source plates are landscape (1.25 and 1.19
     aspect). `object-fit:cover` in a tall narrow panel scaled the anatomical
     plate to ~1065px wide and cropped 63% of it away, leaving one giant eye.
     Mobile now stacks the panels as full-width bands with `object-fit:
     contain` against backgrounds matching each image's own paper/navy, so the
     letterboxing is invisible and both plates read whole.
  2. **Horizontal overflow** in the `.dark` section. `.facts` is a 2-column
     grid whose 35px padding gave it a ~339px min-content width, forcing its
     `1fr` track wider than the section, so the heading and body text spilled
     past the dark background. Fixed with `minmax(0,1fr)` tracks, `min-width:0`
     on items, smaller mobile padding and a clamp on the stat figures.
     Swept 320–1600px: no overflow anywhere.
  3. **Hero text contrast.** The title and subtitle fell over the light plate
     and vanished. Added a `.scrim` gradient across the hero, brightened the
     subtitle to `#dcf1f8`, added text shadows.
- Also stacked the four pipeline steps below 560px (they had ~125px of text
  width) and faded the plate's right edge.
- Rebased onto an out-of-band `Update CNAME` commit rather than force-pushing:
  the custom domain had been changed to `www.drosophilai.com` from outside this
  session, and that change was preserved.

### 2026-09-20
- Created `jimmyardis/drosophilai` (public) from the Midjourney-illustrated
  landing page drafted earlier and saved to Downloads as
  `drosophilai-embedded.html`.
- Chose a single self-contained `index.html` over split assets: the hero
  imagery is already base64-embedded in the source file, and the site is one
  page, so splitting it would add build steps for no benefit. Trap noted — the
  file is *delivered whole*, so overwrite it rather than hand-editing around
  the base64 blobs.
- Added `.nojekyll` (nothing here needs Jekyll, and it avoids Jekyll silently
  eating files) and `CNAME` so GitHub picks up the custom domain on first
  build.
- Enabled Pages via the API on `main` / root. Setting `https_enforced` failed
  as expected — no certificate exists until DNS resolves.
- Left mid-stream: Namecheap DNS records (user's step) and HTTPS enforcement.
