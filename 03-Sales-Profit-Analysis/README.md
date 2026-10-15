# Sales and Profit Analysis using SQL Server

## 📌 Project Overview
This case study focuses on analyzing sales, profit, expenses, inventory, and product performance using Microsoft SQL Server. The project uses relational datasets to answer business-related questions and extract meaningful insights through SQL queries.

## 🎯 Objectives
- Analyze sales and profit across different states, products, and dates.
- Calculate total sales, average sales, profit, expenses, and inventory.
- Compare actual sales and profit with budget values.
- Identify product-wise and state-wise business performance.
- Apply advanced SQL features to solve analytical problems.

## 🗂️ Dataset Description
The project uses three tables:

| Table | Description |
|---|---|
| `FactTable` | Contains sales, profit, expenses, inventory, budget metrics, dates, product IDs, and area codes. |
| `ProductTable` | Contains product IDs, product names, product types, and types. |
| `LocationTable` | Contains area codes, states, markets, and market sizes. |

## 🛠️ Tools and Technologies
- Microsoft SQL Server
- SQL Server Management Studio (SSMS)
- SQL

## 📊 SQL Concepts Covered
- SELECT, WHERE, ORDER BY, and DISTINCT
- Aggregate functions: `SUM()`, `AVG()`, `MIN()`, and `MAX()`
- GROUP BY and HAVING
- INNER JOIN and other join operations
- Subqueries and set operations
- Window functions: `DENSE_RANK()`
- Common Table Expressions and conditional logic, where applicable
- Stored procedures and user-defined functions
- Views and data modification statements
- Transactions with COMMIT and ROLLBACK
- ROLLUP for hierarchical aggregation
- String and date functions

## 🔍 Key Analysis Areas
1. **Sales Analysis:** Total, average, minimum, and maximum sales.
2. **Profit Analysis:** State-wise and product-wise profit calculations.
3. **Product Analysis:** Product types, product details, and product performance.
4. **Expense Analysis:** Total expenses and expense-based profit/loss classification.
5. **Budget Analysis:** Comparison and aggregation of budget metrics.
6. **Time-Based Analysis:** Date-wise and weekly sales summaries.
7. **Advanced SQL:** Ranking, stored procedures, user-defined functions, and transactions.

## 📁 Project Structure
```text
03-Sales-Profit-Analysis/
├── README.md
└── sales_profit_analysis.sql
```

## 💡 Learning Outcomes
- Improved SQL querying and data analysis skills.
- Practiced joining multiple relational tables.
- Applied aggregate and window functions to business data.
- Gained experience with stored procedures, user-defined functions, and transaction handling.
- Developed an understanding of how SQL supports sales and profitability analysis.

## ▶️ How to Run
1. Open Microsoft SQL Server Management Studio.
2. Import or restore the dataset and create the required tables.
3. Open `sales_profit_analysis.sql`.
4. Execute the queries against the database containing the three tables.

**Note:** Ensure the table and column names in the SQL file match the database schema.

## 👩‍💻 Project Type
SQL Case Study – Sales and Profit Analysis
