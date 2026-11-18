# SUM, SUMX, and VALUES

## SUM
`SUM()` adds the values in one numeric column.

```dax
Total Revenue =
SUM(SalesData[Revenue])
```

## SUMX
`SUMX()` is an iterator. It evaluates an expression for each row of a table and adds the results.

```dax
Total Sales Revenue =
SUMX(
    SalesData,
    SalesData[Quantity] * SalesData[Unit Price]
)
```

Use it when the calculation must be performed row by row before aggregation.

## VALUES
`VALUES(SalesData[Region])` returns the distinct Region values in the current filter context.

```dax
Total Revenue by Region =
SUMX(
    VALUES(SalesData[Region]),
    CALCULATE([Total Revenue])
)
```

Because `[Total Revenue]` is a measure, it automatically receives context transition when evaluated inside the row context.

**Key takeaway:** `SUM()` aggregates a column; `SUMX()` iterates over a table and aggregates an expression; `VALUES()` can provide distinct values to iterate over.
