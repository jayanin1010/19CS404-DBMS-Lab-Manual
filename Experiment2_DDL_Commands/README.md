# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
    Create a table named Members with the following columns:
    
    MemberID as INTEGER
    MemberName as TEXT
    JoinDate as DATE
    For example:
    
    Test	Result
    pragma table_info('Members');
    cid         name        type        notnull     dflt_value  pk
    ----------  ----------  ----------  ----------  ----------  ----------
    0           MemberID    INTEGER     0                       0
    1           MemberName  TEXT        0                       0
    2           JoinDate    DATE        0                       0


```sql
CREATE TABLE Members(
MemberID INTEGER,
MemberName TEXT,
JoinDate DATE
);
```

**Output:**

<img width="1276" height="276" alt="image" src="https://github.com/user-attachments/assets/0fcad0bb-6c3a-4790-8a08-9a066214b1f4" />


**Question 2**
---
    Insert a customer with CustomerID 301, Name Michael Jordan, Address 123 Maple St, City Chicago, and ZipCode 60616 into the Customers table.
    
    For example:
    
    Test	Result
    SELECT * FROM Customers WHERE CustomerID = 301;
    CustomerID  Name            Address       City        ZipCode
    ----------  --------------  ------------  ----------  ----------
    301         Michael Jordan  123 Maple St  Chicago     60616


```sql
INSERT INTO Customers(CustomerID,Name,Address,City,ZipCode)
VALUES(301,'Michael Jordan','123 Maple St','Chicago','60616');


```

**Output:**

<img width="1234" height="159" alt="image" src="https://github.com/user-attachments/assets/ced65a60-fc86-4251-9f16-1f2ea44eb4b3" />


**Question 3**
---
    Create a new table named contacts with the following specifications:
    contact_id as INTEGER and primary key.
    first_name as TEXT and not NULL.
    last_name as TEXT and not NULL.
    email as TEXT.
    phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.
    For example:
    
    Test	Result
    INSERT INTO contacts (contact_id, first_name, last_name, email, phone) VALUES (1, 'John', 'Doe', 'john.doe@example.com', '1234567890');
    SELECT * FROM contacts;
    contact_id  first_name  last_name   email                 phone
    ----------  ----------  ----------  --------------------  ----------
    1           John        Doe         john.doe@example.com  1234567890


```sql
CREATE TABLE contacts(
contact_id INTEGER PRIMARY KEY,
first_name TEXT NOT NULL,
last_name TEXTNOT NULL,
email TEXT,
phone TEXT NOT NULL CHECK(LENGTH(phone)>=10)
);
```

**Output:**

<img width="1542" height="186" alt="image" src="https://github.com/user-attachments/assets/61651924-7c53-4693-97e9-59321fff4794" />


**Question 4**
---
    Create a new table named item with the following specifications and constraints:
    item_id as TEXT and as primary key.
    item_desc as TEXT.
    rate as INTEGER.
    icom_id as TEXT with a length of 4.
    icom_id is a foreign key referencing com_id in the company table.
    The foreign key should set NULL on updates and deletes.
    item_desc and rate should not accept NULL.
    For example:
    
    Test	Result
    INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
    UPDATE company SET com_id='COM5' WHERE com_id='COM4';
    SELECT * FROM item;
    item_id     item_desc     rate        icom_id
    ----------  ------------  ----------  ----------
    ITM5        Charlie Gold  700

```sql
CREATE TABLE item(
item_id TEXT PRIMARY KEY,
item_desc TEXT NOT NULL,
rate INTEGER NOT NULL,
icom_id TEXT(4),
FOREIGN KEY(icom_id) REFERENCES company(com_id)
ON UPDATE SET NULL
ON DELETE SET NULL
);
```

**Output:**

<img width="981" height="214" alt="image" src="https://github.com/user-attachments/assets/932a9eb6-8c80-4e36-a48f-2e0ae4ad3655" />


**Question 5**
---
    Insert all products from Discontinued_products into Products.
    
    Table attributes are ProductID, ProductName, Price, Stock
    
    For example:
    
    Test	Result
    select * from Products;
    ProductID   ProductName     Price       Stock
    ----------  --------------  ----------  ----------
    101         Old Smartphone  199.99      0
    102         Vintage Laptop  399.99      10
    103         Classic Tablet  149.99      5


```sql
INSERT INTO Products(ProductID,ProductName,Price,Stock)
SELECT ProductID,ProductName,Price,Stock FROM Discontinued_products;
```

**Output:**

<img width="937" height="186" alt="image" src="https://github.com/user-attachments/assets/a5c1a0f8-206c-4a94-9889-f29008cb066d" />


