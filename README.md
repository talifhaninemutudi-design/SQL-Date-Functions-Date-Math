# SQL-Date-Functions-Date-Math
A collection of Databricks SQL exercises showcasing database design, data transformation, date functions, conditional logic, and query optimization using Spark SQL.
# 📅 Databricks SQL Date Functions

## 📌 Project Overview

This project demonstrates the use of **Date Functions in Databricks (Spark SQL)** through practical business scenarios. The exercises cover creating tables, inserting sample data, manipulating dates, extracting date components, formatting dates, and classifying records using conditional logic.

The project is designed to strengthen SQL skills commonly used by Data Analysts, Business Analysts, and Data Engineers when working with transactional and customer data.

---

## 🎯 Objectives

- Create SQL tables using Databricks Spark SQL
- Insert sample data into tables
- Perform date calculations
- Format dates for reporting
- Extract year, month, and day from dates
- Calculate customer age
- Calculate days between dates
- Add days to dates
- Classify records using CASE statements

---

## 🛠 Technologies Used

- Databricks
- Spark SQL
- GitHub

---

## 📂 Tables Created

The following tables were created during the exercises:

- SALESQ3
- TRANSACTIONS
- DELIVERIES
- EMPLOYEES
- ONLINE_ORDERS
- PAYMENT_DATES
- CUSTOMER_PURCHASES
- SHIPPING_ORDERS
- YEARLY_ORDERS
- BOOKINGS
- CAMPAIGN_SENDS
- INVOICE_DATES
- CUSTOMER_BIRTHDAYS
- ORDERS

---

## 📚 Date Functions Covered

This project demonstrates the following Databricks SQL date functions:

| Function | Purpose |
|----------|---------|
| `CURRENT_DATE()` | Returns today's date |
| `DATEDIFF()` | Calculates the difference between two dates |
| `DATE_ADD()` | Adds a specified number of days to a date |
| `TO_DATE()` | Converts a string into a date |
| `DATE_FORMAT()` | Formats dates for reporting |
| `DATE_TRUNC()` | Returns the first day of a specified date period |
| `YEAR()` | Extracts the year from a date |
| `MONTH()` | Extracts the month from a date |
| `DAY()` | Extracts the day from a date |
| `DAYOFWEEK()` | Returns the day of the week as a number |
| `MONTHS_BETWEEN()` | Calculates the number of months between two dates |

---

## 📊 Business Scenarios Implemented

The project includes SQL solutions for:

- Calculating customer age
- Identifying active, at-risk, and inactive customers
- Calculating days since last purchase
- Determining expected delivery dates
- Extracting booking year, month, and day
- Formatting invoice dates for reports
- Extracting order year
- Identifying weekday and weekend orders
- Finding the first day of each month
- Converting text values to dates

---

## 💡 Example Query

```sql
SELECT
    customer_id,
    customer_name,
    last_purchase_date,
    datediff(current_date(), last_purchase_date) AS days_since_last_purchase,
    CASE
        WHEN datediff(current_date(), last_purchase_date) <= 30 THEN 'Active Customer'
        WHEN datediff(current_date(), last_purchase_date) BETWEEN 31 AND 90 THEN 'At Risk Customer'
        ELSE 'Inactive Customer'
    END AS customer_status
FROM CUSTOMER_PURCHASES;
```

---

## 🎓 Skills Demonstrated

- SQL Programming
- Spark SQL
- Date and Time Functions
- Data Transformation
- Data Cleaning
- Business Reporting
- Conditional Logic
- Database Design
- Analytical Query Writing
- Customer Segmentation

---

## 🚀 Learning Outcomes

Through this project, I gained hands-on experience with Databricks Spark SQL by applying date functions to solve real-world business problems. These exercises strengthened my understanding of data transformation, reporting, and analytical query development while improving my ability to write clean and efficient SQL code.

---

## 👤 Author

**Talifhani Nemutudi**

Aspiring Data Analyst | SQL | Power BI | Excel | Databricks | Financial Analytics

---

## 📄 License

This project is intended for educational and portfolio purposes.

-----------------------------------------------------------SQL QUERIES-----------------------------------------------------------------------------
-- Create the orders table
CREATE OR REPLACE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT NOT NULL,
    order_date DATE NOT NULL
);

