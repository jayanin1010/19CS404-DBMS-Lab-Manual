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
      Write a SQL statement to change the email column of employees table with 'Unavailable' for all employees in employees table.
      
      Employees table
      
      ---------------
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
       
      
      For example:
      
      Test	Result
      SELECT EMPLOYEE_ID,FIRST_NAME,EMAIL FROM EMPLOYEES LIMIT 2;
      EMPLOYEE_ID  FIRST_NAME  EMAIL
      -----------  ----------  -----------
      100          Steven      Unavailable
      101          Neena       Unavailable


```sql
UPDATE employees SET email='Unavailable';
```

**Output:**

<img width="1223" height="383" alt="image" src="https://github.com/user-attachments/assets/8914df21-1632-4d92-a6cb-bd96247050ae" />


**Question 2**
---
    Write a SQL statement to Update the address to '58 Lakeview, Magnolia' where supplier ID is 5 in the suppliers table.
    
    Suppliers Table 
    
    name               type
    -----------------  ---------------
    supplier_id        INT
    supplier_name      VARCHAR(100)
    contact_person     VARCHAR(100)
    phone_number       VARCHAR(20)
    email              VARCHAR(100)
    address            VARCHAR(250)
    For example:
    
    Test	Result
    select changes();
    changes()
    ----------
    1


```sql
UPDATE Suppliers SET address='58 Lakeview, Magnolia' WHERE supplier_id=5;
```

**Output:**

<img width="1316" height="172" alt="image" src="https://github.com/user-attachments/assets/35c89591-0019-4b9a-8546-6e77f5ed0020" />


**Question 3**
---
    Write a SQL statement to Increase the selling price by 10% for all products in the 'Bakery' category in the products table.
    
    Products table
    
    ---------------
    product_id
    product_name
    category
    cost_price
    sell_price
    reorder_lvl
    quantity
    supplier_id

```sql
UPDATE Products SET sell_price=sell_price*1.10 WHERE category='Bakery';
```

**Output:**

<img width="1874" height="348" alt="image" src="https://github.com/user-attachments/assets/ac1b3997-7100-478a-83e0-7f53869982f1" />


**Question 4**
---
     Update the total selling price to quantity sold multiplied by updated selling price per unit where product id is 10 in the sales table.
    
    SALES TABLE
    name               type
    -----------------  ---------------
    sale_id            INT
    sale_date          DATE
    product_id         INT
    quantity           INT
    sell_price         DECIMAL(10,2)
    total_sell_price   DECIMAL(10,2)
    For example:
    
    Test	Result
    select changes();
    changes()
    ----------
    3


```sql
UPDATE SALES SET total_sell_price=quantity*sell_price WHERE sale_id IN (10,11,12);
```

**Output:**

<img width="1522" height="379" alt="image" src="https://github.com/user-attachments/assets/4883117c-7b16-41e3-bc80-5aca9491bdc6" />


**Question 5**
---
    Write a SQL query to reduce the reorder level by 30% where cost price is more than 50 and quantity in stock is less than 100 in the products table.
    
    Products Table 
    
    name          type       
    ----------    ---------- 
    product_id     INT PRIMARY KEY        
    product_name   VARCHAR(10) 
    category       VARCHAR(50) 
    cost_price     DECIMAL(10) 
    sell_price     DECIMAL(10) 
    reorder_lvl    INT        
    quantity       INT        
    supplier_id    INT               
    For example:
    
    Test	Result
    --pragma table_info('products');
    select changes();
    changes()
    ----------
    2


```sql
UPDATE Products SET reorder_lvl=reorder_lvl*0.70 WHERE cost_price>50 AND quantity<100;
```

**Output:**
<img width="1719" height="320" alt="image" src="https://github.com/user-attachments/assets/7f0dce43-f2e8-444b-8867-86736eebe81f" />


**Question 6**
---
    Write a SQL query to Delete All Doctors whose ID ranges from 2 to 4.
    
    Sample table: Doctors
    
    attributes : doctor_id, first_name, last_name, specialization
    For example:
    
    Test	Result
    SELECT * FROM doctors;
    doctor_id   first_name  last_name   specialization
    ----------  ----------  ----------  --------------
    1           John        Smith       Cardiology
    2           Emily       Johnson     Orthopedics
    3           Michael     Brown       Pediatrics
    doctor_id   first_name  last_name   specialization
    ----------  ----------  ----------  --------------
    1           John        Smith       Cardiology

