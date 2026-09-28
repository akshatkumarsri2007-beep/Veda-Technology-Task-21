# Task 21: Basic SQL SELECT

**Author:** Akshat Srivastava
**Internship:** Veda Technology, Data Analytics Track
**Level / Day:** Level 1, Day 21

Basic SQL practice on the **Northwind** database using `SELECT`, `WHERE` and `ORDER BY`, run in Google Colab with SQLite.

---

## Objective

Build SQL fundamentals by writing simple queries on real business data (customers, products, orders and employees).

## Tools Used

| Tool | Purpose |
|------|---------|
| Google Colab | Notebook to write and run the queries |
| SQLite | Database engine |
| Python (pandas) | Load the Excel data and display query results |
| Northwind dataset | Sample business database |

## Dataset

The Northwind database is a well-known sample database of a food trading company.

| Table | Rows | Description |
|-------|------|-------------|
| customers | 91 | Companies that buy products |
| products | 77 | Items sold, with price and stock |
| orders | 830 | Orders placed by customers |
| order_details | 2155 | Products included in each order |
| employees | 9 | Staff who handle the orders |
| categories | 8 | Product categories |

## Repository Structure

```
.
├── README.md
├── Task21_SQL_Queries.ipynb                    # Colab notebook with queries and outputs
├── northwind_data.xlsx                         # Dataset (one sheet per table)
├── northwind.db                                # Same dataset as a SQLite database
└── Task21_SQL_Report_Akshat_Srivastava.pdf     # Final report
```

## How to Run

1. Open the notebook in Google Colab.
2. Upload `northwind_data.xlsx` to the Colab files panel.
3. Run the setup cell to load the Excel sheets into an SQLite database:

```python
import pandas as pd
import sqlite3

sheets = pd.read_excel("northwind_data.xlsx", sheet_name=None)

conn = sqlite3.connect(":memory:")
for name, df in sheets.items():
    df.to_sql(name, conn, index=False, if_exists="replace")

def run(query):
    return pd.read_sql_query(query, conn)
```

4. Run each query cell, for example `run("SELECT * FROM customers")`.

## Queries

```sql
-- 1. Retrieve all customers
SELECT * FROM customers;

-- 2. Select specific columns
SELECT company_name, country FROM customers;

-- 3. Customers from Germany
SELECT * FROM customers WHERE country = 'Germany';

-- 4. Products with price greater than 50
SELECT product_name, unit_price FROM products WHERE unit_price > 50;

-- 5. Products sorted by price (high to low)
SELECT product_name, unit_price FROM products ORDER BY unit_price DESC;

-- 6. Customers sorted A-Z
SELECT company_name, city FROM customers ORDER BY company_name ASC;

-- 7. Orders placed in 1997
SELECT order_id, order_date FROM orders WHERE strftime('%Y', order_date) = '1997';

-- 8. Top 5 most expensive products
SELECT product_name, unit_price FROM products ORDER BY unit_price DESC LIMIT 5;

-- 9. Customers from the USA or UK
SELECT company_name, country FROM customers WHERE country IN ('USA', 'UK');

-- 10. Employees based in London
SELECT first_name, last_name, city FROM employees WHERE city = 'London';
```

## Results Summary

| # | Query | Rows returned |
|---|-------|---------------|
| 1 | All customers | 91 |
| 2 | Company name and country | 91 |
| 3 | Customers from Germany | 11 |
| 4 | Products priced above 50 | 7 |
| 5 | Products by price (high to low) | 77 |
| 6 | Customers A-Z | 91 |
| 7 | Orders in 1997 | 408 |
| 8 | Top 5 expensive products | 5 |
| 9 | Customers from USA or UK | 20 |
| 10 | Employees in London | 4 |

## What I Learned

- Selecting, filtering and sorting data with `SELECT`, `WHERE` and `ORDER BY`.
- Using the `IN` operator and the `LIMIT` clause.
- Writing clean, readable queries with capitalised keywords and one clause per line.
- Working with real business data such as customers, orders and products.

## Conclusion

This task built a solid foundation in SQL fundamentals, which will be useful for learning joins, aggregations and data analysis in the upcoming tasks.

## Acknowledgements

The Northwind sample database was originally created by Microsoft. This project uses a publicly available copy converted to SQLite for learning purposes.

---

Made by **Akshat Srivastava**
