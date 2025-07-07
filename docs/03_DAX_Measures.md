# 3. Key DAX Measures

The analytical power of the Nexus Trading Co. dashboard comes from a set of core DAX (Data Analysis Expressions) measures. These formulas transform raw data into a rich set of business metrics that tell a story. This document provides a complete reference for all key calculations used in the report.

The measures are grouped into logical categories:
1.  **Core Metrics:** Fundamental calculations for sales, volume, and transactions.
2.  **Profitability Metrics:** Measures focused on understanding business profitability.
3.  **Averaging Metrics:** Calculations for understanding the typical transaction value.
4.  **Year-over-Year (YoY) Growth Metrics:** A suite of measures for contextual performance analysis.

---

### Core Metrics

These are the foundational building blocks of the dashboard.

#### Total Sales
*   **Business Definition:** Calculates the total revenue generated from all sales transactions by multiplying the quantity of each line item by its unit price.
*   **DAX Code:**
    ```dax
    Total Sales =
    SUMX(
        Sales,
        Sales[Order Quantity] * Sales[Unit Price]
    )
    ```

#### Total Transactions
*   **Business Definition:** Provides a simple count of the total number of individual sales transaction line items.
*   **DAX Code:**
    ```dax
    Total Transactions = COUNTROWS(Sales)
    ```

#### Total Quantity Sold
*   **Business Definition:** Sums the total number of individual units sold across all transactions. This is a key metric for understanding product volume.
*   **DAX Code:**
    ```dax
    Total Quantity Sold = SUM(Sales[Order Quantity])
    ```

---

### Profitability Metrics

These measures shift the focus from simple revenue to the actual profitability of the business.

#### Profit Margin
*   **Business Definition:** Calculates the percentage of revenue that remains as profit. A value of 37% means that for every dollar of sales, 37 cents is profit.
*   **Note:** This measure depends on a `[Total Profits]` measure, which is typically calculated as `[Total Sales] - [Total Cost]`.
*   **DAX Code:**
    ```dax
    Profit Margin =
    DIVIDE(
        [Total Profits],
        [Total Sales],
        0
    )
    ```

---

### Averaging Metrics

This measure helps understand the typical value of a transaction line.

#### Avg Order Size
*   **Business Definition:** This measure calculates the average financial value per individual transaction line item. It is displayed as "Avg Transactions" on the dashboard.
*   **Note:** This formula calculates the average *line item value*. A different approach would be needed to calculate the average *total order value* (which would involve grouping by `OrderNumber`).
*   **DAX Code:**
    ```dax
    Avg Order Size =
    AVERAGEX(
        Sales,
        [Total Sales]
    )
    ```

---

### Year-over-Year (YoY) Growth Metrics

YoY calculations are essential for providing context and understanding performance trends. They compare the current period's performance to the same period in the previous year.

#### The "Last Year" (LY) Calculation Pattern
All YoY growth measures depend on a corresponding base measure that calculates the value for the prior year. They all use the following pattern with `CALCULATE` and `SAMEPERIODLASTYEAR`.

**Base Last Year Measure Template:**
```dax
Measure LY =
CALCULATE(
    [Base Measure],
    SAMEPERIODLASTYEAR('Dates'[Date])
)
```
*(e.g., `[Sales LY]`, `[Profit Margin LY]`, etc., are created using this pattern.)*

---

#### % Sales Growth
*   **Business Definition:** The percentage increase or decrease in `Total Sales` compared to the same period in the previous year.
*   **DAX Code:**
    ```dax
    % Sales Growth =
    VAR sales_dif = [Total Sales] - [Sales LY]
    VAR pct_growth =
        DIVIDE(
            sales_dif,
            [Sales LY],
            0
        )
    RETURN
        pct_growth
    ```

#### % Profit Margin Growth
*   **Business Definition:** The absolute percentage point change in `Profit Margin` compared to the previous year. For example, a change from 35% to 37% would be a growth of 2%.
*   **DAX Code:**
    ```dax
    % Profit Margin Growth =
    VAR pm_dif = [Profit Margin] - [Profit Margin LY]
    VAR pm_growth =
        DIVIDE(
            pm_dif,
            [Profit Margin LY],
            0
        )
    RETURN
        pm_dif
    ```

#### % Avg Order Size Growth
*   **Business Definition:** Tracks the YoY growth of the average line item value, showing if the company is selling higher or lower-value items over time.
*   **DAX Code:**
    ```dax
    % Avg Order Size Growth =
    VAR AOS_dif = [Avg Order Size] - [Avg Order Size LY]
    VAR AOS_growth =
        DIVIDE(
            AOS_dif,
            [Avg Order Size LY],
            0
        )
    RETURN
        AOS_growth
    ```

#### Total Sold Growth
*   **Business Definition:** Measures the YoY growth in the total volume of units sold, indicating changes in market demand or sales velocity.
*   **DAX Code:**
    ```dax
    Total Sold Growth =
    VAR ts_dif = [Total Quantity Sold] - [Total Quantity Sold LY]
    VAR ts_growth =
        DIVIDE(
            ts_dif,
            [Total Quantity Sold LY],
            0
        )
    RETURN
        ts_growth
    ```
```