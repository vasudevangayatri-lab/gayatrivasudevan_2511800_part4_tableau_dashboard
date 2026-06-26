# Chart Selection Justification (Task 10)
**Project:** Executive Sales Performance Dashboard — Retail Chain  


---

## Overview

Every chart in the executive dashboard was selected based on the specific business question it answers, the nature of the data being displayed, and established data visualisation principles. This document explains each major chart choice, the design rationale, and the mistakes that were deliberately avoided.

---

## Chart 1 — Sales & Profit Trend (Dual-Axis Line Chart)

**Business Question:** How are monthly sales and profit trending over the 24-month period? Are they moving together or diverging?

**Why This Chart Type:**
A line chart is the most appropriate visualisation for time-series data because it naturally encodes the sequential ordering of dates along the horizontal axis and makes trends, peaks, and troughs immediately visible. A dual-axis design (Sales on left axis, Profit on right axis) allows both metrics to be overlaid without one dominating the scale of the other. The area fill under the sales line reinforces volume context.

**Fields Used:**
- X-axis: `order_date` (aggregated to Month)
- Left Y-axis: `SUM(sales)`
- Right Y-axis: `SUM(profit)`
- Color: Blue for Sales, Orange dashed for Profit
- Labels: Year-month tick labels; peak annotation

**Design Principle Applied:** Pre-attentive encoding — the two lines are easily distinguished by color and line style (solid vs. dashed). The area fill creates a visual anchor for the scale.

**Mistake Avoided:** Did not use a bar chart for this data (bars are less effective for continuous trend communication over 24 months). Did not truncate the Y-axis, which would exaggerate fluctuations.

---

## Chart 2 — Regional Performance (Horizontal Bar Chart)

**Business Question:** Which region generates the most sales and profit? How do regions compare at a glance?

**Why This Chart Type:**
A horizontal bar chart is the standard for comparing a discrete categorical variable (Region = 4 categories) across a quantitative measure (Sales). Horizontal orientation is preferred over vertical bars when category labels are long enough to cause rotation on vertical charts. Bar length is the most accurate visual encoding for magnitude comparison — superior to pie charts or bubble charts for this purpose.

**Fields Used:**
- Y-axis: `region` (categorical)
- X-axis: `SUM(sales)`
- Color: Distinct color per region (not encoding additional data; for differentiation only)
- Labels: Sales value labeled at end of each bar

**Design Principle Applied:** Gestalt principle of similarity — consistent bar width and clear value labels allow rapid comparison. Sorted by ascending sales so the highest-performing region reads last (most prominent position in a horizontal layout, top of chart).

**Mistake Avoided:** Did not use a map for this comparison — while maps are visually appealing for geographic data, India's four regions (North/South/East/West) are too few and too unevenly shaped for a map to communicate magnitude accurately. A bar chart communicates the ranking and gap more precisely.

---

## Chart 3 — Category Sales vs Profit (Grouped Bar Chart)

**Business Question:** Which category drives the most sales? Does that match where profit comes from, or are there mismatches?

**Why This Chart Type:**
A grouped bar chart with two bars per category (Sales and Profit) is ideal for showing both the absolute magnitude and the relationship between two related measures across a small number of categories (3). The juxtaposition immediately reveals Furniture's disproportionately large sales-to-profit gap.

**Fields Used:**
- X-axis: `category`
- Y-axis: `SUM(sales)` and `SUM(profit)` (side by side)
- Color: Blue for Sales, Green for Profit
- Labels: Axis labels and legend

**Design Principle Applied:** Visual hierarchy — the grouped bars enable direct comparison both within each category (sales vs. profit) and across categories. Color consistency is maintained throughout the dashboard (blue = sales, green = profit).

**Mistake Avoided:** Did not use a stacked bar (which would make it impossible to read individual Profit bars accurately due to the scale difference between Technology and Furniture). Did not use a pie chart (which cannot represent two measures simultaneously).

---

## Chart 4 — Discount vs Profit (Scatter Plot)

**Business Question:** Is there a relationship between discount level and profit generated? Does higher discounting correlate with profit erosion?

**Why This Chart Type:**
A scatter plot is the only chart type that simultaneously shows the relationship (correlation) between two continuous quantitative variables (discount %, profit ₹). Each dot represents one order, making the spread and trend visible across the entire dataset. The color encoding by category adds a third dimension, allowing viewers to see whether the discount-profit relationship differs by category.

**Fields Used:**
- X-axis: `discount` (continuous, 0–0.35)
- Y-axis: `profit`
- Color: `category` (Furniture = Orange, Office Supplies = Blue, Technology = Green)
- Reference Line: Y=0 (break-even line in red dashed)

**Design Principle Applied:** Reference line at zero profit is a key annotation that separates profitable orders from loss-making ones. This transforms the scatter from a descriptive chart into a risk-identification tool.

**Mistake Avoided:** Did not use a line chart (which would imply a smooth function across all discount values). Did not aggregate data into bins (which would hide the full dispersion of profit outcomes at each discount level). Used alpha (transparency) on dots to handle overplotting without losing data.

---

## Chart 5 — Customer Segment Contribution (Pie Chart)