INSERT INTO orders (order_id, customer_id, order_date)
VALUES
    (1001, 101, '2026-05-01'),
    (1002, 102, '2026-05-02'),
    (1003, 103, '2026-05-03'),
    (1004, 104, '2026-05-04'),
    (1005, 105, '2026-05-05');

    SELECT *
FROM orders;

SELECT order_id, customer_id, order_date,
       DAYNAME(order_date) AS day_name
FROM orders;

-------------QUESTION 2---------------
-- Create the customer_signups table
CREATE OR REPLACE TABLE customer_signups (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(50) NOT NULL,
    signup_date DATE NOT NULL
);

INSERT INTO customer_signups (customer_id, customer_name, signup_date)
VALUES
    (201, 'John', '2026-01-15'),
    (202, 'Mary', '2026-02-20'),
    (203, 'Peter', '2026-03-05'),
    (204, 'Sarah', '2026-04-18'),
    (205, 'Thabo', '2026-05-30');


SELECT *
FROM customer_signups;

SELECT customer_id, customer_name, signup_date,
       MONTHNAME(signup_date) AS signup_month_name
FROM customer_signups;

------QUESTION 03----------
CREATE OR REPLACE TABLE SALESQ3 (
    sale_id VARCHAR(10) PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    sale_date DATE NOT NULL,
    amount DECIMAL(10,2) NOT NULL
);

-- Insert data into SALESQ3
INSERT INTO SALESQ3 (sale_id, product_name, sale_date, amount)
VALUES
('S001', 'Laptop',  '2026-01-10', 12000.00),
('S002', 'Mouse',   '2026-02-15',   250.00),
('S003', 'Keyboard','2026-03-20',   700.00),
('S004', 'Monitor', '2026-04-25',  3500.00),
('S005', 'Desk',    '2026-05-30',  2000.00);

SELECT * 
FROM SALESQ3;

SELECT sale_id, product_name, sale_date,
       MONTH(sale_date) AS sale_month
FROM SALESQ3;

------QUESTION 4-----------
CREATE TABLE TRANSACTIONSQ4 (
    transaction_id VARCHAR(10) PRIMARY KEY,
    customer_id INT NOT NULL,
    transaction_date DATE NOT NULL,
    amount DECIMAL(10,2) NOT NULL
);

-- Insert sample data
INSERT INTO TRANSACTIONSQ4 (transaction_id, customer_id, transaction_date, amount)
VALUES
('T001', 101, '2024-12-15', 500.00),
('T002', 102, '2025-01-20', 1200.00),
('T003', 103, '2025-06-10', 800.00),
('T004', 104, '2026-02-05', 1500.00),
('T005', 105, '2026-05-25', 2000.00);

-- View the table
SELECT * FROM TRANSACTIONSQ4;

SELECT transaction_id, customer_id, transaction_date,
       YEAR(transaction_date) AS transaction_year
FROM transactionsQ4;

--------QUESTION05-------
CREATE TABLE DELIVERIES (
    delivery_id VARCHAR(10) PRIMARY KEY,
    customer_id INT NOT NULL,
    delivery_date DATE NOT NULL
);

-- Insert sample data
INSERT INTO DELIVERIES (delivery_id, customer_id, delivery_date)
VALUES
('D001', 101, '2026-05-01'),
('D002', 102, '2026-05-08'),
('D003', 103, '2026-05-15'),
('D004', 104, '2026-05-22'),
('D005', 105, '2026-05-29');

-- View the table
SELECT * FROM DELIVERIES;

SELECT delivery_id, customer_id, delivery_date,
       DAY(delivery_date) AS day_of_month
FROM deliveries;

----QUESTION 6----------
CREATE TABLE EMPLOYEES (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(100) NOT NULL,
    department VARCHAR(100) NOT NULL
);

-- Insert sample data
INSERT INTO EMPLOYEES (employee_id, employee_name, department)
VALUES
(301, 'Nandi', 'Sales'),
(302, 'Brian', 'IT'),
(303, 'Lerato', 'Finance'),
(304, 'Sipho', 'HR'),
(305, 'Aisha', 'Marketing');

