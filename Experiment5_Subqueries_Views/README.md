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
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi and age below 30

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

```sql
select *
from CUSTOMERS
where id in(
select ID from customers
where ADDRESS="Delhi" and AGE<30);
```

**Output:**

![image](https://github.com/user-attachments/assets/a96f21ff-5cb2-431a-863e-0e42176a9320)


**Question 2**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose AGE is LESS than $30

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

```sql
select *
from CUSTOMERS
where age<30

```

**Output:**

![image](https://github.com/user-attachments/assets/e5e3cc3b-ba2a-49b8-9d0e-6c699dde654d)


**Question 3**
---
Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER

```sql
select id,name,city,email,phone
from customer
where city<>(
select city
from customer
where id=(select max(id) from customer));
```

**Output:**

![image](https://github.com/user-attachments/assets/58b754f7-122b-4ddb-ac32-cdac7b4830b7)


**Question 4**
---
From the following tables, write a SQL query to determine the commission of the salespeople in Paris. Return commission.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

customer table

name         type
-----------  ----------
customer_id  int
cust_name    text
city         text
grade        int
salesman_id  int

```sql
select commission
from salesman
where salesman_id in(
select salesman_id from customer
where city='Paris');
```

**Output:**

![image](https://github.com/user-attachments/assets/b44de8b4-e32b-4fb6-beff-13704d232f4b)


**Question 5**
---
Write a SQL query to List departments with names longer than the average length

Departments Table (attributes: department_id, department_name)
![image](https://github.com/user-attachments/assets/32611b58-a65d-4526-a337-eb6ef704b8f2)


```sql
select *
from Departments
where length(department_name)>
(
select avg(length(department_name))
from Departments)
```

**Output:**
![image](https://github.com/user-attachments/assets/ec6e4721-69ab-486f-99d6-c685840fb909)



**Question 6**
---
Write a SQL query to Retrieve the medications with dosages equal to the highest dosage

Table Name: Medications (attributes: medication_id, medication_name, dosage)
![image](https://github.com/user-attachments/assets/1d1728b4-d787-4be4-adf3-398c9f8df269)


```sql
select *
from Medications
where dosage IN(
select max(dosage)
from medications)
```

**Output:**

![image](https://github.com/user-attachments/assets/80f7c6ed-9dc5-4cda-a2c1-78176fe6cdf2)

**Question 7**
---
From the following tables write a SQL query to find salespeople who had more than one customer. Return salesman_id and name.

salesman table

name                 type
---------------   ---------------
salesman_id       numeric(5)
name                  varchar(30)
city                     varchar(15)
commission       decimal(5,2)

customer table

name              type
-----------       ----------
customer_id   int
cust_name     text
city                text
grade            int
salesman_id  int

```sqlselect salesman_id,name
from salesman
where salesman_id IN(
select salesman_id
from customer
group by salesman_Id
having count(customer_id)>1)
```

**Output:**

![image](https://github.com/user-attachments/assets/07ce649b-3d5c-4151-b269-5bc0087af9dd)


**Question 8**
---
Write a SQL query to Retrieve the names of customers who have a phone number that is not shared with any other customer.

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER

```sql
select name
from customer
where phone is NOT NULL
AND phone IN(
select phone
from customer
group by phone
having count(*)=1
);
```

**Output:**
![image](https://github.com/user-attachments/assets/817b3888-0bb9-4087-b346-e68d7263acc3)



**Question 9**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

![image](https://github.com/user-attachments/assets/d274709a-dec4-4f17-b3bd-aafa0a89480c)


```sql
select student_name,grade
from grades g1
where grade=(select MIN(grade)
from grades g2
where g2.subject=g1.subject)
```

**Output:**
![image](https://github.com/user-attachments/assets/9f8aa09a-f97a-44fc-8d35-5a396ab29627)


**Question 10**
---
From the following tables, write a SQL query to find all orders generated by the salespeople who may work for customers whose id is 3007. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

Table Name: orders

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int

```sql
select ord_no, purch_amt, ord_date, customer_id, salesman_id
from orders 
where salesman_id IN(
select salesman_id
from orders
where customer_id=3007);
```

**Output:**

![image](https://github.com/user-attachments/assets/9a42e574-b995-4e94-8995-3c840a4cea1d)



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
