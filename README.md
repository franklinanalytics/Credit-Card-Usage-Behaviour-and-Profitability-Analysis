# Credit Card Usage Behavior & Profitability Analysis

## 📊 Project Overview

This project analyzes customer behavior, repayment patterns, and profitability in a simulated credit card dataset using SQL. It provides insights into spending habits, repayment consistency, and identifies high-value customers using advanced query logic. The dataset and insights are tailored to reflect realistic banking scenarios in emerging economies like Nigeria.

---

## 📁 Project Structure

```
├── README.md
├── schema_setup.sql         # SQL script to set up the database schema
├── queries.sql              # Main SQL analysis queries
├── screenshots/
│   ├── customer_table.png   # Preview of customer table
│   ├── repayment_table.png  # Preview of repayment table
│   └── transaction_table.png# Preview of transaction table
```

---

## 📌 Objectives

* Understand customer spending behavior by demographic groups.
* Evaluate repayment discipline and risk indicators.
* Estimate customer profitability using reward-based credit usage models.
* Segment customers for better decision-making and targeted upgrades.

---

## 🧾 Data Tables Preview

<table>
  <tr>
    <td><img src="screenshots/customer_table.png" width="250"></td>
    <td><img src="screenshots/transaction_table.png" width="250"></td>
    <td><img src="screenshots/repayment_table.png" width="250"></td>
  </tr>
  <tr>
    <td align="center">Customer Table</td>
    <td align="center">Transaction Table</td>
    <td align="center">Repayment Table</td>
  </tr>
</table>

---

## 🧠 Key Insights

### Card Usage Behavior

1. **Spending Patterns by Income Level & Region**

   * Higher income groups in urban regions tend to spend more and transact more frequently.
```sql
SELECT
    c.income_level,
    c.region,
    ROUND(SUM(t.amount), 2) AS total_spent,
    COUNT(t.transaction_id) AS transaction_count,
    ROUND(AVG(t.amount), 2) AS avg_transaction_amount
FROM transactions t
JOIN customers c ON t.customer_id = c.customer_id
GROUP BY c.income_level, c.region
ORDER BY c.income_level, c.region, total_spent DESC;
```

2. **Most Used Channel by Card Type & Age Group**

   * Younger customers (18–35) prefer digital channels for credit usage, especially with Platinum cards.

3. **Transaction Size & Frequency by Segment**

   * Medium-income customers showed higher average transaction sizes despite fewer total transactions.

### Repayment Behavior

4. **Late Payers**

   * 18.2% of customers have missed 3+ due dates, posing a credit risk.

5. **Repayment Rates by Age Group**

   * Customers aged 36–50 have the best repayment consistency.

6. **Unpaid Debt Over Time**

   * Notable spikes in unpaid debt during mid-year months, suggesting potential seasonal credit strain.

### Customer Profitability

7. **Top 10 Most Profitable Customers**

   * Profit = Annual Fee + (Spending × Reward Rate) - Unpaid Amount
   * These customers are consistent spenders with low default ratios.

8. **Group Contribution to Profit**

   * Urban, middle-aged, and upper-income groups contribute significantly to profit margins.

### Segmentation & Recommendations

9. **Customer Segments**

   * Segmented into: High Spenders (On-time vs Late), Medium Spenders, Low Spenders.

10. **Platinum Card Upgrade Targets**

* High spenders with excellent credit scores and low late repayment ratios.

11. **Regions Needing Financial Education or Credit Control**

* Regions with high overdue amounts and frequent late repayments need policy interventions.

12. **Year-on-Year Spending Growth by Income Group**
* Understand how each income group's credit usage is evolving to spot emerging segments.*

```sql
SELECT
    income_level,
    EXTRACT(YEAR FROM t.transaction_date) AS year,
    ROUND(SUM(t.amount), 2) AS total_spent
FROM transactions t
JOIN customers c ON t.customer_id = c.customer_id
GROUP BY income_level, year
ORDER BY income_level, year;
```

---

## ⚙️ Setup Instructions

1. **Run the schema**

   ```sql
   -- Run schema_setup.sql to create and populate tables
   ```
2. **Run the queries**

   ```sql
   -- Execute queries.sql to explore behaviors and insights
   ```
3. **Use PgAdmin or DBeaver** for optimal SQL interface and result visualization.

---

## 📌 Tools Used

* PostgreSQL (via PgAdmin)
* SQL (CTEs, Aggregations, CASE WHEN logic)
* Screenshots from database table previews

---

## 🧑‍💼 Author

**Durueke Franklin**
Data Analyst | Finance-focused Analytics | Portfolio-ready Projects

📧 [duruekefranklin@gmail.com](mailto:duruekefranklin@gmail.com)
🔗 [LinkedIn](https://linkedin.com/in/duruekefranklin)
💼 [GitHub Portfolio](https://github.com/DuruekeFranklin)

---

## ⭐ Final Thoughts

This analysis simulates a robust financial analytics use case involving behavior segmentation, credit risk evaluation, and profitability analysis. It can be extended into dashboard development, ML credit scoring, or campaign recommendation systems.
