# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
Write a SQL query to return the total number of rows in the 'customer' table where the city is Noida.

Sample table: customer

<img width="668" height="138" alt="image" src="https://github.com/user-attachments/assets/7a063807-8b7b-4bed-9ac5-c9f84ebc9a69" />


```sql
SELECT COUNT(*) AS COUNT FROM customer WHERE city = 'Noida';
```

**Output:**

<img width="241" height="177" alt="image" src="https://github.com/user-attachments/assets/22615eec-08fb-4d55-89d8-409d17b2b159" />

**Question 2**
---
Write a SQL query to find the number of employees who are having the same age removing the duplicate values.

```sql
SELECT COUNT(DISTINCT age) AS COUNT FROM employee;
```

**Output:**

<img width="254" height="180" alt="image" src="https://github.com/user-attachments/assets/7bef38c9-3f27-4b10-ba3f-823317ca14fd" />


**Question 3**
---
Write a SQL query to Calculate the average income of the employees with names starting with 'A': 

```sql
SELECT AVG(income) AS avg_income FROM employee WHERE name LIKE 'A%';
```

**Output:**

<img width="253" height="185" alt="image" src="https://github.com/user-attachments/assets/778f51d4-ce14-4c47-874c-930666c2f344" />


**Question 4**
---
How many doctors specialize in each medical specialty?

Sample table:Doctors Table

<img width="1039" height="162" alt="image" src="https://github.com/user-attachments/assets/30d3654b-d573-4226-a347-9e5d2e18dab5" />


```sql
SELECT Specialty, COUNT(DoctorID) AS TotalDoctors FROM Doctors GROUP BY Specialty;
```

**Output:**

<img width="508" height="464" alt="image" src="https://github.com/user-attachments/assets/8386641a-167f-4729-8859-8d8f3714267f" />


**Question 5**
---
How many appointments are scheduled for each patient?

Sample table: Appointments Table

```sql
SELECT PatientID, COUNT(*) AS TotalAppointments FROM Appointments GROUP BY PatientID;
```

**Output:**

<img width="510" height="424" alt="image" src="https://github.com/user-attachments/assets/1ca69262-8164-4920-9269-9fd14767dd31" />


**Question 6**
---
How many medical records does each doctor have?

Sample table:MedicalRecords Table

<img width="1089" height="164" alt="image" src="https://github.com/user-attachments/assets/8fb7e5c5-e92d-416d-b05c-0e019d13c500" />


```sql
SELECT DoctorID, COUNT(RecordID) AS TotalRecords FROM MedicalRecords GROUP BY DoctorID;
```

**Output:**

<img width="434" height="419" alt="image" src="https://github.com/user-attachments/assets/c3128393-e502-4cb4-adab-3aa774f950c9" />


**Question 7**
---
Write the SQL query that accomplishes the selection of total number of products for each category from the "products" table, and includes only those products where the minimum category ID is less than 3.

Sample table: products

```sql
SELECT category_id, COUNT(product_name) AS "count(product_name)" FROM products GROUP BY category_id HAVING MIN(category_id) < 3;
```

**Output:**

<img width="549" height="221" alt="image" src="https://github.com/user-attachments/assets/5b14e23e-ccbe-470d-b0b9-26fa94a83656" />


**Question 8**
---
Write the SQL query that achieves the grouping of data by occupation, calculates the minimum work hours for each occupation, and excludes occupations where the minimum work hour is not greater than 8.

Sample table: employee1

<img width="1031" height="203" alt="image" src="https://github.com/user-attachments/assets/dbad6f6e-05fa-4d46-b62f-a60acf2f8233" />


```sql
SELECT occupation, MIN(workhour) FROM employee1 GROUP BY occupation HAVING MIN(workhour) > 8;
```

**Output:**

<img width="447" height="314" alt="image" src="https://github.com/user-attachments/assets/e2689b9d-0cb8-46a4-81fa-46e8c5ff63f6" />


**Question 9**
---
Write a SQL query to find the average length of email addresses (in characters):


```sql
select avg(length(email)) as "avg_email_length" from customer;
```

**Output:**

<img width="431" height="240" alt="image" src="https://github.com/user-attachments/assets/03a4e5ed-7288-4a31-b5ea-d8d4945dcf1f" />


**Question 10**
---
Write the SQL query that accomplishes the grouping of data by addresses, calculates the sum of salaries for each address, and excludes addresses where the total salary sum is not greater than 2000.

Sample table: customer1

<img width="992" height="173" alt="image" src="https://github.com/user-attachments/assets/4127719f-3951-461d-8d6b-2ddb4e643910" />


```sql
SELECT address, SUM(salary) FROM customer1 GROUP BY address HAVING SUM(salary) > 2000;
```

**Output:**

<img width="423" height="311" alt="image" src="https://github.com/user-attachments/assets/24bb2269-b4dc-4b6d-9c0e-73b813c40381" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
