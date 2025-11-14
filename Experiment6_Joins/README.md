# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--


```sql
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the city 'New York'.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

For example:

Result
name
---------------
Bob Emily

```

**Program:**

    SELECT s.name
    FROM salesman s
    LEFT JOIN customer c
      ON s.salesman_id = c.salesman_id
    WHERE c.city = 'New York';


**Output:**

<img width="549" height="391" alt="image" src="https://github.com/user-attachments/assets/ff957b86-6e88-4af0-a8d8-4651712e056b" />


**Question 2**
---
    From the following tables write a SQL query to find those customers with a grade less than 300. Return cust_name, customer city, grade, Salesman, salesmancity. The result should be ordered by ascending customer_id. 
    
    Sample table: customer
    
     customer_id |   cust_name    |    city    | grade | salesman_id 
    -------------+----------------+------------+-------+-------------
            3002 | Nick Rimando   | New York   |   100 |        5001
            3007 | Brad Davis     | New York   |   200 |        5001
            3005 | Graham Zusi    | California |   200 |        5002
            3008 | Julian Green   | London     |   300 |        5002
            3004 | Fabian Johnson | Paris      |   300 |        5006
            3009 | Geoff Cameron  | Berlin     |   100 |        5003
            3003 | Jozy Altidor   | Moscow     |   200 |        5007
            3001 | Brad Guzan     | London     |       |        5005
    Sample table: salesman
    
     salesman_id |    name    |   city   | commission 
    -------------+------------+----------+------------
            5001 | James Hoog | New York |       0.15
            5002 | Nail Knite | Paris    |       0.13
            5005 | Pit Alex   | London   |       0.11
            5006 | Mc Lyon    | Paris    |       0.14
            5007 | Paul Adam  | Rome     |       0.13
            5003 | Lauson Hen | San Jose |       0.12

```sql
SELECT 
    c.cust_name,
    c.city AS city,
    c.grade,
    s.name AS Salesman,
    s.city AS city
FROM 
    customer c
JOIN 
    salesman s ON c.salesman_id = s.salesman_id
WHERE 
    c.grade < 300
ORDER BY 
    c.customer_id;
```

**Output:**

<img width="1203" height="732" alt="image" src="https://github.com/user-attachments/assets/a76ecd20-b250-4cd2-8f8f-d028c359ce52" />


**Question 3**
---
    From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission. 
    
    Sample table: orders
    
    ord_no      purch_amt   ord_date    customer_id  salesman_id
    ----------  ----------  ----------  -----------  -----------
    70001       150.5       2012-10-05  3005         5002
    70009       270.65      2012-09-10  3001         5005
    70002       65.26       2012-10-05  3002         5001
    70004       110.5       2012-08-17  3009         5003
    70007       948.5       2012-09-10  3005         5002
    70005       2400.6      2012-07-27  3007         5001
    70008       5760        2012-09-10  3002         5001
    70010       1983.43     2012-10-10  3004         5006
    70003       2480.4      2012-10-10  3009         5003
    70012       250.45      2012-06-27  3008         5002
    70011       75.29       2012-08-17  3003         5007
    70013       3045.6      2012-04-25  3002         5001
    Sample table: customer
    
     customer_id |   cust_name    |    city    | grade | salesman_id 
    -------------+----------------+------------+-------+-------------
            3002 | Nick Rimando   | New York   |   100 |        5001
            3007 | Brad Davis     | New York   |   200 |        5001
            3005 | Graham Zusi    | California |   200 |        5002
            3008 | Julian Green   | London     |   300 |        5002
            3004 | Fabian Johnson | Paris      |   300 |        5006
            3009 | Geoff Cameron  | Berlin     |   100 |        5003
            3003 | Jozy Altidor   | Moscow     |   200 |        5007
            3001 | Brad Guzan     | London     |       |        5005
    Sample table: salesman
    
     salesman_id |    name    |   city   | commission 
    -------------+------------+----------+------------
            5001 | James Hoog | New York |       0.15
            5002 | Nail Knite | Paris    |       0.13
            5005 | Pit Alex   | London   |       0.11
            5006 | Mc Lyon    | Paris    |       0.14
            5007 | Paul Adam  | Rome     |       0.13
            5003 | Lauson Hen | San Jose |       0.12
    For example:
    
    Result
    ord_no           ord_date         purch_amt        Customer Name    grade       Salesman    commission
    ---------------  ---------------  ---------------  ---------------  ----------  ----------  ----------
    70001            2012-10-05       150.5            Graham Zusi      200         Nail Knite  0.13
    70009            2012-09-10       270.65           Brad Guzan       100         Pit Alex    0.11
    70002            2012-10-05       65.26            Nick Rimando     100         Bob Emily   0.15
    70004            2012-08-17       110.5            Geoff Cameron    100         Lauson Hen  0.12
    70007            2012-09-10       948.5            Graham Zusi      200         Nail Knite  0.13
    70005            2012-07-27       2400.6           Brad Davis       200         Bob Emily   0.15
    70008            2012-09-10       5760.0           Nick Rimando     100         Bob Emily   0.15
    70010            2012-10-10       1983.43          Fabian Johns     300         Mc Lyon     0.14
    70003            2012-10-10       2480.4           Geoff Cameron    100         Lauson Hen  0.12
    70012            2012-06-27       250.45           Julian Green     300         Nail Knite  0.13
    70011            2012-08-17       75.29            Jozy Altidore    200         Paul Adam   0.13
    70013            2012-04-25       3045.6           Nick Rimando     100         Bob Emily   0.15

