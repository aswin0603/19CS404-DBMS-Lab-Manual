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

<img width="267" height="227" alt="image" src="https://github.com/user-attachments/assets/793d9bd1-667b-487d-9f9a-0c161f88c964" />



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

<img width="705" height="361" alt="image" src="https://github.com/user-attachments/assets/718072b6-de98-4898-ad61-a17e310ffb95" />



**Question 3**
---
Write a SQL query to Retrieve the names of customers who have a phone number that is not shared with any other customer.

<img width="270" height="217" alt="image" src="https://github.com/user-attachments/assets/3f5b043d-f7f7-40ce-9610-7e22aed2dfbe" />



```sql
select name from customer where phone in (
select phone from customer group by phone having count(*)=1);
```

**Output:**

<img width="404" height="380" alt="image" src="https://github.com/user-attachments/assets/247fada1-ac2c-4729-b67a-40bb5164a094" />



**Question 4**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $4500.

<img width="456" height="315" alt="image" src="https://github.com/user-attachments/assets/5e5c4507-30a0-4b25-a729-82d3b254416d" />



```sql
SELECT * FROM CUSTOMERS 
WHERE SALARY > 4500;
```

**Output:**

<img width="1191" height="371" alt="image" src="https://github.com/user-attachments/assets/85a8318f-080f-401c-a123-b7f364c04161" />



**Question 5**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 1 million

<img width="241" height="295" alt="image" src="https://github.com/user-attachments/assets/97525741-8897-42be-9445-51c130f3ad9c" />



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

<img width="1099" height="269" alt="image" src="https://github.com/user-attachments/assets/ff4ee007-864d-4f6e-be75-6c6baeb46e97" />



**Question 6**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES

<img width="602" height="233" alt="image" src="https://github.com/user-attachments/assets/23aabc16-bca8-4866-8fd8-7883cbc36c28" />



```sql
SELECT student_name, grade 
FROM GRADES g 
WHERE grade = (SELECT MIN(grade) FROM GRADES WHERE subject = g.subject);
```

**Output:**

<img width="575" height="295" alt="image" src="https://github.com/user-attachments/assets/91f2dcd8-daa8-42ce-9b17-3ac3b6f0a412" />



**Question 7**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi

<img width="376" height="253" alt="image" src="https://github.com/user-attachments/assets/079df394-7b82-474e-9f24-8da25eed4ea9" />



```sql
SELECT * FROM CUSTOMERS WHERE ADDRESS = 'Delhi';
```

**Output:**

<img width="955" height="213" alt="image" src="https://github.com/user-attachments/assets/409bdc25-dda5-477a-8b37-f3dde8e2c98e" />



**Question 8**
---
Write a query to display all the customers whose ID is the difference between the salesperson ID of Mc Lyon and 2001.

<img width="223" height="353" alt="image" src="https://github.com/user-attachments/assets/31d39800-3bcf-4570-9691-74b35e3a98ad" />



```sql
select * from customer where customer_id=(
select salesman_id-2001 from salesman where name='Mc Lyon');
```

**Output:**

<img width="1007" height="196" alt="image" src="https://github.com/user-attachments/assets/de6a5a33-3594-4085-8d57-6666b2ddff74" />



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



```sql
select o.ord_no,o.purch_amt,ord_date,o.customer_id,o.salesman_id from orders o join salesman s on o.salesman_id=s.salesman_id where s.name='Paul Adam';
```

**Output:**

<img width="1103" height="281" alt="image" src="https://github.com/user-attachments/assets/ad5d3bf1-566e-455f-8501-28718d895033" />




## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