**Business Question:** What proportion of total sales does each customer segment contribute?

**Why This Chart Type:**
A pie chart is justified here specifically because there are only three segments (Consumer, Corporate, Home Office) and the business question is explicitly about proportional contribution (share of total), not absolute comparison. Three slices are within the recommended maximum of 5–6 for pie charts to remain readable. The near-equal split (32–34% each) is actually a notable business insight that a pie chart communicates clearly.

**Fields Used:**
- Slices: `customer_segment`
- Size: `SUM(sales)`
- Color: Distinct colors per segment
- Labels: Segment name + percentage

**Design Principle Applied:** Pie charts are used sparingly — only when part-to-whole comparison is the primary business question and the number of segments is small. This is one of two charts on the dashboard where a pie is genuinely appropriate.

**Mistake Avoided:** Did not use a pie chart for sub-category profitability (where 13 slices would be unreadable). Did not use a 3D pie chart (which distorts front vs. back slice sizes). All labels are external to avoid text overlap on small slices.

---

## Chart 6 — Shipping Performance (Horizontal Bar Chart)

**Business Question:** Which shipping mode is the fastest? How much slower is Standard Class compared to premium options?

**Why This Chart Type:**
A horizontal bar chart for 4 shipping modes (categories) against average delivery days (quantitative) is the clearest way to communicate ranking and magnitude of delivery performance differences. The color encoding uses a traffic-light system (green = fast, amber = normal, red = slow) to add instant interpretability without requiring the reader to study the axis scale.

**Fields Used:**
- Y-axis: `ship_mode`
- X-axis: `AVG(delivery_days)`
- Color: Traffic-light encoding (green/amber/red based on delay bucket)
- Labels: Average days labeled at bar end

**Design Principle Applied:** Traffic-light color coding (red-amber-green) exploits pre-attentive color perception — the viewer's eye immediately identifies red bars as problematic without reading any labels.

**Mistake Avoided:** Did not use a line chart (shipping modes are categorical, not sequential). Did not sort alphabetically — sorted by delivery days descending so the slowest mode is most prominent and visible at the top.

---

## Chart 7 — Return Rate by Category (Bar Chart)

**Business Question:** Which category has the highest return rate? Is the return problem concentrated in one area?

**Why This Chart Type:**
A simple vertical bar chart with 3 bars (one per category) and percentage labels is the clearest choice for this question. The bars directly compare the three discrete rates, and the value labels above each bar allow precise reading without axis extrapolation.

**Fields Used:**
- X-axis: `category`
- Y-axis: `SUM(return_flag) / COUNT(order_id)` × 100
- Color: Category-consistent colors (same scheme used throughout the dashboard)
- Labels: Percentage labeled above each bar

**Design Principle Applied:** Minimal clutter — no gridlines in the foreground, no legend needed (categories are already labeled on X-axis). Consistent color scheme with the Category Profitability chart reinforces cross-chart association.

**Mistake Avoided:** Did not use a pie chart (return rates are not parts of a whole — they are independent rates per category). Did not show absolute return counts without normalising to rate (categories have different order volumes, making raw counts misleading).

---

## Chart 8 — State-level Sales Heatmap / Highlight Table (Regional View)

**Business Question:** Within each region, which states are the strongest contributors?

**Why This Chart Type:**
A highlight table (heatmap with text labels) is Tableau's recommended chart for multi-dimensional comparative analysis where both the color gradient (magnitude) and exact value labels are needed simultaneously. It combines the colour encoding of a heatmap with the precision of a table — the best of both worlds for an executive audience that needs both pattern recognition and specific numbers.

**Fields Used:**
- Rows: `state` (top 15 by sales)
- Columns: `region`
- Color: `SUM(sales)` (yellow-to-red gradient)
- Labels: Sales value (₹M) in each cell

**Design Principle Applied:** Colour gradient from light (low sales) to dark (high sales) follows perceptual convention. Text labels on cells allow precise reading without tooltip hover, which is critical for screenshots and printed reports.

**Mistake Avoided:** Did not attempt to show all states in a geographic map (India has 28 states + UTs; a map with 28 choropleth regions at dashboard scale becomes unreadable). A ranked table of top 15 is more actionable than a complete geographic distribution.

---

## General Dashboard Design Principles Applied

| Principle | Implementation |
|---|---|
| Dark background theme | Reduces eye strain in executive presentation settings; high contrast for key metrics |
| Consistent color vocabulary | Blue = sales, Green = profit, Orange = secondary metric, Red = risk/negative |
| KPI cards at top | Most important summary metrics are visible without scrolling |
| Chart titles are questions, not descriptions | E.g., "Discount vs Profit" (what it answers) rather than "Scatter Plot of Discount and Profit" |
| Filters at bottom (not sidebar) | Maximises chart area; filters are secondary to the charts |
| Traffic-light encoding for shipping | Instant interpretability; green = good, amber = caution, red = problem |
| Alphabetical category labels | Consistent across charts; prevents cognitive load from different orderings |
| Minimal grid lines | Grid lines use low alpha to guide without competing with data |
| No 3D charts | 3D visualisations distort perspective and mislead magnitude perception |
| Value labels on bars | Allows precise reading without axis extrapolation |
