# Star Schema vs. Snowflake Schema

## Star schema

A star schema places a central fact table around denormalised dimensions. Dimension tables connect directly to the fact table.

**Advantages**

- Simple model navigation.
- Fewer relationships.
- More intuitive report authoring.
- Often simpler DAX and filter propagation.
- A strong default for many Power BI semantic models.

## Snowflake schema

A snowflake schema normalises dimensions into related sub-dimensions. For example, `Dim_Product` could connect to a separate `Dim_Category` table rather than storing category attributes directly.

**Potential advantages**

- Less repeated descriptive data in some designs.
- Can reflect governed enterprise structures or shared hierarchies.

**Trade-offs**

- More tables and relationships.
- More complex filter paths.
- A less straightforward experience for report authors.

## Design decision in this exercise

The exercise uses a simple star-schema approach: `Dim_Customer` and `Dim_Date` connect directly to `Fact_Sales`.

A separate category dimension was not required by the sample data. The guiding principle is to use a star schema as a practical default, then normalise dimensions only when there is a clear modelling or governance reason.
