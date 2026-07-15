# AtliQ-Hotels-Occupancy-Revenue-Analysis
Exploratory data analysis on a 25-property hotel chain (AtliQ Grands) spanning 4 Indian cities, using Python and pandas to clean booking data, engineer an occupancy metric, and surface revenue and occupancy trends for the business.
# AtliQ Hotels — Occupancy & Revenue Analysis

Exploratory data analysis on a 25-property hotel chain (AtliQ Grands) spanning 4 Indian cities, using Python and pandas to clean booking data, engineer an occupancy metric, and surface revenue and occupancy trends for the business.

## Dataset

Five relational CSVs (star-schema style: 1 fact table of bookings, 1 aggregated fact table, 3 dimension tables), plus a late-arriving monthly file to simulate a real reporting cycle:

| File | Rows | Description |
|---|---|---|
| `fact_bookings.csv` | 134,590 | Booking-level transactions: guests, revenue generated/realized, platform, status, rating |
| `fact_aggregated_bookings.csv` | 9,200 | Daily bookings vs. room capacity per property |
| `dim_hotels.csv` | 25 | Property, category (Luxury/Business), city |
| `dim_rooms.csv` | 4 | Room class mapping (Standard, Elite, Premium, Presidential) |
| `dim_date.csv` | 92 | Calendar table (month, week, weekday/weekend flag) |
| `new_data_august.csv` | — | August data appended to simulate an incremental refresh |

## Tools

Python, pandas, Jupyter Notebook, Matplotlib.

## What was done

1. **Data exploration** — shape, dtypes, unique values, and distribution checks across all 5 tables.
2. **Data cleaning** — removed invalid records (negative/zero guest counts), detected and removed statistical outliers in revenue using the mean ± 3σ rule, and made a deliberate call *not* to impute the ~58% of bookings with null ratings (too large a share to fill without biasing the metric).
3. **Data transformation** — engineered an `occupancy %` field (successful bookings ÷ capacity), joined fact and dimension tables, converted and standardized date fields, and appended a new month of data to simulate a live refresh.
4. **Insight generation** — aggregated occupancy and revenue by room class, city, weekday/weekend, and month.

## Key insights

- **Weekend occupancy (72.4%) is ~21 points higher than weekday occupancy (50.9%)** — the single largest lever in the dataset, suggesting weekday-specific promotions or dynamic pricing would have more impact than uniform discounting.
- **Delhi has the highest occupancy (60.4%) but the lowest revenue realized (₹29.5 Cr)** of the four cities, while Mumbai has mid-pack occupancy (56.8%) but the highest revenue (₹66.9 Cr) — occupancy and revenue don't move together, pointing to a pricing or room-mix gap in Delhi worth investigating.
- **Room class barely affects occupancy** — Presidential (58.1%) vs. Standard (56.8%) is only a ~1.3-point spread, meaning premium inventory isn't an occupancy bottleneck; revenue differences across classes are driven by rate, not demand.
- **17.4% revenue leakage** — total revenue generated (₹206.9 Cr) vs. revenue actually realized (₹170.9 Cr), explained by a 24.8% cancellation rate and 5.0% no-show rate.
- **Ratings are under-captured** — 57.9% of bookings have no rating submitted, which limits how much satisfaction data can currently drive decisions.

## Repo structure

```
3_project_hospitality_analysis/
├── datasets/                  # source CSVs
├── hotels_analysis.ipynb      # main analysis notebook
├── exercise_solution.ipynb    # solved exercises
└── README.md
```

## How to run

```bash
pip install pandas matplotlib jupyter
jupyter notebook hotels_analysis.ipynb
```
