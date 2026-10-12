# School Infrastructure & Learning Conditions

**Identifying the educational resources most closely associated with student outcomes in Nigerian secondary schools, 2016–2021**
Group 6 · Data Science Internship

## Question

Which school resources (students per teacher, teacher qualification, classroom condition, toilet provision, school size) are most closely associated with the share of WAEC candidates who obtain **five credits including English and Mathematics**?

## Data

| Source | Content |
|---|---|
| **NEMIS** (National Education Management Information System) | Students, teachers, qualified teachers, classrooms and toilets, by state and sector (public / private) |
| **NBS** (National Bureau of Statistics) | WAEC candidates and credit counts, by state and sector |

- `data/Raw CSVs.zip`: the raw files after conversion (resource PDFs via Tabula, WAEC Excel sheets via CloudConvert)
- `data/Cleaned CSVs.zip`: the 44 cleaned CSV files produced by the cleaning notebooks

Coverage: 37 states (incl. FCT) × 2 sectors × 6 years = **444 state-sector-years**. Classroom and toilet data exist only for 2019–2021; school counts only for 2016–2017.

## Repository structure

```
data/
  Raw CSVs.zip              raw converted files
  Cleaned CSVs.zip          cleaned files used by the analysis
notebooks/
  01_cleaning/              one notebook per WAEC year + resource data cleaning
  02_analysis/
    group_6_project_analysis.ipynb   panel building, correlation and partial correlation
presentation/               final slide deck
```

## Method

1. **Cleaning:** drop header clutter rows, rename columns, standardise state names, convert text numbers, fill missing values with the column median and recompute totals from their parts.
2. **Panel:** one row per state × sector × year; resource ratios (student-teacher ratio, qualified-teacher %, students per school / good classroom / toilet) and the pass rate.
3. **Correlation:** Pearson and Spearman, pooled and within year and sector.
4. **Partial correlation:** each resource vs pass rate, holding the other resources and year × sector constant; for both sectors, public only and private only.

## Main findings

- The **student-teacher ratio** is the resource most consistently linked to WAEC results in **public schools**: partial ρ = −0.30 (p < 0.001), unchanged when classrooms and toilets are held constant (−0.28, p = 0.005).
- **Qualified-teacher share:** positive but weak (partial ρ ≈ 0.16–0.18, 2019–2021 only).
- **Classrooms and toilets:** no reliable association.
- **School size (2016–2017):** strongly linked (within-year ρ = −0.42), but only two years of data.
- **Private schools:** no reliable pattern, likely because of a 2018–2019 reporting shift and missing teacher data.

All results are state-level associations, not causal effects.

## How to run

1. Open a notebook in Google Colab (or Jupyter).
2. **Cleaning notebooks:** unzip `data/Raw CSVs.zip` and upload the needed CSVs to `/content`.
3. **Analysis notebook:** upload `data/Cleaned CSVs.zip` next to the notebook; the first cells unzip it.
4. Run all cells. Requirements: `pandas`, `numpy`, `scipy`, `statsmodels`, `matplotlib`, `seaborn` (all pre-installed on Colab).
