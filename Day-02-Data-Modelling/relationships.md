# Relationships in Power BI

## Relationship design

A relationship connects a key in a dimension to the corresponding foreign key in a fact table.

For this exercise:

| Dimension key | Fact foreign key | Cardinality | Direction |
|---|---|---|---|
| `Dim_Customer[CustomerID]` | `Fact_Sales[CustomerID]` | One-to-many | Single |
| `Dim_Date[Date]` | `Fact_Sales[OrderDate]` | One-to-many | Single, active |
| `Dim_Date[Date]` | `Fact_Sales[DeliveryDate]` | One-to-many | Single, inactive |

## Cardinality

One-to-many (`1:*`) means each dimension key occurs once on the one-side and can match multiple rows on the fact-side.

For example, customer 101 appears in two sales rows. It must appear only once in `Dim_Customer`.

## Cross-filter direction

Single-direction filtering from dimension to fact is a clear default for a star schema. A customer selection filters matching sales rows.

Bidirectional filtering can be useful in specific designs, but should not be enabled automatically. It can introduce ambiguous filter paths and make model behaviour harder to reason about.

## Active and inactive relationships

Power BI generally allows one active relationship between the same pair of tables at a time. The active order-date relationship is used by default.

The delivery-date relationship is inactive in this model. A measure can explicitly activate it for a calculation using `USERELATIONSHIP()`.

## Validation checklist

- Dimension keys are unique.
- Fact foreign keys use compatible data types.
- Unmatched keys are investigated.
- Cardinality is correct.
- Filter direction is intentional.
- Active and inactive relationships match the intended default analysis.
