# Retail Sales Executive Dashboard — README

---

## 1. Business Problem Summary

The retail leadership team needs a centralized executive dashboard to monitor and act on key performance areas across the business. Without a unified view, leadership cannot quickly identify which regions, categories, customer segments, or shipping modes are driving growth — or causing losses.

This dashboard addresses seven core business questions:
- Are overall sales trending up or down over time?
- Which regions and states are over- or under-performing?
- Which product categories and sub-categories are most (and least) profitable?
- How do customer segments differ in revenue, profitability, and behavior?
- Is heavy discounting harming profitability?
- Are shipping delays concentrated in certain modes or regions?
- Where are returns occurring most, and what is the financial risk?

The goal is to support faster, evidence-based decisions at the leadership level.

---

## 2. Dataset Description

| Attribute | Detail |
|---|---|
| **File** | `dashboard_sales_data.xlsx` |
| **Total Records** | 4,200 orders |
| **Date Range** | January 1, 2024 – December 31, 2025 (2 full years) |
| **Granularity** | One row per order |

### Field Reference

| Field | Data Type | Description |
|---|---|---|
| `order_id` | Categorical (String) | Unique order identifier |
| `order_date` | Date | Date the order was placed |
| `ship_date` | Date | Date the order was shipped |
| `customer_id` | Categorical (String) | Unique customer identifier |
| `customer_segment` | Categorical | Customer segment: Consumer, Corporate, Home Office |
| `region` | Categorical / Geographic | Sales region: North, South, East, West |
| `state` | Categorical / Geographic | U.S. state of the order |
| `city` | Categorical / Geographic | City of the order |
| `category` | Categorical | Product category: Furniture, Office Supplies, Technology |
| `sub_category` | Categorical | Product sub-category (13 values, e.g., Chairs, Phones, Binders) |
| `product_name` | Categorical (String) | Product name |
| `ship_mode` | Categorical | Shipping method: Standard Class, Second Class, First Class, Same Day |
| `sales` | Numerical Measure | Order revenue in USD |
| `quantity` | Numerical Measure | Units ordered |
| `discount` | Numerical Measure | Discount rate applied (0.00 – 0.35) |
| `profit` | Numerical Measure | Net profit in USD (can be negative) |
| `return_flag` | Binary / Flag | 1 = returned order, 0 = not returned |
| `delivery_days` | Numerical Measure | Days between order date and ship date |
| `customer_rating` | Numerical Measure | Customer satisfaction rating (32 missing values) |
| `campaign_channel` | Categorical | Marketing channel: Organic, Social, Referral, Paid, Email (24 missing values) |

---

## 3. Tableau Workbook Description

The Tableau workbook (`Retail_Executive_Dashboard.twbx`) contains:

- **7 supporting worksheet tabs**, each answering a specific business question
- **1 executive dashboard** combining key views with KPI cards and interactive filters
- All calculated fields embedded in the workbook
- Filters, actions, and tooltips configured for leadership use

The workbook opens to the Executive Dashboard by default. All supporting sheets are accessible via tabs.

---

## 4. Calculated Fields Created

| Calculated Field | Formula Logic | Purpose |
|---|---|---|
| **Profit Margin** | `SUM([Profit]) / SUM([Sales])` | Measures what percentage of revenue becomes profit |
| **Cost** | `SUM([Sales]) - SUM([Profit])` | Derives the implied cost of goods/operations |
| **Average Order Value** | `SUM([Sales]) / COUNTD([Order ID])` | Measures revenue per unique order |
| **Return Rate** | `SUM([Return Flag]) / COUNT([Order ID])` | Percentage of orders that were returned |
| **Shipping Delay Bucket** | `IF [Delivery Days] <= 1 THEN "Same Day / Next Day" ELSEIF [Delivery Days] <= 3 THEN "2–3 Days" ELSEIF [Delivery Days] <= 5 THEN "4–5 Days" ELSE "6+ Days (Delayed)" END` | Groups delivery speed into meaningful performance buckets |

Additional supporting fields:
- **Profit Flag**: `IF SUM([Profit]) < 0 THEN "Loss" ELSE "Profit" END` — used to highlight loss-making categories/regions in red
- **Discount Band**: `IF [Discount] = 0 THEN "No Discount" ELSEIF [Discount] <= 0.10 THEN "Low (1–10%)" ELSEIF [Discount] <= 0.20 THEN "Medium (11–20%)" ELSE "High (21–35%)" END` — groups discount levels for scatter analysis

---

## 5. Dashboard Components

The Executive Dashboard includes:

### KPI Summary Cards (top strip)
- **Total Sales** — SUM of all sales revenue
- **Total Profit** — SUM of all profit
- **Overall Profit Margin** — Profit ÷ Sales
- **Return Rate** — % of returned orders
- **Average Order Value** — Sales ÷ Distinct Orders

### Charts / Views (5 embedded sheets)
1. **Sales Trend (Line Chart)** — Monthly sales over time, colored by year, showing seasonality and YoY growth
2. **Regional Performance (Filled Map + Bar)** — Sales and profit by region/state; color encodes profit margin
3. **Category & Sub-Category Profitability (Bar Chart / Highlight Table)** — Horizontal bars ranked by profit; red = loss
4. **Discount vs. Profit (Scatter Plot)** — Each point = sub-category; X = avg discount, Y = profit margin; reveals discount-harm threshold
5. **Shipping Performance (Bar Chart)** — Delivery day buckets by ship mode; shows delay concentration

