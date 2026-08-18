# Retail Banking Performance Dashboard — DAX Measures

This document contains the key DAX measures used in the Retail Banking Performance Dashboard.

---

## 1. Total Transaction Value

Calculates the total monetary value of all transactions within the selected filter context.

```DAX
Total Transaction Value =
SUM(Transactions[Amount])
```

---

## 2. Previous Year Transaction Value

Calculates transaction value for the equivalent period in the previous year.

```DAX
Previous Year Transaction Value =
CALCULATE(
    [Total Transaction Value],
    SAMEPERIODLASTYEAR('Date'[Date])
)
```

---

## 3. YoY Transaction Growth %

Calculates the percentage change in transaction value compared with the same period in the previous year.

```DAX
YoY Transaction Growth % =
DIVIDE(
    [Total Transaction Value] - [Previous Year Transaction Value],
    [Previous Year Transaction Value],
    0
)
```

---

## 4. Previous Month Transaction Value

Calculates transaction value for the previous month.

```DAX
Previous Month Transaction Value =
CALCULATE(
    [Total Transaction Value],
    DATEADD('Date'[Date], -1, MONTH)
)
```

---

## 5. MoM Transaction Growth %

Calculates the percentage change in transaction value compared with the previous month.

```DAX
MoM Transaction Growth % =
DIVIDE(
    [Total Transaction Value] - [Previous Month Transaction Value],
    [Previous Month Transaction Value],
    0
)
```

---

## 6. Active Customers

Counts the number of distinct customers with transaction activity in the selected period.

```DAX
Active Customers =
DISTINCTCOUNT(Transactions[CustomerID])
```

---

## 7. Active Accounts

Counts the number of distinct accounts with transaction activity in the selected period.

```DAX
Active Accounts =
DISTINCTCOUNT(Transactions[AccountID])
```

---

## 8. Average Transaction Value

Calculates the average monetary value per transaction.

```DAX
Average Transaction Value =
DIVIDE(
    [Total Transaction Value],
    DISTINCTCOUNT(Transactions[TransactionID]),
    0
)
```

---

## 9. Accounts Opened

Counts the number of accounts opened within the selected reporting period.

```DAX
Accounts Opened =
DISTINCTCOUNT(Accounts[AccountID])
```

> The final implementation can use the account opening date relationship with the Date table depending on the data model.

---

## 10. New Customers

Counts customers acquired within the selected reporting period.

```DAX
New Customers =
DISTINCTCOUNT(Customers[CustomerID])
```

> The final implementation can use the customer join date relationship with the Date table depending on the data model.

---

## Dashboard Usage

These measures support the dashboard's:

- Executive KPI cards
- Year-over-year performance analysis
- Month-over-month growth analysis
- Transaction trend analysis
- Customer activity analysis
- Account activity analysis
- Channel and transaction performance reporting

---

## Note

Measure and column names may vary depending on the final Power BI semantic model. The measures should be aligned with the relationships and business definitions used in the PBIX model.