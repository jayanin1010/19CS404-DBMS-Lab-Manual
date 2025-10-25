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
    How many appointments are scheduled in each hour of the day?
    
    Sample table:Appointments Table
    
    name                              type
    --------------------          ----------
    AppointmentID               INTEGER
    PatientID                         INTEGER
    DoctorID                         INTEGER
    AppointmentDateTime   DATETIME
    Purpose                           TEXT
    Status                              TEXT     
    
    For example:
    
    Result
    HourOfDay   TotalAppointments
    ----------  -----------------
    09          2
    10          5
    11          1
    14          1
    16          1

```sql
SELECT strftime('%H',AppointmentDateTime) AS HourOfDay,
COUNT(*) AS TotalAppointments FROM Appointments GROUP BY HourOfDay;
```

**Output:**

<img width="811" height="518" alt="image" src="https://github.com/user-attachments/assets/67f4000a-ba8c-4b3d-a929-207b380e21e6" />


**Question 2**
---
    What is the average age of doctors in each medical specialty?
    
    Sample table:Doctors Table
    
    
    
    For example:
    
    Result
    Specialty          AvgAge
    -----------------  ----------
    Endocrinology      44.0
    Gastroenterology   39.0
    Neurology          41.0
    Obstetrics         53.0
    Pediatrics         48.0
    Urology            44.0


```sql
--SELECT Specialty,AVG(strftime('%Y','now')-strftime('%Y',DateOfBirth)) AS AvgAge FROM Doctors GROUP BY Specialty;

SELECT Specialty,AVG((strftime('%Y','now')-strftime('%Y',DateOfBirth))-(strftime('%m-%d','now')<strftime('%m-%d',DateOfBirth))
)AS AvgAge FROM Doctors GROUP BY Specialty;
```

**Output:**

<img width="804" height="624" alt="image" src="https://github.com/user-attachments/assets/33875cb4-cfb5-4963-9e89-4168db2685bb" />


**Question 3**
---
    How many prescriptions were written by each doctor?
    
    Sample tablePrescriptions Table
    
    
    
    For example:
    
    Result
    DoctorID    TotalPrescriptions
    ----------  ------------------
    1           1
    2           1
    3           1
    4           1
    5           1
    6           1
    7           1
    8           1
    9           1
    10          1


```sql
SELECT DoctorID,COUNT(*)AS TotalPrescriptions FROM Prescriptions GROUP BY DoctorID;
```

**Output:**

<img width="746" height="722" alt="image" src="https://github.com/user-attachments/assets/a9926073-7196-48ef-95d1-e7cd81e55cf2" />


**Question 4**
---
    Write a SQL query to calculate the total number of working hours of all employees
    
    Sample table: employee1
    
    
     
    
    For example:
    
    Result
    Total working hours
    -------------------
    111


```sql
SELECT SUM(workhour)AS "Total working hours" FROM employee1;
```

**Output:**

<img width="642" height="293" alt="image" src="https://github.com/user-attachments/assets/41887aba-8796-43fc-8b22-5511f95eda07" />


**Question 5**
---
    Write a SQL query to find the number of employees whose age is greater than 32.
    
    Sample table: employee
    
    id
    
    name
    
    age
    
    address
    
    salary
    
    1
    
    Paul
    
    32
    
    California
    
    20000
    
    4
    
    Mark
    
    25
    
    Richtown
    
    65000
    
    5
    
    David
    
    27
    
    Texas
    
    85000
    
     
    
    For example:
    
    Result
    COUNT
    ----------
    5


```sql
SELECT COUNT(*) AS COUNT FROM employee WHERE age>32;
```

**Output:**

<img width="436" height="263" alt="image" src="https://github.com/user-attachments/assets/c27fae78-ba08-40a7-9a01-f68abc71d4c4" />


**Question 6**
---
    Write a SQL query to find What is the age difference between the youngest and oldest employee in the company.
    
    Table: employee
    
    name        type
    ----------  ----------
    id          INTEGER
    name        TEXT
    age         INTEGER
    city        TEXT
    income      INTEGER
    For example:
    
    Result
    age_difference
    --------------
    13


```sql
SELECT MAX(age)-MIN(age)AS age_difference FROM employee;
```

**Output:**

<img width="503" height="278" alt="image" src="https://github.com/user-attachments/assets/7c11538d-8582-4a6c-a05b-2d66f66a065c" />


**Question 7**
---
    Write a SQL query to find the average length of email addresses (in characters):
    
    Table: customer
    
    name        type
    ----------  ----------
    id          INTEGER
    name        TEXT
    city        TEXT
    email       TEXT
    phone       INTEGER
    For example:
    
    Result
    avg_email_length
    ----------------
    15.0


```sql
SELECT AVG(LENGTH(email)) AS avg_email_length FROM customer;
```

**Output:**

<img width="668" height="274" alt="image" src="https://github.com/user-attachments/assets/d23e04ce-e622-4ed9-8ab5-b2586aae1299" />


**Question 8**
---
    Write the SQL query that accomplishes the grouping of data by age intervals using the expression (age/5)5, calculates the minimum age for each group, and excludes groups where the minimum age is not less than 25.
    
    Sample table: customer1
    
    
    
    For example:
    
    Result
    age_group   MIN(age)
    ----------  ----------
    20          22


```sql
SELECT (age/5)*5 AS age_group,MIN(age) FROM customer1 GROUP BY age_group HAVING MIN(age)<25;
```

**Output:**

<img width="752" height="285" alt="image" src="https://github.com/user-attachments/assets/197c119f-231a-4b88-832d-3eb390043851" />


**Question 9**
---
    Write the SQL query that achieves the grouping of data by city, calculates the total income for each city, and includes only those cities where the total income sum is greater than 200,000.
    
    Sample table: employee
    
    
    
    For example:
    
    Result
    city        Income
    ----------  ----------
    Alaska      450000
    Arizona     1000000
    California  5300000
    Florida     5350000
    Georgia     250000


```sql
SELECT city,SUM(income)AS Income FROM employee GROUP BY city HAVING SUM(income)>200000;
```

**Output:**

<img width="724" height="515" alt="image" src="https://github.com/user-attachments/assets/6cc9aac1-257b-4bd0-83db-69037770a78a" />


**Question 10**
---
    Write the SQL query that achieves the grouping of data by occupation, calculates the minimum work hours for each occupation, and excludes occupations where the minimum work hour is not greater than 8.
    
    Sample table: employee1
    
    
    
    For example:
    
    Result
    occupation  MIN(workhour)
    ----------  -------------
    Business    10
    Doctor      15
    Engineer    12
    Teacher     9


```sql
SELECT occupation,MIN(workhour)
FROM employee1
GROUP BY occupation HAVING MIN(workhour)>8;
```

**Output:**
<img width="903" height="459" alt="image" src="https://github.com/user-attachments/assets/0cc9ec7e-2d39-4e01-95aa-d7819ba9f2d6" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
