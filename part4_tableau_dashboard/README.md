# Part 4: Tableau Executive Dashboard — Retail Chain Sales Performance
**Dataset:** dashboard_sales_data.xlsx | 4,200 orders | FY 2024–2025 | India Retail Chain

---

## 1. Business Problem Summary

The retail chain leadership team requires an executive dashboard to monitor and interpret sales performance across multiple business dimensions simultaneously. Leadership needs to understand:
- What is driving monthly revenue and profit trends?
- Which regions, categories, and customer segments are performing well or poorly?
- How is the business being impacted by discounting, shipping choices, and product returns?
- What actions should leadership prioritise to improve profitability and customer satisfaction?

The dashboard was designed to answer all of these questions in a single, filterable executive view — providing both a high-level overview and drill-down capability by region, category, segment, and date range.

---

## 2. Dataset Description

| Attribute | Detail |
|---|---|
| File | `data/dashboard_sales_data.xlsx` |
| Rows | 4,200 orders |
| Columns | 20 |
| Date Range | January 2024 – December 2025 |
| Geography | India (4 regions, 28 states, multiple cities) |
| Missing Values | `customer_rating`: 32 nulls | `campaign_channel`: 24 nulls |

### Column Reference

| Column | Type | Description |
|---|---|---|
| order_id | Identifier | Unique order reference |
| order_date | Date | Date order was placed |
| ship_date | Date | Date order was shipped |
| customer_id | Identifier | Customer reference |
| customer_segment | Categorical | Consumer / Corporate / Home Office |
| region | Categorical | North / South / East / West |
| state | Categorical | Indian state name |
| city | Categorical | City name |
| category | Categorical | Furniture / Office Supplies / Technology |
| sub_category | Categorical | 13 sub-categories |
| product_name | Text | Product description |
| ship_mode | Categorical | Same Day / First Class / Second Class / Standard Class |
| sales | Measure | Order sales value (₹) |
| quantity | Measure | Number of units |
| discount | Measure | Discount rate (0.0–0.35) |
| profit | Measure | Order profit (₹) |
| return_flag | Binary (0/1) | 1 = returned order |
| delivery_days | Measure | Days from order to delivery |
| customer_rating | Measure | Satisfaction rating (1–5); 32 nulls |
| campaign_channel | Categorical | Organic / Social / Paid / Email / Referral; 24 nulls |

---

## 3. Tableau Workbook Description

**File:** `tableau/executive_dashboard.twbx`  
**Format:** Tableau Packaged Workbook (ZIP containing .twb + embedded data)

The workbook contains:

| Sheet | View Type | Purpose |
|---|---|---|
| Sales Trend | Dual-axis line chart | Monthly sales & profit trend + margin bar |
| Regional Performance | Horizontal bar + heatmap | Sales/profit/return by region + state-level highlight table |
| Category Profitability | Grouped bar + treemap | Category & sub-category performance |
| Customer Segment | Pie chart + bar | Segment contribution to sales & profit |
| Shipping Performance | Horizontal bar | Average delivery days by ship mode |
| Discount vs Profit | Scatter plot | Discount rate vs profit relationship |
| Return Analysis | Bar chart | Return rate by category, segment, region |
| KPI Summary | Text table | Top-line KPIs for dashboard header |
| Sub-Category Bar | Horizontal bar | Profit by sub-category (profitability drill-down) |
| **Executive Dashboard** | Combined dashboard | Aggregates 5+ charts with 5 filters and action interactions |

---

## 4. Calculated Fields Created

| Calculated Field | Formula | Purpose |
|---|---|---|
| **Profit Margin** | `[profit] / [sales]` | Core profitability KPI; shown as % |
| **Cost** | `[sales] - [profit]` | Derived cost for cost structure analysis |
| **Average Order Value** | `SUM([sales]) / COUNTD([order_id])` | Revenue intensity per order |
| **Return Rate** | `SUM([return_flag]) / COUNT([order_id])` | Quality proxy; shown as % |
| **Shipping Delay Bucket** | `IF [delivery_days] <= 1 THEN "0-1 Days (Fast)" ELSEIF [delivery_days] <= 3 THEN "2-3 Days (Normal)" ELSEIF [delivery_days] <= 5 THEN "4-5 Days (Slow)" ELSE "6+ Days (Very Slow)" END` | Delivery performance classification |
| **Discount Band** | `IF [discount] = 0 THEN "No Discount" ELSEIF [discount] <= 0.1 THEN "Low (1-10%)" ELSEIF [discount] <= 0.2 THEN "Medium (11-20%)" ELSE "High (21-35%)" END` | Discount level segmentation |
| **Profit/Loss Flag** | `IF [profit] >= 0 THEN "Profitable" ELSE "Loss-Making" END` | Binary profitability flag for filtering |

