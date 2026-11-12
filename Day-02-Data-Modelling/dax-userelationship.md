# DAX: Analysing Revenue by Order Date and Delivery Date

## Measures

### Total Revenue

```dax
Total Revenue =
SUM(Fact_Sales[Revenue])
```

This measure sums revenue in the current filter context. With the active date relationship, a date selection filters sales by `OrderDate`.

### Total Customers

```dax
Total Customers =
DISTINCTCOUNT(Fact_Sales[CustomerID])
```

This counts distinct customers represented in the filtered sales rows. It is not necessarily the same as the total number of customers in the customer dimension.

### Revenue by Delivery Date

```dax
Revenue by Delivery Date =
CALCULATE(
    [Total Revenue],
    USERELATIONSHIP(
        Dim_Date[Date],
        Fact_Sales[DeliveryDate]
    )
)
```

`CALCULATE()` evaluates an expression in a modified filter context. `USERELATIONSHIP()` tells the calculation to use the existing inactive relationship between the date dimension and `DeliveryDate`.

## Expected results

Overall totals:

| Measure | Expected result |
|---|---:|
| Total Revenue | 3,000 |
| Total Customers | 4 |
| Revenue by Delivery Date | 3,000 |

By order date:

| Date | Revenue |
|---|---:|
| 2026-01-01 | 500 |
| 2026-01-02 | 1,000 |
| 2026-01-03 | 1,500 |

By delivery date:

| Date | Revenue |
|---|---:|
| 2026-01-04 | 500 |
| 2026-01-05 | 300 |
| 2026-01-06 | 700 |
| 2026-01-07 | 900 |
| 2026-01-08 | 600 |

## Interpretation

The total revenue is unchanged because the same five sales transactions are being summed. What changes is the date used to assign each transaction to a point on the timeline.

This is useful when business users ask questions such as:

- How much revenue was booked by order date?
- How much revenue was delivered by delivery date?
- Are delivery patterns different from order patterns?

## Important distinction

`USERELATIONSHIP()` does not create a new relationship. It uses an existing relationship in the calculation. The relationship must already exist in the model.
