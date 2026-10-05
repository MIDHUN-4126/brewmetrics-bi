# Copilot-Assisted DAX Development

This document records the initial suggestions provided by codex as my GitHub Copilot is not working,the changes made by the me, and the reasons for those changes.

## Month-over-month sales growth

```DAX
MoM Sales Growth % =
VAR PreviousMonthSales =
    CALCULATE (
        [Total Sales],
        DATEADD ( Dim_Date[Date], -1, MONTH )
    )
RETURN
    DIVIDE ( [Total Sales] - PreviousMonthSales, PreviousMonthSales )
```

The measure is formatted as a percentage. It returns blank when there is no
prior-month sales value or when that value is zero.

## Cumulative running total sales

```DAX
Running Total Sales =
CALCULATE (
    [Total Sales],
    FILTER (
        ALLSELECTED ( Dim_Date[Date] ),
        Dim_Date[Date] <= MAX ( Dim_Date[Date] )
    )
)
```

`ALLSELECTED` keeps report and slicer selections, while removing the current
date-row filter so each date includes sales from the start of the selected
period through that date.

## City sales rank

```DAX
City Sales Rank =
RANKX (
    ALLSELECTED ( Dim_City[city] ),
    CALCULATE (
        [Total Sales],
        REMOVEFILTERS ( Fact_Sales[city] )
    ),
    ,
    DESC,
    DENSE
)
```

### Purpose
Ranks cities according to their total sales.

### Codex assistance
Codex suggested RANKX over the city dimension and descending
sales order.

### Validation
I checked the result against a table visual and confirmed that the city
with the highest sales received rank 1.

## Measure 4 -Average sales per transaction

```DAX
Average Sales per Transaction =
DIVIDE (
    [Total Sales],
    DISTINCTCOUNT ( Fact_Sales[sale_id] )
)
```
### Purpose
Calculates the average sales amount per unique transaction.

### Codex assistance
Codex suggested dividing total sales by the number of transactions.
It used DISTINCTCOUNT on sale_id so that each transaction is counted
once rather than counting individual product quantities.

## Dashboard implementation

The Power BI Desktop dashboard has been completed on a single report page
titled **BREWMETRICS COFFEE SALES DASHBOARD**.

Implemented dashboard elements:

- KPI cards for Total Sales, Total Transactions, Total Quantity, and
  Average Sales per Transaction.
- A sales trend line chart using `Dim_Date[Date]` and Total Sales.
- A Cold Brew monthly sales trend line chart.
- A product sales column chart.
- A city and store-format sales column chart for drill-down analysis.
- A city table showing Total Sales and City Sales Rank.
- Date, city, and category slicers for interactive filtering.
- An action button for report navigation or interaction.

The visuals use the measures and star-schema dimension tables defined in
this semantic model.
