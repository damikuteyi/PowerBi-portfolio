# Evaluation Context in Report Visuals

A manager wants to see each region's contribution to total revenue.

## Dynamic measure
```dax
Region Revenue % =
DIVIDE(
    [Total Revenue],
    CALCULATE(
        [Total Revenue],
        REMOVEFILTERS(SalesData[Region])
    ),
    0
)
```

## Table visual results
| Region | Total Revenue | Revenue % |
|---|---:|---:|
| Germany | 2,000 | 42.55% |
| France | 2,700 | 57.45% |
| **Total** | **4,700** | **100.00%** |

Each Region row creates its own filter context.

## Card visual
With no Region filter, the numerator is 4,700 and the denominator is also 4,700. The card displays 100.00%.

## SELECTEDVALUE nuance
`SELECTEDVALUE(SalesData[Region])` returns a single region when exactly one distinct region is in the current filter context. When there is no single distinct value, it returns `BLANK()` by default.

The final percentage measure does not depend on `SELECTEDVALUE()`. On a card with no Region filter, `[Total Revenue]` evaluates to 4,700, so the measure returns 100.00%.

**Key takeaway:** A measure can respond dynamically to the filter context supplied by a visual without hardcoding each category.
