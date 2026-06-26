# Business Insights
**Project:** Executive Sales Performance Dashboard — Retail Chain  
**Dataset:** dashboard_sales_data.xlsx | 4,200 orders | FY 2024–2025 | India

---

## Calculated Fields Explained (Task 2)

The following calculated fields were created in Tableau to support the dashboard:

| Field Name | Formula | Business Purpose |
|---|---|---|
| **Profit Margin** | `[profit] / [sales]` | Measures profitability as a % of revenue; essential KPI for leadership |
| **Cost** | `[sales] - [profit]` | Derives cost of goods sold; enables cost structure analysis |
| **Average Order Value** | `SUM([sales]) / COUNTD([order_id])` | Revenue per order; tracks customer spending intensity |
| **Return Rate** | `SUM([return_flag]) / COUNT([order_id])` | % of orders returned; proxy for product/service quality |
| **Shipping Delay Bucket** | `IF [delivery_days] <= 1 THEN "0-1 Days (Fast)" ELSEIF [delivery_days] <= 3 THEN "2-3 Days (Normal)" ELSEIF [delivery_days] <= 5 THEN "4-5 Days (Slow)" ELSE "6+ Days (Very Slow)" END` | Classifies delivery speed for performance benchmarking |
| **Discount Band** | `IF [discount] = 0 THEN "No Discount" ELSEIF [discount] <= 0.1 THEN "Low (1-10%)" ELSEIF [discount] <= 0.2 THEN "Medium (11-20%)" ELSE "High (21-35%)" END` | Groups discount levels for impact analysis |
| **Profit/Loss Flag** | `IF [profit] >= 0 THEN "Profitable" ELSE "Loss-Making" END` | Binary label for quick profitability filtering |

---
## Business Insights (Task 8)

## Insight 1 — Sales Trend: Technology Drives Monthly Peaks

**Observation:** Monthly sales fluctuate between ₹6.3M and ₹10.5M over the 24-month period, with noticeable spikes in January 2024 and September 2024.

**Data Evidence:** Total sales = ₹21.7 Crore over FY 2024–2025. January 2024 and September 2024 each exceeded ₹10.4M in monthly revenue. The lowest month was August 2024 at ₹6.3M — a 40% dip from peak.

**Business Interpretation:** The January spike may reflect year-start capital purchases (particularly Technology: Copiers, Machines) by Corporate customers. The September uplift could be driven by festive season purchases. The August trough may reflect pre-festive budget freezes.

**Recommended Action:** Plan inventory build-up and marketing campaigns for January and September. Investigate whether August low can be countered with a targeted mid-year promotion for Home Office or Consumer segments.

---

## Insight 2 — Regional Performance: South Region Leads; West Underperforms on Margin

**Observation:** The South region generates the highest total sales (₹6.47 Crore, 30% of total) but the West and East regions appear to have lower profit margins.

**Data Evidence:** South: ₹6.47M profit | North: ₹8.31M | East: ₹7.60M | West: ₹7.40M. South margin ≈ 15.4%. West margin ≈ 15.1% — marginally the lowest.

**Business Interpretation:** South's volume leadership is notable, but the profit margin differential between regions is slim. This suggests consistent pricing strategy across geographies, with South benefiting from higher absolute order volumes or better product mix (more Technology orders).

**Recommended Action:** Analyse SKU mix in South to understand what drives volume. Identify whether West's slightly lower margin reflects higher discount usage or unfavourable product mix. Consider region-specific discount guardrails to protect margin.

---

## Insight 3 — Category Profitability: Technology Dominates, Furniture Underperforms

**Observation:** Technology generates 70.9% of total sales (₹15.4 Crore) but Furniture accounts for 23.8% of sales with only 6.9% of total profit.

**Data Evidence:** Technology: sales ₹15.39 Crore, profit ₹2.80 Crore (margin: 18.2%). Furniture: sales ₹5.16 Crore, profit ₹3.56 million (margin: 6.9%). Office Supplies: smallest in both sales and profit.

**Business Interpretation:** Furniture has a structurally poor margin — potentially due to high logistics costs, return rates (7.7%), and heavy discounting on items like Tables. Technology items (Copiers, Accessories, Phones) deliver strong margins even at high price points.

**Recommended Action:** Review Furniture pricing strategy and delivery cost structure. Consider reducing range of low-margin sub-categories (e.g., Tables at 5.7% margin vs. Copiers at 18.0%). Consider increasing Technology's share of marketing investment.

---

## Insight 4 — Sub-Category Profitability: Copiers and Accessories Top; Tables and Bookcases Drag

**Observation:** Within Technology, Copiers (₹7.31M profit), Accessories (₹7.19M), and Phones (₹7.10M) are the strongest performers. Within Furniture, Tables and Bookcases are the weakest sub-categories by profit.

**Data Evidence:** Copiers profit margin: \~18.0%. Tables: profit ₹7.3L from ₹1.29 Crore sales (\~5.7%). Bookcases: similar margin around 5.7%.

