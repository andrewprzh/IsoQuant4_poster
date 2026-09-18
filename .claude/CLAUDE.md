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

- `\usetheme[COM, twocolumn]{HYposter}`; column width `0.45\paperwidth`,
  explicit gutter via `\guttercolumn` (0.04\paperwidth spacer column)
  between the two `\newcolumn`s; page side margins ~0.025\paperwidth.
- `beamerposter` scale **1.0** + `\linespread{1.06}` → body text ~0.88cm,
  line spacing ~1.1cm (conference guidelines).
- Title `\VeryHuge`, `\titlestart{IsoQuant4: }` orange + grey rest, manual
  `\\` break; title area is 0.83\paperwidth — re-check breaks if size
  changes.
- Fonts: **Calibri**, falling back to metric-compatible **Carlito**
  (installed) via `\IfFontExistsTF` — matches the slide figures.
- Captions shrunk from the theme's fixed 40pt via `\captionsetup`;
  bibliography font `\tiny`.
- Three QR codes (LaTeX `qrcode` package, `[nolinks]`) at the bottom of
  the left column: IsoQuant repo, Spl-IsoFind repo, doi.org link to the
  Nature Methods paper. 4.5cm, labels below. NOT scan-verified — no QR
  decoder on this machine; user should phone-test before printing.

## Local modifications to beamerthemeHYposter.sty

Portrait headline fully reworked (landscape branch kept as original):
flame logo (0.10\paperwidth) and title side by side at the very top,
authors and affiliations below them as full-width lines stretched with
`\hbox to \textwidth` (put `\hfill` between entries in `\author`/
`\institute` in main.tex). Poster-env edge filler columns 0.02 (was
0.04/0.01); `\guttercolumn` command added; block-title top skip 2.2ex
(was 2.60ex). Footline unchanged but `\leftcorner` is no longer set, so
the bottom-left corner is empty.

## Column balance (beamerposter columns do NOT flow)

Content that exceeds the column height silently overflows past the page
bottom over the footer — always render and eyeball the bottom of both
columns after edits.

## TODOs / placeholders

- `[GRANT ACKNOWLEDGEMENTS PLACEHOLDER]` in main.tex — funding unknown
  (not in paper draft or slides); user fills in.
- Right column is to be reworked by the user; its references currently
  overlap the footer's grey UNIVERSITY OF HELSINKI text slightly.
- QR codes not yet verified with a scanner.

## Git conventions

Small, focused commits. Author: Andrey Prjibelski <andrewprzh@gmail.com>
(set per-commit with `git -c user.name=... -c user.email=...`).
Remote: git@github.com:andrewprzh/IsoQuant4_poster.git (nothing pushed yet).