-- View the table
SELECT * FROM EMPLOYEES;

SELECT employee_id, employee_name, department,
       CURRENT_DATE() AS today_date
FROM employees;

-----QUESTION 07--------
CREATE TABLE ONLINE_ORDERS (
    order_id INT PRIMARY KEY,
    customer_id INT NOT NULL,
    order_date_text VARCHAR(10) NOT NULL
);

-- Insert sample data
INSERT INTO ONLINE_ORDERS (order_id, customer_id, order_date_text)
VALUES
(4001, 101, '2026-01-15'),
(4002, 102, '2026-02-20'),
(4003, 103, '2026-03-25'),
(4004, 104, '2026-04-10'),
(4005, 105, '2026-05-05');

-- View the table
SELECT * FROM ONLINE_ORDERS;

SELECT
    order_id,
    customer_id,
    order_date_text,
    TO_DATE(order_date_text, 'yyyy-MM-dd') AS order_date
FROM ONLINE_ORDERS;

-------------QUESTION 08 ---------
CREATE TABLE PAYMENT_DATES (
    payment_id VARCHAR(10) PRIMARY KEY,
    customer_id INT NOT NULL,
    payment_date DATE NOT NULL
);

-- Insert sample data
INSERT INTO PAYMENT_DATES (payment_id, customer_id, payment_date)
VALUES
('P001', 101, '2026-01-05'),
('P002', 102, '2026-02-10'),
('P003', 103, '2026-03-15'),
('P004', 104, '2026-04-20'),
('P005', 105, '2026-05-25');

-- View the table
SELECT * FROM PAYMENT_DATES;

SELECT payment_id, customer_id, payment_date,
       TO_CHAR(payment_date, 'yyy-MM-dd') AS formatted_payment_date
FROM payment_dates;

-------QUESTION 09----------
CREATE TABLE CUSTOMER_PURCHASES (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100) NOT NULL,
    last_purchase_date DATE NOT NULL
);

-- Insert sample data
INSERT INTO CUSTOMER_PURCHASES (customer_id, customer_name, last_purchase_date)
VALUES
(501, 'John',  '2026-05-01'),
(502, 'Mary',  '2026-05-10'),
(503, 'Peter', '2026-05-15'),
(504, 'Sarah', '2026-05-20'),
(505, 'Thabo', '2026-05-25');

-- View the table
SELECT * FROM CUSTOMER_PURCHASES;

---------
SELECT
    SELECT
    customer_id,
    customer_name,
    last_purchase_date,
    datediff(current_date(), to_date(last_purchase_date, 'yyyy-MM-dd')) AS days_since_last_purchase
FROM CUSTOMER_PURCHASES;

--------QUESTION 10----------
CREATE TABLE SHIPPING_ORDERS (
    order_id INT PRIMARY KEY,
    customer_id INT NOT NULL,
    order_date DATE NOT NULL
);

-- Insert sample data
INSERT INTO SHIPPING_ORDERS (order_id, customer_id, order_date)
VALUES
(6001, 101, '2026-05-01'),
(6002, 102, '2026-05-03'),
(6003, 103, '2026-05-05'),
(6004, 104, '2026-05-07'),
(6005, 105, '2026-05-09');

-- View the table
SELECT * FROM SHIPPING_ORDERS;

SELECT
    order_id,
    customer_id,
    order_date,
    date_add(order_date, 7) AS expected_delivery_date
FROM SHIPPING_ORDERS;
----QUESTION11--------------
CREATE TABLE BOOKINGS (
    booking_id VARCHAR(10) PRIMARY KEY,
    customer_id INT NOT NULL,
    booking_date DATE NOT NULL
);

-- Insert sample data
INSERT INTO BOOKINGS (booking_id, customer_id, booking_date)
VALUES
('B001', 101, '2026-01-12'),
('B002', 102, '2026-02-18'),
('B003', 103, '2026-03-22'),
('B004', 104, '2026-04-09'),
('B005', 105, '2026-05-27');

-- View the table
SELECT * FROM BOOKINGS;

