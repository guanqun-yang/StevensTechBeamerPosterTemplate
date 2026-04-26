# Stevens Institute of Technology Beamer Poster Template

[![LaTeX](https://img.shields.io/badge/Made%20with-LaTeX-1f425f.svg)](https://www.latex-project.org/)
[![beamerposter](https://img.shields.io/badge/Class-beamerposter-A32638.svg)](#)
[![Stevens](https://img.shields.io/badge/Stevens%20Institute-of%20Technology-A32638.svg)](https://www.stevens.edu/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A clean, professional **A0 conference poster template** in official **Stevens Institute of Technology** branding. Built on `beamerposter` with the [Moloch](https://github.com/jolists/moloch) theme, Stevens red color scheme, custom block environments, an adaptive multi-column layout, and a one-line orientation toggle.

<p align="center">
  <img src="assets/preview-landscape.png" alt="Poster preview (A0 landscape)" width="900"/>
</p>

<p align="center"><sub>Default A0 landscape compile -- four-column adaptive flow, Stevens-branded header, QR / image corner, and footer URL strip.</sub></p>

---

## You only edit two things

> 1. **Content in `sections/*.tex`** -- one block after another, no layout hints.
> 2. **The metadata block at the top of `main.tex`** -- title, authors, institutes, project / code URLs.

Everything else -- column widths, block placement, header banner, footer rule, QR-code corner, orientation geometry -- is handled by the template. No `\filbreak`, no manual column splits, no rebalancing when you add or remove a block.

## What's automatic

| Concern                                | How it's handled                                                                                                |
|----------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| **Adaptive column flow**               | All section content streams into a single balanced `multicols` block; LaTeX distributes blocks across columns. |
| **Block atomicity**                    | Every `block` / `colorblock` / `contribblock` is wrapped in a minipage, so blocks move whole between columns -- never sliced mid-content. |
| **Orientation**                        | One switch (`\posterlandscapetrue` / commented-out for portrait) picks A0 landscape (4 columns) or portrait (3 columns). |
| **Title centering**                    | Header is symmetric: logo on the left, title block in the middle, image corner on the right -- title always page-centered. |
| **Multi-institution authors**          | Beamer's `\inst{N}` superscripts; authors and institutes render on a single line each, comma-separated.        |
| **Footer divider at the bottom**       | Footer is in beamer's `footline` template, anchored to the bottom of every frame regardless of body height.    |
| **QR / image corner conditional**      | Two switches drive a 3-way layout: two images side-by-side, one centered, or empty (title still centered).     |
| **Footer URL strip**                   | Project URL, code URL, contact, and date pulled from the same metadata commands as the QR codes.               |

## Features

- **Out-of-the-box A0** -- portrait or landscape, switchable with a single line
- **Adaptive multi-column body** -- balanced columns, atomic blocks, no manual splits
- **Stevens-branded color scheme** -- Stevens red (#A32638) on block titles, accent rules, and links
- **Moloch-inspired styling** -- minimal, information-dense blocks
- **Full-width header banner** with Stevens long logo, title, multi-affiliation authors, and a 2-image corner (QR codes / photos / placeholders)
- **Three custom block types** -- `block`, `colorblock`, `contribblock` -- on top of beamer's `alertblock` and `exampleblock`
- **Check / cross marks** -- `\cmark` and `\xmark` for comparison tables
- **Stevens red footer rule** with project URL, code URL, contact, and date

## Quick Start

```bash
git clone https://github.com/guanqun-yang/StevensTechBeamerPosterTemplate.git
cd StevensTechBeamerPosterTemplate
pdflatex main.tex
pdflatex main.tex   # twice so multicol balances columns
```

Open `main.tex`, edit the metadata block at the top (title, authors, institutes, URLs), then edit the four section files in `sections/`. That's it. Or use any LaTeX editor (Overleaf, Texifier, VSCode + Tectonic).

## Orientation

```latex
\newif\ifposterlandscape
\posterlandscapetrue   % comment out this line for portrait
```

| Mode      | Page size        | Columns |
|-----------|------------------|---------|
| Landscape | A0 (1189x841 mm) | 4       |
| Portrait  | A0 (841x1189 mm) | 3       |

## Project Structure

```
.
├── main.tex                    # Entry point -- preamble, header, body, footer
├── sections/
│   ├── 001-introduction.tex    # Motivation, RQs, contributions
│   ├── 002-methods.tex         # Comparison table, pipeline, math
│   ├── 003-results.tex         # Main results, ablation, findings
│   └── 004-conclusion.tex      # Summary, take-home, contact
├── figures/                    # Project images: author photos, diagrams, plots
├── assets/
│   ├── stevens-long-logo.png   # Stevens logo (header banner, left)
│   ├── logo_RGB.png            # Alt Stevens logo
│   ├── beamerthememoloch.sty   # Moloch theme files
│   ├── beamerthemesintef.sty   # SINTEF base theme
│   ├── sintefcolor.sty         # Color definitions
│   └── ...                     # Other Beamer theme .sty files
└── README.md
```

`assets/` holds theme / branding files (logos, `.sty`); `figures/` holds project-specific images you'd swap per poster (author photos, diagrams, plots). Both are on `\graphicspath`, so `\includegraphics{photo-author1}` resolves wherever the file lives.

## Customization

Most posters never need anything below this line -- defaults are sensible. Skim if you want to tweak.

### Adding / removing a section

Drop a new file in `sections/` following the `NNN-<desc>.tex` convention (e.g. `005-related-work.tex`) containing only `\begin{block}…\end{block}` calls. Add a single line `\input{sections/005-related-work.tex}` inside `\posterbody` in `main.tex`. Done -- the multicol layout re-flows automatically. No column rebalancing, no width tweaks.

### Block environments

- `\begin{block}{Title} ... \end{block}` -- Stevens-red header on light-gray body
- `\begin{colorblock}[text color]{bg color}{Title} ... \end{colorblock}` -- arbitrary fg / bg
- `\begin{contribblock}{Title} ... \end{contribblock}` -- red header on near-white body
- Standard `alertblock` / `exampleblock` also work.

### Multi-institution author lists

Beamer's `\inst{N}` superscript convention; literal `,\enspace` separators keep authors and institutes each on a single line:

```latex
\author{%
  First Author\inst{1},\enspace
  Second Author\inst{2},\enspace
  Third Author\inst{1,3}%
}
\institute{%
  \inst{1}Stevens Institute of Technology,\enspace
  \inst{2}Partner University,\enspace
  \inst{3}Third Institution%
}
```

- Use `\inst{1,3}` for an author affiliated with multiple institutions.
- For a **single-institution** poster, drop all `\inst{...}` markers.

### Right-corner images (top-right)

Two images sit in the top-right of the header. The shipped template uses `example-image-a` / `example-image-b` from the `mwe` package as placeholders so the layout is visible immediately. Configure URLs and toggles near the metadata block:

```latex
\newcommand{\projecturl}{https://example.com/project}
\newcommand{\projectlabel}{example.com/project}
\newcommand{\codeurl}{https://github.com/your-repo}
\newcommand{\codelabel}{github.com/your-repo}

\newif\ifshowprojectqr  \showprojectqrtrue  % comment out to hide project image
\newif\ifshowcodeqr     \showcodeqrtrue     % comment out to hide code image
```

`*url` strings feed both the QR-code encoding (when you swap to QR codes) and the clickable footer hyperlinks; `*label` strings are the footer's human-readable link text.

**Conditional layout** (handled automatically):

| Switches            | Render                                              |
|---------------------|-----------------------------------------------------|
| both true           | two images side-by-side, each fills its half-slot   |
| exactly one true    | one image centered, ~0.85 of corner width           |
| both false          | corner is empty (title stays centered on page)      |

**Swap to real QR codes.** Add `\usepackage{qrcode}` and replace each `\includegraphics{example-image-*}` inside `\posterrightcorner` with `\qrcode[height=10cm]{\projecturl}` (or `\codeurl`).

**Swap to author photos.** Drop headshots into `figures/` (e.g. `figures/photo-author1.png`) and replace the `example-image-*` filenames with your photo filenames.

### Colors

All Stevens colors are defined in `main.tex` and can be overridden. The primary accent is `stevensred` (RGB 163, 38, 56).

### Header banner

Customize logo placement, font sizes, or banner height by editing the `\posterheader` macro in `main.tex`.

## Requirements

- A LaTeX distribution with Beamer + `beamerposter` + `multicol` + `etoolbox` + `qrcode` + `mwe` (TeX Live, MiKTeX, or MacTeX -- all standard packages, nothing exotic).
- No external installation needed beyond the standard distribution; theme `.sty` files are bundled in `assets/`.

## Troubleshooting

- **Columns look uneven.** Run `pdflatex` twice -- multicol needs the second pass to balance.
- **A block overflows past a column.** That single block is taller than one column; split it into two blocks. (You'll see a visible vertical overshoot, not a silent error.)
- **Title looks off-center.** The right-corner minipage is hidden but kept at width 0.22 to balance the left logo. Don't delete the minipage; toggle the QR switches off instead.

## Contributing

Contributions are welcome -- bug fixes, additional block styles, alternate layouts. Open an issue or pull request.

## License

[MIT License](LICENSE). The Stevens Institute of Technology logo and branding are the property of Stevens Institute of Technology.
