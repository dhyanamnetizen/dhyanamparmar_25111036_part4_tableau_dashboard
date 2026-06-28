# Dashboard Story — Retail Sales Executive Dashboard
### Written for Leadership Audience | Fiscal Years 2024–2025

---

## 1. Executive Summary

Across 4,200 orders and two full fiscal years (2024–2025), this retail business generated strong top-line sales — but the profitability picture beneath the surface tells a more complex story. Revenue is growing and Q4 seasonality demonstrates consistent customer demand. However, a specific combination of factors — aggressive discounting in low-margin categories, elevated returns in the Furniture segment, and delivery delays in the default shipping mode — is suppressing profit at a rate that should concern leadership.

The dashboard was built to answer one overriding question: **Where is the business creating value, and where is it destroying it?** The answer is clear: Technology and Office Supplies create value; Furniture, particularly when discounted and returned, destroys it. The West generates volume; the East generates margin. Corporate customers drive high-value orders; Home Office customers drive high return costs.

Leadership now has the visibility to act.

---

## 2. What Is Performing Well

**Technology is the profit engine.** Technology sub-categories — particularly Copiers and Phones — deliver strong sales and the highest profit margins in the business. These products are being purchased at list price or minimal discount, and return rates are low. The customer satisfaction signal (customer rating) is also strongest here.

**The East region operates with the highest efficiency.** Despite not leading in raw sales volume, the East achieves superior profit margins. Its product mix skews toward Office Supplies and Technology, and discount rates are demonstrably lower than the West. This is the model the rest of the business should study.

**Corporate segment customers are the highest-value accounts.** Corporate orders are fewer but significantly larger (highest Average Order Value), suggesting deliberate purchasing decisions rather than speculative orders. Their lower return rate reinforces this — Corporate customers know what they need before they order.

**Q4 demand is robust and predictable.** Both 2024 and 2025 show consistent November–December revenue peaks, validating the business's seasonal model and providing a clear planning window for inventory, staffing, and logistics preparation each year.

**Email and Paid campaign channels are generating higher-quality orders.** Orders attributed to Email and Paid channels show higher Average Order Values compared to Organic or Social, suggesting that targeted outreach is reaching higher-intent buyers.

---

## 3. What Is Underperforming

**Furniture is the business's most significant financial liability.** Tables and Bookcases are generating negative aggregate profit. This is not a one-time anomaly — it persists across both years and across all regions. When combined with the above-average return rate in this category, every Furniture sale carries a high probability of producing a net loss after accounting for reverse logistics and restocking costs.

**The South region is underperforming on both volume and margin.** While it is not generating losses, it is the least efficient region in the business with the thinnest margins and lowest sales contribution. Without intervention, the South risks becoming a persistent drag on overall profitability.

**Standard Class shipping is failing a subset of customers.** A material portion of Standard Class orders take 6 or more days to ship — longer than customers likely expect from a "standard" service. This is translating into lower customer ratings and represents a hidden risk to repeat purchase rates, particularly in the Consumer segment where price sensitivity makes alternatives easy to find.

**Home Office is the most return-prone segment.** The combination of Home Office customers purchasing Furniture is the highest-risk pairing in the dataset. These customers appear to be purchasing speculatively — buying before they are certain — and the product experience is not meeting expectations.

---

## 4. What Risks Are Visible

**Discount-driven losses are a structural risk, not a temporary condition.** The scatter plot shows an unmistakable pattern: discounts above 20% produce negative profit margins across all categories. The business appears to be using discounting as a default tool to drive volume, particularly in Furniture. Without a discount policy with hard approval thresholds, this pattern will continue to scale as the business grows.

**Compounding losses in Furniture × Home Office represent an existential margin risk at scale.** If the Home Office segment continues to grow (a reasonable assumption in a hybrid-work environment), and Furniture remains the go-to purchase for that segment, the losses in this quadrant will grow proportionally. The current trajectory is financially unsustainable in this specific product-segment combination.

**Campaign channel data has gaps.** Approximately 0.57% of orders have no campaign channel attribution. While small, this gap will widen if tracking is not improved — and it means some marketing spend is invisible in ROI analysis. Leadership is making channel investment decisions with incomplete data.

**Delivery delays may be accelerating customer churn silently.** Customers who experience 6+ day Standard Class delays do not necessarily complain — they simply do not return. This "silent churn" is difficult to detect in sales data alone but is visible in the correlation between high delivery days and lower customer ratings.

---

## 5. What Opportunities Are Visible

**Repricing Furniture to cost-neutral levels would immediately improve overall margins.** The Furniture category does not need to be a high-margin category — it simply needs to stop being a loss leader. A modest price increase of 8–12% on Tables and Bookcases, combined with tighter discount controls, would likely move this category to breakeven or slight profitability without significantly reducing demand (as these are relatively inelastic product categories).

