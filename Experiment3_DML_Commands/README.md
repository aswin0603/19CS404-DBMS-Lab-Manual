# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
Show the categoryName and description from the categories table sorted by categoryName.

name                     type
---------------       ---------------
CategoryID           INTEGER
CategoryName     VARCHAR(25)
Description          VARCHAR(255)

```sql
SELECT CategoryName, Description FROM Categories ORDER BY CategoryName;
```

**Output:**

<img width="944" height="375" alt="image" src="https://github.com/user-attachments/assets/4d03b3f3-a2a6-4c4c-ac9e-67522ae51b86" />


**Question 2**
---
Write a SQL query to calculate the discounted price for products whose original price is between $50 and $150. Return product_id, original_price, discount_percentage, and discounted_price.

Sample table: Products

product_id | original_price | discount_percentage

 ------------+----------------+--------------------- 

101 | 50.00 | 0.10 

102 | 125.00 | 0.15

 103 | 200.00 | 0.20

 

```sql
SELECT
    product_id,
    original_price,
    discount_percentage,
    original_price * (1 - discount_percentage) AS discounted_price
FROM Products
WHERE original_price BETWEEN 50 AND 150;
```

**Output:**

<img width="1053" height="164" alt="image" src="https://github.com/user-attachments/assets/c65d0a7f-7f1f-4877-82d1-3f7001944054" />


**Question 3**
---
Increase the reorder level by 30% for products from 'Food' category having quantity in stock less than 50% of existing reorder level in the products table
name               type
--------------  ----------
product_id         INT
product_name       VARCHAR(10)
category           VARCHAR(50)
cost_price         DECIMAL(10)
sell_price         DECIMAL(10)
reorder_lvl        INT
quantity              INT
supplier_id           INT

```sql
update products
set reorder_lvl = reorder_lvl * 1.3
where category = 'Food' and quantity<reorder_lvl*0.5;
```

**Output:**

<img width="1166" height="167" alt="image" src="https://github.com/user-attachments/assets/7e1af73e-4016-4369-8d75-0a38d4c11339" />


**Question 4**
---
Write a SQL query to find customers who are from the city 'London' who have a grade greater than 200. Return customer_id, cust_name, city, grade, and salesman_id.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id    \
-------------+----------------+------------+-------+-------------   \
        3002 | Nick Rimando   | New York   |   100 |        5001    \
        3007 | Brad Davis     | New York   |   200 |        5001    \
        3005 | Graham Zusi    | California |   200 |        5002    

```sql
SELECT customer_id, cust_name, city, grade, salesman_id
FROM customer
WHERE city = 'London' AND grade > 200;
```

**Output:**

<img width="954" height="202" alt="image" src="https://github.com/user-attachments/assets/38d72c1e-76e1-4492-a808-835c7a29a5f5" />


**Question 5**
---
Write a SQL statement to Increase the salary by 500 and email as 'updated' for employees with job ID 'SA_REP' and commission percentage greater than 0.15


Employees table

--------------- \
employee_id  \
first_name    \
last_name    \
email    \ 
phone_number    \
hire_date    \
job_id    \
salary    \
commission_pct  \
manager_id  \  
department_id \

```sql
UPDATE EMPLOYEES SET salary = salary + 500, email = 'updated' WHERE job_id = 'SA_REP' AND commission_pct > 0.15;
```

**Output:**

<img width="1229" height="297" alt="image" src="https://github.com/user-attachments/assets/9b4ce3ca-8d9a-41f8-b3d5-757f2965af3a" />


**Question 6**
---
Write a SQL statement to increase the salary of employees under the department 40, 90 and 110 according to the company rules.

Salary will be increased by 25% for the department 40, 15% for department 90 and 10% for the department 110 and the rest of the departments will remain same.


Employees table

--------------- \
employee_id  \
first_name    \
last_name    \
email    \ 
phone_number    \
hire_date    \
job_id    \
salary    \
commission_pct  \
manager_id  \  
department_id \

```sql
UPDATE EMPLOYEES
SET salary = CAST(round( salary * CASE department_id
        WHEN 40 THEN 1.25
        WHEN 90 THEN 1.15
        WHEN 110 THEN 1.10
        ELSE 1
    END, 0) AS INT)
where department_id IN (40, 90, 110);
```

**Output:**

<img width="940" height="253" alt="image" src="https://github.com/user-attachments/assets/9959a45c-33a2-4faa-80cc-d3d51596866b" />


**Question 7**
---
Write a SQL statement to Update the reorder level to 20 where the quantity in stock is less than 10 and product category is 'Snacks' in the products table.

Products table

<img width="700" height="102" alt="image" src="https://github.com/user-attachments/assets/29c3ba3a-3189-40ce-8c98-699270820bad" />


```sql
UPDATE products SET reorder_lvl = 20 WHERE quantity < 10 AND category = 'Snacks';
```

**Output:**

<img width="1239" height="333" alt="image" src="https://github.com/user-attachments/assets/c2304c0f-7873-4b61-971f-f3bb6f7a45a7" />


**Question 8**
---
Write a SQL query to categorize decimal as 'High', 'Medium', or 'Low' based on whether it is greater than 100, between 50 and 100, or less than 50 in the Calculations table

```sql
SELECT
    id,
    decimal,
    CASE
        WHEN decimal > 100 THEN 'High'
        WHEN decimal >= 50 THEN 'Medium'
        ELSE 'Low'
    END AS category
FROM Calculations;
```

**Output:**

<img width="610" height="332" alt="image" src="https://github.com/user-attachments/assets/65c0f139-3af0-4db1-9e0d-962ce17103b5" />


**Question 9**
---
Write a SQL query to Delete customers with following conditions

'CUST_COUNTRY' is not in a list of specified countries ('UK', 'USA', 'Canada')
'GRADE' is greater than or equal to 3


```sql
DELETE FROM Customer WHERE CUST_COUNTRY NOT IN ('UK', 'USA', 'Canada') AND GRADE >= 3;
```

**Output:**

<img width="1060" height="253" alt="image" src="https://github.com/user-attachments/assets/5420267e-f4e2-43fa-82a0-4682401a888b" />    \

<img width="1101" height="249" alt="image" src="https://github.com/user-attachments/assets/5538e5dc-d37d-4169-9317-f35f58889bdf" />



**Question 10**
---
Write a SQL query to Delete customers from 'customer' table where 'OPENING_AMT' is between 4000 and 6000.

```sql
DELETE FROM customer WHERE OPENING_AMT BETWEEN 4000 AND 6000;
```

**Output:**

<img width="1056" height="405" alt="image" src="https://github.com/user-attachments/assets/430ced80-5a0f-4ff5-a8fc-d3c5671c08a6" />    \

<img width="1099" height="402" alt="image" src="https://github.com/user-attachments/assets/933d8bb5-77f1-4d1a-941d-0026af420973" />



## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
