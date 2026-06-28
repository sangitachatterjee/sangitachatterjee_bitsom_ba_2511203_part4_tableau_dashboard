# Executive Sales Performance & Profitability Dashboard
**Author:** Sangita Chatterjee

This repository contains the dataset, Tableau packaged workbook, static visualization assets, and analytical reports for the Executive Sales Performance & Profitability Dashboard project. 

The dashboard provides the retail leadership team with interactive views to monitor sales performance, profitability margins, customer segments, product categories, shipping modes, returns behavior, and promotion/discount impacts.

---

## Repository Structure

```
part4_tableau_dashboard/
├── data/
│   ├── dashboard_sales_data.xlsx              # Raw Excel dataset
│   └── data_analysis_results.txt             # Summary statistics of key aggregates
├── tableau/
│   └── executive_dashboard.twbx              # Tableau packaged workbook
├── outputs/
│   ├── dashboard_story.md                    # Executive dashboard story for leadership
│   ├── business_insights.md                  # 8 detailed business insights with metrics
│   └── chart_selection_justification.md      # Chart selection and design justifications
├── screenshots/
│   ├── full_dashboard.png                    # Screen capture of the entire dashboard
│   ├── sales_trend_view.png                  # Monthly sales and profit trend chart
│   ├── regional_performance_view.png         # Sales/Profit comparative chart by Region
│   ├── category_profitability_view.png       # Sorted sub-category profit & margins chart
│   └── filter_interaction_view.png           # Scatter plot showing discount vs. profit
└── README.md                                 # Project documentation
```

---

## 1. Business Problem Summary
The retail leadership team requires an executive dashboard to serve as a single source of truth for tracking sales and profitability metrics. The business face-to-face challenges including:
- Identifying drivers of sales volumes and profit margins.
- Uncovering unprofitable product segments dragging down corporate performance.
- Quantifying the impact of marketing campaigns and target pricing discounts.
- Pinpointing operational risks, such as product return spikes and shipping delays.

This dashboard translates transaction logs into a cohesive business narrative that supports decision-making.

---

## 2. Dataset Description
The dataset contains **4,200 transaction records** spanning from **January 1, 2024, to December 31, 2025**. Each row represents a unique order (`order_id` is unique across all rows). The dataset contains 20 columns:
- **Order Details**: `order_id`, `order_date`, `ship_date`, `ship_mode`
- **Customer Profiles**: `customer_id`, `customer_segment` (Consumer, Corporate, Home Office), `campaign_channel` (Acquisition channel)
- **Geographic Details**: `region` (North, South, East, West), `state`, `city`
- **Product Information**: `category` (Furniture, Office Supplies, Technology), `sub_category`, `product_name`
- **Financial Metrics**: `sales` (revenue amount), `quantity`, `discount` (decimal), `profit` (net amount)
- **Operational Metrics**: `return_flag` (1 if returned, 0 otherwise), `delivery_days` (difference between ship and order date), `customer_rating` (1 to 5 stars)

---

## 3. Calculated Fields Created
To support advanced visualizations and business logic, five calculated fields were created in Tableau:

| Calculated Field | Formulation Logic / Code | Purpose |
| :--- | :--- | :--- |
| **Profit Margin** | `[Profit] / [Sales]` | Expresses net profit as a percentage of revenue. Formatted as custom percentage `0.0%`. |
| **Cost** | `[Sales] - [Profit]` | Calculates the total cost of goods sold plus delivery/operational expenses. |
| **Average Order Value (AOV)** | `SUM([Sales]) / COUNTD([Order ID])` | Tracks the average transaction size. Calculates unique order count using `COUNTD` to support standard practices. |
| **Return Rate** | `SUM([Return Flag]) / COUNTD([Order ID])` | Monitors the proportion of order transactions returned by customers. |
| **Shipping Delay Bucket** | `IF [delivery_days] <= 2 THEN "Fast (0-2 Days)" ELSEIF [delivery_days] <= 5 THEN "Standard (3-5 Days)" ELSE "Late (6+ Days)" END` | Categorizes delivery cycle times into operational performance buckets. |

---

