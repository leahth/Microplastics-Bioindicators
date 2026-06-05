# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains data analyses for exploring bioindicators for microplastics in California, primarily using Bight 2023 Regional Monitoring Survey data and the ToMEx 2.0 toxicity database.

## Rendering Documents

Documents are written in Quarto (`.qmd`) and rendered with R. To render from the terminal:

```powershell
quarto render "Bight23.qmd"
quarto render "Data Exploration.qmd"
```

Or from within RStudio/Positron, use the Render button.

## Repository Structure

Two main analysis scripts:

- **`Bight23.qmd`** — Correlates Bight 2023 field data: microplastics sediment concentrations (`mp_sed_con`) vs. benthic health indices (`condition_scores`) and benthic taxon abundance (`benthic_abundance`). Focuses on Spearman correlation with assumption-checking (Shapiro-Wilk, Q-Q plots, LOESS vs. linear fit).

- **`Data Exploration.qmd`** — Explores the ToMEx 2.0 toxicity database. Filters studies by red criteria, groups species into four bioindicator categories (amphipod, bivalve, benthic invertebrate, plankton), and summarizes MP particle characteristics (size, polymer, shape) and dose-response data across species groups.

## Data Files (`Data/`)

| File | Contents |
|---|---|
| `sed_mp_con.csv` | Bight 23 MP concentrations in sediment by station (`n_g_sed_dw` = particles/g dry weight) |
| `b23_conditionscores.csv` | Bight 23 benthic condition scores by station and index (M-AMBI, etc.) |
| `B23 Post SDR benthic data.csv` | Bight 23 benthic taxon abundance by station |
| `B23 sediment variables.csv` | Bight 23 sediment physicochemical variables |
| `ToMEx_Search2026-03-04.csv` | ToMEx 2.0 raw toxicity database export |
| `MarineSed_Vol_Count_ToMEx2.csv` | ToMEx data volume-aligned to marine sediment alpha values |
| `MarineWater_Vol_Count_ToMEx2.csv` | ToMEx data volume-aligned to marine surface water alpha values |
| `ed14 historical Bight infauna for unified DB v2.csv` | Historical Bight infauna data |

## Key Conventions

- Station IDs follow the format `B23-XXXXX` (e.g., `B23-12074`)
- MP concentration key variable: `n_g_sed_dw` (particles per gram sediment dry weight)
- ToMEx filtering: only use records where both `technical_red_criteria` and `risk_assessment_red_criteria` equal `"Red Criteria Passed"`
- Correlation method throughout: **Spearman** (data consistently fails normality assumptions)
- Quarto chunk options use `#|` syntax (e.g., `#| label: chunk-name`, `#| echo: false`)