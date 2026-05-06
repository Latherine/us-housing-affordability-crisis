# U.S. Housing Affordability Crisis
### Financial Pressures Facing Younger Generations in the United States

---

## Position

> The U.S. housing affordability crisis for first-time millennial buyers is rooted in the collapse of homebuilding after 2008 which permanently starved the market of supply. When mortgage rates increased in 2022, buyers faced record-high prices and record-high borrowing costs simultaneously. However, geographic opportunity still exists in stable, affordable metros where people can enter the market today.

---

## Project Overview

This is Part 2 of a broader analysis on financial pressures facing younger generations in the U.S. Part 1 established that housing costs have outpaced income growth since 2007. This project investigates the structural root cause — the 2008 construction collapse — and identifies where geographic opportunity still exists for first-time millennial buyers.

The dashboard is built in **Power BI** across 3 pages and validated with Python.

---

## Repository Structure

```
us-housing-affordability-crisis/
│
├── orginal_dataset/        # Raw CSV files downloaded from FRED, Census, Zillow
├── clean_data/             # Cleaned and merged datasets ready for Power BI
├── analyzing.pbix          # Power BI dashboard file
├── analyzing.pdf           # Dashboard export (static view)
├── housing_position_report.docx  # Full position report
└── validate.ipynb          # Python notebook validating all claims
```

---

## Dashboard Pages

### Page 1 — The Crisis Story
| Panel | Chart Type | What It Shows |
|---|---|---|
| The Collapse That Started It All | Line chart | Housing starts 2000–2025 — collapsed 74% in 2008, never recovered |
| Higher Borrowing Cost | Bar chart | Mortgage rates 2016–2025 — spiked from 3.0% to 6.8% in 2022 |
| The Price Burden Keeps Growing | Area chart | Home Price Index 2000–2025 — tripled since 2000 |

### Page 2 — A Generation Left Behind
| Panel | Chart Type | What It Shows |
|---|---|---|
| A Generation Locked Out | Line chart + slicer | Homeownership by age group — Under 35 dropped from 43% to 34% post-2008 |

### Page 3 — Where You Live Matters
| Panel | Chart Type | What It Shows |
|---|---|---|
| The Crisis Is Not Equal Across America | Choropleth map | Average home price by state — Hawaii $856k vs West Virginia $164k |
| Top 5 Expensive States | Table | HI, MA, CA, CO, UT |
| Top 5 Affordable States | Table | WV, MS, IL, OK, AR |

---

## Key Validated Findings

| Claim | Finding |
|---|---|
| Housing starts collapsed after 2008 | Down 74% from 1,718k (2005) to 442k (2009) |
| Construction never recovered | Still 30.6% below pre-crisis average in 2025 |
| Prices surged to all-time highs | Home Price Index tripled since 2000 |
| Rates barely cooled prices | Rates tripled 2021→2023, prices still rose 11.4% |
| Generational lockout confirmed | Under 35 ownership dropped from 43.1% to 34.5% post-crisis |
| Geographic opportunity exists | 5x price gap between most and least expensive states |

---

## Data Sources

| Source | Dataset |
|---|---|
| [FRED — Federal Reserve](https://fred.stlouisfed.org) | HOUST1F, ACTLISCOUUS, CSUSHPISA, MSPUS, MORTGAGE30US, MSACSR |
| [U.S. Census Bureau (CPS/HVS)](https://www.census.gov/housing/hvs/) | Historical Table 12 — Homeownership by Age 1982–Present |
| [Zillow Research](https://www.zillow.com/research/data/) | Metro Home Value Index (ZHVI) — Single Family Condo Tier 0.33–0.67 |

---

## How to Run the Validation

1. Clone this repository
2. Open `validate.ipynb` in Jupyter Notebook
3. Make sure the raw CSV files are in the `orginal_dataset/` folder
4. Run all cells — the notebook validates all 4 claims against the raw data and exports clean files to `clean_data/`

**Requirements:**
```
pip install pandas openpyxl matplotlib
```

---

## How to View the Dashboard

Open `analyzing.pbix` in **Power BI Desktop** (free download at [powerbi.microsoft.com](https://powerbi.microsoft.com)).

For a static view without Power BI, open `analyzing.pdf`.

---

*Part of a two-project series on Financial Pressures Facing Younger Generations in the United States.*