```sql
SELECT
    o.ord_no,
    o.ord_date,
    o.purch_amt,
    c.cust_name AS "Customer Name",
    c.grade,
    s.name AS "Salesman",
    s.commission
FROM
    orders AS o
JOIN
    customer AS c ON o.customer_id = c.customer_id
JOIN
    salesman AS s ON o.salesman_id = s.salesman_id;
```

**Output:**

<img width="1273" height="890" alt="image" src="https://github.com/user-attachments/assets/5fcdae9e-945c-4154-bb56-874243202e0a" />


**Question 4**
---
    Write a SQL statement to join the tables salesman, customer and orders so that the same column of each table appears once and only the relational rows are returned. 
    
    Sample table: orders
    
    ord_no      purch_amt   ord_date    customer_id  salesman_id
    ----------  ----------  ----------  -----------  -----------
    70001       150.5       2012-10-05  3005         5002
    70009       270.65      2012-09-10  3001         5005
    70002       65.26       2012-10-05  3002         5001
    70004       110.5       2012-08-17  3009         5003
    70007       948.5       2012-09-10  3005         5002
    70005       2400.6      2012-07-27  3007         5001
    70008       5760        2012-09-10  3002         5001
    70010       1983.43     2012-10-10  3004         5006
    70003       2480.4      2012-10-10  3009         5003
    70012       250.45      2012-06-27  3008         5002
    70011       75.29       2012-08-17  3003         5007
    70013       3045.6      2012-04-25  3002         5001
    Sample table: customer
    
     customer_id |   cust_name    |    city    | grade | salesman_id 
    -------------+----------------+------------+-------+-------------
            3002 | Nick Rimando   | New York   |   100 |        5001
            3007 | Brad Davis     | New York   |   200 |        5001
            3005 | Graham Zusi    | California |   200 |        5002
            3008 | Julian Green   | London     |   300 |        5002
            3004 | Fabian Johnson | Paris      |   300 |        5006
            3009 | Geoff Cameron  | Berlin     |   100 |        5003
            3003 | Jozy Altidor   | Moscow     |   200 |        5007
            3001 | Brad Guzan     | London     |       |        5005
    Sample table : salesman
    
     salesman_id |    name    |   city   | commission 
    -------------+------------+----------+------------
            5001 | James Hoog | New York |       0.15
            5002 | Nail Knite | Paris    |       0.13
            5005 | Pit Alex   | London   |       0.11
            5006 | Mc Lyon    | Paris    |       0.14
            5007 | Paul Adam  | Rome     |       0.13
            5003 | Lauson Hen | San Jose |       0.12
    For example:
    
    Result
    ord_no           purch_amt        ord_date         cust_name        customer_city  grade       salesman_name  salesman_city  commission
    ---------------  ---------------  ---------------  ---------------  -------------  ----------  -------------  -------------  ----------
    70001            150.5            2012-10-05       Graham Zusi      California     200         Nail Knite     Paris          0.13
    70009            270.65           2012-09-10       Brad Guzan       London         100         Pit Alex       London         0.11
    70002            65.26            2012-10-05       Nick Rimando     Chennai        100         Bob Emily      New York       0.15
    70004            110.5            2012-08-17       Geoff Cameron    Berlin         100         Lauson Hen     San Jose       0.12
    70007            948.5            2012-09-10       Graham Zusi      California     200         Nail Knite     Paris          0.13
    70005            2400.6           2012-07-27       Brad Davis       New York       200         Bob Emily      New York       0.15
    70008            5760.0           2012-09-10       Nick Rimando     Chennai        100         Bob Emily      New York       0.15
    70010            1983.43          2012-10-10       Fabian Johns     Paris          300         Mc Lyon        Paris          0.14
    70003            2480.4           2012-10-10       Geoff Cameron    Berlin         100         Lauson Hen     San Jose       0.12
    70012            250.45           2012-06-27       Julian Green     London         300         Nail Knite     Paris          0.13
    70011            75.29            2012-08-17       Jozy Altidore    Moscow         200         Paul Adam      Rome           0.13
    70013            3045.6           2012-04-25       Nick Rimando     Chennai        100         Bob Emily      New York       0.15

