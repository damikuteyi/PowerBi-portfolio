# Power BI Mastery & Analytics Portfolio

![Power BI](https://img.shields.io/badge/Power%20BI-Analytics-F2C811?logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Data%20Modelling-blue)
![Status](https://img.shields.io/badge/Portfolio-In%20Progress-orange)
![Learning](https://img.shields.io/badge/10--Day%20Programme-Active-success)

## About This Project

Welcome to my Power BI learning and professional portfolio.

This repository documents my journey towards advanced Power BI development, enterprise business intelligence, and data analytics.

The objective is to build practical expertise in designing, developing, optimising, and deploying Power BI solutions that support business intelligence and strategic decision-making.

Rather than focusing exclusively on theoretical concepts, this portfolio emphasises practical implementation, real-world business scenarios, technical documentation, and reproducible projects.

## Learning Objectives

By the end of this programme, I aim to demonstrate the ability to:

- Design scalable and efficient Power BI data models.
- Transform and prepare data using Power Query and M.
- Develop advanced DAX measures and calculations.
- Build interactive and insightful business intelligence dashboards.
- Optimise semantic models and report performance.
- Implement enterprise security and governance.
- Integrate Power BI with Microsoft Fabric, APIs, Python, and AI tools.
- Apply AI-assisted workflows to improve analytics development.
- Translate business requirements into actionable insights.

## Learning Roadmap

The programme is structured as a 10-day intensive learning journey.

| Day | Topic | Status |
|---|---|---|
| 01 | Power BI Architecture and Foundations | Completed |
| 02 | Advanced Data Modelling | Completed |
| 03 | DAX Fundamentals | Upcoming |
| 04 | Advanced DAX and Time Intelligence | Upcoming |
| 05 | Advanced Visualisation and Analytics | Upcoming |
| 06 | AI Integration: Claude, Copilot and MCP | Upcoming |
| 07 | Power BI Performance Optimisation | Upcoming |
| 08 | Enterprise Governance, Security and Deployment | Upcoming |
| 09 | Microsoft Fabric, APIs and Automation | Upcoming |
| 10 | Capstone Project | Upcoming |

---

## Completed Learning Modules

### Day 01 – Power BI Architecture and Foundations

**Focus:** Understanding the Power BI ecosystem and the fundamentals of data preparation and reporting.

Topics covered:

- Power BI architecture and ecosystem.
- Power Query and its role in ETL/ELT.
- Introduction to the M language.
- Semantic models and their responsibilities.
- Import, DirectQuery, Direct Lake and Live Connection.
- Composite models.
- Query folding.
- Incremental refresh.
- Measures versus calculated columns.
- Data cleaning and transformation.

Practical work:

- Created and transformed sample datasets.
- Identified and removed duplicate records.
- Applied filters and renamed columns.
- Changed data types.
- Explored M expressions in Power Query.
- Built an interactive Power BI report.

**Key learning:** Power Query prepares data, the semantic model defines relationships and business logic, and reports communicate insights through visualisations.

### Day 02 – Advanced Data Modelling

**Focus:** Building a structured Power BI semantic model using dimensional modelling principles.

Topics covered:

- Fact tables and dimension tables.
- Fact table grain.
- Primary keys and foreign keys.
- Star schema versus snowflake schema.
- Relationship cardinality.
- Single-direction and bidirectional filtering.
- Active and inactive relationships.
- Date dimensions.
- Role-playing dimensions.
- DAX `USERELATIONSHIP()`.

Practical project:

Developed a Power BI model containing:

- `Dim_Customer`
- `Dim_Date`
- `Fact_Sales`

Established three relationships:

| Relationship | Cardinality | Status |
|---|---|---|
| Customer to Sales | One-to-many | Active |
| Date to OrderDate | One-to-many | Active |
| Date to DeliveryDate | One-to-many | Inactive |

Developed the following DAX measures:

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

Validation results:

| Measure | Result |
|---|---:|
| Total Revenue | 3,000 |
| Total Customers | 4 |
| Revenue by Delivery Date | 3,000 |

**Key learning:** A single date dimension can support different business date analyses through active and inactive relationships. `USERELATIONSHIP()` enables a measure to use an existing inactive relationship.

**Project documentation:** [View Day 2 – Advanced Data Modelling](./Day-02-Data-Modelling/README.md)

---

## Upcoming Modules

### Day 03 – DAX Fundamentals
- DAX syntax and functions.
- Calculated columns and measures.
- Row context.
- Filter context.
- Context transition.
- `CALCULATE()`.
- Basic aggregation and iterator functions.

### Day 04 – Advanced DAX and Time Intelligence
- Variables using `VAR` and `RETURN`.
- Time intelligence functions.
- Year-to-date and month-to-date calculations.
- Previous-period comparisons.
- Rolling averages.
- Dynamic measures.
- Advanced filter manipulation.

### Day 05 – Advanced Visualisation and Analytics
- Executive dashboards.
- Drill-through and tooltips.
- Bookmarks and navigation.
- Conditional formatting.
- Dynamic titles and KPIs.
- Forecasting and analytical storytelling.

### Day 06 – AI Integration
- Claude-assisted Power BI development.
- Microsoft Copilot capabilities.
- AI-assisted DAX development.
- Model Context Protocol (MCP).
- AI-assisted documentation and analysis.
- Responsible use of AI in BI workflows.

### Day 07 – Performance Optimisation
- VertiPaq storage engine.
- Formula engine versus storage engine.
- Performance Analyzer.
- DAX Studio.
- Model optimisation.
- Query performance.
- Reducing model size and improving responsiveness.

### Day 08 – Enterprise Governance and Deployment
- Row-Level Security (RLS).
- Object-Level Security (OLS).
- Workspace management.
- Deployment pipelines.
- Gateways and scheduled refresh.
- PBIP and TMDL.
- Version control and governance.

### Day 09 – Fabric, APIs and Automation
- Microsoft Fabric architecture.
- OneLake and Lakehouse.
- Direct Lake.
- Power BI REST APIs.
- Python integration.
- BigQuery integration.
- Power Automate.
- Analytics workflow automation.

### Day 10 – Capstone Project

**Project:** Business Performance and Strategic Decision Intelligence Dashboard.

The capstone will bring together the skills developed throughout the programme.

Planned capabilities:

- Executive KPI dashboard.
- Revenue and profitability analysis.
- Customer segmentation.
- Product and regional performance.
- Period-over-period comparisons.
- Time intelligence.
- Forecasting and scenario analysis.
- Dynamic business insights.
- AI-assisted analytical commentary.

---

## Technology Stack

| Technology | Purpose |
|---|---|
| Power BI Desktop | Data modelling and report development |
| Power Query | Data transformation |
| M Language | Data preparation and transformation logic |
| DAX | Measures and analytical calculations |
| Microsoft Fabric | Modern analytics architecture |
| SQL | Data querying |
| Python | Data analysis and automation |
| BigQuery | Cloud data integration |
| Claude | AI-assisted development and analysis |
| Git and GitHub | Version control and portfolio documentation |

*Tools and features will be introduced progressively throughout the programme.*

## Repository Structure

```text
PowerBi-portfolio/
│
├── README.md
│
├── Day-01-PowerBI-Foundations/
│   └── (Documentation and practical exercises)
│
├── Day-02-Data-Modelling/
│   ├── README.md
│   ├── fact-and-dimension-tables.md
│   ├── star-vs-snowflake.md
│   ├── relationships.md
│   ├── date-table.md
│   ├── dax-userelationship.md
│   └── images/
│       └── day-02-date-analysis.png
│
├── Day-03-DAX-Fundamentals/
│
├── Day-04-Advanced-DAX/
│
├── Day-05-Visualisation-and-Analytics/
│
├── Day-06-AI-Integration/
│
├── Day-07-Performance-Optimisation/
│
├── Day-08-Enterprise-Governance/
│
├── Day-09-Fabric-APIs-Automation/
│
└── Day-10-Capstone-Project/
```

Folders will be populated as each learning module is completed.

## Learning and Documentation Approach

Each module follows a practical learning structure:

1. Understand the underlying concepts.
2. Apply the concepts in Power BI Desktop.
3. Complete practical exercises.
4. Validate results and investigate errors.
5. Document the technical implementation.
6. Publish meaningful contributions to GitHub.

The goal is to maintain a consistent record of learning, practical implementation, and technical progress.

## Portfolio Goal

This repository is part of my broader professional development in Business Intelligence, Data Engineering, and AI-driven analytics.

The long-term objective is to demonstrate the ability to move beyond building reports and develop reliable, scalable, and decision-oriented analytics solutions.

**Learning by building. Improving through practice. Documenting the journey.**

---

**Repository:** [PowerBi-portfolio](https://github.com/damikuteyi/PowerBi-portfolio)