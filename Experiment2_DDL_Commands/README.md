# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
Write an SQL Query to add the attributes designation, net_salary, and dob to the Companies table with the following data types:
designation as VARCHAR(50)
net_salary as NUMBER
dob as DATE

```sql
alter table Companies add designation varchar(50);
alter table Companies add net_salary number;
alter table Companies add dob date;
```

**Output:**

<img width="1147" height="224" alt="image" src="https://github.com/user-attachments/assets/9d5fecfb-39b8-49ce-a5d3-2f5d3a479954" />


**Question 2**
---
Insert the below data into the Books table, allowing the Publisher and Year columns to take their default values.

ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

Note: The Publisher and Year columns will use their default values.

```sql
INSERT INTO Books (ISBN, Title, Author) VALUES ('978-6655443321', 'Big Data Analytics', 'Karen Adams');
```

**Output:**

<img width="1113" height="201" alt="image" src="https://github.com/user-attachments/assets/abe0a9c1-7978-4e29-9a2d-920f18168be7" />


**Question 3**
---
Write a SQL query to Add a new ParentsNumber column  as number and Adhar_Number as Number in the Student_details table.

```sql
alter table Student_details add ParentsNumber number;
alter table Student_details add Adhar_Number number;
```

**Output:**

<img width="1171" height="201" alt="image" src="https://github.com/user-attachments/assets/5bfd14fd-1d00-467a-85ed-b7845906fc15" />


**Question 4**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.

```sql
create table item(
    item_id text primary key,
    item_desc text,
    rate integer,
    icom_id text(4),
    foreign key (icom_id) references company(com_id) ON UPDATE SET NULL ON DELETE SET NULL
);
```

**Output:**

<img width="1033" height="179" alt="image" src="https://github.com/user-attachments/assets/6e184cf7-adeb-420f-96b1-35e13d414bba" />


**Question 5**
---
Insert all products from Discontinued_products into Products.
Table attributes are ProductID, ProductName, Price, Stock

```sql
INSERT INTO Products (ProductID, ProductName, Price, Stock)
SELECT ProductID, ProductName, Price, Stock FROM Discontinued_products;
```

**Output:**

<img width="851" height="136" alt="image" src="https://github.com/user-attachments/assets/19768c9c-02d7-449e-8400-8843fdf83235" />


**Question 6**
---
Create a table named Customers with the following columns:

CustomerID as INTEGER
Name as TEXT
Email as TEXT
JoinDate as DATETIME

```sql
CREATE TABLE Customers(
    CustomerID INTEGER,
    Name TEXT,
    Email TEXT,
    JoinDate DATETIME
);
```

**Output:**

<img width="1058" height="160" alt="image" src="https://github.com/user-attachments/assets/e8fad386-9658-4081-a00a-acd686beeb31" />


**Question 7**
---
Create a table named Products with the following constraints:
ProductID as INTEGER should be the primary key.
ProductName as TEXT should be unique and not NULL.
Price as REAL should be greater than 0.
StockQuantity as INTEGER should be non-negative.

```sql
create table Products(
    ProductID integer primary key,
    ProductName text unique not null,
    Price real CHECK (Price>0),
    StockQuantity integer check(StockQuantity > 0)
);
```

**Output:**

<img width="1145" height="102" alt="image" src="https://github.com/user-attachments/assets/d70c99aa-4e77-43fe-a934-97f1b5b3ae0d" />


**Question 8**
---
Create a table named Orders with the following columns:

OrderID as INTEGER
OrderDate as TEXT
CustomerID as INTEGER

```sql
CREATE TABLE Orders(
    OrderID INTEGER,
    OrderDate TEXT,
    CustomerID INTEGER
);
```

**Output:**
<img width="1188" height="203" alt="image" src="https://github.com/user-attachments/assets/511bb59b-76e1-402a-9305-02f69948192c" />


**Question 9**
---
Insert the below data into the Customers table, allowing the City and ZipCode columns to take their default values.

CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St      

Note: The City and ZipCode columns will use their default values.
 

```sql
INSERT INTO Customers (CustomerID, Name, Address) VALUES ('304', 'Peter Parker', 'Spider St');
```

**Output:**

<img width="1001" height="218" alt="image" src="https://github.com/user-attachments/assets/2f4af6ef-da12-4d86-b89e-8680af747a65" />


**Question 10**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.

```sql
create table item(
    item_id text primary key,
    item_desc text,
    rate integer,
    icom_id text(4),
    foreign key (icom_id) references company(com_id) ON UPDATE CASCADE ON DELETE CASCADE
);
```

**Output:**

<img width="1245" height="213" alt="image" src="https://github.com/user-attachments/assets/7f013714-b032-431c-93d7-7f29caa676cc" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