```sql
SELECT o.ord_no,
       o.purch_amt,
       o.ord_date,
       c.cust_name,
       c.city AS customer_city,
       c.grade,
       s.name AS salesman_name,
       s.city AS salesman_city,
       s.commission
FROM orders o
INNER JOIN customer c ON o.customer_id = c.customer_id
INNER JOIN salesman s ON o.salesman_id = s.salesman_id;
```

**Output:**

<img width="1293" height="901" alt="image" src="https://github.com/user-attachments/assets/3aad3a92-46b7-4a38-bdce-a13342bbcd61" />


**Question 5**
---
     From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission.
    
    Sample table: customer
    
     customer_id |   cust_name    |    city    | grade | salesman_id 
    -------------+----------------+------------+-------+-------------
            3002 | Nick Rimando   | New York   |   100 |        5001
            3007 | Brad Davis     | New York   |   200 |        5001
            3005 | Graham Zusi    | California |   200 |        5002
            3008 | Julian Green   | London     |   300 |        5002
            3004 | Fabian Johnson | Paris      |   300 |        5006
            3009 | Geoff Cameron  | Berlin     |   100 |        5003
            3003 | Jozy Altidor   | Moscow     |   200 |        5007
            3001 | Brad Guzan     | London     |       |        5005
    Sample table: salesman
    
     salesman_id |    name    |   city   | commission 
    -------------+------------+----------+------------
            5001 | James Hoog | New York |       0.15
            5002 | Nail Knite | Paris    |       0.13
            5005 | Pit Alex   | London   |       0.11
            5006 | Mc Lyon    | Paris    |       0.14
            5007 | Paul Adam  | Rome     |       0.13
            5003 | Lauson Hen | San Jose |       0.12
    For example:
    
    Result
    Customer Name    city             Salesman         commission
    ---------------  ---------------  ---------------  ---------------
    Nick Rimando     Chennai          Bob Emily        0.15
    Graham Zusi      California       Nail Knite       0.13
    Brad Guzan       London           Pit Alex         0.11
    Fabian Johns     Paris            Mc Lyon          0.14
    Brad Davis       New York         Bob Emily        0.15
    Geoff Cameron    Berlin           Lauson Hen       0.12
    Julian Green     London           Nail Knite       0.13
    Jozy Altidore    Moscow           Paul Adam        0.13


```sql
SELECT c.cust_name AS "Customer Name",
       c.city,
       s.name AS "Salesman",
       s.commission
FROM customer c
JOIN salesman s ON c.salesman_id = s.salesman_id;
```

**Output:**

<img width="1102" height="676" alt="image" src="https://github.com/user-attachments/assets/b50cd600-1aee-4306-9535-0cdec4b1a6b1" />


**Question 6**
---
    Write the SQL query that achieves the selection of the "nurse_id" from the "nurses" table (aliased as "n") and the "department_name" from the "departments" table, with an inner join on the "department_id" column and conditions filtering for a nurse with the first name 'David' and last name 'Moore'.
    
    NURSES TABLE:
    
    ATTRIBUTES - nurse_id, first_name, last_name, department_id
    
    
    
    DEPARTMENTS TABLE:
    
    ATTRIBUTES - department_id, department_name
    
    
    
    For example:
    
    Result
    nurse_id         department_name
    ---------------  ---------------
    2                Orthopedics


