# U.S. Housing Affordability Crisis
### Financial Pressures Facing Younger Generations in the United States

**Tech stack:** Python (Pandas, Matplotlib) · Power BI

---

## Position

> The U.S. housing affordability crisis for first-time millennial buyers is rooted in the collapse of homebuilding after 2008 which permanently starved the market of supply. When mortgage rates increased in 2022, buyers faced record-high prices and record-high borrowing costs simultaneously. However, geographic opportunity still exists in stable, affordable metros where people can enter the market today.

---

## Project Overview

This is Part 2 of a broader analysis on financial pressures facing younger generations in the U.S. Part 1 established that housing costs have outpaced income growth since 2007. This project investigates the structural root cause — the 2008 construction collapse — and identifies where geographic opportunity still exists for first-time millennial buyers.

The project has three layers:
1. **ETL pipeline (Python):** 11 time-series datasets from FRED, the U.S. Census Bureau, and Zillow, resampled from weekly / monthly / quarterly / annual frequencies and merged into analysis-ready tables.
2. **Validation & evaluation (Python):** every dashboard claim is recomputed in `validate.ipynb`, followed by deeper analysis — payment-to-income, a price-vs-rate decomposition, a homeownership counterfactual, and inflation adjustment.
3. **Dashboard (Power BI):** visual story from cause → consequence → geography.

---

## Key Findings

| Question | Finding |
|---|---|
| Did homebuilding recover after 2008? | Single-family starts fell **74.7%** (1,718k in 2005 → 434k in 2011, annual averages) and in 2025 were still **35% below** the 2000–2006 average (942k vs 1,453k) |
| How affordable is buying a home? | Mortgage payment on the median home reached **37.2% of median household income in 2023**, the highest since 2000 (10% down, 30-year fixed, principal + interest) |
| Prices or rates — what drove the 2021→2023 shock? | Monthly payment rose **73%** ($1,445 → $2,501). A Shapley decomposition attributes **80% to higher rates** and 20% to higher prices |
| Is it just inflation? | 2000→2025: nominal home prices **+213%**, CPI +87% → **real home prices +67%** vs **real median income +11%** |
| Who is locked out? | Under-35 homeownership fell from **43.1% (2004) to 37.0% (2025)**, a **6.1-percentage-point** drop (−14.2% relative). At the 2004 rate there would be **~1.6M more homeowners under 35** (upper-end estimate, since 2004 was a credit-bubble peak) |
| Where is it still affordable? | State-level home values range from **$832k (HI) to $177k (WV)**, a **4.7x** gap. Most affordable: WV, MS, LA, OK, AR. Most expensive: HI, CA, MA, WA, DC |

---

## Audit & Revisions

After the first version, every number was re-checked against the raw data. Three corrections were made:

| Issue | Before | After |
|---|---|---|
| **Aggregation bias in state prices** — state values were an unweighted average of metro areas, so 25 small Illinois metros outweighed Chicago | Illinois ranked 3rd most affordable ($169k), 5x price gap | Zillow's **state-level ZHVI** (every home weighted equally): Illinois ranks 17th ($293k), **4.7x** gap |
| **Inconsistent units for housing starts** — notebook used single months, report used annual averages | Peak 1,823k / trough 353k / −80.6% | **Annual averages** everywhere: 1,718k (2005) → 434k (2011), **−74.7%** |
| **Percent vs percentage points** — homeownership drop reported as "8.6%" using the lowest year | "8.6% decline" (2004 → 2016) | **−6.1 percentage points** (2004 → 2025, latest data) |

The evaluation also refined the thesis: the long-run supply shortage explains the steady rise in real prices, but the **2022 affordability shock was primarily rate-driven** (80% of the payment increase).

---

## Repository Structure

```
us-housing-affordability-crisis/
│
├── orginal_dataset/        # Raw files from FRED, Census, Zillow (metro level)
├── fred_extra/             # CPI (CPIAUCSL) and median household income (MEHOINUSA646N) from FRED
├── zillow_state/           # Zillow state-level ZHVI (fixes the aggregation bias)
├── clean_data/             # Cleaned and merged datasets used by the original dashboard
├── powerbi_data/           # Exports for the updated dashboard (affordability, waterfall, ownership change, state map)
├── analyzing.pbix          # Power BI dashboard file
├── analyzing.pdf           # Dashboard export (static view)
├── housing_position_report.docx  # Full position report
└── validate.ipynb          # ETL, validation of all claims, fixes, and evaluation
```

