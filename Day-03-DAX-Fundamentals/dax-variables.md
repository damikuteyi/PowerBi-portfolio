# DAX Variables: VAR and RETURN

`VAR` defines a variable that stores the result of an expression for use later. `RETURN` defines the final expression that the measure evaluates.

```dax
France Revenue % =
VAR FranceRevenue =
    CALCULATE(
        [Total Revenue],
        SalesData[Region] = "France"
    )
VAR AllRevenue =
    CALCULATE(
        [Total Revenue],
        REMOVEFILTERS(SalesData[Region])
    )
RETURN
    DIVIDE(
        FranceRevenue,
        AllRevenue,
        0
    )
```

Expected result: 2,700 / 4,700 = 57.45%.

## Why use variables?
- Make complex measures easier to read.
- Avoid repeating expressions.
- Name intermediate calculations.
- Make measures easier to debug and maintain.

**Important:** A variable stores the result evaluated in the context where it is defined. Referencing it later does not cause its expression to be recalculated in a new context.
