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
Write a SQL statement to Change the supplier name to 'A1 Suppliers' where the supplier ID is 8 in the suppliers table.

Table info

suppliers(supplier_id,supplier_name,contact_person,phone_number,email,address)

```sql
update suppliers
set supplier_name='A1 Suppliers'
where supplier_id=8;
```

**Output:**

![image](https://github.com/user-attachments/assets/9a8ded14-f3c4-4e05-8b57-e65af1c77353)


**Question 2**
---
Write a SQL statement to Update the reorder level to 20 where the quantity in stock is less than 10 and product category is 'Snacks' in the products table.

Products table


product_id

product_name

category

cost_price

sell_price

reorder_lvl

quantity

supplier_id

![image](https://github.com/user-attachments/assets/bc2dfbe6-48f7-49b0-9afa-834d069050be)


```sql
update Products
set reorder_lvl='20'
where quantity<10 and category='Snacks';
```

**Output:**
![image](https://github.com/user-attachments/assets/ff73a40c-6001-4415-896c-228bbcecd599)



**Question 3**
---
Write a SQL statement to update the product_name as 'Grapefruit' whose product_id is 4 in the products table.

products table



product_id

product_name

category_id

availability

```sql
update products
set product_name='Grapefruit'
where product_id=4;
```

**Output:**

![image](https://github.com/user-attachments/assets/afaa2e45-2af9-40c4-a773-55bfb0229528)



**Question 4**
---
Write a SQL statement to Update the hire_date of employees in department 50 to 2024-01-24.

Employees table


employee_id

first_name

last_name

email

phone_number

hire_date

job_id

salary

commission_pct

manager_id

department_id
```sql
update Employees
set hire_date='2024-01-24'
where department_id=50;
```

**Output:**
![image](https://github.com/user-attachments/assets/3accd3c1-8eee-4077-ae3d-bbe75bff9762)



**Question 5**
---
Update the reorder level to 40 pieces for all products belonging to the 'Grocery' category in the products table.

PRODUCTS TABLE

name               type
----------------  ---------------

product_id         INT

product_name       VARCHAR(100)

category           VARCHAR(50)

cost_price         DECIMAL(10,2)

sell_price         DECIMAL(10,2)

reorder_lvl        INT

quantity           INT

supplier_id        INT
```sql
update PRODUCTS
set reorder_lvl=40
where category='Grocery';
```

**Output:**

![image](https://github.com/user-attachments/assets/c3500396-0e42-4483-b161-521dccc62402)


**Question 6**
---
Write a query to display the unique employee ID from EmployeePosition table who joined in 2024 and have a salary greater than 50000.

EmpID   EmpPosition      	DateOfJoining    Salary

1        Manager          01/05/2024       	500000

2        Executive        02/05/2024        75000

 
```sql
SELECT DISTINCT EmpID FROM EmployeePosition
WHERE strftime('%Y',DateOfJoining)='2024' AND Salary>50000;0
```

**Output:**
![image](https://github.com/user-attachments/assets/acdf50c1-e197-45e1-9c77-30049cce14f7)




**Question 7**
Write a SQL statement to Find those salesmen with all information whose name containing the 1st character is 'N' and the 4th character is 'l' and rests may be any character.

salesman table

cid         name         type        
----------  -----------  ----------  

0           salesman_id  numeric(5)  

1           name         varchar(30)  

2           city         varchar(15)  

3           commission   decimal(5,2)  

```sql
SELECT *
FROM salesman
WHERE name LIKE 'N_i%';
```

**Output:**

![image](https://github.com/user-attachments/assets/ec714e32-8cd2-49cb-abb1-2d3d3bd646ee)



**Question 8**
---
write a SQL query to create a union of two queries that shows the customer id, cities, and ratings of all customers. Those with a rating of 300 or greater will have the words 'High Rating', while the others will have the words 'Low Rating'.

customer table

cid           name          type   notnull       dflt_value  pk
------------  ------------  -----  ------------  ----------  ----------

0             customer_id   int    0                         0

1             cust_name     text   0                         0

2             city          text   0                         0

3             grade         int    0                         0

4             salesman_id   int    0                         0
```sql
SELECT customer_id,city,grade,
'High Rating' AS Rating
FROM customer
WHERE grade>=300
UNION
SELECT customer_id,city,grade,
'Low Rating' AS Rating
FROM customer
WHERE GRADE<300;
```

**Output:**




**Question 9**
---
Write a SQL query to calculate the absolute value of the value1 column from the Calculations table.

cid            name         type         notnull      dflt_value   pk
----------  ----------  ----------  ----------  ----------  ----------

0            id           INTEGER       0                       1

1            value1       REAL         0                       0

2            value2       REAL         0                       0

3            base         INTEGER      0                       0

4            exponent     INTEGER      0                       0

5            number       REAL         0                       0

6            decimal      REAL         0                       0
 
```sql
SELECT id,value1,ABS(value1) AS absolute_value
FROM calculations;
```

**Output:**

![image](https://github.com/user-attachments/assets/32590cc3-3830-4b97-83f5-61504d0aa969)



**Question 10**
---
Write a SQL query to Delete a Specific Surgery whose ID is 3

Sample table: Surgeries

attributes:    surgery_id, patient_id, surgeon_id, surgery_date


```sql
DELETE FROM Surgeries
WHERE surgery_id=3;
```

**Output:**

![image](https://github.com/user-attachments/assets/423eee6d-6755-4d6e-acc3-e06dbbf23137)



## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
