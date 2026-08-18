# Retail Sales Analytics Dashboard — DAX Measures

This document contains the key DAX measures used in the Retail Sales Analytics Dashboard.

---

## Total Sales

Calculates total sales within the current filter context.

```DAX
Total Sales =
SUM(Sales[SalesAmount])
```

---

## Total Orders

Counts the number of distinct orders.

```DAX
Total Orders =
DISTINCTCOUNT(Sales[OrderID])
```

---

## Total Customers

Counts the number of distinct customers.

```DAX
Total Customers =
DISTINCTCOUNT(Sales[CustomerID])
```

---

## Total Products

Counts the number of distinct products.

```DAX
Total Products =
DISTINCTCOUNT(Sales[ProductID])
```

---

## Sales YTD

Calculates year-to-date sales.

```DAX
Sales YTD =
TOTALYTD(
    [Total Sales],
    'Date'[Date]
)
```

---

## Previous Year Sales

Calculates sales for the equivalent period in the previous year.

```DAX
Previous Year Sales =
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR('Date'[Date])
)
```

---

## Sales YoY Growth %

Calculates the percentage change in sales compared with the previous year.

```DAX
Sales YoY Growth % =
DIVIDE(
    [Total Sales] - [Previous Year Sales],
    [Previous Year Sales],
    0
)
```

---

## Previous Year Orders

Calculates the number of orders for the equivalent previous-year period.

```DAX
Previous Year Orders =
CALCULATE(
    [Total Orders],
    SAMEPERIODLASTYEAR('Date'[Date])
)
```

---

## Orders YoY Growth %

Calculates year-over-year growth in total orders.

```DAX
Orders YoY Growth % =
DIVIDE(
    [Total Orders] - [Previous Year Orders],
    [Previous Year Orders],
    0
)
```

---

## Previous Year Customers

Calculates the number of customers for the equivalent period in the previous year.

```DAX
Previous Year Customers =
CALCULATE(
    [Total Customers],
    SAMEPERIODLASTYEAR('Date'[Date])
)
```

---

## Customers YoY Growth %

Calculates year-over-year customer growth.

```DAX
Customers YoY Growth % =
DIVIDE(
    [Total Customers] - [Previous Year Customers],
    [Previous Year Customers],
    0
)
```

---

## Previous Year Products

Calculates the number of products sold during the equivalent previous-year period.

```DAX
Previous Year Products =
CALCULATE(
    [Total Products],
    SAMEPERIODLASTYEAR('Date'[Date])
)
```

---

## Products YoY Growth %

Calculates year-over-year growth in the number of products sold.

```DAX
Products YoY Growth % =
DIVIDE(
    [Total Products] - [Previous Year Products],
    [Previous Year Products],
    0
)
```

---

## Running Total Sales

Calculates cumulative sales from the beginning of the reporting period through the current date.

```DAX
Running Total Sales =
CALCULATE(
    [Total Sales],
    FILTER(
        ALLSELECTED('Date'[Date]),
        'Date'[Date] <= MAX('Date'[Date])
    )
)
```

---

## Sales Previous Month

Calculates total sales for the previous month.

```DAX
Sales Previous Month =
CALCULATE(
    [Total Sales],
    DATEADD(
        'Date'[Date],
        -1,
        MONTH
    )
)
```

---

## Sales MoM Growth %

Calculates month-over-month sales growth.

```DAX
Sales MoM Growth % =
DIVIDE(
    [Total Sales] - [Sales Previous Month],
    [Sales Previous Month],
    0
)
```

---

## Average Order Value

Calculates average sales value per order.

```DAX
Average Order Value =
DIVIDE(
    [Total Sales],
    [Total Orders],
    0
)
```

---

## Sales Contribution %

Calculates each product or category's contribution to total sales.

```DAX
Sales Contribution % =
DIVIDE(
    [Total Sales],
    CALCULATE(
        [Total Sales],
        ALLSELECTED(Sales)
    ),
    0
)
```

---

## Dashboard Usage

These measures support:

- Executive KPI cards
- Current-year versus previous-year comparison
- Year-to-date sales analysis
- Monthly sales trends
- Running total sales
- Top 10 product analysis
- Sales and order trend comparison
- Product and category filtering

---

## Note

Table and column names should be aligned with the final Power BI semantic model. The measures shown here represent the business logic used for the portfolio project and may require minor adjustment depending on the exact relationships and source schema.