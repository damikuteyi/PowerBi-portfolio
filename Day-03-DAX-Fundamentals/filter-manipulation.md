# DAX Filter Manipulation

## REMOVEFILTERS
Removes filters from specified tables or columns when used within `CALCULATE()` or `CALCULATETABLE()`.

```dax
All Region Revenue =
CALCULATE(
    [Total Revenue],
    REMOVEFILTERS(SalesData[Region])
)
```

This removes the Region filter while leaving other applicable filters in place.

## ALL
`ALL()` can be used as a table expression or as a filter modifier to remove filters from specified tables or columns.

## ALLEXCEPT
`ALLEXCEPT()` removes filters from a table except for the specified columns.

```dax
Revenue by Region =
CALCULATE(
    [Total Revenue],
    ALLEXCEPT(
        SalesData,
        SalesData[Region]
    )
)
```

## Percentage example
```dax
Germany Revenue =
CALCULATE(
    [Total Revenue],
    SalesData[Region] = "Germany"
)
```

```dax
All Region Revenue =
CALCULATE(
    [Total Revenue],
    REMOVEFILTERS(SalesData[Region])
)
```

```dax
Germany Revenue % =
DIVIDE(
    [Germany Revenue],
    [All Region Revenue],
    0
)
```

Expected result: 2,000 / 4,700 = 42.55%.

**Key takeaway:** Choose the filter modifier based on which filters must be retained and which must be removed.
