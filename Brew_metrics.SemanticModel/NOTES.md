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