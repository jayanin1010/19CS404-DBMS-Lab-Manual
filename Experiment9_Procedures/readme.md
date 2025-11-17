# Experiment 9: PL/SQL – Procedures and Functions

## AIM
To understand and implement procedures and functions in PL/SQL for performing various operations such as calculations, decision-making, and looping.

---

## THEORY

PL/SQL (Procedural Language/SQL) extends SQL by adding procedural constructs like variables, conditions, loops, procedures, and functions. Procedures and functions are subprograms that help modularize the code and improve reusability.

### **Procedure**
A PL/SQL **procedure** is a subprogram that performs a specific action. It does not return a value directly but can return values using `OUT` parameters.

**Syntax:**
```sql
CREATE OR REPLACE PROCEDURE procedure_name (parameters)
IS
BEGIN
   -- statements
END;
```

To call the procedure

```sql
EXEC procedure_name(arguments);
```

### **Function**
A PL/SQL **function** is a subprogram that returns a single value using the RETURN keyword.

```sql
CREATE OR REPLACE FUNCTION function_name (parameters)
RETURN datatype
IS
BEGIN
   -- statements
   RETURN value;
END;
```

To call the function:

```sql
SELECT function_name(arguments) FROM DUAL;
```

Key Differences:

-A procedure does not return a value, whereas a function must return a value.
-Functions can be called from SQL queries, procedures cannot (in most cases).

## 1. Write a PL/SQL Procedure to Find the Square of a Number

### Steps:
- Create a procedure named `find_square`.
- Declare a parameter to accept a number.
- Inside the procedure, compute the square of the input number.
- Use `DBMS_OUTPUT.PUT_LINE` to display the result.
- Call the procedure with a number as input.

**Program**

      SET SERVEROUTPUT ON;
      
      CREATE OR REPLACE PROCEDURE find_square(n IN NUMBER)
      IS
          sq NUMBER;
      BEGIN
          sq := n * n;
          DBMS_OUTPUT.PUT_LINE('Square of ' || n || ' is ' || sq);
      END;
      /
      
      -- CALL THE PROCEDURE
      BEGIN
          find_square(6);
      END;
      /


**Expected Output:**  
Square of 6 is 36
<img width="259" height="131" alt="image" src="https://github.com/user-attachments/assets/473afdab-468e-4572-851d-ff7cfc3c8eae" />


---

## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- Create a function named `get_factorial`.
- Declare a parameter to accept a number.
- Use a loop to calculate the factorial.
- Return the result using the `RETURN` statement.
- Call the function using a `SELECT` statement or in an anonymous block.

**Program**

      SET SERVEROUTPUT ON;
      
      CREATE OR REPLACE FUNCTION get_factorial(n IN NUMBER)
      RETURN NUMBER
      IS
          fact NUMBER := 1;
          i NUMBER;
      BEGIN
          FOR i IN 1..n LOOP
              fact := fact * i;
          END LOOP;
      
          RETURN fact;
      END;
      /
      
      -- CALL THE FUNCTION
      DECLARE
          x NUMBER;
      BEGIN
          x := get_factorial(5);
          DBMS_OUTPUT.PUT_LINE('Factorial of 5 is ' || x);
      END;
      /


**Expected Output:**  
Factorial of 5 is 120
<img width="567" height="296" alt="image" src="https://github.com/user-attachments/assets/f02df78a-bbbd-43e2-b229-298beff12c99" />


---

## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- Create a procedure named `check_even_odd`.
- Accept an input parameter.
- Use the `MOD` function to check if the number is divisible by 2.
- Display whether it is Even or Odd using `DBMS_OUTPUT.PUT_LINE`.

**Program**

      SET SERVEROUTPUT ON;
      
      CREATE OR REPLACE PROCEDURE check_even_odd(n IN NUMBER)
      IS
      BEGIN
          IF MOD(n, 2) = 0 THEN
              DBMS_OUTPUT.PUT_LINE(n || ' is Even');
          ELSE
              DBMS_OUTPUT.PUT_LINE(n || ' is Odd');
          END IF;
      END;
      /
      
      -- CALL THE PROCEDURE
      BEGIN
          check_even_odd(12);
      END;
      /


**Expected Output:**  
12 is Even
<img width="405" height="201" alt="image" src="https://github.com/user-attachments/assets/f08da2c5-5e40-4251-bceb-2365323ec4cd" />


---

## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- Create a function named `reverse_number`.
- Accept an input number as parameter.
- Use a loop to reverse the digits of the number.
- Return the reversed number.
- Call the function and display the output.

**Program**

      SET SERVEROUTPUT ON;
      
      CREATE OR REPLACE FUNCTION reverse_number(n IN NUMBER)
      RETURN NUMBER
      IS
          rev NUMBER := 0;
          temp NUMBER := n;
      BEGIN
          WHILE temp > 0 LOOP
              rev := rev * 10 + MOD(temp, 10);
              temp := FLOOR(temp / 10);
          END LOOP;
      
          RETURN rev;
      END;
      /
      
      -- CALL FUNCTION
      DECLARE
          ans NUMBER;
      BEGIN
          ans := reverse_number(1234);
          DBMS_OUTPUT.PUT_LINE('Reversed number of 1234 is ' || ans);
      END;
      /


**Expected Output:**  
Reversed number of 1234 is 4321
<img width="422" height="199" alt="image" src="https://github.com/user-attachments/assets/55a00034-dd61-4ded-8aec-11989b5b6072" />


---

## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

### Steps:
- Create a procedure named `print_table`.
- Accept an input number.
- Use a loop from 1 to 10 to multiply the input number.
- Display the multiplication results using `DBMS_OUTPUT.PUT_LINE`.

**Program**

      SET SERVEROUTPUT ON;
      
      CREATE OR REPLACE PROCEDURE print_table(n IN NUMBER)
      IS
      BEGIN
          DBMS_OUTPUT.PUT_LINE('Multiplication Table of ' || n || ':');
      
          FOR i IN 1..10 LOOP
              DBMS_OUTPUT.PUT_LINE(n || ' x ' || i || ' = ' || (n * i));
          END LOOP;
      END;
      /
      
      -- CALL PROCEDURE
      BEGIN
          print_table(5);
      END;
      /



**Expected Output:**  
Multiplication table of 5:  
5 x 1 = 5  
5 x 2 = 10  
5 x 3 = 15  
...  
5 x 10 = 50
<img width="484" height="394" alt="image" src="https://github.com/user-attachments/assets/ecf087ae-3d21-4733-9087-8f9e1136d77b" />


## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.
