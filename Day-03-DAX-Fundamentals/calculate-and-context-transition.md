# CALCULATE and Context Transition

`CALCULATE()` evaluates an expression in a modified filter context.

```dax
France Revenue =
CALCULATE(
    [Total Revenue],
    SalesData[Region] = "France"
)
```

This evaluates Total Revenue with the Region filter set to France.

## Context transition
Context transition occurs when `CALCULATE()` converts an existing row context into filter context.

Example calculated column:

```dax
Revenue Calculation =
CALCULATE(
    SUM(SalesData[Revenue])
)
```

In a calculated column, `CALCULATE()` transitions the current row context into filter context, so the expression is evaluated for the current row's values.

When a measure is evaluated inside a row context, DAX automatically performs context transition. An explicit `CALCULATE()` around a measure can therefore be redundant, although it can make the operation clearer when learning.

**Key takeaway:** Use `CALCULATE()` to change filter context, and understand context transition when combining row context with filter context.
