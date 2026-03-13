# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "salesman_name") and the "cust_name" column from the "customer" table (aliased as "customer_name"), with a left join on the "salesman_id" column.

Customer Table:
<img width="1021" height="171" alt="image" src="https://github.com/user-attachments/assets/62fb0e55-016f-4e96-9f96-2bb7c7443764" />

Salesmen Table:
<img width="1046" height="171" alt="image" src="https://github.com/user-attachments/assets/30968a85-befc-45fc-b7ae-aa139261a6dc" />


```sql
select s.name as "salesman_name" , c.cust_name as "customer_name" from salesman s left join customer c on s.salesman_id = c.salesman_id;
```

**Output:**

<img width="713" height="837" alt="image" src="https://github.com/user-attachments/assets/dacdbb62-28a5-41c2-a530-8fbd9550771a" />


**Question 2**
---
Write the SQL query that achieves the selection of all columns from the "patients" table, with an inner join on the "doctor_id" column, and includes a condition filtering for patients whose doctors have the first name 'John' and last name 'Smith'.

<img width="293" height="496" alt="image" src="https://github.com/user-attachments/assets/6b4b8a32-5c52-4ce3-9661-7a3a084a6ca1" />


```sql
select p.* from patients p inner join doctors d on p.doctor_id = d.doctor_id where d.first_name = 'John' and d.last_name = 'Smith';
```

**Output:**

<img width="1023" height="333" alt="image" src="https://github.com/user-attachments/assets/6ac6e536-c427-420a-a244-333dd62107d3" />

<img width="1016" height="323" alt="image" src="https://github.com/user-attachments/assets/876447f1-e69e-4b5b-ae4a-01c1667e9253" />



**Question 3**
---
Write the SQL query that achieves the selection of the "nurse_id" from the "nurses" table (aliased as "n") and the "department_name" from the "departments" table, with an inner join on the "department_id" column and conditions filtering for a nurse with the first name 'David' and last name 'Moore'.

NURSES TABLE:
<img width="1002" height="166" alt="image" src="https://github.com/user-attachments/assets/c666084f-85f3-4d69-9727-15aa374ef4b1" />

DEPARTMENTS TABLE:
<img width="1017" height="173" alt="image" src="https://github.com/user-attachments/assets/da777da2-f4c7-4f79-a8bf-6cf7af0da224" />


```sql
select n.nurse_id, d.department_name from nurses n inner join departments d on n.department_id = d.department_id where n.first_name = 'David' and n.last_name = 'Moore';
```

**Output:**

<img width="715" height="329" alt="image" src="https://github.com/user-attachments/assets/12c68c86-d554-4168-b5fc-069b515a228f" />


**Question 4**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "appointments" table (aliased as "a"), with an inner join on the "patient_id" column.

<img width="801" height="352" alt="image" src="https://github.com/user-attachments/assets/ee5a4efe-d409-49fd-b48b-71a185f2404e" />


```sql
select patient_name.first_name as "patient_name", a.* from patients as patient_name inner join appointments as a on patient_name.patient_id = a.patient_id;
```

**Output:**

<img width="1211" height="355" alt="image" src="https://github.com/user-attachments/assets/bb4d161b-b475-4255-9284-c01a0deb8dd0" />


**Question 5**
---
Write a SQL statement to make a report with customer name, city, order number, order date, and order amount in ascending order according to the order date to determine whether any of the existing customers have placed an order or not.

<img width="619" height="664" alt="image" src="https://github.com/user-attachments/assets/a9d329bb-8e0a-411d-bb85-139a3dfced71" />


```sql
select c.cust_name, c.city, o.ord_no, o.ord_date, o.purch_amt as "Order Amount" from customer c left join orders o on c.customer_id = o.customer_id order by o.ord_date asc;
```

**Output:**

<img width="1184" height="904" alt="image" src="https://github.com/user-attachments/assets/da94c674-00ce-4165-8f58-460d871bfda5" />


**Question 6**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the city 'London'.

<img width="805" height="356" alt="image" src="https://github.com/user-attachments/assets/c4d51c3c-d161-400f-a53f-93172c47382a" />




```sql
select s.name from salesman s left join customer c on s.salesman_id = c.salesman_id where c.city = 'London';
```

**Output:**

<img width="408" height="402" alt="image" src="https://github.com/user-attachments/assets/d4f8205c-38b6-49e3-abaa-25defaeea60d" />


**Question 7**
---
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.  

<img width="621" height="549" alt="image" src="https://github.com/user-attachments/assets/f58dab5c-c653-4042-b4fa-fab8e5f15fa9" />


```sql
select c.cust_name, c.city, c.grade, s.name as "Salesman", s.city from customer c left join salesman s on c.salesman_id = s.salesman_id order by c.customer_id asc;
```

**Output:**

<img width="1160" height="668" alt="image" src="https://github.com/user-attachments/assets/55388208-aa6a-43a8-ad42-9f038c9dd13c" />


**Question 8**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the test name from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column.

<img width="802" height="345" alt="image" src="https://github.com/user-attachments/assets/5841dbb5-7910-4684-a717-5b1ef304a489" />


```sql
select p.first_name as "patient_name", t.test_name from patients p inner join test_results t on p.patient_id = t.patient_id;
```

**Output:**

<img width="718" height="476" alt="image" src="https://github.com/user-attachments/assets/7063e8ad-1d5a-4633-96d3-cc2f7d4495ff" />


**Question 9**
---
write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

<img width="603" height="550" alt="image" src="https://github.com/user-attachments/assets/eb64f61a-b1bc-4bb2-b95b-833e9bbba16b" />


```sql
SELECT s.name AS "Salesman", c.cust_name, c.city FROM salesman s INNER JOIN customer c ON s.city = c.city;
```

**Output:**

<img width="1021" height="620" alt="image" src="https://github.com/user-attachments/assets/bf75cf40-8f5e-4a14-80e9-a8e9c0a58942" />


**Question 10**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c") and the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the same city as the salesman.

<img width="799" height="353" alt="image" src="https://github.com/user-attachments/assets/64724a2c-3bbd-4e98-b5b2-924bb75d8e26" />


```sql
SELECT 
    c.cust_name, 
    s.name
FROM customer c
LEFT JOIN salesman s 
    ON c.salesman_id = s.salesman_id
WHERE c.city = s.city;
```

**Output:**

<img width="715" height="475" alt="image" src="https://github.com/user-attachments/assets/b2a72f18-5e51-412d-8386-614807e91ae1" />


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