### Additional Detail Sheets (accessible via tabs)
6. **Customer Segment View** — Sales, profit, AOV, and return rate by segment
7. **Return Analysis View** — Return rate heatmap by category and segment

---

## 6. Filters and Interactions Used

### Interactive Filters (applied globally across the dashboard)
- **Region** — Single/multi-select; filters all views
- **Category** — Single/multi-select; filters relevant charts
- **Customer Segment** — Single/multi-select
- **Order Date (Year/Month range)** — Relative date filter
- **Ship Mode** — Single/multi-select
- **Campaign Channel** — Single/multi-select

### Dashboard Actions
- **Highlight Action**: Clicking a region on the map highlights corresponding bars in the Category Profitability chart
- **Filter Action**: Clicking a category bar filters the Discount vs. Profit scatter to show only that category's sub-categories
- **URL Action**: Order ID tooltip links to a placeholder detail view

---

## 7. Key Business Insights

1. **Technology drives the highest revenue but Furniture drives losses** — Tables and Bookcases consistently post negative profit margins, especially at higher discount rates.

2. **High discounts (>20%) destroy profitability** — Orders with discounts above 20% have a negative average profit margin across all categories. The scatter plot shows a clear negative correlation between discount rate and profit margin.

3. **The West region leads in sales volume but the East has the strongest profit margin** — Regional performance diverges significantly when comparing revenue vs. profitability.

4. **Corporate segment has the highest Average Order Value**, but the Consumer segment drives the most volume. Home Office has the highest return rate, signaling potential product-fit issues.

5. **Standard Class shipping accumulates the most 6+ day delays** despite being the most used mode. Same Day shipping, as expected, has near-zero delays but higher cost.

6. **Sales show a strong Q4 seasonality pattern** — Revenue peaks in November–December in both 2024 and 2025, suggesting leadership should plan inventory and staffing accordingly.

7. **Return rate is highest in Furniture** — Combined with its low profit margin, returns in this category represent the largest financial risk to the business.

8. **Paid and Email campaign channels generate higher Average Order Values** compared to Organic or Social, suggesting a reallocation of marketing budget could improve revenue quality.

---

## 8. Dashboard Story Summary

The business entered 2024–2025 with strong top-line sales growth, but the underlying profitability story is more complex. Technology and Office Supplies are the profit engines, while Furniture — particularly Tables — is actively losing money at scale. A key driver of those losses is aggressive discounting: the data shows that discounts above 20% consistently produce negative margins, regardless of category.

Regionally, the West generates the most sales but the East operates more efficiently. The South is a risk area with lower volume and thinner margins. Leadership should consider whether current pricing and discount policies in the South and Furniture category are sustainable.

Shipping performance reveals that Standard Class — the default mode — is generating the most delayed deliveries, which correlates with lower customer ratings. Shifting higher-value orders to First Class may improve satisfaction without significantly impacting margin.

Return patterns, concentrated in Furniture and the Home Office segment, suggest a product-market fit issue that warrants further investigation — potentially through customer feedback and product quality review.

The dashboard is designed to move leadership from "what happened" to "what should we do next."

---

## 9. Assumptions and Limitations

### Assumptions
- `return_flag = 1` is treated as a fully returned order (partial returns are not distinguished)
- `delivery_days` is calculated as the difference between `order_date` and `ship_date` (not delivery confirmation date)
- Orders with `delivery_days = 0` are treated as Same Day fulfillment, not data errors
- Negative profit values are assumed to be accurate and reflect real loss-making orders after discounts and costs
- The 24 missing `campaign_channel` values are excluded from campaign-channel analysis (not imputed)
- The 32 missing `customer_rating` values are excluded from rating-based analysis (not imputed)
- USD is assumed as the currency for all monetary fields

### Limitations
- No customer-level data (e.g., lifetime value, repeat purchase rate) — analysis is order-level only
- No cost breakdown (COGS, shipping cost, overhead) — "Cost" is a derived estimate only
- `campaign_channel` has 0.57% missing values — campaign analysis may slightly underrepresent one or more channels
- The dataset covers only 2 years (2024–2025); longer trends cannot be confirmed
- Geographic analysis is limited to region and state — city-level analysis may produce sparse results for less-populated states
- Return reasons are not captured — root-cause analysis of returns is not possible from this dataset alone

---

## 10. Screenshots Included

The following screenshots are saved in the `screenshots/` folder:

| File | Contents |
|---|---|
| `screenshots/full_dashboard.png` | Complete executive dashboard with all KPI cards, 5 charts, and filters visible |
| `screenshots/sales_trend_view.png` | Sales trend line chart sheet — monthly sales over 2024–2025 |
| `screenshots/regional_performance_view.png` | Regional/state-level sales and profit map + bar chart |
| `screenshots/category_profitability_view.png` | Category and sub-category profitability bar chart |
| `screenshots/filter_interaction_view.png` | Dashboard with Region filter applied, showing cross-chart filter action in effect |

> **Note:** Screenshots were captured at 1920×1080 resolution with all labels and axes fully visible. Filters were set to "All" for the `full_dashboard.png` capture.