```sql
DELETE FROM Doctors WHERE doctor_id>=2 AND doctor_id<=4;
```

**Output:**

<img width="986" height="562" alt="image" src="https://github.com/user-attachments/assets/e9ad5959-d356-43ed-89cf-ffaff769460f" />


**Question 7**
---
    Write a SQL query to remove rows from the table 'customer' with the following condition -
    
    1. 'cust_city' should begin with the letter 'L',
    
    Sample table: Customer
    
    +-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
    |CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
    +-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
    | C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
    | C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
    | C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
    For example:
    
    Test	Result
    SELECT * FROM customer WHERE cust_country='UK';
    CUST_CODE   CUST_NAME   CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE
    ----------  ----------  ----------  ------------  ------------  ----------  -----------  -----------  -----------  ---------------  ----------  ----------
    C00013      Holmes      London      London        UK            2           6000         5000         7000         4000             BBBBBBB     A003
    C00024      Cook        London      London        UK            2           4000         9000         7000         6000             FSDDSDF     A006
    C00015      Stuart      London      London        UK            1           6000         8000         3000         11000            GFSGERS     A003
    C00023      Karl        London      London        UK            0           4000         6000         7000         3000             AAAABAA     A006
    C00010      Charles     Hampshair   Hampshair     UK            3           6000         4000         5000         5000             MMMMMMM     A009
    CUST_CODE   CUST_NAME   CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE
    ----------  ----------  ----------  ------------  ------------  ----------  -----------  -----------  -----------  ---------------  ----------  ----------
    C00010      Charles     Hampshair   Hampshair     UK            3           6000         4000         5000         5000             MMMMMMM     A009

```sql
DELETE FROM customer WHERE cust_city LIKE 'L%';
```

**Output:**

<img width="1485" height="546" alt="image" src="https://github.com/user-attachments/assets/a4ea97c3-c119-4984-b1b0-220d1cb5bd78" />


**Question 8**
---
    Write a SQL query to Delete customers with 'CUST_COUNTRY' 'UK' and 'WORKING_AREA' 'London' whose 'GRADE' is less than 3
    
    Sample table: Customer
    
    +-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
    |CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
    +-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
    | C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
    | C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
    | C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
    For example:
    
    Test	Result
    select changes();
    changes()
    ----------
    4


```sql
DELETE FROM Customer WHERE CUST_COUNTRY='UK' AND WORKING_AREA='London' AND GRADE<3;
```

**Output:**

<img width="1838" height="281" alt="image" src="https://github.com/user-attachments/assets/b768d4a6-e535-49b3-a8ab-d39676cfdd9b" />


**Question 9**
---
    Write a SQL query to Delete customers with 'GRADE' 2 and 'CUST_NAME' starting with 'M', and whose 'PAYMENT_AMT' is less than 3000
    
    Sample table: Customer
    
    +-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
    |CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
    +-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
    | C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
    | C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
    | C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
    For example:
    
    Test	Result
    select changes();
    changes()
    ----------
    1


```sql
DELETE FROM Customer WHERE GRADE=2 AND CUST_NAME LIKE 'M%' AND PAYMENT_AMT<3000;
```

**Output:**

<img width="1775" height="205" alt="image" src="https://github.com/user-attachments/assets/cd8591a9-f118-454b-8e0e-05678ad077d4" />


**Question 10**
---
    Write a SQL query to Delete customers from 'customer' table where 'AGENT_CODE' is either 'A003' or 'A008'.
    
     
    Sample table: Customer
    
    +-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
    |CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
    +-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
    | C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
    | C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
    | C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
    For example:
    
    Test	Result
    select distinct(agent_code)from customer;
    AGENT_CODE
    ----------
    A003
    A008
    A011
    A006
    A005
    A010
    A002
    A004
    A009
    A007
    A012
    A001
    AGENT_CODE
    ----------
    A011
    A006
    A005
    A010
    A002
    A004
    A009
    A007
    A012
    A001


```sql
DELETE FROM customer WHERE AGENT_CODE='A003' OR AGENT_CODE='A008';
```

**Output:**

<img width="615" height="702" alt="image" src="https://github.com/user-attachments/assets/2f5fe9be-27d2-4b66-86da-55e5d6c4d170" />


## RESULT
<img width="1860" height="697" alt="image" src="https://github.com/user-attachments/assets/35d5d529-d820-42af-a728-3aae080ccd1f" />

Thus, the SQL queries to implement DML commands have been executed successfully.