```sql
SELECT n.nurse_id,
       d.department_name
FROM nurses n
INNER JOIN departments d ON n.department_id = d.department_id
WHERE n.first_name = 'David' 
  AND n.last_name = 'Moore';
```

**Output:**

<img width="643" height="295" alt="image" src="https://github.com/user-attachments/assets/2a70aef4-635c-4fe8-b34d-b0a0a0725a9b" />


**Question 7**
---
    SQL statement to generate a report with customer name, city, order number, order date, order amount, salesperson name, and commission to determine if any of the existing customers have not placed orders or if they have placed orders through their salesman or by themselves.
    
    Sample table: customer
    
     customer_id |   cust_name    |    city    | grade | salesman_id 
    -------------+----------------+------------+-------+-------------
            3002 | Nick Rimando   | New York   |   100 |        5001
            3007 | Brad Davis     | New York   |   200 |        5001
            3005 | Graham Zusi    | California |   200 |        5002
            3008 | Julian Green   | London     |   300 |        5002
            3004 | Fabian Johnson | Paris      |   300 |        5006
            3009 | Geoff Cameron  | Berlin     |   100 |        5003
            3003 | Jozy Altidor   | Moscow     |   200 |        5007
            3001 | Brad Guzan     | London     |       |        5005
    Sample table: orders
    
    ord_no      purch_amt   ord_date    customer_id  salesman_id
    ----------  ----------  ----------  -----------  -----------
    70001       150.5       2012-10-05  3005         5002
    70009       270.65      2012-09-10  3001         5005
    70002       65.26       2012-10-05  3002         5001
    70004       110.5       2012-08-17  3009         5003
    70007       948.5       2012-09-10  3005         5002
    70005       2400.6      2012-07-27  3007         5001
    70008       5760        2012-09-10  3002         5001
    70010       1983.43     2012-10-10  3004         5006
    70003       2480.4      2012-10-10  3009         5003
    70012       250.45      2012-06-27  3008         5002
    70011       75.29       2012-08-17  3003         5007
    70013       3045.6      2012-04-25  3002         5001
    Sample table: salesman
    
     salesman_id |    name    |   city   | commission 
    -------------+------------+----------+------------
            5001 | James Hoog | New York |       0.15
            5002 | Nail Knite | Paris    |       0.13
            5005 | Pit Alex   | London   |       0.11
            5006 | Mc Lyon    | Paris    |       0.14
            5007 | Paul Adam  | Rome     |       0.13
            5003 | Lauson Hen | San Jose |       0.12
    For example:
    
    Result
    cust_name        city             ord_no           ord_date         Order Amount  name        commission
    ---------------  ---------------  ---------------  ---------------  ------------  ----------  ----------
    Nick Rimando     Chennai          70002            2012-10-05       65.26         Bob Emily   0.15
    Nick Rimando     Chennai          70008            2012-09-10       5760.0        Bob Emily   0.15
    Nick Rimando     Chennai          70013            2012-04-25       3045.6        Bob Emily   0.15
    Graham Zusi      California       70001            2012-10-05       150.5         Nail Knite  0.13
    Graham Zusi      California       70007            2012-09-10       948.5         Nail Knite  0.13
    Brad Guzan       London           70009            2012-09-10       270.65        Pit Alex    0.11
    Fabian Johns     Paris            70010            2012-10-10       1983.43       Mc Lyon     0.14
    Brad Davis       New York         70005            2012-07-27       2400.6        Bob Emily   0.15
    Geoff Cameron    Berlin           70003            2012-10-10       2480.4        Lauson Hen  0.12
    Geoff Cameron    Berlin           70004            2012-08-17       110.5         Lauson Hen  0.12
    Julian Green     London           70012            2012-06-27       250.45        Nail Knite  0.13
    Jozy Altidore    Moscow           70011            2012-08-17       75.29         Paul Adam   0.13

```sql
SELECT 
    c.cust_name,
    c.city,
    o.ord_no,
    o.ord_date,
    o.purch_amt AS "Order Amount",
    s.name,
    s.commission
FROM customer c
LEFT JOIN orders o ON c.customer_id = o.customer_id
LEFT JOIN salesman s ON o.salesman_id = s.salesman_id
ORDER BY c.customer_id, o.ord_no;

```

**Output:**

