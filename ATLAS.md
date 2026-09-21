# Drosophil·AI

## Meta
| Field | Value |
| --- | --- |
| Last Active | 2026-09-20 |
| Status | shipping |
| Repo | jimmyardis/drosophilai (public) |
| Live | https://drosophilai.com (pending DNS) · https://jimmyardis.github.io/drosophilai |
| Local | /home/wner/drosophilai |

## Current State
Landing page for Drosophil·AI — an experimental lab framing around the
*Drosophila* connectome ("biological hardware, alien problems"). A single
self-contained `index.html` (858 KB, two hero PNGs embedded as base64, Google
Fonts the only external dependency) is committed and deployed to GitHub Pages.
The repo carries `CNAME` (drosophilai.com) and `.nojekyll`. Pages is enabled on
`main` / root. The domain is registered at Namecheap but the DNS records have
not been pointed at GitHub yet, so the apex does not resolve.

## Next Action
Add the four GitHub Pages A records (plus the `www` CNAME) at Namecheap, then
re-run the Pages API call to enable HTTPS enforcement once the certificate
issues.

## Blockers
- Namecheap DNS not yet pointed at GitHub Pages — apex is dead until then.
- HTTPS enforcement cannot be set until the certificate provisions (needs DNS
  first); the Pages API currently returns "The certificate does not exist yet".

## Open Questions
- What is Experiment 001? The page deliberately ships with the first question
  unlocked ("What should we ask first?").
- Does the lab stay a static page, or does it eventually need a backend to run
  and display actual connectome simulations?

## Session Log

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
