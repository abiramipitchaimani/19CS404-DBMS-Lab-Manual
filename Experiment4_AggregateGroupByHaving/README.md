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
How many doctors specialize in each medical specialty?

Sample table:Doctors Table
![image (4)](https://github.com/user-attachments/assets/50622837-bd89-47d4-81ff-7fcc0b1a80af)



```sql
SELECT Specialty,COUNT(*) AS TotalDocto
FROM Doctors
GROUP BY Specialty
```

**Output:**

![image](https://github.com/user-attachments/assets/d54319fb-24e6-4c5a-91dd-eae3620f220e)


**Question 2**
---
What is the total number of appointments scheduled by each doctor?

Sample table:Appointments Table
![image (5)](https://github.com/user-attachments/assets/58757848-2b52-46c0-adc1-7d98d237bc44)

```sql
SELECT DoctorID,COUNT(AppointmentID) AS TotalAppointments
FROM Appointments
GROUP BY DoctorID
```

**Output:**

![image](https://github.com/user-attachments/assets/844b17e7-a9f7-4753-91c6-0dae671f40c4)


**Question 3**
---
How many patients are covered by each insurance company?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
ValidityPeriod     TEXT

```sql
SELECT InsuranceCompany,COUNT(PatientID) AS TotalPatients
FROM Insurance
GROUP BY InsuranceCompany
```

**Output:**

![image](https://github.com/user-attachments/assets/e3f7ea8b-6591-45c3-98d3-8e1a8101d2fc)


**Question 4**
---
Write a SQL query to  find the average salary of all employees?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER

```sql
SELECT AVG(income) AS Average_Salary
FROM employee
```

**Output:**

![image](https://github.com/user-attachments/assets/67479fb9-c38c-4ccc-820c-5d0b8458cf3b)


**Question 5**
---
Write a SQL query to find the youngest employee in the company?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER

```sql
SELECT name AS Employee_Name,MIN(age) AS Age
FROM employee
```

**Output:**

![image](https://github.com/user-attachments/assets/2099e0bd-a7f5-49cd-9fa3-33bd822d497f)


**Question 6**
---
Write a SQL query to find the Fruit with the lowest available quantity.

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL

```sql
SELECT name AS fruit_name,MIN(inventory) AS lowest_quantity
FROM fruits
```

**Output:**

![image](https://github.com/user-attachments/assets/a973a36e-e5d4-47d6-810d-e425e459e368)


**Question 7**
---
Write a SQL query to find the minimum purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

```sql
SELECT MIN(purch_amt) AS MINIMUM
FROM orders
```

**Output:**

![image](https://github.com/user-attachments/assets/06d59419-9d2b-40e2-a7b9-0d9176ad99ad)

**Question 8**
---
Write the SQL query that accomplishes the grouping of data by age, calculates the average income for each age group, and includes only those age groups where the average income falls between 300,000 and 500,000.

Sample table: employee
![unnamed](https://github.com/user-attachments/assets/e5ba9903-7b2e-49e1-98e3-b7f80c06b18c)


```sql
SELECT age,AVG(income) AS "AVG(income)"
FROM employee
GROUP BY age
HAVING  AVG(income) BETWEEN 300000 AND 500000;
```

**Output:**

![image](https://github.com/user-attachments/assets/bd722ca2-5666-4b26-a7b0-0ef56460dbe6)


**Question 9**
---
Write the SQL query that performs grouping by age groups and displays the maximum salary for each group, excluding groups where the maximum salary is not greater than 8000. 

Note: Calculate the age group as multiples of 5.

Eg., 20,22,23 comes in age group 20. 

25,27,29 comes in age group 25.

Sample table: customer1
![unnamed](https://github.com/user-attachments/assets/cfc79f7e-4099-4f6c-875e-e82168bd3f89)


```sql
SELECT (age/5)*5 AS age_group ,MAX(salary) AS "MAX(salary)" 
FROM customer1
GROUP BY age_group
HAVING MAX(salary)>8000;
```

**Output:**

![image](https://github.com/user-attachments/assets/6b8073b6-ec88-4041-a316-7a5fe503a211)


**Question 10**
---
Write the SQL query that accomplishes the selection of product which has lowest price in each category from the "products" table and includes only those products where the minimum price is less than 10.

Sample table: products
![unnamed](https://github.com/user-attachments/assets/960d4ad2-16c0-4016-a7f9-2be9713115a8)


```sql
SELECT category_id,MIN(price) AS Price
FROM products
GROUP BY category_id
HAVING PRICE<10;
```

**Output:**

![image](https://github.com/user-attachments/assets/13a2b31c-8470-4d30-b00e-6e76aee0d330)


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
