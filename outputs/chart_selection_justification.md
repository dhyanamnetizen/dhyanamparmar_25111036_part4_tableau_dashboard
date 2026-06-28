# Chart Selection Justification — Retail Sales Executive Dashboard

> For each major chart in the dashboard, this document explains: (1) the business question answered, (2) why the chart type is appropriate, (3) what field is used for color/size/label/filter, (4) the design principle applied, and (5) the mistake avoided.

---

## Chart 1 — Sales Trend View (Line Chart)

**1. Business Question Answered:**
How are sales changing over time? Is there seasonality? Is the business growing year-over-year?

**2. Why This Chart Type Is Appropriate:**
A line chart is the standard choice for continuous time-series data. It makes trends, seasonality, and inflection points immediately visible. The human eye is wired to interpret slope as change — a rising line is unmistakably "growth" without needing annotation.

**3. Fields Used:**
- X-axis: `Order Date` (aggregated to Month)
- Y-axis: `SUM(Sales)`
- Color: `YEAR(Order Date)` — two distinct lines for 2024 and 2025 allow direct year-over-year comparison
- Filter: Date range filter (global dashboard filter)

**4. Design Principle Applied:**
*Preattentive processing* — color encodes year, making the YoY comparison effortless. Grid lines are minimal (every other month labeled) to reduce clutter. The chart starts at zero on the Y-axis to avoid misleading the magnitude of change.

**5. Mistake Avoided:**
Avoided using a bar chart for this time series. While bars work for discrete time comparisons (e.g., quarterly totals), they obscure the continuous trend line that reveals seasonality patterns. Also avoided dual-axis confusion by keeping the view to a single measure (Sales), with Profit available as a second tab rather than overlaid.

---

## Chart 2 — Regional Performance View (Filled Map + Bar Chart)

**1. Business Question Answered:**
Which regions and states are performing best on sales and profitability? Where are the geographic concentrations of risk or opportunity?

**2. Why This Chart Type Is Appropriate:**
A filled (choropleth) map leverages the audience's existing geographic intuition. Leadership can instantly see "the South is lighter (lower margin)" without reading labels. The companion bar chart provides precise ranked values that the map's continuous color scale cannot communicate with precision.

**3. Fields Used:**
- Map: `State` (geographic role), color encodes `Profit Margin` (calculated field)
- Bar chart: `Region` on rows, `SUM(Sales)` and `SUM(Profit)` as dual bars
- Color: Diverging color palette (red = negative margin, green/blue = positive margin)
- Filter: Region filter (global)

**4. Design Principle Applied:**
*Redundant encoding* — both the map color and the bar height communicate performance, so the viewer can use either channel. Diverging color palette makes the loss/profit boundary immediately visible without requiring the viewer to read exact values.

**5. Mistake Avoided:**
Avoided using a pie chart for regional share — pies require precise angle reading and cannot show profit vs. sales simultaneously. Also avoided a purely table-based view, which would force the audience to scan rows rather than perceive geographic patterns spatially.

---

## Chart 3 — Category Profitability View (Horizontal Bar Chart)

**1. Business Question Answered:**
Which product categories and sub-categories drive profit or losses? Which sub-categories should leadership prioritize or investigate?

**2. Why This Chart Type Is Appropriate:**
Horizontal bar charts are ideal for ranked categorical comparisons. They allow long sub-category names to be read left-to-right (unlike vertical bars where labels require rotation). Sorting by profit immediately shows the best and worst performers at the top and bottom.

**3. Fields Used:**
- Y-axis: `Sub-Category` (sorted descending by profit)
- X-axis: `SUM(Profit)`
- Color: `Profit Flag` calculated field — red for loss, blue/teal for profit
- Size/Label: Profit value labeled at end of each bar
- Filter: Category filter (global), enables drill-down from category to sub-category

**4. Design Principle Applied:**
*Gestalt principle of similarity* — color grouping (red = problem, blue = healthy) allows leadership to instantly scan for risk without reading every label. Sorting by profit rather than alphabetically respects the executive audience's need to quickly identify the bottom performers.

**5. Mistake Avoided:**
Avoided a treemap for this view. Treemaps encode value in area, which the human eye judges poorly for comparison. A ranked bar chart communicates rank order and magnitude simultaneously with much greater precision. Also avoided 3D bars, which distort the perceived height/value relationship.

---

## Chart 4 — Discount vs. Profit Scatter Plot

**1. Business Question Answered:**
How does discount rate relate to profit margin? Is there a discount threshold beyond which profitability breaks down?

**2. Why This Chart Type Is Appropriate:**
A scatter plot is the correct tool for showing the relationship (correlation) between two continuous numerical variables. It reveals the direction, strength, and shape of the discount-profit relationship — something a bar chart or table cannot show. Each point represents a sub-category, making the pattern actionable at the product level.

**3. Fields Used:**
- X-axis: `AVG(Discount)` — average discount rate per sub-category
- Y-axis: `SUM(Profit) / SUM(Sales)` — profit margin (Profit Margin calculated field)
- Color: `Category` — three colors for Furniture, Office Supplies, Technology
- Size: `SUM(Sales)` — larger circles = higher revenue sub-categories
- Reference Line: Horizontal line at Y = 0 (breakeven) to make the loss zone explicit
- Filter: Category filter (global)