### Notebook outline (`validate.ipynb`)
| Section | What it does |
|---|---|
| Load & merge FRED series | Resample weekly mortgage rates to monthly averages, forward-fill quarterly prices, outer-join on date |
| Claim 1 + **FIX 1** | Housing-starts collapse, recomputed with annual averages |
| Census Table 12 parsing + **FIX 4** | Homeownership rate by age; change in percentage points vs relative % |
| Zillow + **FIX 2** | Old unweighted metro averages vs state-level ZHVI; ranking comparison |
| **EVAL 1** | Monthly payment, payment-to-income, price-to-income (2000–2025) |
| **EVAL 1b** | Shapley decomposition of the 2021→2023 payment increase into price and rate effects |
| **EVAL 2** | Counterfactual: "missing" homeowners under 35 and 35–44 |
| **EVAL 3** | CPI-deflated (real) home prices and income |
| **EXPORT** | Writes all Power BI inputs to `powerbi_data/` |

---

## Dashboard Pages (current version)

### Page 1 — The Crisis Story
| Panel | Chart Type | What It Shows |
|---|---|---|
| The Collapse That Started It All | Line chart | Single-family housing starts 2000–2025 |
| Higher Borrowing Cost | Bar chart | Mortgage rates 2016–2025 — from 3.0% (2021) to 6.8% (2023) |
| The Price Burden Keeps Growing | Area chart | Case-Shiller Home Price Index 2000–2025 (nominal) |

### Page 2 — A Generation Left Behind
| Panel | Chart Type | What It Shows |
|---|---|---|
| A Generation Locked Out | Line chart + slicer | Homeownership rate by age group, pre- vs post-crisis |

### Page 3 — Where You Live Matters
| Panel | Chart Type | What It Shows |
|---|---|---|
| The Crisis Is Not Equal Across America | Choropleth map | Home value by state |
| Top 5 Expensive / Affordable States | Tables | Highest and lowest state home values |

> **Planned update:** switch the map and tables to `powerbi_data/state_home_values.csv`, and add a page for payment-to-income and the price-vs-rate waterfall using `powerbi_data/affordability_yearly.csv` and `payment_waterfall.csv`.

---

## Data Sources

| Source | Dataset |
|---|---|
| [FRED — Federal Reserve](https://fred.stlouisfed.org) | HOUST1F, ACTLISCOUUS, CSUSHPISA, MSPUS, MORTGAGE30US, MSACSR, CPIAUCSL, MEHOINUSA646N |
| [U.S. Census Bureau (CPS/HVS)](https://www.census.gov/housing/hvs/) | Historical Table 12 — Homeownership by Age 1982–Present |
| [Zillow Research](https://www.zillow.com/research/data/) | ZHVI (Single-family + condo, mid tier 0.33–0.67, smoothed & seasonally adjusted) — Metro and State level |

---

## Limitations

- Mortgage payments include principal and interest only (no property tax, insurance, or PMI), so the true burden is higher.
- The "missing homeowners" counterfactual uses 2004 as the baseline, a credit-bubble peak, so it is an upper-end estimate.
- The analysis is correlational: it shows timing and magnitude, not proof of causation.

---

## How to Run the Validation

1. Clone this repository
2. Open `validate.ipynb` in Jupyter Notebook
3. Place the raw files from `orginal_dataset/` next to the notebook (the notebook reads them from its own folder) and update the absolute path in the Zillow metro cell
4. Run all cells — the notebook validates the claims, runs the evaluation, and exports Power BI inputs to `powerbi_data/`

**Requirements:**
```
pip install pandas openpyxl matplotlib jinja2
```

---

## How to View the Dashboard

Open `analyzing.pbix` in **Power BI Desktop** (free download at [powerbi.microsoft.com](https://powerbi.microsoft.com)).

For a static view without Power BI, open `analyzing.pdf`.

---

*Part of a two-project series on Financial Pressures Facing Younger Generations in the United States.*
