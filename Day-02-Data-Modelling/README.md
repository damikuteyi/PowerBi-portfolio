# Day 2 – Advanced Data Modelling in Power BI

This project documents a practical Power BI data-modelling exercise covering dimensional modelling, star schemas, relationship design, date dimensions, and role-playing dates.

## Learning objectives

- Distinguish fact tables from dimension tables.
- Define and document the grain of a fact table.
- Explain star schema versus snowflake schema.
- Configure one-to-many relationships with single-direction filtering.
- Use one date dimension for multiple date roles.
- Apply `USERELATIONSHIP()` to analyse a measure using an inactive relationship.

## Model overview

The model contains three tables:

- `Dim_Customer`: one row per customer.
- `Dim_Date`: one row per calendar date.
- `Fact_Sales`: one row per sales transaction.

The grain of `Fact_Sales` in this exercise is one row per sales transaction (`SalesID`).

### Relationships

| One-side | Many-side | Cardinality | Filter direction | Status |
|---|---|---|---|---|
| `Dim_Customer[CustomerID]` | `Fact_Sales[CustomerID]` | One-to-many | Single | Active |
| `Dim_Date[Date]` | `Fact_Sales[OrderDate]` | One-to-many | Single | Active |
| `Dim_Date[Date]` | `Fact_Sales[DeliveryDate]` | One-to-many | Single | Inactive |

`Dim_Date` is a role-playing dimension: it represents different business date roles (order date and delivery date). The active relationship supports the default order-date analysis. A measure can use the inactive delivery-date relationship with `USERELATIONSHIP()`.

## DAX measures

```dax
Total Revenue =
SUM(Fact_Sales[Revenue])
```

```dax
Total Customers =
DISTINCTCOUNT(Fact_Sales[CustomerID])
```

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

## Expected validation results

- Total Revenue: **3,000**
- Total Customers: **4**
- Revenue by Delivery Date (unfiltered total): **3,000**

### Revenue by order date

| Date | Revenue |
|---|---:|
| 1 January 2026 | 500 |
| 2 January 2026 | 1,000 |
| 3 January 2026 | 1,500 |

### Revenue by delivery date

| Date | Revenue |
|---|---:|
| 4 January 2026 | 500 |
| 5 January 2026 | 300 |
| 6 January 2026 | 700 |
| 7 January 2026 | 900 |
| 8 January 2026 | 600 |

The two line charts should show different date distributions while reconciling to the same overall revenue total.

## Files in this folder

- `fact-and-dimension-tables.md` – table roles and grain.
- `star-vs-snowflake.md` – dimensional schema design choices.
- `relationships.md` – cardinality, filter direction, and active/inactive relationships.
- `date-table.md` – date dimension setup and recommended enhancements.
- `dax-userelationship.md` – measures and role-playing date analysis.
- `images/day-02-date-analysis.png` – screenshot of the two validated line charts.

## Reproduce the exercise

1. Create the three tables using the sample data documented in the supporting files.
2. Set `OrderDate`, `DeliveryDate`, and `Dim_Date[Date]` to the Date data type.
3. Create the relationships exactly as shown above.
4. Add the measures.
5. Put `Dim_Date[Date]` on the X-axis and `Total Revenue` on the Y-axis.
6. Replace the measure with `Revenue by Delivery Date` and compare the date distribution.

## Notes and limitations

This is a small learning model designed to demonstrate modelling concepts. A production model would normally include a fuller date dimension, explicit measures, documented business definitions, data-quality checks, and a source-system refresh strategy.

The chart screenshot is evidence of the exercise output, not a substitute for the Power BI `.pbix` file. Add the `.pbix` file to the repository only if you intend to share the model and it does not contain sensitive data.
