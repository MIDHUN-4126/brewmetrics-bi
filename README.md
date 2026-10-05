# BrewMetrics BI

Brew metrics report with Dashboard

## Project Overview

BrewMetrics Coffee Co. operates Flagship stores, Kiosks,
and Drive-Thrus across four cities. This project develops
a Power BI business intelligence solution for analyzing
sales performance, product trends, city performance,
and seasonal patterns.

## Dataset

The project uses the provided brewmetrics_sales.csv file.

The dataset contains transaction-level sales information
including date, city, store format, category, item,
quantity, unit price, and sales amount.

## Data Model

The Power BI semantic model follows a star-schema design.

### Fact Table

Fact_Sales contains transaction-level sales information.

### Dimension Tables

- Dim_Date
- Dim_City
- Dim_Product
- Dim_StoreFormat

The dimension tables provide descriptive attributes used
to analyze the sales fact table.

## DAX Measures

The project contains:

- Total Sales
- Previous Month Sales
- MoM Growth %
- Running Total Sales
- City Sales Rank
- Average Order Value
- Total Transactions
- Total Quantity
- Cold Brew Sales

## Dashboard

The dashboard contains:

- KPI cards
- Monthly sales trend
- Sales by city
- Cold Brew sales trend
- Product sales ranking
- City-to-store-format drill-down
- Interactive slicers

## Key Insights

1. Bengaluru records the highest total sales among the
   four cities in the supplied dataset.

2. Cold Brew is the highest-sales individual product
   in the supplied dataset.

3. Sales vary across the available months, with the
   dashboard making the monthly and Cold Brew patterns
   visible for management analysis.

## Version Control

Git and GitHub were used to maintain an incremental
development history. The project was developed through
separate commits for the data model, DAX measures,
dashboard, and documentation.

## AI-Assisted Development

Codex was used to assist with DAX development.
The NOTES.md file documents the suggestions received
and the validation/corrections made.