**Business Interpretation:** Copiers and Accessories are high-value, high-margin items likely purchased in bulk by Corporate clients. Tables are likely discounted heavily for large orders. The volume of Furniture orders is insufficient to compensate for the margin compression.

**Recommended Action:** Set minimum margin guardrails for Tables and Bookcases orders. Bundle Technology accessories with high-value hardware to increase attach rate. Consider phase-out or premium positioning of Bookcases.

---

## Insight 5 — Customer Segment Behaviour: Home Office Leads in Sales, Segments are Balanced

**Observation:** The three customer segments — Consumer (33.1%), Corporate (32.5%), and Home Office (34.3%) — have nearly equal sales contributions.

**Data Evidence:** Home Office: ₹7.45 Crore | Consumer: ₹7.19 Crore | Corporate: ₹7.06 Crore. Profit contributions are similarly balanced.

**Business Interpretation:** The near-equal three-way split indicates strong diversification across customer types. Home Office slightly leading may reflect post-pandemic demand for home workstation equipment (Technology + Furniture). Corporate segment, though third, likely places larger individual orders (higher AOV).

**Recommended Action:** Segment-specific campaigns — for Home Office: bundle offers on desks + tech; for Corporate: volume pricing on Technology; for Consumer: loyalty programme with seasonal promotions. Track AOV by segment to confirm Corporate high-value hypothesis.

---

## Insight 6 — Discount Impact: Heavy Discounts Correlate with Profit Erosion

**Observation:** As discount percentage increases from 0% to 35%, average profit per order falls significantly.

**Data Evidence:** No discount: avg profit ₹13,203/order. Low discount (1–10%): ₹10,010. Medium (11–20%): ₹6,336. High (21–35%): ₹2,915. A 35% discount is associated with 78% lower profit vs. no-discount orders.

**Business Interpretation:** Discount levels above 20% are destroying margin. The business may be using heavy discounting to compete for large Furniture orders (which already carry low margins). Technology orders should rarely require discounts above 10% given their premium positioning.

**Recommended Action:** Implement a discount approval workflow for orders above 20% discount. Set category-specific discount caps: Furniture max 15%, Office Supplies max 20%, Technology max 10%. Train sales teams on value-selling to reduce discount dependency.

---

## Insight 7 — Shipping Performance: Standard Class Causes Significant Delays

**Observation:** Standard Class shipping averages 4.71 delivery days, nearly 12× longer than Same Day (0.40 days). Standard Class represents the most common shipping choice.

**Data Evidence:** Same Day: 0.40 avg days | First Class: 1.77 days | Second Class: 2.68 days | Standard Class: 4.71 days. Longest recorded delivery: 9 days (Standard Class).

**Business Interpretation:** Standard Class is likely chosen for cost savings, but the 4.71-day average will impact customer satisfaction for high-urgency orders. Given customer_rating is available, there may be a correlation between Standard Class shipments and lower ratings.

**Recommended Action:** Analyse whether Standard Class orders have lower customer ratings than First Class or Same Day. Set a policy that Technology orders above ₹50,000 are automatically upgraded to Second Class minimum. Offer free First Class upgrade as a loyalty benefit.

---

## Insight 8 — Return Pattern: Furniture Returns Most; Technology Returns Least

**Observation:** Furniture has the highest return rate at 7.7% — more than double the Technology return rate of 3.0%.

**Data Evidence:** Furniture: 88 returns out of 1,142 orders (7.7%). Office Supplies: 61 returns out of 1,649 orders (3.7%). Technology: 42 returns out of 1,409 orders (3.0%). Total returns: 191 of 4,200 orders (4.5%).

**Business Interpretation:** Furniture returns likely involve physical damage during transit (high weight, fragile structure) or size/fit mismatch. Each Furniture return is costly given the high average order value and logistics expense. Technology's lower return rate reflects standardised, well-packaged products.

**Recommended Action:** Investigate Furniture return reasons — build a post-return survey workflow. Improve packaging standards for Tables and Chairs. Offer a 48-hour inspection window with photographic evidence requirements to reduce frivolous returns. Consider tightening return policy for Furniture orders above ₹1L.

---

## Insight 9 — Business Risk: Campaign Channel Gap May Affect Attribution

**Observation:** 24 orders (0.6% of total) have a missing campaign_channel value, suggesting attribution tracking gaps.

**Data Evidence:** Organic: largest share. Social, Paid, Email, Referral also present. 24 records with null campaign_channel.

**Business Interpretation:** Even 0.6% attribution gap can affect marketing ROI calculations significantly when campaign budgets are reallocated based on channel performance data. If Email and Paid campaigns are being assessed on incomplete data, investments may be misallocated.

**Recommended Action:** Fix CRM/order management system to make campaign_channel a mandatory field. Back-fill missing values where possible using customer/order correlation to known campaigns. Add a data quality monitoring card to the executive dashboard to flag ongoing attribution gaps.
