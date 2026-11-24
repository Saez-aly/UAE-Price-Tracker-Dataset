
# Shein Anchor Price & Fake Discount Detection Dataset

## Overview
This dataset contains historical pricing observations collected from **Shein** to train tabular machine learning models (**Random Forest** and **XGBoost**) for detecting anchor price inflation and deceptive discounting.

## Dataset Structure
- **Format:** CSV (`shein_price_dataset.csv`)
- **Granularity:** One row (observation) per tracked product listing
- **Target Classes (`label`):**
  - `0` — **Fake Discount / Anchor Inflation:** Strikethrough price was artificially inflated or current "sale" price is near/above historical median.
  - `1` — **Normal Price:** Standard everyday retail price with no deceptive discount framing.
  - `2` — **Genuine Great Deal:** Verified price drop significantly below historical median.

## Data Dictionary (Features)

| Column Name | Type | Description |
| :--- | :--- | :--- |
| `product_id` | String | Unique Shein product identifier (Goods ID) |
| `category` | String | Product category (e.g., Apparel, Accessories, Home) |
| `currency` | String | Standardized currency code (e.g., USD, AED) |
| `current_sale_price` | Float | Active checkout price displayed on the listing |
| `claimed_retail_price` | Float | Strikethrough "original" anchor price displayed on the listing |
| `claimed_discount_pct` | Float | Percentage discount advertised by the listing |
| `median_price_90d` | Float | Historical median price over the prior 90 days |
| `min_price_180d` | Float | Lowest recorded price over the prior 180 days |
| `max_price_180d` | Float | Highest recorded price over the prior 180 days |
| `pre_sale_spike_14d` | Float | Percentage price increase in the 14 days prior to the current price |
| `price_vs_median_ratio` | Float | Ratio of `current_sale_price` to `median_price_90d` |
| `label` | Integer | Ground-truth classification (`0` = Fake Discount, `1` = Normal, `2` = Great Deal) |

## Methodology & Data Hygiene
- Multi-variant listings with mismatched SKU pricing tiers are excluded to prevent baseline distortion.
- Currency values are standardized prior to feature calculation to eliminate exchange-rate anomalies.