## 4. Dashboard Components & Visualizations
The executive dashboard consists of five core views:
1. **Sales & Profit Trend (Dual-Axis Line Chart)**: Tracks monthly movements in sales and profit, identifying seasonal Q1 and Q3/Q4 peaks.
2. **Regional Performance (Grouped Bar Chart)**: Compares total sales and profits side-by-side across the North, South, East, and West regions.
3. **Category Profitability (Sorted Horizontal Bar Chart)**: Ranks all 13 sub-categories by overall net profit, color-coded by parent category.
4. **Discount vs. Profit Relationship (Scatter Plot)**: Shows the distribution of individual order profits against discount levels (0% to 35%) with a red overlay representing mean profit.
5. **Segment Performance (Pie Chart)**: Represents the parts-to-a-whole sales contribution of the Consumer, Corporate, and Home Office segments.

---

## 5. Filters and Interactions
To support leadership self-service, the dashboard incorporates the following interactive controls:
* **Global Filters Panel**: Allows scoping the entire dashboard by:
  * **Region**: Focus on specific regional territories.
  * **Category**: Filter all charts to view specific categories (e.g. Technology).
  * **Customer Segment**: Filter by Consumer, Corporate, or Home Office.
  * **Order Date (Year/Month)**: Dynamic slider to adjust the analysis window.
  * **Ship Mode**: Filter by Same Day, First Class, Second Class, and Standard Class.
* **Filter Action (Interactive Chart Linkage)**: Clicking on a specific region in the *Regional Performance view* or a category in the *Category Profitability view* acts as a filter, updating all other visualizations on the dashboard instantly.

---

## 6. Key Business Insights

* **Overall Baseline (2024-2025)**: Total sales achieved **$217,017,651.92** with net profits of **$33,306,312.84** (Margin **15.35%**). Total orders are **4,200** with an Average Order Value of **$51,670.87**.
* **Furniture Category Drag**: Furniture runs at a low **6.89% margin** ($3.56M profit on $51.64M sales). Bookcases (5.71% margin) and Tables (5.67% margin) represent primary profit-draining lines.
* **Technology Margin Engine**: Technology provides **84.2%** of all net profits ($28.04M), operating at a high **18.22% margin**.
* **The 35% Discount Profit Drain**: Sales at a 35% discount margin run at a net loss (representing a direct cash drain of **-$102,494.13** on $2.07M sales). Furthermore, the return rate spikes dynamically to **12.50%**.
* **Home Office Return Risk**: The Home Office segment holds a Return Rate of **5.67%**. When Home Office customers order Furniture, the return rate spikes to an alarming **9.14%**.
* **Goa Return Outlier**: Goa is the state with the highest return rate (**8.12%** across 197 orders).

*For a detailed break-out, see [outputs/business_insights.md](outputs/business_insights.md).*

---

## 7. Dashboard Story Summary
While the retail team displays flat, stable sales growth (+4.27% YoY) and steady profit growth (+2.19% YoY), profitability is hindered by structural inefficiencies. To optimize margins, the leadership team must transition from a top-line volume focus to targeted margin management:
- Cap discounts at **30%** to eliminate loss-making 35%-discounted transactions.
- Implement pre-delivery verification calls for Furniture orders (particularly Bookcases and Furnishings) going to Home Office buyers.
- Reallocate marketing capital from Referral channels with high return rates (5.61%) to Social (15.79% margin) and Email (15.54% margin) campaigns.

*For the full leadership report, see [outputs/dashboard_story.md](outputs/dashboard_story.md).*

---

## 8. Assumptions and Limitations
1. **Order-to-Row Mapping**: Assumes that each entry in `dashboard_sales_data.xlsx` represents one complete order (since `order_id` is unique across all 4,200 rows).
2. **Missing Customer Ratings**: Missing values in `customer_rating` (32 records) and `campaign_channel` (24 records) are left blank in calculations rather than imputed, as they impact non-critical dimensions.
3. **No Direct Logistics Costing**: Profit calculations are assumed to incorporate base COGS, but do not split out shipping charges or restocking fees, leaving a minor uncertainty in return logistics losses.

---

## 9. Screenshots Included
The following high-definition screenshots of the dashboard are included in the repository:
1. `screenshots/full_dashboard.png`: Screen capture of the entire Executive Dashboard.
2. `screenshots/sales_trend_view.png`: Trends in sales and profits showing seasonal patterns.
3. `screenshots/regional_performance_view.png`: Comparative analysis of regional sales & profits.
4. `screenshots/category_profitability_view.png`: Sub-category profitability horizontal bar chart.
5. `screenshots/filter_interaction_view.png`: Scatter plot tracking discount vs. profit correlation.
