# IsoQuant4 conference poster (GCB)

A0 portrait poster for the GCB conference, built on the University of
Helsinki **HYposter** beamerposter template, two-column layout.

## Build

```bash
latexmk -xelatex main.tex        # produces main.pdf (XeLaTeX or LuaLaTeX only)
latexmk -c                       # clean build artifacts
```

Quick visual check: `pdftoppm -png -r 40 main.pdf preview`.

## Source materials (outside this repo, in ..)

- `../GCB abstract.docx.pdf` — title, authors, affiliations, abstract.
- `../BELBI_IS_AndreyPrzhibelskiy.pptx.pdf` (73 slides, 720x405pt pages) —
  all graphics were cropped from this PDF.
- `../IsoQuant4 paper.pdf` — draft paper (no funding info yet).
- `../requirements.txt` — conference poster guidelines (loose, need not be
  followed precisely): A0 portrait; title >=3cm, headings >=1.5cm,
  body text >=0.8cm, graphs >=20cm.
- `../s41592-026-03211-w.pdf` — Michielsen et al., Nature Methods 2026
  (biological results; cited as [1] / `michielsen2026`).
- `/home/andreyp/ablab/IsoQuant` — IsoQuant repo (README feature list).
- `/home/andreyp/ablab/IsoQuant4_reproducibility` — supplementary tables.

## Naming convention

The abstract says "Spl-IsoQuant"; **use "IsoQuant4" everywhere** (the main
original name). **Spl-IsoFind keeps its own name** (separate package,
github.com/tilgnerlab/Spl-IsoFind).

## Figures (figures/, all vector crops from the presentation PDF)

Made with `pdfseparate` + `pdfcrop --hires --bbox` (bbox in pt, page is
720x405pt; slide titles and page numbers cropped out):

| file | slide | content |
|---|---|---|
| pipeline.pdf | 18 | analysis pipeline (page number "18" whited out via a standalone tikz overlay, see git log) |
| barcode_calling.pdf | 23 | barcode calling scheme |
| variability.pdf | 51 | cell-type abundance vs true variability |
| splisofind.pdf | 52 | Moran's I permutation test |
| sv_isoforms.pdf | 53 | SVIs per cell type + PacBio/ONT venn |
| sv_genes_ighm.pdf | 54 | predefined-vs-autocorrelation venn + Ighm brain |
| protocol_overlap.pdf | 55 | Stereo-seq vs Visium HD venn |

Tables from slides 25, 26, 29 were recreated natively in LaTeX (scaling
table, simulated-ONT accuracy, Visium HD vs SpaceRanger). Conclusions from
slide 56.

## Layout decisions in main.tex

- `\usetheme[COM, twocolumn]{HYposter}`; column width overridden to
  `0.43\paperwidth` (down from the theme's 0.4451) to widen the gutter.
- `beamerposter` scale **0.95** → body text ~0.84cm. Content JUST fits:
  the right column (references) ends close to the footer; the left column
  has a little more slack. If content gets trimmed, scale=1.0 may fit.
- Title `\veryHuge` on 4 manually broken lines (`\\` in `\titleend`).
  If title size or scale changes, re-check the line breaks against the
  0.625\paperwidth title area.
- Captions shrunk from the theme's fixed 40pt via `\captionsetup` in the
  preamble; bibliography font `\tiny`.
- Fonts: Georgia/Arial required by UH brand; falls back automatically to
  Liberation Serif/Sans via `\IfFontExistsTF` (Georgia/Arial not installed
  on this machine; `sudo apt install ttf-mscorefonts-installer` would
  provide them and gets picked up with no edits).

## Local modifications to beamerthemeHYposter.sty

Portrait headline reworked (landscape untouched): flame logo (0.10
\paperwidth, was 0.20) sits **beside** the title in minipages instead of
above it; title typeset as one paragraph (with `\par` inside the size
group) so manual breaks get even line spacing; `\vskip1.5cm` top margin;
the original `\hskip-15ex` removed (it pushed the logo off-page).

## Column balance (beamerposter columns do NOT flow)

Content that exceeds the column height silently overflows past the page
bottom over the footer — always render and eyeball the bottom of both
columns after edits.

## TODOs / placeholders

- `[GRANT ACKNOWLEDGEMENTS PLACEHOLDER]` in main.tex — funding unknown
  (not in paper draft or slides); user fills in.
- `flames/logo.png` (bottom-left corner) is the template dummy
  ("logo logo logo") — replace with partner logos, e.g. Weill Cornell.
- User plans to trim content further.

## Git conventions

Small, focused commits. Author: Andrey Prjibelski <andrewprzh@gmail.com>
(set per-commit with `git -c user.name=... -c user.email=...`).
Remote: git@github.com:andrewprzh/IsoQuant4_poster.git (nothing pushed yet).
