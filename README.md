# Econ-Midterm-Project

# Do higher minimum wages lower teen employment? U.S. states, 2015–2024

**Question.** Within U.S. states, is a higher minimum wage associated with a lower employment rate among 16–19 year olds, 2015–2024, holding adult unemployment, the teen population share and median household income fixed?

**Headline finding.** Across states, places with higher minimum wages have clearly lower teen employment. Comparing each state with itself over time (state and year fixed effects), a 10% higher real minimum wage goes with a teen employment rate about 0.25 percentage points lower (95% CI −0.53 to +0.03; 386 state-years, 48 states). That is a small conditional association, not distinguishable from zero at the 5% level, and not a causal estimate.

## Data

All raw files are in `data/raw/`, saved unmodified on 2026-11-09.

| File | Source | URL |
|---|---|---|
| `all-tables-2015.xlsx` … `all-tables-2024.xlsx` | BLS, *Geographic Profile of Employment and Unemployment*, Table 14 (CPS annual averages by state) | https://www.bls.gov/opub/geographic-profile/ (files at `/opub/geographic-profile/{year}/tables/all-tables-{year}.xlsx`) |
| `dol_state_minwage_history.csv` | U.S. Dept. of Labor, *Changes in Basic Minimum Wages in Non-Farm Employment Under State Law, 1968–2024*: the published table written out cell by cell, footnotes kept | https://www.dol.gov/agencies/whd/state/minimum-wage/history |
| `fred_median_hh_income.csv` | FRED series `MEHOINUS{XX}A646N`, median household income by state, current dollars (Census CPS ASEC) | https://fred.stlouisfed.org/series/MEHOINUSCAA646N |
| `fred_cpi_annual.csv` | FRED series `CPIAUCSL`, annual average, used to convert dollars to 2024 dollars | https://fred.stlouisfed.org/series/CPIAUCSL |

## How to run

1. Open `teen_minwage_midterm.ipynb` in Google Colab (File › Open notebook › GitHub, then paste this repository's URL).
2. In the **Setup** cell, set `GITHUB_REPO = "your-username/your-repo"` (this repository). The cell clones the repo so the notebook can read `data/raw/`. The repository must be public.
3. *Runtime › Run all.* It needs only pandas, numpy, matplotlib, statsmodels and openpyxl, all preinstalled in Colab. Running locally also works: run it from the repository folder and the clone step is skipped.

Every number in the report is printed in the notebook's last code cell, **Numbers my report quotes**. The figures are saved as `fig1…fig5*.png` and the tables in `output/`.

## Repository contents

```
teen_minwage_midterm.ipynb   analysis notebook (Sections 1–5 + appendix)
report.pdf                   written report (add before submitting)
data/raw/                    the original downloaded files
output/                      tables written by the notebook
fig*.png                     figures written by the notebook
```
