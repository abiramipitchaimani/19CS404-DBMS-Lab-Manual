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
-- Create a table named Shipments with the following constraints:

    ShipmentID as INTEGER should be the primary key.
    ShipmentDate as DATE.
    SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
    OrderID as INTEGER should be a foreign key referencing Orders(OrderID).


```sql
--CREATE TABLE Shipments
(
ShipmentID INTEGER primary key,
ShipmentDate DATE,
SupplierID INTEGER,
OrderID INTEGER,
FOREIGN KEY(SupplierID) REFERENCES Suppliers(SupplierID),
FOREIGN KEY(OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

![image](https://github.com/user-attachments/assets/4c3755b1-4e7b-4566-b871-136bd41644bf)


**Question 2**
---
--Insert the following customers into the Customers table:

CustomerID  Name         Address     City        ZipCode
----------  -----------  ----------  ----------  ----------
302         Laura Croft  456 Elm St  Seattle     98101
303         Bruce Wayne  789 Oak St  Gotham      10001

```sql
-- INSERT INTO Customers (CustomerID,Name,Address,City,ZipCode)
VALUES
(302,'Laura Croft','456 Elm St','Seattle',98101),
(303,'Bruce Wayne','789 Oak St','Gotham',10001);
```

**Output:**

![image](https://github.com/user-attachments/assets/8e7cbbdb-456c-4e38-a73f-250d43bcec44)


**Question 3**
---
--Write a SQL query to add a column named Date_of_birth as Date in the Student_details table.
```sql
-- ALTER TABLE Student_details
ADD COLUMN Date_of_birth Date;
```

**Output:**

![image](https://github.com/user-attachments/assets/6c2a76f0-703e-49fa-9f15-a88b9c8a4b1d)


**Question 4**
---
-- Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email

```sql
--INSERT INTO Customers (CustomerID, Name, Address, Email)
SELECT CustomerID, Name, Address, Email FROM Old_customers;
```

**Output:**

![image](https://github.com/user-attachments/assets/6a4007f1-6f9f-428e-8cc2-aa131c92e9a3)


**Question 5**
---
-- Write an SQL command can to add a column named email of type TEXT to the customers table

```sql
--ALTER TABLE Customers
ADD COLUMN email TEXT;
```

**Output:**

![image](https://github.com/user-attachments/assets/a4055014-288a-4e4d-a30f-7d5622b3471d)


**Question 6**
---
--Create a table named Invoices with the following constraints:

    InvoiceID as INTEGER should be the primary key.
    InvoiceDate as DATE.
    Amount as REAL should be greater than 0.
    DueDate as DATE should be greater than the InvoiceDate.
    OrderID as INTEGER should be a foreign key referencing Orders(OrderID).


```sql
-- CREATE TABLE Invoices
(
    InvoiceID INTEGER primary key,
    InvoiceDate DATE,
    Amount REAL CHECK(Amount>0),
    DueDate DATE CHECK(DueDate>InvoiceDate),
    OrderID INTEGER,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

![image](https://github.com/user-attachments/assets/30371d25-83df-41c4-ac6c-5f76be3818ea)



**Question 7**
---
--Insert the below data into the Books table, allowing the Publisher and Year columns to take their default values.

ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

Note: The Publisher and Year columns will use their default values.
```sql
--INSERT INTO Books(ISBN,Title,Author)
VALUES('978-6655443321','Big Data Analytics','Karen Adams');
```

**Output:**
![image](https://github.com/user-attachments/assets/05e2a2c3-8496-46dd-8d44-5d085b361505)


**Question 8**
---
-- Create a new table named products with the following specifications:

    product_id as INTEGER and primary key.
    product_name as TEXT and not NULL.
    list_price as DECIMAL (10, 2) and not NULL.
    discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
    A CHECK constraint at the table level to ensure:
        list_price is greater than or equal to discount
        discount is greater than or equal to 0
        list_price is greater than or equal to 0


```sql
--CREATE TABLE products
(
  product_id INTEGER primary key,
  product_name TEXT NOT NULL,
  list_price DECIMAL(10, 2) NOT NULL,
  discount DECIMAL(10, 2) DEFAULT 0 NOT NULL,
  CHECK (list_price>=discount),
  CHECK (discount>=0),
  CHECK (list_price>=0)
);
```

**Output:**

![image](https://github.com/user-attachments/assets/3aeeda95-f9c5-433f-8172-f6f9ac614af4)


**Question 9**
---
--Create a table named Events with the following columns:

    EventID as INTEGER
    EventName as TEXT
    EventDate as DATE

```sql
-- CREATE TABLE Events
(
EventID INTEGER,
EventName TEXT,
EventDate DATE
);
```

**Output:**

![image](https://github.com/user-attachments/assets/e1a46426-9f20-4be7-8a97-f7c8d8d1b886)


**Question 10**
---
-- Create a table named Attendance with the following constraints:

    AttendanceID as INTEGER should be the primary key.
    EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
    AttendanceDate as DATE.
    Status as TEXT should be one of 'Present', 'Absent', 'Leave'.

```sql
--CREATE TABLE Attendance
(
 AttendanceID INTEGER primary key,
 EmployeeID INTEGER,
 AttendanceDate DATE,
 Status TEXT CHECK(Status IN('Present','Absent','Leave')),
 FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);
```

**Output:**

![image](https://github.com/user-attachments/assets/831a7c1a-f7a1-4abf-a827-59010cae7162)




## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
