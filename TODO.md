# Thesis TODO List

Tracking all known tech debt, missing content, and pending items.

## Build Status

- **Errors**: 0
- **Warnings**: 2 (both expected/benign)
  - `hyperref Draft mode on` — goes away when switching `\documentclass` from `draft` to final
  - `Empty thebibliography` — goes away when `\cite{}` calls are added
  - `Overfull \hbox (1.6pt)` in introduction line 65 — negligible, resolves in final mode

## Content: Must Fill In

### Front Matter
- [ ] **University ID**: Replace `N#` placeholder on title page with actual ID
- [ ] **Vita**: Fill in place of birth, undergrad details, enrollment year, research period, funding source
- [ ] **Acknowledgements**: Write acknowledgements (max 1 page per guidelines)
- [ ] **Dedication**: Replace placeholder text or remove section

### Bibliography
- [ ] **Add all references to `thesis.bib`**: Currently has only a placeholder entry. Key refs needed:
  - Dauner et al. — NAVSIM benchmark
  - Assran et al., 2023 — I-JEPA
  - Oquab et al., 2023 — DINOv2
  - He et al., 2022 — MAE
  - Chitta et al., 2022 — TransFuser
  - Chen et al., 2025 — LAW
  - Liang et al., 2025 — DiffusionDrive / DiffusionDriveV2
  - Drive-JEPA, 2026
  - PRIX, 2025
  - He et al., 2016 — ResNet
  - Dosovitskiy et al., 2021 — ViT
  - Caesar et al. — nuPlan
- [ ] **Remove `placeholder_remove_me` entry** from thesis.bib once real refs are added
- [ ] **Add `\cite{}` calls** throughout all chapters as prose is written

### Chapter Prose (replace italic placeholders)
- [ ] Chapter 1: Introduction — write actual prose for all sections
- [ ] Chapter 2: Background — write all section content
- [ ] Chapter 3: Related Work — write all section content
- [ ] Chapter 4: Methodology — write all section content
- [ ] Chapter 5: Experiments — write prose around existing tables, fill in TODO results
- [ ] Chapter 6: Conclusions — write final prose with concrete numbers

## Pending Experiment Results (mark in .tex with TODO comments)

- [ ] **Phase 3**: DiffusionDrive cross-city training runs (8 training x 4 evals)
- [ ] **I-JEPA camera-only**: DiffusionDrive + I-JEPA camera-only all-city run
- [ ] **EPDMS evaluation**: Run on best DiffusionDrive models
- [ ] **Why SSL Works analyses**: CKA, linear probing, attention maps, MMD, effective rank
- [ ] **RL post-training** (optional): GRPO/DPO transfer experiment

## Final Submission Checklist (before defense)

- [ ] Switch `\documentclass` from `[12pt,draft,letterpaper]` to `[12pt,letterpaper]`
- [ ] Verify all figures render (draft mode suppresses images)
- [ ] Run full compile cycle: `pdflatex && bibtex && pdflatex && pdflatex`
- [ ] Verify zero warnings (except hyperref/natbib if acceptable)
- [ ] Get advisor + department chair digital signatures on title page
- [ ] Upload to ProQuest
- [ ] Email signed PDF to Prof. Jose Ulerio (julerio@nyu.edu)
