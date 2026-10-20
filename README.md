# Eulerian Motion Guidance — project page

Static project page for *Eulerian Motion Guidance: Robust Image Animation via
Bidirectional Geometric Consistency* (ACM MM '26).

Built on the **Nerfies project-page template** (Bulma CSS), the standard
academic project-page layout.

## Structure

```
index.html            page markup (Nerfies/Bulma structure)
static/css/bulma.min.css   vendored Bulma framework
static/css/index.css       Nerfies base styles + this page's additions
static/images/        method diagrams (paradigm, BGC)
static/videos/        looping result GIFs (see "Video slots" below)
```

Fonts (Google Sans / Noto Sans) and icons (Font Awesome, Academicons) load
from CDNs — fine on GitHub Pages. To go fully offline, vendor those too.

> Note: if the page ever looks stale in your browser, hard-refresh
> (Cmd+Shift+R) — the dev server sends fresh files but browsers cache CSS/HTML.

## Video slots

`static/videos/` holds looping GIFs:

- **Showcase** (`showcase_01..03.gif`) — image-to-video renderings generated
  with **Veo 3.1** from the paper's clean reference frames (bear character,
  boat on river, baker shaping dough).
- **Comparisons** (`cmp_*`, `portrait_*`) — each method's published frames
  (reference, t = 10/50/100) extracted from the figure PDFs at 200 dpi, the
  red/green annotation boxes inpainted out (OpenCV TELEA), and intermediate
  frames synthesized with motion-compensated interpolation (ffmpeg
  `minterpolate`, 12 fps) so each clip plays as continuous video anchored at
  the published keyframes.

| File | Scene (paper figure) | Method shown |
|---|---|---|
| `showcase_01.gif` | Character / bear (Fig. long-horizon) | Veo render of EMG scene |
| `showcase_02.gif` | Boat on river (Fig. long-horizon) | Veo render of EMG scene |
| `showcase_03.gif` | Baker / dough (Fig. ablation) | Veo render of EMG scene |
| `cmp_mofa_baseline.gif` / `cmp_mofa_ours.gif` | Car (Fig. long-horizon) | MOFA vs EMG |
| `cmp_conductor_baseline.gif` / `cmp_conductor_ours.gif` | Jet-ski (Fig. trajectory) | ImageConductor vs EMG |
| `portrait_baseline.gif` / `portrait_ours.gif` | Sunglasses subject (Fig. keypoint) | FactorPortrait vs EMG |

To replace any slot with a true rendered video from the model, convert it to
GIF with the same filename — no HTML edits needed:

```sh
ffmpeg -i input.mp4 -vf "fps=10,scale=560:-2:flags=lanczos,split[a][b];\
[a]palettegen=stats_mode=diff[p];[b][p]paletteuse=dither=bayer:bayer_scale=4" \
       -loop 0 static/videos/<name>.gif
```

Comparison pairs sit side by side; keep both GIFs of a pair the same length
so the loops stay synchronized.

## Deploy to GitHub Pages

1. Create a repository, e.g. `emg2026` (or `<your-handle>.github.io`).
2. Push the contents of this `website/` folder to the repo root:

   ```sh
   cd website
   git init && git add -A && git commit -m "Project page"
   git branch -M main
   git remote add origin git@github.com:<your-handle>/emg2026.git
   git push -u origin main
   ```

3. In the repo: Settings → Pages → Source: `main` branch, `/ (root)`.
   The page appears at `https://<your-handle>.github.io/emg2026/`.

## Links

- **Paper**: https://arxiv.org/pdf/2605.06280
- **arXiv**: https://arxiv.org/abs/2605.06280
- **Code**: https://github.com/nguyentthong/eulerian_motion_guidance
- **BibTeX**: currently cites the arXiv preprint.
  Switch it to the ACM MM proceedings entry once the DOI is available.

Fonts load from Google Fonts (Spectral, Schibsted Grotesk, Spline Sans Mono);
if you need the page fully self-hosted, download the woff2 files and swap the
`<link>` for local `@font-face` rules. Everything else is self-contained.