**Expanding Corporate segment share in Technology would be highly accretive.** The highest AOV segment (Corporate) combined with the highest margin category (Technology) is the most profitable quadrant in the business. Targeted sales outreach to Corporate accounts — particularly for Copiers and high-end Phones — represents the clearest near-term revenue quality opportunity.

**Upgrading high-value orders to faster shipping modes could improve LTV at low cost.** For orders above $500, automatically upgrading from Standard Class to Second Class (or First Class where feasible) would reduce the 6+ day delay risk for the most revenue-significant orders. The incremental shipping cost is likely offset by improved customer ratings and repeat purchase rates.

**East region playbook could be replicated in the South.** The East's efficiency metrics — product mix, discount discipline, lower return rate — are not geographic accidents. They reflect operational and sales behaviors that can be documented and trained. Applying the East's approach to the South's market could meaningfully improve the South's margin contribution within 2–3 quarters.

**Investing in pre-purchase guidance for Furniture could reduce returns.** Many Furniture returns are likely the result of dimension mismatches, color expectation gaps, or assembly complexity surprises. Simple pre-sale interventions — 3D room planners, detailed specification sheets, assembly requirement disclosures — could reduce return rates in this category without requiring product changes.

---

## 6. Recommended Business Actions

| Priority | Action | Owner | Timeline |
|---|---|---|---|
| **Critical** | Implement discount approval thresholds: 15%+ requires manager sign-off, 25%+ requires VP approval | Sales Leadership | 30 days |
| **Critical** | Conduct Furniture × Home Office P&L review; establish minimum margin floor or exit lowest-margin SKUs | Merchandising + Finance | 60 days |
| **High** | Audit Standard Class orders >5 days; identify root cause by region and warehouse | Operations / Logistics | 45 days |
| **High** | Launch Corporate + Technology targeted sales program in West and South regions | Sales | 90 days |
| **Medium** | Fix campaign channel tracking gaps; achieve 100% attribution coverage | Marketing / Analytics | 60 days |
| **Medium** | Develop East region operational playbook; pilot in South region | Regional Management | 90 days |
| **Low** | Add Furniture pre-purchase guidance tools to product pages | Product / E-commerce | 120 days |

---

## 7. Limitations of the Dashboard

- **No customer-level view.** The dashboard is order-level. Repeat purchase rates, customer lifetime value, and churn rates cannot be computed from this dataset without a customer dimension table.
- **Cost is derived, not measured.** The "Cost" field is calculated as Sales minus Profit. Actual cost components (COGS, shipping cost, overhead allocation) are not available — so cost-reduction opportunities cannot be precisely identified.
- **Return reasons are unknown.** The `return_flag` field records whether an order was returned, but not why. Root-cause analysis of returns requires a separate return reason dataset.
- **Two years is a limited trend window.** YoY comparisons are meaningful, but multi-year trend confidence (e.g., "is Q4 growth accelerating?") requires at least 3–4 years of data.
- **Campaign channel has missing values.** 24 orders (~0.57%) have no channel attribution. Channel ROI analysis slightly underrepresents one or more channels.
- **Geographic analysis is region/state level.** City-level patterns exist in the data but produce sparse results for less-populated states and are excluded from the main dashboard to avoid misleading conclusions from small sample sizes.

---

## 8. Suggested Next Analysis

1. **Customer cohort analysis** — Build a customer-level view linking `customer_id` across orders to measure repeat purchase rates, lifetime value, and churn by segment. This would validate or challenge the assumption that high-discount Furniture orders are justified by downstream LTV.

2. **Return reason analysis** — Append a return reason dimension (if available from CRM or customer service data) to determine whether Furniture returns are driven by product quality, expectation gaps, or delivery damage. This directly informs whether the solution is a product fix, a listing fix, or a packaging fix.

3. **Shipping cost analysis** — Integrate actual shipping cost data to compute true net margin by shipping mode. The current dashboard shows delivery speed but not shipping cost — combining both would allow a full cost-benefit analysis of upgrading Standard Class orders.

4. **Campaign ROI analysis** — Link campaign channel data to profit margin and repeat purchase rate (not just AOV) to determine which channels are acquiring high-quality customers vs. one-time buyers. This would enable a defensible budget reallocation recommendation.

5. **Predictive return risk model** — Using the existing features (category, segment, discount rate, shipping mode, region), build a simple logistic regression or decision tree to predict return probability at the order level. High-risk orders could trigger proactive customer outreach before the return occurs.

---

*This dashboard was designed to connect the business's data to its decisions. The charts do not exist to report what happened — they exist to focus leadership attention on the specific actions that will improve the trajectory of the business.*
