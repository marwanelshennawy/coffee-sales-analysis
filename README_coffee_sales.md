# Coffee Sales: Processing & Analysis

A fully commented Jupyter notebook that cleans and analyzes transaction-level coffee sales (1 March 2024 to 23 March 2025) to understand what sells, when, and to whom.

## Contents

| File | Description |
|---|---|
| `Coffee_Sales_Analysis.ipynb` | The analysis notebook (code comments plus markdown explanations) |
| `index_1.csv` | The dataset: 3,636 transactions, 6 columns. Place it next to the notebook |
| `README_coffee_sales.md` | This file |

### Dataset columns

| Column | Meaning |
|---|---|
| `date` | Transaction date |
| `datetime` | Exact timestamp |
| `cash_type` | `card` or `cash` |
| `card` | Anonymized card ID (empty for cash payments) |
| `money` | Amount paid (currency not stated in the data) |
| `coffee_name` | Drink sold (8 types) |

## What the notebook covers

1. **Setup and load**: libraries, plot style, datetime parsing
2. **Cleaning and validation**
   - Confirms every missing `card` value is a cash payment and labels them explicitly
   - Checks duplicates, non-positive amounts and date consistency
   - Finds calendar days with no sales (7 days)
3. **Feature engineering**: month, weekday, hour, weekend flag, part of day
4. **Exploratory analysis**
   - Headline numbers
   - Product revenue and volume
   - Monthly and daily trends with a 7-day rolling average
   - Weekday and hourly patterns, including a weekday-by-hour heatmap
   - Product mix by time of day
   - Payment type
   - Price changes over time
   - Customer loyalty from card IDs
5. **Statistical tests**: chi-square (product vs. time of day) with Cramer's V, Mann-Whitney (weekday vs. weekend), Kruskal-Wallis (across weekdays)
6. **Forecast baseline**: weekday-average forecast compared with a flat average
7. **Key takeaways and limitations**

## Main findings

- About **115,400** in revenue from **3,636** transactions over 381 selling days (about 303 per day).
- **Latte** (24% of revenue) and **Americano with Milk** (22%) lead. Espresso is only about 2%.
- October and February are the strongest months; the latest month (March 2025) is incomplete.
- Weekdays earn significantly more than weekends. The busiest hour is 10:00.
- Product preferences shift through the day (Cortado and Americano with Milk in the morning, milk and chocolate drinks in the evening), though the effect is small.
- About 98% of transactions are by card.
- Drink prices dipped in summer 2024 and rose in autumn, so revenue trends mix price and volume effects.
- About 41% of card IDs return, and they account for about 78% of card sales.
- A simple weekday forecast did not beat a flat average.

## Getting started

Requirements: Python 3.9+, pandas, numpy, matplotlib, seaborn, scipy, Jupyter.

```bash
pip install pandas numpy matplotlib seaborn scipy jupyter
jupyter notebook Coffee_Sales_Analysis.ipynb
```

Choose **Kernel > Restart & Run All**. If your CSV is elsewhere, change `DATA_PATH` in the Load cell.

## Limitations

- Currency and the reasons for price changes are not in the data.
- Cash customers cannot be tracked, and some card IDs may be shared or corporate cards.
- Just over a year of data is too short to separate seasonality from growth.
