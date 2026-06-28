# Chart Selection & Justification Document

This document justifies the design choices and chart selections implemented in the Executive Sales Performance & Profitability Dashboard. The layout has been designed using visualization best practices to ensure it tells a clear business story and supports decision-making.

---

## 1. Sales and Profit Trend View (Line Chart)

* **Key Question Answered**: How are sales and profits changing over time, and do they exhibit seasonal patterns between 2024 and 2025?
* **Chart Type and Appropriateness**: A dual-axis line chart was selected. Line charts are the industry standard for showing continuous time-series trends. They are appropriate because they allow the user to easily track patterns, shifts, and seasonality over 24 calendar months.
* **Encoding Channels (Color, Size, Label, Filter)**:
  * **X-Axis**: Order Date (aggregated to Month/Year).
  * **Primary Y-Axis Line (Sales)**: Colored deep blue (`#2b5c8f`) with a subtle shaded area beneath to emphasize volume.
  * **Secondary Y-Axis Line (Profit)**: Colored coral-red (`#e05a47`) with a dashed stroke to distinguish it from sales.
  * **Labels**: Point data labels are removed to prevent clutter, with hover tooltips providing precise numbers.
* **Design Principle Applied**: **Dual-Axis Contrast & Gestalt Proximity**. By keeping the lines distinct in style (solid blue vs. dashed red) and color, the reader can track both metrics in one view. A clear visual legend groups the elements.
* **Mistakes Avoided**: Avoided using a bar chart for monthly sales over two years, which would create visual clutter. Also avoided mixing unrelated scales on the same axis; using two separate Y-axes ensures both lines are scaled properly.

---

## 2. Regional Sales & Profit Performance (Grouped Bar Chart)

* **Key Question Answered**: Which geographical regions drive the highest revenue volume, and how does their profit contribution compare?
* **Chart Type and Appropriateness**: A side-by-side grouped vertical bar chart. Bar charts are highly effective for comparing categorical values. The grouped approach allows the reader to compare Sales (volume) and Profit (value) side-by-side for each of the four business regions.
* **Encoding Channels (Color, Size, Label, Filter)**:
  * **X-Axis Categories**: Region (North, South, East, West).
  * **Bar Color (Sales)**: Slate blue (`#4682b4`).
  * **Bar Color (Profit)**: Forest green (`#2e8b57`).
  * **Labels**: Data labels on top of the bars show values in millions (e.g. `$64.7M`) to avoid axis reading strain.
* **Design Principle Applied**: **Direct Labeling & Color Association**. Using distinct, business-friendly colors (blue for revenue, green for profit) allows for quick interpretation. Direct labels remove the need for horizontal gridlines.
* **Mistakes Avoided**: Avoided using a map visualization for this specific comparison, as maps can distort values based on geographic size rather than business performance.

---

## 3. Product Sub-Category Profitability (Horizontal Bar Chart)

* **Key Question Answered**: Which products are our biggest profit contributors, and which sub-categories present a financial risk to the business?
* **Chart Type and Appropriateness**: A sorted horizontal bar chart. Horizontal bars are ideal when category names are long (e.g., "Office Supplies - Binders"), as they prevent text overlap. Sorting the bars in ascending order puts the lowest-profit categories at the bottom to draw quick attention.
* **Encoding Channels (Color, Size, Label, Filter)**:
  * **Y-Axis**: Sub-Category and Category.
  * **X-Axis**: Profit ($ Millions).
  * **Color Hue**: Encoded by Category (Technology: Blue, Furniture: Orange, Office Supplies: Green) to help the user identify category groupings.
  * **Labels**: Margins (e.g. `5.7% Margin`) are labeled next to each bar to provide context.
* **Design Principle Applied**: **Sorting for Visual Hierarchy & Color Categorization**. Sorting by profit exposes negative-margin areas (Tables, Bookcases) at a glance.
* **Mistakes Avoided**: Avoided using a pie chart to compare 13 sub-categories, which would create a confusing visual. Avoided sorting alphabetically, which makes it harder to identify top performers.

---

## 4. Discount Impact Analysis (Scatter Plot & Trendline)

* **Key Question Answered**: How does customer discounting affect individual order profitability, and where is the profitability threshold?
* **Chart Type and Appropriateness**: A joint scatter plot with a superimposed mean profit trendline. A scatter plot is the best chart type to show relationships between two numerical variables. The trendline helps identify the average profit drop as discounts increase.
* **Encoding Channels (Color, Size, Label, Filter)**:
  * **X-Axis**: Discount percentage (0% to 35%).
  * **Y-Axis**: Transaction Profit ($).
  * **Scatter Points**: Translucent grey (`#7f7f7f` with 0.3 alpha) to represent order transactions.
  * **Trendline**: Bold red (`#d62728`) representing mean profit per discount rate.
* **Design Principle Applied**: **Data Density & Overlaying Analytics**. Using transparency allows the user to see the distribution of orders at each discount level without visual overlap.
* **Mistakes Avoided**: Avoided using a line chart for all transactions, which would create a confusing chart. Also avoided hiding the outliers, as showing the negative transactions at 35% discount is a key insight.

---

## 5. Segment Contribution & Interactive Filters Panel (Pie Chart / Filters Panel)

* **Key Question Answered**: How are sales distributed across the customer segments, and how can the dashboard be filtered to see specific categories?
* **Chart Type and Appropriateness**: A simple 3-slice pie chart for customer segments, paired with a structured filter card. Pie charts are appropriate only when comparing a small number of parts-to-a-whole slices (in this case: Home Office, Corporate, and Consumer).
* **Encoding Channels (Color, Size, Label, Filter)**:
  * **Slices**: Customer Segment.
  * **Color**: Shades of blue (`#2b5c8f`, `#4682b4`, `#93c5fd`) to represent a cohesive segment category.
  * **Labels**: Segment names and percentages (e.g. `34.3% Home Office`).
  * **Filters Card**: Provides checkbox controls to filter the rest of the views (Region, Category, Segment, Date, Ship Mode).
* **Design Principle Applied**: **Visual Minimalism & Interactive Scoping**. The pie chart provides a clean part-to-whole view, while the filter panel provides context on active search parameters.
* **Mistakes Avoided**: Avoided using a pie chart with more than 3-4 slices, and avoided using bright colors that compete for the reader's attention.
