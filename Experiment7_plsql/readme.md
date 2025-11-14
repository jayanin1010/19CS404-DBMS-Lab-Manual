# Experiment 7: PL/SQL – Variables, Control Structures and Loops

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

**Program:**

      SET SERVEROUTPUT ON;
      
      DECLARE
          a NUMBER := 50;
          b NUMBER := 80;
      BEGIN
          IF a > b THEN
              DBMS_OUTPUT.PUT_LINE('Greater number is: ' || a);
          ELSE
              DBMS_OUTPUT.PUT_LINE('Greater number is: ' || b);
          END IF;
      END;
      /


**Expected Output:**  
Greater number is: 80
<img width="369" height="219" alt="image" src="https://github.com/user-attachments/assets/115f57a5-d19a-43a6-8766-5e100603edc3" />


---

## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.

**Program:**

      SET SERVEROUTPUT ON;
      
      DECLARE
          n   NUMBER := 10;
          i   NUMBER := 1;
          sum NUMBER := 0;
      BEGIN
          WHILE i <= n LOOP
              sum := sum + i;
              i := i + 1;
          END LOOP;
      
          DBMS_OUTPUT.PUT_LINE('Sum of first ' || n || ' natural numbers is: ' || sum);
      END;
      /



**Expected Output:**  
Sum of first 10 natural numbers is: 55
<img width="476" height="330" alt="image" src="https://github.com/user-attachments/assets/13c7f919-ec1b-405f-9717-55e4084f716f" />


---

## 3. Write a PL/SQL program to generate Fibonacci series

### Steps:
- Declare the variable `n` to indicate how many terms to generate.
- Initialize the first two Fibonacci numbers (0 and 1).
- Use a loop to generate the next terms using the formula `c = a + b`.
- Print each term in the series.

**Program:**

      SET SERVEROUTPUT ON;
      
      DECLARE
          n NUMBER := 7;
          a NUMBER := 0;
          b NUMBER := 1;
          c NUMBER;
          i NUMBER := 1;
      BEGIN
          DBMS_OUTPUT.PUT_LINE('Fibonacci sequence:');
      
          WHILE i <= n LOOP
              DBMS_OUTPUT.PUT(a || ' ');
              c := a + b;
              a := b;
              b := c;
              i := i + 1;
          END LOOP;
      END;
      /


**Expected Output:**  
n = 7  
Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8

---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.

**Program:**

      SET SERVEROUTPUT ON;
      
      DECLARE
          n NUMBER := 1535;
          rem NUMBER;
          rev NUMBER := 0;
          temp NUMBER;
      BEGIN
          temp := n;
      
          WHILE temp > 0 LOOP
              rem := MOD(temp, 10);
              rev := rev * 10 + rem;
              temp := FLOOR(temp / 10);
          END LOOP;
      
          DBMS_OUTPUT.PUT_LINE('Reversed number is: ' || rev);
      END;
      /


**Expected Output:**  
n = 1535  
Reversed number is 5351
<img width="438" height="213" alt="image" src="https://github.com/user-attachments/assets/83c7cd58-01fd-4e85-a43e-ff589d1edc71" />


---

## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.

**Program:**

      SET SERVEROUTPUT ON;
      
      DECLARE
          a NUMBER := 10;
          b NUMBER := 9;
          c NUMBER := 15;
          largest NUMBER;
      BEGIN
          IF a > b AND a > c THEN
              largest := a;
          ELSIF b > c THEN
              largest := b;
          ELSE
              largest := c;
          END IF;
      
          DBMS_OUTPUT.PUT_LINE('Largest number is: ' || largest);
      END;
      /


**Expected Output:**  
a = 10, b = 9, c = 15  
Largest of three number is 15
<img width="334" height="158" alt="image" src="https://github.com/user-attachments/assets/ec30eb48-1da3-4798-8c16-fff2081af410" />


## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.

