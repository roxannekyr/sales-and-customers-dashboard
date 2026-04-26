# Sales & Customer Performance Dashboard
### Tableau | Business Intelligence | Year-over-Year Analytics

## 🟢 Live Interactive Dashboard

> **Click below to open the fully interactive dashboard** — explore both the Sales and Customer views, filter by year, hover over charts, and drill into customer-level data.

[![▶ Open Live Dashboard](https://img.shields.io/badge/▶%20Open%20Live%20Dashboard-E97627?style=for-the-badge&logo=tableau&logoColor=white)](https://YOUR_USERNAME.github.io/sales-dashboard-tableau/)

> _Hosted via GitHub Pages · Powered by Tableau Public_

---

## Project Overview

A dual-dashboard Tableau solution delivering **executive-level visibility** into sales performance and customer behavior. Built for data-driven decision-making, the dashboards enable business leaders to instantly benchmark current-year results against the prior year across four core KPIs — all driven by a single dynamic year parameter.

**Business problem solved:** Sales teams and executives lacked a unified, interactive view to compare current performance against historical benchmarks, identify top customers, and detect weekly revenue trends at a glance.

---

## Dashboard Structure

| Dashboard | Purpose |
|---|---|
| **Sales Dashboard** | KPI tracking (Sales, Profit, Qty), weekly trends, subcategory comparison |
| **Customer Dashboard** | Customer distribution, top customers, orders per customer, customer KPIs |

---

## Key Features & Technical Highlights

### Dynamic KPI Cards (4 Metrics)
- **Sales · Profit · Quantity · Customer Count** tracked for Current Year vs. Prior Year
- Automatic **% difference calculation** with directional indicators
- Color logic flags performance **above/below the weekly average** using `WINDOW_AVG()`

### Year-over-Year Engine
All comparisons are driven by a single **dynamic year parameter** — switch the selected year and every view recalculates instantly:

```
[CY Sales] = IF YEAR([Order Date]) = [Select Year] THEN [Sales] END
[PY Sales] = IF YEAR([Order Date]) = [Select Year] - 1 THEN [Sales] END
[% Diff Sales] = (SUM([CY Sales]) - SUM([PY Sales])) / SUM([PY Sales])
```

### Weekly Trend Analysis
Sparkline-style view surfaces the **highest and lowest performing weeks** using:
```
[Min/Max Sales] = IF SUM([CY Sales]) = WINDOW_MAX(SUM([CY Sales]))
                  OR SUM([CY Sales]) = WINDOW_MIN(SUM([CY Sales]))
                  THEN SUM([CY Sales]) END
```

###  Customer Intelligence
- **Customer Distribution** view by segment or region
- **Top Customers** ranked by revenue contribution
- **Sales per Customer** metric with CY vs PY delta
- **Orders per Customer** using FIXED LOD:
  ```
  [Nr of Orders per Customer] = { FIXED [Customer ID] : COUNTD([Order ID]) }
  ```

### Conditional Formatting Engine
Dynamic color coding built with `WINDOW_MAX()` / `WINDOW_AVG()` comparisons highlights winners, losers, and trend outliers — no manual formatting required.

## Technical Stack

| Component | Detail |
|---|---|
| **Tool** | Tableau Desktop + Tableau Public |
| **Data Source** | Sales DataSource (Orders, Customers, Products) |
| **Calc Techniques** | LOD Expressions · Table Calculations · Window Functions · Parameters |
| **LOD Types** | `FIXED` (customer-level aggregations) |
| **Table Calcs** | `WINDOW_AVG`, `WINDOW_MAX`, `INDEX` |
| **Interactivity** | Year parameter · Dashboard filter actions · Dynamic color logic |


## 🚀 Enabling GitHub Pages (one-time setup)

1. Push both files (`index.html` + `README.md`) to your repo's **main** branch
2. Go to **Settings → Pages**
3. Set source to **Deploy from a branch → main → / (root)**
4. After ~60 seconds, your live URL will be:
   `https://YOUR_USERNAME.github.io/sales-dashboard-tableau/`
5. Replace `YOUR_USERNAME` in this README with your actual GitHub username