SELECT
    booking_id,
    customer_id,
    booking_date,
    YEAR(booking_date) AS booking_year,
    MONTH(booking_date) AS booking_month,
    DAY(booking_date) AS booking_day
FROM BOOKINGS;
-----QUESTION 12--------
CREATE TABLE yearly_ordersQ12 (
  order_id     INT,
  customer_id  INT,
  order_date   DATE,
  amount       DECIMAL(10,2)
);


INSERT INTO yearly_ordersQ12 (order_id, customer_id, order_date, amount)
VALUES
  (7001, 101, '2024-12-15', 500),
  (7002, 102, '2025-01-20', 1200),
  (7003, 103, '2025-06-10', 800),
  (7004, 104, '2026-02-05', 1500),
  (7005, 105, '2026-05-25', 2000);

  SELECT * FROM yearly_ordersQ12 ;

  SELECT order_id, customer_id, order_date,
       YEAR(order_date) AS order_year, amount
FROM yearly_ordersQ12
WHERE YEAR(order_date) = 2026;

------QUESTION 13---------
CREATE TABLE monthly_orders (
  order_id     INT,
  customer_id  INT,
  order_date   DATE,
  amount       DECIMAL(10,2)
);


INSERT INTO monthly_orders (order_id, customer_id, order_date, amount)
VALUES
  (8001, 101, '2026-01-15', 500),
  (8002, 102, '2026-02-20', 1200),
  (8003, 103, '2026-03-10', 800),
  (8004, 104, '2026-03-25', 1500),
  (8005, 105, '2026-05-30', 2000);


SELECT * FROM monthly_orders ORDER BY order_date;

SELECT order_id, customer_id, order_date,
       MONTH(order_date) AS order_month, amount
FROM monthly_orders
WHERE MONTH(order_date) = 3;

-----QUESTION 14----------
CREATE TABLE subscriptions (
  subscription_id  STRING,
  customer_id      INT,
  start_date       DATE
);


INSERT INTO subscriptions (subscription_id, customer_id, start_date)
VALUES
  ('SUB001', 101, '2026-01-10'),
  ('SUB002', 102, '2026-02-15'),
  ('SUB003', 103, '2026-03-20'),
  ('SUB004', 104, '2026-04-25'),
  ('SUB005', 105, '2026-05-30');


SELECT * FROM subscriptions ORDER BY start_date;

SELECT subscription_id, customer_id, start_date,
       LAST_DAY(start_date) AS month_end_date
FROM subscriptions;

----QUESTION15------
CREATE TABLE campaign_sends (
  send_id      STRING,
  customer_id  INT,
  send_date    DATE
);


INSERT INTO campaign_sends (send_id, customer_id, send_date)
VALUES
  ('C001', 101, '2026-01-12'),
  ('C002', 102, '2026-02-18'),
  ('C003', 103, '2026-03-22'),
  ('C004', 104, '2026-04-09'),
  ('C005', 105, '2026-05-27');


SELECT * FROM campaign_sends ORDER BY send_date;

SELECT
    send_id,
    customer_id,
    send_date,
    CAST(date_trunc('month', send_date) AS DATE) AS month_start_date
FROM campaign_sends;

---------QUESTION16----------
CREATE TABLE invoice_dates (
  invoice_id    STRING,
  customer_id   INT,
  invoice_date  DATE
);


INSERT INTO invoice_dates (invoice_id, customer_id, invoice_date)
VALUES
  ('INV001', 101, '2026-01-05'),
  ('INV002', 102, '2026-02-10'),
  ('INV003', 103, '2026-03-15'),
  ('INV004', 104, '2026-04-20'),
  ('INV005', 105, '2026-05-25');


SELECT * FROM invoice_dates ORDER BY invoice_date;

SELECT
    invoice_id,
    customer_id,
    invoice_date,
    date_format(invoice_date, 'MMMM yyyy') AS invoice_month_year
FROM INVOICE_DATES;

-----QUESTION17-----------
CREATE TABLE customer_birthdays (
  customer_id    INT,
  customer_name  STRING,
  date_of_birth  DATE
);


