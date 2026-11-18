# Day 03 – DAX Fundamentals

## Objective
Understand how DAX evaluates calculations and build measures that respond to report filter context.

## Topics
- Row context and filter context
- `CALCULATE()` and context transition
- `SUM()` versus `SUMX()`
- `VALUES()` and iterators
- `REMOVEFILTERS()`, `ALL()`, and `ALLEXCEPT()`
- `VAR` and `RETURN`
- Dynamic measures in table and card visuals

## Practice data: SalesData

| Region | Revenue |
|---|---:|
| Germany | 1,700 |
| France | 2,200 |
| Germany | 300 |
| France | 500 |
| **Total** | **4,700** |

Base measure:
```dax
Total Revenue =
SUM(SalesData[Revenue])
```

## Final dynamic measure
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

## Validation
| Region | Total Revenue | Revenue % |
|---|---:|---:|
| Germany | 2,000 | 42.55% |
| France | 2,700 | 57.45% |
| **Total** | **4,700** | **100.00%** |

Validated in a Table visual and a Card visual. With no Region filter, the card displays 100.00%.

## Learning outcome
Measures inherit the filter context established by report visuals. Removing the Region filter from the denominator allows one measure to calculate each region's share of total revenue.

## Files
- `row-context-and-filter-context.md`
- `calculate-and-context-transition.md`
- `sum-vs-sumx-and-values.md`
- `filter-manipulation.md`
- `dax-variables.md`
- `evaluation-context-in-visuals.md`

## Evidence
Add your Power BI screenshots to `images/`:
1. Table visual showing Germany, France, and total.
2. Card visual showing 100.00%.