**4. Design Principle Applied:**
*Reference lines as visual anchors* — the zero-profit reference line divides the chart into "healthy" and "loss" zones, allowing leadership to immediately see which sub-categories have crossed into loss territory. Size encoding adds a third dimension (revenue weight) without adding a third axis.

**5. Mistake Avoided:**
Avoided using a line chart to show this relationship. A line chart implies sequence/order on the X-axis, which would suggest that discount rates are applied in a deliberate sequence rather than varying independently. The scatter correctly communicates these as independent variables measured simultaneously.

---

## Chart 5 — Shipping Performance View (Bar Chart by Delay Bucket)

**1. Business Question Answered:**
Which shipping modes cause the most delays? What proportion of orders fall into unacceptable delivery time buckets?

**2. Why This Chart Type Is Appropriate:**
A stacked or grouped bar chart is appropriate here because it shows both the absolute count (how many orders) and the composition (what share falls into each delay bucket) by shipping mode. The `Shipping Delay Bucket` calculated field transforms a continuous variable (delivery days) into meaningful categorical buckets that leadership can act on.

**3. Fields Used:**
- X-axis: `Ship Mode`
- Y-axis: `COUNT(Order ID)` (number of orders)
- Color: `Shipping Delay Bucket` calculated field (4 buckets: Same Day/Next Day, 2–3 Days, 4–5 Days, 6+ Days Delayed)
- Color palette: Sequential — light = fast, dark red = delayed
- Filter: Ship Mode filter (global), Region filter (global)

**4. Design Principle Applied:**
*Meaningful data transformation* — raw delivery days (0–9) are hard for leadership to interpret. Bucketing into four operationally meaningful categories (Same Day/Next Day, 2–3 Days, 4–5 Days, 6+ Days) aligns the visualization with how the business actually defines service levels. Color progression from green to red makes the "6+ Days" bucket immediately visible as the risk zone.

**5. Mistake Avoided:**
Avoided using a raw histogram of delivery days (0–9). While statistically valid, a histogram does not communicate operational meaning — "4 days" means nothing to a logistics manager without context. The bucketed bar chart directly maps to the question "are we meeting our delivery promises?" Also avoided a pie chart, which cannot show comparison across shipping modes.

---

## Chart 6 — Customer Segment View (Bar + KPI Summary)

**1. Business Question Answered:**
How do the three customer segments (Consumer, Corporate, Home Office) compare on revenue, profitability, average order value, and return behavior?

**2. Why This Chart Type Is Appropriate:**
A grouped bar chart or side-by-side bar chart with KPI callouts is appropriate because it enables direct segment comparison across multiple measures. Summary KPI cards above the chart provide quick-read totals for each segment.

**3. Fields Used:**
- X-axis: `Customer Segment`
- Y-axis (bars): `SUM(Sales)`, `SUM(Profit)`, `AVG(Average Order Value)` — displayed in separate panels
- Color: `Customer Segment` (consistent color encoding across the dashboard)
- Label: Profit Margin % labeled on profit bars
- Filter: Segment filter (global), Category filter (global)

**4. Design Principle Applied:**
*Consistent color encoding* — the same segment colors used here are maintained throughout the dashboard (Consumer = blue, Corporate = orange, Home Office = green). This allows leadership to track segment performance across multiple charts without re-reading legends.

**5. Mistake Avoided:**
Avoided combining all three measures into a single dual-axis chart. Dual-axis charts with multiple measure types (revenue, %, count) are confusing because the scales are incompatible. Separate panels for each measure are cleaner and more readable for an executive audience.

---

## Chart 7 — Return Analysis View (Highlight Table / Heatmap)

**1. Business Question Answered:**
Where are returns concentrated? Which combinations of category and customer segment have the highest return rates?

**2. Why This Chart Type Is Appropriate:**
A highlight table (text table with color encoding) is appropriate for showing the intersection of two categorical dimensions (Category × Segment) at a glance. Color intensity encodes return rate, making high-risk combinations instantly visible without requiring the viewer to read every number.

**3. Fields Used:**
- Rows: `Category`
- Columns: `Customer Segment`
- Color: `Return Rate` calculated field (SUM of return_flag / COUNT of orders) — sequential color from light (low return rate) to dark red (high return rate)
- Label: Return rate % displayed in each cell
- Filter: Region filter (global), Date filter (global)

**4. Design Principle Applied:**
*Small multiples / matrix view* — the highlight table is essentially a 3×3 matrix that communicates 9 data points simultaneously in a compact space. For an executive audience that needs to scan quickly, this is more efficient than 9 separate charts or a table they have to read row by row.

**5. Mistake Avoided:**
Avoided using a pie chart to show return distribution — a pie cannot show the two-dimensional breakdown (Category × Segment) that reveals where the intersection of risk occurs. Also avoided sorting alphabetically, opting instead to sort by return rate so the highest-risk combinations appear first.

---

*Chart selection reflects the principle that every visualization must answer a specific business question. Charts chosen for aesthetic reasons or to demonstrate variety — rather than to communicate insight — were explicitly excluded from this dashboard.*