INSERT INTO customer_birthdays (customer_id, customer_name, date_of_birth)
VALUES
  (901, 'John',  '1998-05-10'),
  (902, 'Mary',  '1990-08-20'),
  (903, 'Peter', '2002-03-15'),
  (904, 'Sarah', '1985-12-01'),
  (905, 'Thabo', '2000-07-30');


SELECT * FROM customer_birthdays ORDER BY date_of_birth;

SELECT
    customer_id,
    customer_name,
    date_of_birth,
    FLOOR(months_between(current_date(), date_of_birth) / 12) AS customer_age
FROM CUSTOMER_BIRTHDAYS;

--------QUESTION18-----------
CREATE TABLE weekend_orders (
  order_id     INT,
  customer_id  INT,
  order_date   DATE
);


INSERT INTO weekend_orders (order_id, customer_id, order_date)
VALUES
  (9001, 101, '2026-05-01'),
  (9002, 102, '2026-05-02'),
  (9003, 103, '2026-05-03'),
  (9004, 104, '2026-05-04'),
  (9005, 105, '2026-05-05');


SELECT * FROM weekend_orders ORDER BY order_date;

SELECT
    order_id,
    customer_id,
    order_date,
    date_format(order_date, 'EEEE') AS day_name,
    CASE
        WHEN dayofweek(order_date) IN (1, 7)
        THEN 'Weekend'
        ELSE 'Weekday'
    END AS day_type
FROM ORDERS;

------QUESTION19-------------

CREATE TABLE quarterly_transactions (
  transaction_id    STRING,
  customer_id       INT,
  transaction_date  DATE,
  amount            DECIMAL(10,2)
);


INSERT INTO quarterly_transactions (transaction_id, customer_id, transaction_date, amount)
VALUES
  ('Q001', 101, '2026-01-15', 500),
  ('Q002', 102, '2026-03-20', 1200),
  ('Q003', 103, '2026-04-10', 800),
  ('Q004', 104, '2026-07-05', 1500),
  ('Q005', 105, '2026-10-25', 2000);


SELECT * FROM quarterly_transactions ORDER BY transaction_date;

SELECT transaction_id, customer_id, transaction_date,
       QUARTER(transaction_date) AS transaction_quarter, amount
FROM quarterly_transactions;

----------QUESTION20---------
CREATE TABLE recent_orders (
  order_id     STRING,
  customer_id  INT,
  order_date   DATE,
  amount       DECIMAL(10,2)
);

INSERT INTO recent_orders (order_id, customer_id, order_date, amount)
VALUES
  ('R001', 101, '2026-04-01', 500),
  ('R002', 102, '2026-04-15', 1200),
  ('R003', 103, '2026-05-01', 800),
  ('R004', 104, '2026-05-10', 1500),
  ('R005', 105, '2026-05-25', 2000);


SELECT * FROM recent_orders ORDER BY order_date;

SELECT order_id, customer_id, order_date,
       DATEDIFF(CURRENT_DATE(), order_date) AS days_since_order, amount
FROM recent_orders
WHERE DATEDIFF(CURRENT_DATE(), order_date) > 30;

------BONUS----------------
CREATE TABLE customer_summaryB (
  customer_id        INT,
  customer_name       STRING,
  last_purchase_date  DATE,
  total_spend         DECIMAL(10,2)
);


INSERT INTO customer_summaryB (customer_id, customer_name, last_purchase_date, total_spend)
VALUES
  (1001, 'John',  '2026-05-25', 5000),
  (1002, 'Mary',  '2026-05-10', 2500),
  (1003, 'Peter', '2026-04-01', 700),
  (1004, 'Sarah', '2026-02-15', 15000),
  (1005, 'Thabo', '2025-12-20', 300);


SELECT * FROM customer_summaryB ORDER BY last_purchase_date DESC;

SELECT
    customer_id,
    customer_name,
    last_purchase_date,
    datediff(current_date(), last_purchase_date) AS days_since_last_purchase,
    CASE
        WHEN datediff(current_date(), last_purchase_date) <= 30 THEN 'Active Customer'
        WHEN datediff(current_date(), last_purchase_date) BETWEEN 31 AND 90 THEN 'At Risk Customer'
        ELSE 'Inactive Customer'
    END AS customer_status
FROM CUSTOMER_PURCHASES;
