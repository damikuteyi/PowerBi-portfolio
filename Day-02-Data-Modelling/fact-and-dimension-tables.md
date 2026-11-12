# Fact Tables and Dimension Tables

## Purpose

Dimensional models separate measurable business events from the descriptive context used to analyse those events.

## Fact table: `Fact_Sales`

A fact table records business events or observations. It typically contains:

- Foreign keys that connect to dimensions.
- Numeric measures such as revenue, quantity, cost, or discount.
- A clearly defined grain.

For this exercise, `Fact_Sales` has one row per sales transaction, identified by `SalesID`.

| SalesID | CustomerID | OrderDate | DeliveryDate | Revenue |
|---:|---:|---|---|---:|
| 1 | 101 | 2026-01-01 | 2026-01-04 | 500 |
| 2 | 101 | 2026-01-02 | 2026-01-05 | 300 |
| 3 | 102 | 2026-01-02 | 2026-01-06 | 700 |
| 4 | 103 | 2026-01-03 | 2026-01-07 | 900 |
| 5 | 104 | 2026-01-03 | 2026-01-08 | 600 |

## Dimension table: `Dim_Customer`

A dimension table provides descriptive attributes for filtering, grouping, and slicing facts.

| CustomerID | CustomerName | Country |
|---:|---|---|
| 101 | John | Germany |
| 102 | Mary | Germany |
| 103 | David | Germany |
| 104 | Sarah | Germany |

`CustomerID` is unique in `Dim_Customer` and acts as its key. It appears repeatedly in `Fact_Sales` as a foreign key.

## Why grain matters

Grain is the meaning of one row in a fact table. It must be established before measures or relationships are designed.

If a sales order contains three product lines and the grain is one row per order line, that order appears in three rows. Summing order-level values repeated on every line could overstate results unless the model accounts for the grain.

## Practical rules

- Keep descriptive customer attributes in the customer dimension.
- Keep transactional measures and dimension keys in the fact table.
- Ensure dimension keys are unique on the one-side of relationships.
- Check that fact-table foreign keys have matching dimension records.
- Avoid mixing different grains in one fact table without a deliberate design.
