# Date Dimension and Role-Playing Dates

## Create a date table

The exercise creates a calendar covering 2026:

```dax
Dim_Date =
CALENDAR(
    DATE(2026, 1, 1),
    DATE(2026, 12, 31)
)
```

Add these calculated columns:

```dax
Year = YEAR(Dim_Date[Date])
```

```dax
MonthNumber = MONTH(Dim_Date[Date])
```

```dax
Month = FORMAT(Dim_Date[Date], "MMMM")
```

```dax
MonthYear = FORMAT(Dim_Date[Date], "MMM yyyy")
```

Sort `Month` by `MonthNumber` when using month names in visuals. For a multi-year model, create a numeric YearMonth sort column, for example:

```dax
YearMonthSort = YEAR(Dim_Date[Date]) * 100 + MONTH(Dim_Date[Date])
```

Then sort `MonthYear` by `YearMonthSort`.

## Mark as a date table

In Power BI Desktop, select `Dim_Date`, choose **Table tools > Mark as date table**, and select `Dim_Date[Date]`. The date column should contain unique, contiguous dates without blanks.

## Role-playing date dimension

A sales fact can have several date columns, such as:

- OrderDate
- DeliveryDate
- InvoiceDate
- ReturnDate

These are different business roles played by the calendar dimension.

This exercise uses one `Dim_Date` table with an active relationship to `OrderDate` and an inactive relationship to `DeliveryDate`. This keeps the model compact and demonstrates measure-specific date analysis.

An alternative in some models is to create separate role-playing date tables (for example, `Dim_Order_Date` and `Dim_Delivery_Date`) when users need to slice by both date roles independently in the same report context.
