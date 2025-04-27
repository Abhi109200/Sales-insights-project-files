## Sales Insights Data Analysis Project

### **Introduction**
This project involves analyzing sales data to uncover meaningful insights using SQL and Power BI. The dataset includes customer, transaction, and date information, facilitating detailed analysis of revenue, market performance, and trends over time.
---
### **Setting Up MySQL**
1. Follow [this tutorial](https://www.youtube.com/watch?v=WuBcTJnIuzo) to install MySQL.
2. Download and import the `db_dump.sql` file into your local MySQL database as demonstrated in the tutorial.
---
### **Data Analysis Using SQL**
SQL queries were used to extract and analyze key metrics:
1. Retrieve all customer records:
   ```sql
   SELECT * FROM customers;
   ```
2. Count total number of customers:
   ```sql
   SELECT count(*) FROM customers;
   ```
3. Analyze Chennai market transactions (market code: Mark001):
   ```sql
   SELECT * FROM transactions WHERE market_code = 'Mark001';
   ```
4. Identify distinct products sold in Chennai:
   ```sql
   SELECT DISTINCT product_code FROM transactions WHERE market_code = 'Mark001';
   ```
5. Extract transactions in USD:
   ```sql
   SELECT * FROM transactions WHERE currency = 'USD';
   ```
6. Examine 2020 transactions joined with the date table:
   ```sql
   SELECT transactions.*, date.* FROM transactions 
   INNER JOIN date ON transactions.order_date = date.date 
   WHERE date.year = 2020;
   ```
7. Calculate total revenue in 2020:
   ```sql
   SELECT SUM(transactions.sales_amount) 
   FROM transactions 
   INNER JOIN date ON transactions.order_date = date.date 
   WHERE date.year = 2020 AND (transactions.currency = 'INR' OR transactions.currency = 'USD');
   ```
8. Filter total revenue for January 2020:
   ```sql
   SELECT SUM(transactions.sales_amount) 
   FROM transactions 
   INNER JOIN date ON transactions.order_date = date.date 
   WHERE date.year = 2020 AND date.month_name = 'January' 
   AND (transactions.currency = 'INR' OR transactions.currency = 'USD');
   ```
9. Calculate 2020 revenue for Chennai:
   ```sql
   SELECT SUM(transactions.sales_amount) 
   FROM transactions 
   INNER JOIN date ON transactions.order_date = date.date 
   WHERE date.year = 2020 AND transactions.market_code = 'Mark001';
   ```
### **Data Analysis Using Power BI**
1. A `norm_amount` column was created to normalize sales amounts:
   ```powerquery
   = Table.AddColumn(#"Filtered Rows", "norm_amount", 
   each if [currency] = "USD" or [currency] = "USD#(cr)" 
   then [sales_amount]*75 else [sales_amount], type any)
   ```

2. Interactive dashboards were built to visualize trends, revenue, and market performance.

---
### Dashboard
![Screenshot 2025-04-27 222108](https://github.com/user-attachments/assets/9bbc6928-3246-4645-9437-aeff9fe29587)

### **Conclusion**
This project highlights how SQL and Power BI can be combined for powerful data analysis. SQL facilitated precise data extraction and trend identification, while Power BI enabled dynamic visualization for actionable insights.

