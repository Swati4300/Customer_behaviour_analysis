# Customer_behaviour_analysis
Data Analytics project showing customer behavior analysis using python , sql and power bi
# Customer Behavior Analysis: SQL + Power BI Dashboard

End-to-end analysis of **3,900 retail customers**: raw CSV → PostgreSQL → 10 business questions answered in SQL → interactive Power BI dashboard.

<img width="1384" height="748" alt="image" src="https://github.com/user-attachments/assets/b3f40270-f54d-4117-8e0d-fe1bd50b44bb" />


## Project Overview

A retail business wants to understand **who its customers are, what they buy, how they pay, and which levers (discounts, subscriptions, shipping) actually move spend**. This project cleans the data, answers ten targeted business questions with SQL, and presents the results in a filterable Power BI dashboard.

## Dataset

| Item | Detail |
|---|---|
| Source file | `customer_shopping_behavior_1.csv` |
| Rows / columns | 3,900 customers / 18 columns |
| Key fields | Age, Gender, Item Purchased, Category, Purchase Amount (USD), Location, Season, Review Rating, Subscription Status, Shipping Type, Discount Applied, Previous Purchases, Payment Method, Purchase Frequency |
| Categories | Clothing, Accessories, Footwear, Outerwear (25 distinct items) |
| Data quality | No duplicate customers; 37 missing Review Ratings (~0.9%) |

## Tech Stack

- **PostgreSQL**: data storage and analysis (CTEs, subqueries, window functions, CASE logic)
- **Power BI Desktop**: dashboard, slicers and measures
- **Python (pandas)**: data preparation and loading

## Workflow

1. **Prepare data**: standardised column names to `snake_case` and engineered an `age_group` feature using age quartiles (Young Adult 18–31, Adult 32–44, Middle-aged 45–57, Senior 58–70).
2. **Load to PostgreSQL** as the `customer` table.
3. **Analyse with SQL**: 10 business questions (see below).
4. **Visualise in Power BI**: KPI cards, category and age-group charts, subscription split, and slicers for subscription, gender, category and shipping type.

## SQL Analysis (`customer_behaviour.sql`)

| # | Business question | SQL concepts | Result |
|---|---|---|---|
| 1 | Revenue by gender | `GROUP BY`, `SUM` | Male $157,890 vs Female $75,191 |
| 2 | Discount users who still spent above average | Subquery | 839 customers (21.5%) |
| 3 | Top 5 products by average rating | `AVG`, `ORDER BY`, `LIMIT` | Gloves (3.86), Sandals (3.84), Boots (3.82) lead |
| 4 | Standard vs Express shipping spend | `AVG`, `IN` | Express $60.48 vs Standard $58.46 |
| 5 | Do subscribers spend more? | Multi-metric aggregation | No: $59.49 (subscribers) vs $59.87 (non-subscribers) |
| 6 | Products with highest discount rate | Conditional aggregation (`CASE`) | Hat 50.0%, Sneakers 49.7%, Coat 49.1% |
| 7 | Customer segmentation (New / Returning / Loyal) | CTE + `CASE` | Loyal 3,116, Returning 701, New 83 |
| 8 | Top 3 products per category | CTE + `ROW_NUMBER() OVER (PARTITION BY …)` | e.g. Jewelry, Pants, Sandals, Jacket |
| 9 | Are repeat buyers more likely to subscribe? | Filtering + grouping | 958 of 3,476 repeat buyers (27.6%) subscribe |
| 10 | Revenue contribution by age group | `GROUP BY`, `ORDER BY` | Young Adult leads with $62,143 (26.7%) |

## Power BI Dashboard (`Customer_Behavior.pbix`)

- **KPI cards**: Number of Customers (3.9K), Average Purchase Amount ($59.76), Average Review Rating (3.75)
- **Donut chart**: % of customers by subscription status (27% Yes / 73% No)
- **Column charts**: Revenue by Category and Sales (order count) by Category
- **Bar charts**: Revenue by Age Group and Sales by Age Group
- **Slicers**: Subscription Status, Gender, Category, Shipping Type

## Key Insights

1. **Clothing drives the business**: 44.7% of revenue ($104,264 of $233,081), followed by Accessories (31.8%). Outerwear is only 7.9%.
2. **Male customers generate 68% of revenue, but it is a customer-mix effect.** They are 68% of customers, and average spend is almost identical ($59.54 male vs $60.25 female). The growth opportunity is acquiring more female customers, not raising their spend.
3. **Subscriptions do not increase spend.** Subscribers (27% of customers) spend $59.49 on average versus $59.87 for non-subscribers, so the subscription's value likely lies in retention rather than basket size.
4. **Discounts do not lift order value** ($59.28 with discount vs $60.13 without). Discounts are applied to 43% of purchases, so margin is being given away for no visible spend gain.
5. **Express shipping buyers spend ~$2 more** per order than Standard buyers, which suggests a possible upsell opportunity.
6. **80% of customers are already "Loyal"** (more than 10 previous purchases), so retention is strong; only 2% are new, which signals an acquisition gap.
7. **Age matters less than expected.** Young Adults (18–31) lead revenue, but all four age groups sit between 24% and 27%.

## Repository Structure

```
├── customer_shopping_behavior_1.csv   # raw dataset
├── customer_behaviour.sql             # 10 business-question queries
├── Customer_Behavior.pbix             # Power BI dashboard
├── dashboard.png                      # dashboard screenshot
└── README.md
```

## How to Run

1. Load `customer_shopping_behavior_1.csv` into PostgreSQL as a table named `customer` (snake_case column names, plus the derived `age_group` column).
2. Run the queries in `customer_behaviour.sql`.
3. Open `Customer_Behavior.pbix` in Power BI Desktop and point the data source to your PostgreSQL instance.

## Author

**Swati Yallurkar**: MCA, Pune | AI Engineer & Data Analyst aspirant
[GitHub](https://github.com/Swati4300) · [LinkedIn](https://linkedin.com/in/swati-yallurkar-331584220) · swatiyallurkar28@gmail.com
