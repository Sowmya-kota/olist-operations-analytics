# Olist E-Commerce Operations Analytics

Delivery performance and cancellation analysis across 99,441 orders from a Brazilian e-commerce marketplace (2016–2018), built in Python and pandas.

## Dataset

[Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) — 100k orders across 9 related tables covering order status, timestamps, customer and seller geography, products, payments, and reviews.

Data files are not committed to this repository. Download from Kaggle and place the CSVs in `data/`.

## Key Findings

**On-time delivery: 91.88%** across 96,478 delivered orders. Average delivery time 12 days, median 10 — right-skewed, with 63 orders (0.07%) exceeding 100 days, retained as genuine long-tail cases.

**Percentage rankings and volume-weighted rankings surface entirely different priorities.** São Paulo has one of the best on-time rates (94.1%) but the highest absolute count of late orders (2,394), while the worst state by percentage — Alagoas at 76.1% — accounts for fewer than 100. The same pattern held at seller level, with no overlap between the two top-10 lists.

**Speed and reliability are distinct metrics.** Pará averages 23.3 delivery days yet meets 87.6% of delivery promises, while Rio de Janeiro delivers in 14.8 days but meets only 86.5% — an estimation problem rather than a logistics one.

**The 91.88% average masks a 20-point swing over time.** Monthly on-time performance ranges from 78.6% (March 2018) to 98.6% (June 2018), with a Black Friday capacity dip in November 2017 and a separate two-month operational degradation in early 2018 that later recovered.

**Cancellation is driven by payment method, not geography.** Overall cancellation rate is 0.63%. State-level variation is minimal (0.44%–0.78%), but voucher-paid orders cancel at 3.21% — over five times the rate of card or boleto payments.

## Approach

1. Loaded and validated 7 related tables — column types, null counts, key integrity, and differing grain across orders, items, and payments
2. Confirmed missing delivery timestamps corresponded to incomplete order journeys rather than data quality issues, and identified 2 genuine inconsistencies
3. Derived delivery duration and on-time flags from raw timestamps
4. Defined KPI-eligible populations explicitly (delivered orders for delivery metrics; all orders for cancellation rate)
5. Analysed performance across state, seller, month, and payment method
6. Applied minimum-sample thresholds where small groups would distort rates, documenting coverage in each case

## Limitations

Cancellation reason codes are not available in this dataset, so cancellation drivers are inferred from dimensional patterns rather than stated causes.

## Tools

Python, pandas, NumPy, Matplotlib, Jupyter

## Structure

    olist-operations-analytics/
    ├── data/                                    # source CSVs (not committed)
    ├── notebooks/
    │   └── 01_data_loading_validation.ipynb     # full analysis
    └── README.md