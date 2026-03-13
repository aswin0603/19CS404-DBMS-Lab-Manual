# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

<img width="265" height="221" alt="image" src="https://github.com/user-attachments/assets/54c24a55-0b02-4b11-ba65-82cf946ac742" />


```sql
SELECT name, city
FROM customer
WHERE city IN (
    SELECT city
    FROM customer
    WHERE id IN (3, 7)
);
```

**Output:**

<img width="547" height="384" alt="image" src="https://github.com/user-attachments/assets/4cfa211b-d9e4-4d9a-a5d6-6e6d6fbf1f19" />


**Question 2**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES

<img width="602" height="233" alt="image" src="https://github.com/user-attachments/assets/1c51e911-e436-48ed-a5bd-ed2ee1e6cdaf" />


```sql
select student_name,grade from GRADES g where grade =(
select MAX(grade) from GRADES where subject=g.subject);
```

**Output:**

<img width="258" height="213" alt="image" src="https://github.com/user-attachments/assets/60e1eda1-829a-4c5b-8d09-b00209069531" />


**Question 3**
---
Write a SQL query to Retrieve the names of customers who have a phone number that is not shared with any other customer.

<img width="407" height="382" alt="image" src="https://github.com/user-attachments/assets/3ff5e433-18d4-4086-a59d-87c75543756a" />


```sql
select name from customer where phone in (
select phone from customer group by phone having count(*)=1);
```

**Output:**

<img width="440" height="313" alt="image" src="https://github.com/user-attachments/assets/d966db1e-6c9f-4565-a6fd-9ee0a3b7744c" />


**Question 4**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $4500.

<img width="1190" height="366" alt="image" src="https://github.com/user-attachments/assets/16289e49-d02b-423b-b71d-b33a5a6f5e83" />


```sql
SELECT * FROM CUSTOMERS 
WHERE SALARY > 4500;
```

**Output:**

<img width="264" height="294" alt="image" src="https://github.com/user-attachments/assets/2d3a7ef7-9f2b-4df6-babd-2ecb61bbdf6e" />


**Question 5**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 1 million

<img width="723" height="364" alt="image" src="https://github.com/user-attachments/assets/90691936-39bc-4aa6-be3e-5612c3d7bed0" />


```sql
SELECT *
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 1000000
);
```

**Output:**

<img width="602" height="233" alt="image" src="https://github.com/user-attachments/assets/4ea3a6eb-f66b-43c9-9908-5cf1545bb10f" />


**Question 6**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES

<img width="719" height="366" alt="image" src="https://github.com/user-attachments/assets/6217025c-dbae-41cf-b56f-3a4eddf84c82" />


```sql
SELECT student_name, grade 
FROM GRADES g 
WHERE grade = (SELECT MIN(grade) FROM GRADES WHERE subject = g.subject);
```

**Output:**

<img width="443" height="317" alt="image" src="https://github.com/user-attachments/assets/509609ff-e93c-47b9-af92-94a270228a9d" />


**Question 7**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi

<img width="1181" height="264" alt="image" src="https://github.com/user-attachments/assets/66a10d2f-bf02-4049-8edc-43a213cd59be" />


```sql
SELECT * FROM CUSTOMERS WHERE ADDRESS = 'Delhi';
```

**Output:**

<img width="263" height="425" alt="image" src="https://github.com/user-attachments/assets/58fdc82d-cf0b-46b4-b789-1af4cc4d1208" />


**Question 8**
---
Write a query to display all the customers whose ID is the difference between the salesperson ID of Mc Lyon and 2001.

<img width="1129" height="215" alt="image" src="https://github.com/user-attachments/assets/424af75e-7c7a-4d74-80f6-f5e13113e703" />


```sql
select * from customer where customer_id=(
select salesman_id-2001 from salesman where name='Mc Lyon');
```

**Output:**

<img width="247" height="294" alt="image" src="https://github.com/user-attachments/assets/a3f99d0b-65b2-417c-9714-e8a59ded94bb" />


**Question 9**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh

<img width="440" height="141" alt="image" src="https://github.com/user-attachments/assets/42aef0cc-4710-4547-a446-adb19821686e" />


```sql
SELECT * FROM Employee WHERE age<(SELECT AVG(age) FROM Employee WHERE income>250000);
```

**Output:**

<img width="1221" height="393" alt="image" src="https://github.com/user-attachments/assets/11346e82-c1b3-43c8-a7d5-b3fbdfddf725" />


**Question 10**
---
From the following tables, write a SQL query to find all the orders issued by the salesman 'Paul Adam'. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

<img width="558" height="141" alt="image" src="https://github.com/user-attachments/assets/8f7f1bf5-757d-4fd8-a36f-c9713016dafd" />

<img width="1101" height="283" alt="image" src="https://github.com/user-attachments/assets/ac58127d-974a-4ecf-b457-242594afc086" />



```sql
select o.ord_no,o.purch_amt,ord_date,o.customer_id,o.salesman_id from orders o join salesman s on o.salesman_id=s.salesman_id where s.name='Paul Adam';
```

**Output:**

![Uploading image.png…]()



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
