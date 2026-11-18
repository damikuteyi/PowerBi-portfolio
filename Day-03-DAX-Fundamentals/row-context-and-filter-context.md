# Row Context and Filter Context

**Row context** means DAX is evaluating an expression for a particular row. It commonly appears in calculated columns and iterator functions such as `SUMX()`.

**Filter context** is the set of filters determining which rows are included in a calculation. It can be created by visuals, slicers, page/report filters, and relationships.

When `Region` is placed in a table visual, each row creates a region-specific filter context: Germany returns 2,000 and France returns 2,700.

**Key takeaway:** Row context identifies the current row during row-by-row evaluation. Filter context determines which data is included in a calculation.
