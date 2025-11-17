# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.

**Program**

      SET SERVEROUTPUT ON;
      
      -- MAIN TABLE
      CREATE TABLE employees (
          emp_id NUMBER,
          emp_name VARCHAR2(50),
          salary NUMBER
      );
      
      -- LOG TABLE
      CREATE TABLE employee_log (
          log_id NUMBER GENERATED ALWAYS AS IDENTITY,
          emp_id NUMBER,
          emp_name VARCHAR2(50),
          salary NUMBER,
          log_time TIMESTAMP
      );
      
      -- TRIGGER
      CREATE OR REPLACE TRIGGER log_employee_insert
      AFTER INSERT ON employees
      FOR EACH ROW
      BEGIN
          INSERT INTO employee_log(emp_id, emp_name, salary, log_time)
          VALUES(:NEW.emp_id, :NEW.emp_name, :NEW.salary, SYSTIMESTAMP);
      END;
      /
      
      -- TEST INSERT
      INSERT INTO employees VALUES (1, 'Arun', 30000);
      
      SELECT * FROM employee_log;


**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.
- <img width="589" height="688" alt="image" src="https://github.com/user-attachments/assets/0afd91e3-12e8-4327-a9fd-3e00d288a641" />


---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

**Program**

      -- TABLE
      CREATE TABLE sensitive_data (
          id NUMBER,
          info VARCHAR2(100)
      );
      
      INSERT INTO sensitive_data VALUES (1, 'Top Secret');
      
      -- TRIGGER
      CREATE OR REPLACE TRIGGER prevent_delete_sensitive
      BEFORE DELETE ON sensitive_data
      BEGIN
          RAISE_APPLICATION_ERROR(-20001, 'ERROR: Deletion not allowed on this table.');
      END;
      /
      
      -- TEST DELETE
      DELETE FROM sensitive_data WHERE id = 1;


**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`
- <img width="740" height="575" alt="image" src="https://github.com/user-attachments/assets/dd042936-932e-4701-8c34-5b0aab33436a" />


---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

**Program**

      -- TABLE
      CREATE TABLE products (
          product_id NUMBER,
          product_name VARCHAR2(50),
          price NUMBER,
          last_modified TIMESTAMP
      );
      
      INSERT INTO products VALUES (1, 'Mouse', 500, NULL);
      
      -- TRIGGER
      CREATE OR REPLACE TRIGGER update_last_modified
      BEFORE UPDATE ON products
      FOR EACH ROW
      BEGIN
          :NEW.last_modified := SYSTIMESTAMP;
      END;
      /
      
      -- TEST UPDATE
      UPDATE products
      SET price = 600
      WHERE product_id = 1;
      
      SELECT * FROM products;


**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.
- <img width="738" height="439" alt="image" src="https://github.com/user-attachments/assets/bbcc3942-b173-468a-83a3-147991c97efe" />


---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

**Program**

      -- MAIN TABLE
      CREATE TABLE customer_orders (
          order_id NUMBER,
          amount NUMBER
      );
      
      INSERT INTO customer_orders VALUES (1, 500);
      
      -- AUDIT TABLE
      CREATE TABLE audit_log (
          update_count NUMBER
      );
      
      INSERT INTO audit_log VALUES (0);
      
      -- TRIGGER
      CREATE OR REPLACE TRIGGER count_updates
      AFTER UPDATE ON customer_orders
      BEGIN
          UPDATE audit_log
          SET update_count = update_count + 1;
      END;
      /
      
      -- TEST UPDATE
      UPDATE customer_orders SET amount = 600 WHERE order_id = 1;
      
      SELECT * FROM audit_log;


**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.
- <img width="531" height="381" alt="image" src="https://github.com/user-attachments/assets/fcc4f75e-008e-4da5-a761-1e097ccb64e7" />


---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

**Program**

      -- TABLE
      CREATE TABLE employees2 (
          emp_id NUMBER,
          emp_name VARCHAR2(50),
          salary NUMBER
      );
      
      -- TRIGGER
      CREATE OR REPLACE TRIGGER check_salary_before_insert
      BEFORE INSERT ON employees2
      FOR EACH ROW
      BEGIN
          IF :NEW.salary < 3000 THEN
              RAISE_APPLICATION_ERROR(-20002, 'ERROR: Salary below minimum threshold.');
          END IF;
      END;
      /
      
      -- TEST INSERT (VALID)
      INSERT INTO employees2 VALUES (1, 'Meera', 5000);
      
      -- TEST INSERT (INVALID)
      INSERT INTO employees2 VALUES (2, 'Kumar', 2000);


**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`
- <img width="730" height="439" alt="image" src="https://github.com/user-attachments/assets/88c46ead-83e4-455c-b254-eb6b7c2d317b" />


## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.