**Question 6**
---
    Create a table named Invoices with the following constraints:
    
    InvoiceID as INTEGER should be the primary key.
    InvoiceDate as DATE.
    DueDate as DATE should be greater than the InvoiceDate.
    Amount as REAL should be greater than 0.
    For example:
    
    Test	Result
    INSERT INTO Invoices (InvoiceID, InvoiceDate)
    VALUES (1, '2024-08-08'),(1,'2024-09-08');
    Error: UNIQUE constraint failed: Invoices.InvoiceID


```sql
CREATE TABLE Invoices(
InvoiceID INTEGER PRIMARY KEY,
InvoiceDate DATE,
DueDate DATE CHECK(DueDate>InvoiceDate),
Amount REAL CHECK(Amount>0)
);
```

**Output:**

<img width="1010" height="159" alt="image" src="https://github.com/user-attachments/assets/7c55432c-5ff0-460b-b7c1-b77d7cac8ae8" />


**Question 7**
---
    Write an SQL query to change the name of the column id to employee_id in the table employee.
    
     
    
     
    
     
    
     
    
    For example:
    
    Test	Result
    pragma table_info('employee');
    cid         name         type        notnull     dflt_value  pk
    ----------  -----------  ----------  ----------  ----------  ----------
    0           employee_id  integer     0                       0
    1           salary       number      0                       0


```sql
ALTER TABLE employee RENAME COLUMN id TO employee_id;
```

**Output:**

<img width="1206" height="156" alt="image" src="https://github.com/user-attachments/assets/f4fd726e-74fc-493f-8b42-f74f003b2082" />


**Question 8**
---
    Write a SQL query to Add a new column State as text in the Student_details table.
    
    Sample table: Student_details
    
     cid              name             type   notnull     dflt_value  pk
    ---------------  ---------------  -----  ----------  ----------  ----------
    0                RollNo           int    0                       1
    1                Name             VARCH  1                       0
    2                Gender           TEXT   1                       0
    3                Subject          VARCH  0                       0
    4                MARKS            INT (  0                       0
    For example:
    
    Test	Result
    pragma table_info('Student_details');
    cid         name        type        notnull     dflt_value  pk
    ----------  ----------  ----------  ----------  ----------  ----------
    0           RollNo      int         0                       1
    1           Name        VARCHAR(10  1                       0
    2           Gender      TEXT        1                       0
    3           Subject     VARCHAR(30  0                       0
    4           MARKS       INT (3)     0                       0
    5           State       TEXT        0                       0


```sql
ALTER TABLE Student_details ADD COLUMN State TEXT;
```

**Output:**

<img width="1109" height="191" alt="image" src="https://github.com/user-attachments/assets/1cc09be3-55b1-48f3-8e2e-4b6c744a667f" />


**Question 9**
---
    Insert the following employees into the Employee table:
    
    EmployeeID  Name        Position    Department  Salary
    ----------  ----------  ----------  ----------  ----------
    2           John Smith  Developer   IT          75000
    3           Anna Bell   Designer    Marketing   68000
    For example:
    
    Test	Result
    SELECT * FROM Employee;
    
    EmployeeID  Name        Position    Department  Salary
    ----------  ----------  ----------  ----------  ----------
    2           John Smith  Developer   IT          75000
    3           Anna Bell   Designer    Marketing   68000


```sql
INSERT INTO Employee(EmployeeID,Name,Position,Department,Salary)
VALUES(2,'John Smith','Developer','IT',75000),(3,'Anna Bell','Designer','Marketing',68000);

```

**Output:**

<img width="1216" height="183" alt="image" src="https://github.com/user-attachments/assets/4bfb7e3c-0e8e-4cfc-85bc-62dab102eb89" />


**Question 10**
---
    Create a table named ProjectAssignments with the following constraints:
    AssignmentID as INTEGER should be the primary key.
    EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
    ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
    AssignmentDate as DATE should be NOT NULL.
    For example:
    
    Test	Result
    INSERT INTO ProjectAssignments (AssignmentID, EmployeeID, ProjectID, AssignmentDate) VALUES (2, 99, 1, '2024-01-03');
    Error: FOREIGN KEY constraint failed


```sql
CREATE TABLE ProjectAssignments(
AssignmentID INTEGER PRIMARY KEY,
EmployeeID INTEGER,
ProjectID INTEGER,
AssignmentDate DATE NOT NULL,
FOREIGN KEY (EmployeeID)REFERENCES Employees(EmployeeID),
FOREIGN KEY(ProjectID)REFERENCES Projects(ProjectID)
);
```

**Output:**

<img width="1319" height="145" alt="image" src="https://github.com/user-attachments/assets/005d4fe2-b520-4856-99b9-245d39ba0358" />



## RESULT
<img width="1420" height="246" alt="image" src="https://github.com/user-attachments/assets/29199d76-2982-4b16-a703-98c4ddbc66ad" />

Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
