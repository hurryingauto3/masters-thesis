# End-to-End Trajectory Planning via Self-Supervised Vision Foundation Models

LaTeX source for the M.S. thesis by **Ali Hamza** at NYU Tandon School of Engineering (ECE), 2026.

[![Code](https://img.shields.io/badge/code-navsim--ssl--city--generalization-orange.svg)](https://github.com/hurryingauto3/navsim-ssl-city-generalization)
[![Showcase](https://img.shields.io/badge/showcase-thesis--showcase-9cf.svg)](https://github.com/hurryingauto3/thesis-showcase)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)

- **Advisor**: Prof. Anna Choromanska
- **Committee**: Prof. Chinmay Hegde, Prof. David Fouhey
- **Defense**: April 2026

## Central claim

Cross-city generalization failure in end-to-end autonomous driving is a **representation problem, not a planning-architecture problem**. Self-supervised backbones reduce cross-city transfer-ratio inflation by roughly an order of magnitude relative to a supervised ResNet baseline, and pair cleanly with modern generative planning heads (DiffusionDrive) without compromising in-distribution performance.

## Studies covered

| # | Title |
|---|---|
| Exploratory | Lightweight-Head Study |
| I | Cross-City SSL Benchmark (companion paper) |
| II | SSL Backbones in Generative Planning |
| III | Cross-City Generative Planning Protocol |
| IV | Mechanistic Analysis of Cross-City Representations |

## Related repositories

| Repo | What it is |
|---|---|
| [`hurryingauto3/navsim-ssl-city-generalization`](https://github.com/hurryingauto3/navsim-ssl-city-generalization) | Code, configs, splits, results, figures |
| [`hurryingauto3/thesis-showcase`](https://github.com/hurryingauto3/thesis-showcase) | Browser-based interactive demo |
| `hurryingauto3/masters-thesis` (this repo) | LaTeX manuscript |

## Build

```bash
make           # pdflatex × 4 + bibtex
make clean     # remove aux/log/bbl/blg/toc/lof/lot/pdf
make wc        # rough word count
make check     # lacheck + doubled-word check
```

Built with `pdflatex`. NYU Tandon thesis template (April 2025 guidelines).

Compiled PDF: [`alihamza_ms_thesis_ah7072.pdf`](alihamza_ms_thesis_ah7072.pdf).

## Layout

```
.
├── thesis.tex                # Main entry
├── abstract.tex
├── acknowledge.tex
├── definitions.tex
├── thesis.bib                # Master bibliography
├── introduction/             # Chapter 1
├── background/               # Chapter 2
├── relatedwork/              # Chapter 3
├── methodology/              # Chapter 4
├── experiments/              # Chapter 5
├── conclusions/              # Chapter 6
├── appendix/                 # Appendices
├── fig/                      # Figures (per-chapter subdirs)
├── masters-thesis-presentation/   # Defense slide deck
└── Makefile
```

## Citation

```bibtex
@mastersthesis{hamza2026crosscity,
  title  = {End-to-End Trajectory Planning via Self-Supervised Vision Foundation Models},
  author = {Hamza, Ali},
  school = {New York University Tandon School of Engineering},
  year   = {2026}
}
```

## License

Apache 2.0 — see [`LICENSE`](LICENSE).
