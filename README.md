# Fit.ly Customer Churn Analysis

DataCamp Data Analyst Associate final project. Fit.ly is a subscription-based
fitness app (workout articles, instructional videos, workout tracking, and
workout sharing). Over the past two quarters churn has been rising, putting
pressure on acquisition costs and on the Product and Marketing teams. This
project investigates what is driving churn and turns the findings into
practical recommendations for leadership.

## Data

Three source files (provided as part of the DataCamp project) live in
[`data/`](data/):

| File | Description |
|---|---|
| `da_fitly_account_info.csv` | Customer id, email, state, plan tier, list price, churn status |
| `da_fitly_customer_support.csv` | Support tickets — timestamp, channel, topic, resolution time, comments |
| `da_fitly_user_activity.csv` | Product usage events (watch video, read article, track/share workout) |

## Approach

The analysis, in [`fitly_churn_analysis.ipynb`](fitly_churn_analysis.ipynb), covers:

1. **Data validation** — missing values, duplicates, and consistency checks
   across all three sources.
2. **Exploratory analysis** — churn by plan tier, support resolution time
   distribution, and correlation between engagement, support tickets, and churn.
3. **Engagement deep dive** — churn rate by product engagement level, and
   whether support resolution time still matters after controlling for
   engagement.
4. **Metric to monitor** — a proposed leading-indicator KPI (Customer
   Engagement Rate) with a definition, baseline, and an early-warning threshold
   for the business to track.

## Key findings

- Overall churn is **28.5%**.
- **Product engagement is the dominant driver.** Customers with zero recorded
  activity churn at **53.9%**, over 10x the rate of highly engaged customers
  (**4.2%**) — a far wider gap than any split by plan tier.
- **Support resolution speed is a secondary, independent driver.** Even among
  customers with zero activity, those who churned waited **18.7 hrs** on
  average for a resolution vs **6.1 hrs** for those who stayed.
- Free-tier customers churn the most of any plan (**41.0%**); billing tickets
  have the highest associated churn among ticket topics (**36.4%**).

## Recommendations

1. Launch a re-engagement push for the 38.5% of customers with zero activity.
2. Enforce a 10-hour support SLA, prioritizing billing tickets.
3. Build a Free-tier upgrade path.
4. Fix the missing `signup_date` field and the ambiguous
   `customer_support.state` field.
5. Route the 36 GDPR deletion requests found in the support comments to the
   compliance process.

## Metric to monitor

**Customer Engagement Rate** — the % of customers who log at least one
product activity event (video, article, workout tracked/shared) in a period.
Unlike churn, which only shows up after cancellation, this is a leading
indicator. Recommended tracking: monthly, broken out by plan tier, with an
early-warning trigger on a month-over-month drop of 3–5+ percentage points or
any plan tier falling meaningfully below the overall baseline.

## Tools

- Python (pandas, matplotlib, seaborn) in a Jupyter notebook

## Repository structure

```
.
├── data/
│   ├── da_fitly_account_info.csv
│   ├── da_fitly_customer_support.csv
│   └── da_fitly_user_activity.csv
├── fitly_churn_analysis.ipynb
├── requirements.txt
└── README.md
```

## Running locally

```bash
pip install -r requirements.txt
jupyter notebook fitly_churn_analysis.ipynb
```
