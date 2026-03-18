# CLAUDE.MD -- Academic Project Development with Claude Code

**Project:** Research Portfolio — Paper Summaries
**Institution:** M Csapek SA (formerly Tecnológico de Monterrey)
**Branch:** main

---

## Core Principles

- **Plan first** -- enter plan mode before non-trivial tasks; save plans to `quality_reports/plans/`
- **Verify after** -- compile/render and confirm output at the end of every task
- **Single source of truth** -- Beamer `.tex` is authoritative; Quarto `.qmd` derives from it
- **Quality gates** -- nothing ships below 80/100
- **[LEARN] tags** -- when corrected, save `[LEARN:category] wrong → right` to MEMORY.md

---

## Project Overview

Summarizing 4–8 economics/econometrics research papers as polished presentations.
Each paper gets a Beamer slide deck (authoritative) + a Quarto RevealJS version (web-published to GitHub Pages).
Analysis tools: **R**, **Stata**, **Python**.
Papers (PDFs) → `master_supporting_docs/supporting_papers/`
Existing Beamer source → `Slides/`

---

## Quarto Primer (new to Quarto? start here)

Quarto is a publishing system that turns `.qmd` text files into many output formats — for this project, **RevealJS HTML slides** viewable in any browser.

**Mental model:**
- `.qmd` file = Markdown + code chunks + slide metadata
- `quarto render file.qmd` → produces `file.html` (the slide deck)
- This project: Beamer `.tex` is written first → `/translate-to-quarto` converts it → we get both formats

**Why Quarto?** GitHub Pages hosts the HTML output for free, so anyone with a link can view your slides without LaTeX or a PDF viewer. As we work together, I'll explain Quarto features and suggest ways they help *communicate ideas* (animations, interactive charts, callout boxes, etc.).

---

## Folder Structure

```
Summary own papers/
├── CLAUDE.md                    # This file
├── .claude/                     # Rules, skills, agents, hooks
├── Bibliography_base.bib        # Centralized bibliography
├── Figures/                     # Figures and images
├── Preambles/header.tex         # LaTeX headers/preamble
├── Slides/                      # Beamer .tex files (source of truth)
├── Quarto/                      # RevealJS .qmd files + theme
├── docs/                        # GitHub Pages (auto-generated)
├── scripts/                     # Utility scripts, R, Stata, Python
├── quality_reports/             # Plans, session logs, merge reports
├── explorations/                # Research sandbox
├── templates/                   # Session log, quality report templates
└── master_supporting_docs/
    ├── supporting_papers/       # Paper PDFs
    └── supporting_slides/       # Reference slides (non-Beamer source)
```

**Paper naming convention:** `Paper01_ShortTitle`, `Paper02_ShortTitle`, etc.

---

## Commands

```bash
# LaTeX (3-pass, XeLaTeX only)
cd Slides && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex
BIBINPUTS=..:$BIBINPUTS bibtex file
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex

# Quarto render (run from Quarto/ directory)
quarto render file.qmd

# Deploy Quarto to GitHub Pages
./scripts/sync_to_docs.sh Paper01

# Quality score
python scripts/quality_score.py Quarto/file.qmd
```

---

## Quality Thresholds

| Score | Gate | Meaning |
|-------|------|---------|
| 80 | Commit | Good enough to save |
| 90 | PR | Ready for deployment |
| 95 | Excellence | Aspirational |

---

## Skills Quick Reference

| Command | What It Does |
|---------|-------------|
| `/compile-latex [file]` | 3-pass XeLaTeX + bibtex |
| `/deploy [Paper01]` | Render Quarto + sync to docs/ |
| `/extract-tikz [Paper01]` | TikZ → PDF → SVG |
| `/proofread [file]` | Grammar/typo/overflow review |
| `/visual-audit [file]` | Slide layout audit |
| `/pedagogy-review [file]` | Narrative, notation, pacing review |
| `/review-r [file]` | R code quality review |
| `/qa-quarto [Paper01]` | Adversarial Quarto vs Beamer QA |
| `/slide-excellence [file]` | Combined multi-agent review |
| `/translate-to-quarto [file]` | Beamer → Quarto translation |
| `/validate-bib` | Cross-reference citations |
| `/devils-advocate` | Challenge slide design |
| `/commit [msg]` | Stage, commit, PR, merge |
| `/lit-review [topic]` | Literature search + synthesis |
| `/review-paper [file]` | Manuscript review |
| `/data-analysis [dataset]` | End-to-end R analysis |

---

## Beamer Custom Environments

Defined in `Preambles/header.tex`. Font: TeX Gyre Heros (Helvetica-style, MiKTeX-bundled).

| Environment     | Effect                          | Use Case                         |
|-----------------|---------------------------------|----------------------------------|
| `keybox`        | Gold background, left accent    | Key takeaways, main messages     |
| `methodbox`     | Navy left bar, blue-tinted bg   | Model assumptions, identification|
| `resultbox`     | Gold border on all sides        | Main findings, results           |
| `assumptionbox` | Yellow border + titled header   | Formal assumptions (labeled)     |

**Inline commands:** `\gold{}` (gold bold), `\navy{}` (navy bold), `\bad{}` (red bold), `\pos{}` (green bold), `\hi{}` (navy bold)

## Quarto CSS Classes

*(Fill in when building first Quarto deck)*

| Class              | Effect        | Use Case       |
|--------------------|---------------|----------------|
| `[.your-class]`    | [Description] | [When to use]  |

---

## Current Project State

| Paper | Beamer | Quarto | Key Content |
|-------|--------|--------|-------------|
| 01: Child Sponsorship | `Paper01_ChildSponsorship.tex` ✓ | -- | CI impact on higher-ed aspirations, rural Mexico; Roy model, MTE, subjective expectations |
| 02: [Title TBD] | -- | -- | -- |
| 03: [Title TBD] | -- | -- | -- |
| 04: [Title TBD] | -- | -- | -- |
| 05–08: TBD | -- | -- | -- |