---

## 5. Dashboard Components

### KPI Cards (3 primary + 2 secondary)
1. **Total Sales** — ₹21.7 Crore | 4,200 orders
2. **Total Profit** — ₹3.33 Crore | Margin: 15.35%
3. **Average Order Value** — ₹51,671 per order
4. **Return Rate** — 4.5% | 191 returned orders
5. **Top Region** — South | ₹6.47 Crore | 30% of sales

### Charts (7 views + heatmap)
1. Monthly Sales & Profit Trend (Dual-Axis Line)
2. Profit Margin by Month (Bar)
3. Sales & Profit by Region (Horizontal Bar)
4. State-level Sales Highlight Table (Heatmap)
5. Category Sales vs Profit (Grouped Bar)
6. Sub-Category Profit Ranking (Horizontal Bar)
7. Customer Segment Contribution (Pie)
8. Shipping Mode Delivery Performance (Horizontal Bar)
9. Discount vs Profit Relationship (Scatter Plot)
10. Return Rate by Category (Bar)

---

## 6. Filters and Interactions Used

### Interactive Filters (5 filters)
| Filter | Field | Scope |
|---|---|---|
| Region Filter | `region` | Applied to all sheets |
| Category Filter | `category` | Applied to all sheets |
| Customer Segment Filter | `customer_segment` | Applied to all sheets |
| Date Range | `order_date` | Applied to trend and all sheets |
| Ship Mode Filter | `ship_mode` | Applied to all sheets |

### Dashboard Actions (2 interactions)
1. **Region Bar Click → Filter All Charts:** Clicking a region bar in the Regional Performance chart filters all other charts on the dashboard to show only that region's data.
2. **Category Bar Click → Highlight Scatter:** Clicking a category in the Category chart highlights corresponding dots in the Discount vs Profit scatter plot, revealing category-specific discount patterns.

---

## 7. Key Business Insights

1. **Technology drives 70.9% of sales and 84.2% of profit** — it is the core business engine.
2. **Furniture margin is critically low at 6.9%** — combined with 7.7% return rate, it is a value-destroyer.
3. **South region leads with ₹6.47 Crore** — should receive priority investment.
4. **Heavy discounts (21–35%) reduce profit by 78%** compared to non-discounted orders.
5. **Standard Class shipping averages 4.71 days** — 12× slower than Same Day; satisfaction risk.
6. **Three customer segments are nearly equal** (32–34% each) — healthy diversification.
7. **August is a predictable trough month** — ₹6.3M vs ₹10.5M peak; intervention opportunity.
8. **Copiers, Accessories, Phones** are top sub-categories by profit — protect and grow.

---

## 8. Dashboard Story Summary

The executive dashboard tells a story of a fundamentally sound but unevenly profitable retail business. Technology is the star performer — high revenue, high margin, low returns. Furniture is the problem category — moderate revenue, poor margin, high returns, heavy discounting required to close deals. The South region is the strongest market with growth potential.

Key leadership actions: implement discount guardrails, investigate Furniture return causes, launch an August mid-year campaign to fill the seasonal trough, and upgrade shipping for high-value Technology orders. The business has strong structural foundations; the opportunity lies in margin protection and geographic deepening.

---

## 9. Assumptions and Limitations

| Item | Detail |
|---|---|
| Profit calculation | Profit is taken directly from the dataset; assumed to be gross profit excluding corporate overhead |
| Cost field | Derived as `sales - profit`; may not represent actual COGS |
| Missing customer_rating (32 rows) | Excluded from rating-based analysis; treated as missing at random |
| Missing campaign_channel (24 rows) | Channel performance metrics are approximations |
| Return reasons not available | Return rate computed from binary flag only; root cause unknown |
| India-specific geography | Region/State fields reflect Indian geography; not suitable for global comparison without context |
| Two years of data only | Insufficient to distinguish trend from seasonality with statistical confidence |
| Dashboard replication note | `.twbx` file contains full XML workbook definition and embedded data; open with Tableau Desktop 2024.1+ |

---

## 10. Screenshots Included

| Screenshot | File | Contents |
|---|---|---|
| Full Dashboard | `screenshots/full_dashboard.png` | Complete executive dashboard with all charts, KPIs, and filter panel |
| Sales Trend View | `screenshots/sales_trend_view.png` | Monthly Sales & Profit Trend line chart + Profit Margin bar chart |
| Regional Performance | `screenshots/regional_performance_view.png` | Regional bar charts + state-level highlight table |
| Category Profitability | `screenshots/category_profitability_view.png` | Sub-category profit bar + treemap + margin + return rate |
| Filter Interaction | `screenshots/filter_interaction_view.png` | Dashboard with Region=South filter applied across all charts |

---
