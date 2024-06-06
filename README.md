## Sales Insights Data Analysis Project

1. Download the `db_dump.sql` file to your local computer and import it.

### Data Analysis Using SQL

1. Show all customer records:
   
   SELECT * FROM customers;
  

2. Show the total number of customers:
  
   SELECT COUNT(*) FROM customers;
   

3. Show transactions for the Chennai market (market code for Chennai is Mark001):
   
   SELECT * FROM transactions WHERE market_code = 'Mark001';
  

4. Show distinct product codes that were sold in Chennai:
  
   SELECT DISTINCT product_code FROM transactions WHERE market_code = 'Mark001';
  

5. Show transactions where the currency is US dollars:
   
   SELECT * FROM transactions WHERE currency = 'USD';
 

6. Show transactions in 2020 joined by the date table:
  
   SELECT transactions.*, date.*
   FROM transactions
   INNER JOIN date ON transactions.order_date = date.date
   WHERE date.year = 2020;
  

7. Show total revenue in the year 2020:
   
   SELECT SUM(transactions.sales_amount)
   FROM transactions
   INNER JOIN date ON transactions.order_date = date.date
   WHERE date.year = 2020 AND (transactions.currency = 'INR' OR transactions.currency = 'USD');
   

8. Show total revenue in January 2020:
   
   SELECT SUM(transactions.sales_amount)
   FROM transactions
   INNER JOIN date ON transactions.order_date = date.date
   WHERE date.year = 2020 AND date.month_name = 'January' AND (transactions.currency = 'INR' OR transactions.currency = 'USD');
   

9. Show total revenue in 2020 in Chennai:
   
   SELECT SUM(transactions.sales_amount)
   FROM transactions
   INNER JOIN date ON transactions.order_date = date.date
   WHERE date.year = 2020 AND transactions.market_code = 'Mark001';
 

### Data Analysis Using Power BI

1. Formula to create a new column called `Normalised Sales_Amount`:
   
   = Table.AddColumn(#"Filtered Rows", "Normalised Sales_Amount", each if [currency] = "USD" or [currency] = "USD#(cr)" then [sales_amount] * 75 else [sales_amount], type any)
  