<img width="1296" height="318" alt="image" src="https://github.com/user-attachments/assets/3481f7c5-dd65-4767-a00c-fd017c68477c" />


**Question 8**
---
    Write an SQL query that retrieves all columns from the 'customer' table (using the alias 'c'), performs a LEFT JOIN with the 'orders' table on the 'customer_id' column, and includes only those orders with an order date after '2012-08-17'.
    
    'customer' Table: (customer_id, cust_name, city, grade, salesman_id)
    
    'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)
    
    For example:
    
    Result
    customer_id      cust_name        city             grade            salesman_id
    ---------------  ---------------  ---------------  ---------------  -----------
    3005             Graham Zusi      California       200              5002
    3001             Brad Guzan       London           100              5005
    3002             Nick Rimando     Chennai          100              5001
    3005             Graham Zusi      California       200              5002
    3002             Nick Rimando     Chennai          100              5001
    3004             Fabian Johns     Paris            300              5006
    3009             Geoff Cameron    Berlin           100              5003

```sql
SELECT c.customer_id,
       c.cust_name,
       c.city,
       c.grade,
       c.salesman_id
FROM customer c
LEFT JOIN orders o ON c.customer_id = o.customer_id
WHERE o.ord_date > '2012-08-17';
```

**Output:**

<img width="1277" height="634" alt="image" src="https://github.com/user-attachments/assets/725dd6d5-c194-47ee-8da7-a70949e30d57" />


**Question 9**
---
    Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and conditions filtering for test results with the test name 'X-Ray' and a result of 'Normal'.
    
    PATIENTS TABLE:
    
    ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id
    
    
    
    TEST_RESULT TABLES:
    
    ATTRIBUTES - result_id, patient_id, test_name, result, test_date
    
    
    
    For example:
    
    Result
    patient_id       first_name       last_name        date_of_birth    admission_date  discharge_date  doctor_id
    ---------------  ---------------  ---------------  ---------------  --------------  --------------  ----------
    2                Bob              Miller           1995-08-23       2024-02-15      2024-03-01      2

```sql
SELECT p.patient_id,
       p.first_name,
       p.last_name,
       p.date_of_birth,
       p.admission_date,
       p.discharge_date,
       p.doctor_id
FROM patients p
INNER JOIN test_result t ON p.patient_id = t.patient_id
WHERE t.test_name = 'X-Ray' 
  AND t.result = 'Normal';
```

**Output:**

<img width="1243" height="139" alt="image" src="https://github.com/user-attachments/assets/88e6cc03-ed12-46cd-8efc-077cdd299190" />


**Question 10**
---
    Write the SQL query that achieves the selection of all columns from the "patients" table, with an inner join on the "doctor_id" column, and includes a condition filtering for patients whose doctors have the first name 'John' and last name 'Smith'.
    
    PATIENTS TABLE:
    name             type
    ---------------  ---------------
    patient_id       INT
    first_name       VARCHAR(50)
    last_name        VARCHAR(50)
    date_of_birth    DATE
    admission_date   DATE
    discharge_date   DATE
    doctor_id        INT
    
    DOCTORS TABLE:
    
    name             type
    ---------------  ---------------
    doctor_id        INT
    first_name       VARCHAR(50)
    last_name        VARCHAR(50)
    specialization   VARCHAR(100)
    
    For example:
    
    Result
    patient_id       first_name       last_name        date_of_birth    admission_date  discharge_date  doctor_id
    ---------------  ---------------  ---------------  ---------------  --------------  --------------  ----------
    1                Alice            Williams         1980-05-12       2024-01-10                      1


```sql
SELECT p.patient_id,
       p.first_name,
       p.last_name,
       p.date_of_birth,
       p.admission_date,
       p.discharge_date,
       p.doctor_id
FROM patients p
INNER JOIN doctors d ON p.doctor_id = d.doctor_id
WHERE d.first_name = 'John' 
  AND d.last_name = 'Smith';
```

**Output:**

<img width="1319" height="292" alt="image" src="https://github.com/user-attachments/assets/9e323b84-fc2a-4e21-ab1d-342d2dfbcf51" />



## RESULT
<img width="1453" height="424" alt="image" src="https://github.com/user-attachments/assets/b88f56fa-53cc-4d86-a438-1cbacbbb4d59" />

Thus, the SQL queries to implement different types of joins have been executed successfully.
