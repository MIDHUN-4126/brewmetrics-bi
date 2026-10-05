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
