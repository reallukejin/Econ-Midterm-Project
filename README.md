# Econ-Midterm-Project
Readme · MD
Higher Minimum Wages and Teen Employment in U.S. States, 2015–2024

ECON 3916 Midterm Project · Luke Jin

Objective

I tested whether, within U.S. states from 2015 to 2024, a higher real minimum wage is associated with a lower employment rate for 16–19 year olds.

Question

Within U.S. states, 2015–2024, is a higher real minimum wage associated with a lower teen (16–19) employment rate? Teenagers are the group most likely to earn at or near the minimum wage, so if a higher wage floor costs jobs, it should show up there first. The federal minimum has been $7.25 since 2009, so all the variation in this decade comes from state law.

Data sources

All raw files are in data/raw/. I downloaded them on 2026-11-09.

Data	Source	File
Teen and adult employment by state (CPS annual averages, Table 14)	BLS Geographic Profile of Employment and Unemployment, https://www.bls.gov/opub/geographic-profile/	all-tables-2015.xlsx … all-tables-2024.xlsx
State minimum wage history (rate in effect January 1)	U.S. Department of Labor, https://www.dol.gov/agencies/whd/state/minimum-wage/history	dol_state_minwage_history.csv
State median household income	Census CPS ASEC via FRED, https://fred.stlouisfed.org/series/MEHOINUSCAA646N	fred_median_hh_income.csv
CPI-U, annual average (to convert dollars to 2024 $)	FRED, https://fred.stlouisfed.org/series/CPIAUCSL	fred_cpi_annual.csv

One row is one state-year: 51 × 10 = 510. BLS doesn't publish the teen numbers when a state's sample is too small, so 124 state-years (24.3%) are missing. DC, Maine and South Dakota are never published, which leaves 386 state-years across 48 states.

How to run it
Open Econ_3916_Midterm.ipynb in Google Colab.
In the Setup cell, set GITHUB_REPO to this repository's username/repo-name. The notebook clones the repo to get data/raw/. If you run it locally from the repo folder, you can skip this step.
Click Runtime › Restart and run all. Every table, figure and number in the report is produced by the notebook, and the last code cell prints every number the report quotes.

Packages: numpy, pandas, matplotlib, statsmodels, openpyxl (all preinstalled in Colab).

Methodology
Read Table 14 from each year's BLS file and pulled the "Total" and "16 to 19" rows for every state.
Used the binding minimum wage, max(state rate, federal rate), and the higher large-employer rate where a state has tiers.
Converted the minimum wage and median income to 2024 dollars with the CPI-U, then took logs.
Built adult (20+) unemployment by taking teenagers out of the overall rate, so the outcome isn't on the right-hand side.
Tested the missingness with a logit of "teen row missing" on population, the minimum wage and the overall employment rate.
Made three figures: the outcome's distribution, the raw vs within-state relationship, and trends for states that raised their wage vs states that stayed at $7.25.
Ran OLS of the teen employment rate on the log real minimum wage, adult unemployment, teen population share and log real median income, with state and year dummies and HC1 robust standard errors.
Ran diagnostics: residual plots, a Breusch–Pagan test, VIFs and Cook's distance. As extra checks I re-estimated with state-clustered standard errors and with teen-population weights.
Key findings
Across states, the raw slope is steep: a 10% higher minimum wage goes with teen employment 1.10 percentage points lower.
When I compare each state with itself over time, a 10% higher real minimum wage goes with teen employment about 0.25 percentage points lower (95% CI −0.53 to +0.03; N = 386). That's about 0.7% of the 33.7% average. It isn't distinguishable from zero at the 5% level (p = 0.082), but it rules out an association as large as the raw one.
A 1-point higher adult unemployment rate goes with teen employment about 0.6 points lower (95% CI −1.06 to −0.14), so teen hiring tracks the wider economy.
The Breusch–Pagan test was borderline (p = 0.058), so I kept robust standard errors; they barely differ from the classical ones (1.49 vs 1.57). The minimum wage's VIF is 6.4 with the dummies, which is a large part of why the estimate is imprecise. No single observation dominates (largest Cook's distance 0.059).
This is a conditional association, not a causal effect. Wage increases may be timed with strong labour markets, raising states may be on different trends, and the missing small-state data is probably not random.
Files
Econ_3916_Midterm.ipynb: all of the analysis
report.pdf: the written report
data/raw/: the raw data files
