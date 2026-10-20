# Find the Golden Noise

Code for the blog post **[Find the Golden Noise](https://yuhanchi.github.io/writing/find-the-golden-noise/)**
([PDF version](https://yuhanchi.github.io/files/find-the-golden-noise.pdf)), a survey of methods that steer a
frozen flow or diffusion policy by choosing its input noise.

The repository contains the small 2D experiment from Section 4 of the post, the scripts for all five
figures, and the LaTeX source of the PDF. Please read the post first; this README only explains how to
rerun things.

## Contents

- `experiment/`: the 2D experiment, in PyTorch. It takes a few minutes on a laptop GPU.
  - `python noise_routes.py` trains the frozen flow policy and its one-step student, caching both in
    `results/decoders.pt`. It then trains the noise proposer with all five routes for three seeds and
    writes `results/results.json` and `results/log.txt`.
  - `python gaussian_floor.py` fits the best Gaussian to each state separately (the reference row of
    Table 3) and writes `results/gaussian_floor.json`.
  - `results/` holds the outputs behind the numbers and figures in the post.
- `figures/`: one script per figure. Each writes PDF to `paper/figures/`, plus SVG and PNG for the website.
  - `fig4_experiment.py` (Figures 4 and 5) reads `experiment/results/`; use `STATE_IDX=12`
    (goal angle 67.5°).
  - Set `FONT_DIR` to a folder holding `EBGaramond.ttf` and `EBGaramond-Italic.ttf` (SIL OFL) to match
    the site's font; otherwise matplotlib's default serif font is used.
- `paper/`: the LaTeX version.
  - `python3 md2tex.py` converts the post's Markdown into `body.tex` and `refs.tex`, using the more formal
    wording listed in `FORMAL`. Citations and Figure/Table/Section references become internal PDF links.
  - Then run `pdflatex main.tex` twice.

## Paths

The post's Markdown and web images live in the website repository,
[yuhanchi/yuhanchi.github.io](https://github.com/yuhanchi/yuhanchi.github.io). The scripts expect a
checkout of it next to this repository's parent folder (`../../yuhanchi.github.io` from here). Set
`SITE_REPO` to point elsewhere. Without it, the figure scripts write SVG and PNG to `figures/web/`.

## Requirements

Python 3 with PyTorch, NumPy, SciPy, and Matplotlib; a CUDA GPU is optional but faster. The PDF needs a
TeX Live installation with `pdflatex` (packages `tgpagella`, `mathpazo`, `booktabs`, `tabularx`,
`needspace`, `hyperref`).

## Citation

If this code or the post is useful, please cite the post; the BibTeX entry is at the end of the
[post](https://yuhanchi.github.io/writing/find-the-golden-noise/). Please also cite the original papers for
the methods discussed there.
