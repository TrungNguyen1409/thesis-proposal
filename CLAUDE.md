# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Master's thesis proposal for TUM (Technische Universität München) on "Design and Evaluation of Multi-Agentic AI Systems for Contract Lifecycle Management SaaS Platforms". The project uses a LaTeX template based on the TUM informatics thesis guidelines.

## Build Commands

The project uses `latexmk` as the primary build tool:

```bash
# Build PDF once (output: build/main.pdf)
make pdf

# Build and watch for changes (continuous compilation)
make watch

# Clean auxiliary files (keeps PDF)
make clean

# Remove entire build directory
make purge
```

Build configuration is defined in `.latexmkrc` for glossary support. The output directory is `build/` and the main document is `main.tex`.

## Document Architecture

### Main Document Structure

The thesis proposal follows a specific 4-page compact layout optimized for proposals:

- **main.tex**: Root document that defines thesis metadata (author, supervisor, submission date, title) and includes all components in order
- **settings.tex**: LaTeX package configuration, bibliography backend (biber with alphabetic style), TUM corporate design colors, and typesetting settings
- **pages/title.tex**: Title page template with TUM branding and thesis information
- **bibliography.bib**: BibTeX references

### Content Organization

All content chapters are in `chapters/` and included sequentially in `main.tex`:

1. `1_introduction.tex` - Motivation and research gap
2. `2_research_questions.tex` - Research objectives
3. `3_methodology.tex` - Research approach and methods
4. `4_schedule.tex` - Timeline and milestones
5. `5_expected_contributions.tex` - Expected outcomes

This is a **continuous document without page breaks** between chapters and **no section numbering** (controlled by `\setcounter{secnumdepth}{0}` in main.tex).

### Styling and Packages

Key configurations in `settings.tex`:
- **Bibliography backend**: biber (not BibTeX)
- **Citation style**: alphabetic (can be changed via TODO comment)
- **Font**: Palatino (mathpazo package)
- **Colors**: TUM corporate design colors predefined (TUMBlue, TUMAccentOrange, etc.)
- **Line spacing**: 1.05 for Palatino
- **Hyperlinks**: hidelinks option (no colored boxes)

### Document Class

Uses KOMA-Script `scrbook` class with:
- 10pt font size for compact layout
- One-sided printing (proposal format)
- Custom DIV=10 for margins
- Header and footer separation lines

## Working with Content

### Adding/Modifying Chapters

Chapters follow a flat structure without deep nesting. When editing:
- Maintain the continuous flow style (minimal page breaks)
- Use `\section{}` for major sections (numbering is disabled globally)
- Reference labels use format: `\label{section:name}`
- Keep content focused and concise (4-page limit)

### Citations

The bibliography uses:
- **Backend**: biber (not BibTeX)
- **Style**: alphabetic
- **File**: `bibliography.bib`
- Citation format: `\cite{key}` for standard citations

To rebuild with bibliography changes, `latexmk` handles the biber workflow automatically.

### Figures and Graphics

- **figures/**: Store image files here
- **logos/**: TUM logos (not included in repository due to copyright)
- Use `\includegraphics{}` from graphicx package
- TikZ and pgfplots available for diagrams and plots

## Key Thesis Information

Current thesis metadata (defined in `main.tex`):
- **Author**: Trung Nguyen
- **Type**: Master's Thesis in Informatics
- **Supervisor**: Prof. Dr. Ingo Weber
- **Advisor**: MS Samed Bayer
- **Expected Submission**: April 2026
- **Topic**: Multi-Agentic AI Systems for Contract Lifecycle Management

## Common Issues

### Build Artifacts

LaTeX generates many auxiliary files. These are ignored in `.gitignore`:
- `.aux`, `.log`, `.out`, `.toc`, `.bbl`, `.blg`
- `.synctex.gz`, `.fdb_latexmk`, `.fls`

Only `build/main.pdf` is tracked in the repository.

### Missing Logos

TUM logos are not included due to copyright. The template handles missing logos gracefully with conditional checks (`\IfFileExists{}`).

### Bibliography Compilation

If bibliography doesn't update:
1. Ensure `biber` is installed (not just BibTeX)
2. Run `make clean` then `make pdf`
3. Check `bibliography.bib` for syntax errors

The template requires biber specifically (configured in `settings.tex`).
