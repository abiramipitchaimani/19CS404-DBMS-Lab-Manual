# Experiment 6: PL/SQL – Variables, Control Structures and Loops

## AIM
To write and execute simple PL/SQL programs using variables, loops, and conditional statements.


## THEORY

PL/SQL, which stands for Procedural Language extensions to the Structured Query Language (SQL). It is a combination of SQL along with the procedural features of programming languages.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:
- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

# PL/SQL Programs – Steps and Expected Output

## 1. Write a PL/SQL program to find the Greatest of Two Numbers

### Steps:
- Declare two numeric variables and initialize them.
- Use an `IF` statement to compare the values.
- Display the greater number using `DBMS_OUTPUT.PUT_LINE`.

### Program:
DECLARE
   num1 NUMBER := 45;  -- You can change these values
   num2 NUMBER := 80;
BEGIN
   IF num1 > num2 THEN
      DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num1);
   ELSE
      DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num2);
   END IF;
END;


**Expected Output:**  
Greater number is: 80
## RESULT
![image](https://github.com/user-attachments/assets/dad07bd6-ffe5-4dc5-94f7-1677cd9de09f)

---

## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.

### Program:
DECLARE
   n NUMBER := 10;       
   sum NUMBER := 0;
   i   NUMBER := 1;
BEGIN
   WHILE i <= n LOOP
      sum := sum + i;
      i := i + 1;
   END LOOP;

   DBMS_OUTPUT.PUT_LINE('Sum of first ' || n || ' natural numbers is: ' || sum);
END;
**Expected Output:**  
Sum of first 10 natural numbers is: 55
## RESULT
![image](https://github.com/user-attachments/assets/2b0dc07e-4303-4803-bfc5-e9679fa633d0)

---

## 3. Write a PL/SQL program to generate Fibonacci series

### Steps:
- Declare the variable `n` to indicate how many terms to generate.
- Initialize the first two Fibonacci numbers (0 and 1).
- Use a loop to generate the next terms using the formula `c = a + b`.
- Print each term in the series.

### Program:
DECLARE
    n NUMBER := 7; -- number of terms to generate
    a NUMBER := 0;
    b NUMBER := 1;
    c NUMBER;
    i NUMBER := 1;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Fibonacci sequence:');
    WHILE i <= n LOOP
        IF i = 1 THEN
            DBMS_OUTPUT.PUT(a);
        ELSIF i = 2 THEN
            DBMS_OUTPUT.PUT(', ' || b);
        ELSE
            c := a + b;
            DBMS_OUTPUT.PUT(', ' || c);
            a := b;
            b := c;
        END IF;
        i := i + 1;
    END LOOP;
    DBMS_OUTPUT.NEW_LINE;
END;
**Expected Output:**  
n = 7  
Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8
## RESULT
![image](https://github.com/user-attachments/assets/c09859b9-2eb1-4045-8db2-7d5bd151bbd8)

---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.

### Program:
DECLARE
   n NUMBER := 1535;         
   reversed NUMBER := 0;
   remainder NUMBER;
   original NUMBER := 1535;  
BEGIN
   WHILE n > 0 LOOP
      remainder := MOD(n, 10);           
      reversed := (reversed * 10) + remainder;  
      n := TRUNC(n / 10);                 
   END LOOP;

   DBMS_OUTPUT.PUT_LINE('n = ' || original);
   DBMS_OUTPUT.PUT_LINE('Reversed number is ' || reversed);
END;

**Expected Output:**  
n = 1535  
Reversed number is 5351
## RESULT
![image](https://github.com/user-attachments/assets/b87a937c-147a-47e8-a37e-0ecf4c3d3ea1)

---

## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.

### Program:
DECLARE
   a NUMBER := 10;
   b NUMBER := 9;
   c NUMBER := 15;
   largest NUMBER;
BEGIN
   IF (a >= b) AND (a >= c) THEN
      largest := a;
   ELSIF (b >= a) AND (b >= c) THEN
      largest := b;
   ELSE
      largest := c;
   END IF;

   DBMS_OUTPUT.PUT_LINE('a = ' || a || ', b = ' || b || ', c = ' || c);
   DBMS_OUTPUT.PUT_LINE('Largest of three numbers is ' || largest);
END;
**Expected Output:**  
a = 10, b = 9, c = 15  
Largest of three number is 15
## RESULT
![image](https://github.com/user-attachments/assets/a91ea58b-c5be-49b2-8517-851e5f83467d)

### RESULT:
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.
