# Lab 17 – SQL Views in MS SQL Server

## 📌 Introduction

A **View** is a virtual table created from one or more existing tables using a `SELECT` query.

A view does not normally store the actual data separately. It stores the **query definition**, and when we use the view, SQL Server retrieves the required data from the underlying table(s).

### Basic Idea

```text
Base Table
    ↓
   SELECT Query
    ↓
   VIEW
    ↓
Virtual Table
    ↓
SELECT / UPDATE / DELETE
```

For example, suppose we have an `EMPLOYEE` table:

```text
EMPLOYEE
------------------------------------------------
EID | FIRSTNAME | DEPARTMENT | SALARY | CITY
------------------------------------------------
101 | RAJU      | IT         | 15000  | Rajkot
102 | AMIT      | HR         | 12000  | Surat
103 | NEHA      | IT         | 18000  | Ahmedabad
104 | PRIYA     | ADMIN      | 9000   | Rajkot
```

Instead of writing the same `SELECT` query repeatedly, we can create a view.

---

# 1. CREATE VIEW

The basic syntax for creating a view is:

```sql
CREATE VIEW ViewName
AS
SELECT columns
FROM TableName;
```

### Example

```sql
CREATE VIEW Employee_All
AS
SELECT *
FROM EMPLOYEE;
```

Now we can use:

```sql
SELECT *
FROM Employee_All;
```

The view behaves like a virtual table.

---

# 2. VIEW WITH SELECTED COLUMNS

We do not always need all columns.

```sql
CREATE VIEW Employee_Basic
AS
SELECT EID, FIRSTNAME, DEPARTMENT
FROM EMPLOYEE;
```

Use the view:

```sql
SELECT *
FROM Employee_Basic;
```

Only the selected columns are available through the view.

---

# 3. VIEW WITH WHERE CONDITION

A view can contain a `WHERE` condition.

### Example

Create a view containing only IT employees:

```sql
CREATE VIEW IT_Employees
AS
SELECT *
FROM EMPLOYEE
WHERE DEPARTMENT = 'IT';
```

Use it:

```sql
SELECT *
FROM IT_Employees;
```

### Flow

```text
EMPLOYEE
   ↓
WHERE DEPARTMENT = 'IT'
   ↓
IT_Employees VIEW
   ↓
SELECT * FROM IT_Employees
```

---

# 4. VIEW WITH MULTIPLE CONDITIONS

A view can contain multiple conditions.

```sql
CREATE VIEW High_Salary_Employees
AS
SELECT *
FROM EMPLOYEE
WHERE SALARY > 12000
  AND DEPARTMENT = 'IT';
```

Use:

```sql
SELECT *
FROM High_Salary_Employees;
```

---

# 5. VIEW WITH BETWEEN

`BETWEEN` can be used inside a view.

```sql
CREATE VIEW Salary_Between
AS
SELECT *
FROM EMPLOYEE
WHERE SALARY BETWEEN 10000 AND 14000;
```

Use:

```sql
SELECT *
FROM Salary_Between;
```

`BETWEEN` includes both boundary values.

```text
10000 <= SALARY <= 14000
```

---

# 6. VIEW WITH LIKE

A view can also use the `LIKE` operator.

### Name starts with R

```sql
CREATE VIEW Employees_Start_R
AS
SELECT *
FROM EMPLOYEE
WHERE FIRSTNAME LIKE 'R%';
```

### Name ends with A

```sql
CREATE VIEW Employees_End_A
AS
SELECT *
FROM EMPLOYEE
WHERE FIRSTNAME LIKE '%A';
```

### Name contains H

```sql
CREATE VIEW Employees_NameContains_H
AS
SELECT *
FROM EMPLOYEE
WHERE FIRSTNAME LIKE '%H%';
```

---

# 7. VIEW WITH DATE CONDITION

A view can filter records using dates.

```sql
CREATE VIEW Employee_2026
AS
SELECT *
FROM EMPLOYEE
WHERE YEAR(JOINING_DATE) = 2026;
```

Another example:

```sql
CREATE VIEW Recent_Employees
AS
SELECT *
FROM EMPLOYEE
WHERE JOINING_DATE > '2023-01-01';
```

---

# 8. VIEW WITH ORDER BY

Normally, a view should be treated as an unordered set of rows.

If sorting is required, use `ORDER BY` when selecting from the view:

```sql
CREATE VIEW Employee_Basic
AS
SELECT EID, FIRSTNAME, SALARY
FROM EMPLOYEE;
```

Then:

```sql
SELECT *
FROM Employee_Basic
ORDER BY SALARY DESC;
```

This is the preferred approach because the final query decides how the result should be sorted.

---

# 9. VIEW WITH JOIN

A view can be created using more than one table.

Suppose we have:

```text
EMPLOYEE
    |
    | DEPARTMENT
    ↓
DEPARTMENT
```

Example:

```sql
CREATE VIEW Employee_Department
AS
SELECT
    E.EID,
    E.FIRSTNAME,
    E.SALARY,
    D.DEPARTMENTNAME
FROM EMPLOYEE AS E
INNER JOIN DEPARTMENT AS D
    ON E.DEPARTMENTID = D.DEPARTMENTID;
```

Use:

```sql
SELECT *
FROM Employee_Department;
```

### Flow

```text
EMPLOYEE
     +
DEPARTMENT
     ↓
   JOIN
     ↓
 Employee_Department
     ↓
    SELECT
```

---

# 10. VIEW WITH AGGREGATE FUNCTION

A view can contain aggregate functions such as:

- `COUNT()`
- `SUM()`
- `AVG()`
- `MAX()`
- `MIN()`

Example:

```sql
CREATE VIEW Department_Salary
AS
SELECT
    DEPARTMENT,
    AVG(SALARY) AS Average_Salary,
    MAX(SALARY) AS Maximum_Salary,
    MIN(SALARY) AS Minimum_Salary
FROM EMPLOYEE
GROUP BY DEPARTMENT;
```

Use:

```sql
SELECT *
FROM Department_Salary;
```

---

# 11. VIEW WITH GROUP BY

A view can store grouped information.

```sql
CREATE VIEW Department_Employee_Count
AS
SELECT
    DEPARTMENT,
    COUNT(*) AS Total_Employees
FROM EMPLOYEE
GROUP BY DEPARTMENT;
```

Use:

```sql
SELECT *
FROM Department_Employee_Count;
```

### Flow

```text
EMPLOYEE
   ↓
GROUP BY DEPARTMENT
   ↓
COUNT employees
   ↓
VIEW
```

---

# 12. VIEW WITH ALIAS

Column aliases can be used inside a view.

```sql
CREATE VIEW Employee_Salary
AS
SELECT
    EID AS Employee_ID,
    FIRSTNAME AS Employee_Name,
    SALARY AS Employee_Salary
FROM EMPLOYEE;
```

Then:

```sql
SELECT *
FROM Employee_Salary;
```

The view will display the renamed column names.

---

# 13. USING A VIEW

Once a view is created, we can query it just like a table.

### SELECT

```sql
SELECT *
FROM Employee_Basic;
```

### Select specific columns

```sql
SELECT EID, FIRSTNAME
FROM Employee_Basic;
```

### WHERE

```sql
SELECT *
FROM Employee_Basic
WHERE DEPARTMENT = 'IT';
```

### ORDER BY

```sql
SELECT *
FROM Employee_Basic
ORDER BY FIRSTNAME;
```

### GROUP BY

```sql
SELECT DEPARTMENT, COUNT(*)
FROM Employee_Basic
GROUP BY DEPARTMENT;
```

---

# 14. UPDATE THROUGH A VIEW

Some views are **updatable**.

For example:

```sql
CREATE VIEW Employee_Basic
AS
SELECT EID, FIRSTNAME, DEPARTMENT, SALARY
FROM EMPLOYEE;
```

We can update an underlying row through the view:

```sql
UPDATE Employee_Basic
SET SALARY = 20000
WHERE EID = 101;
```

The corresponding row in `EMPLOYEE` is updated.

### Important

```text
View
 ↓
Underlying Table
 ↓
Data is actually changed in the base table
```

A view is not normally a separate copy of the data.

---

# 15. INSERT THROUGH A VIEW

If the view satisfies SQL Server's rules for an updatable view, an `INSERT` may be possible.

Example:

```sql
CREATE VIEW Employee_Basic
AS
SELECT EID, FIRSTNAME, DEPARTMENT
FROM EMPLOYEE;
```

Then:

```sql
INSERT INTO Employee_Basic
(EID, FIRSTNAME, DEPARTMENT)
VALUES
(110, 'KARAN', 'IT');
```

The record is inserted into the underlying `EMPLOYEE` table if the view and base table allow it.

---

# 16. DELETE THROUGH A VIEW

For a suitable updatable view, records can also be deleted.

```sql
DELETE FROM Employee_Basic
WHERE EID = 110;
```

The corresponding record is deleted from the underlying table.

### Important

Be careful with `UPDATE`, `INSERT`, and `DELETE` through views because they can modify the actual base table data.

---

# 17. ALTER VIEW

If we want to change the query definition of an existing view, use `ALTER VIEW`.

### Syntax

```sql
ALTER VIEW ViewName
AS
SELECT ...
FROM ...;
```

### Example

Original:

```sql
CREATE VIEW IT_Employees
AS
SELECT *
FROM EMPLOYEE
WHERE DEPARTMENT = 'IT';
```

Change the view:

```sql
ALTER VIEW IT_Employees
AS
SELECT EID, FIRSTNAME, SALARY
FROM EMPLOYEE
WHERE DEPARTMENT = 'IT';
```

Now the view contains only:

```text
EID
FIRSTNAME
SALARY
```

---

# 18. DROP VIEW

To permanently remove a view:

```sql
DROP VIEW Employee_Basic;
```

After dropping:

```sql
SELECT *
FROM Employee_Basic;
```

will give an error because the view no longer exists.

### Important

Dropping a view does **not** delete the original table data.

```text
DROP VIEW
     ↓
View deleted
     ↓
Base table remains
     ↓
Base table data remains
```

---

# 19. CREATE OR ALTER VIEW

SQL Server also supports `CREATE OR ALTER VIEW`.

It is useful when we are not sure whether the view already exists.

```sql
CREATE OR ALTER VIEW Employee_Basic
AS
SELECT
    EID,
    FIRSTNAME,
    DEPARTMENT,
    SALARY
FROM EMPLOYEE;
```

If the view does not exist → it is created.

If the view already exists → it is modified.

---

# 20. VIEW WITH CHECK OPTION

`WITH CHECK OPTION` ensures that changes made through the view do not create rows that fall outside the view's condition.

Example:

```sql
CREATE VIEW IT_Employees
AS
SELECT EID, FIRSTNAME, DEPARTMENT, SALARY
FROM EMPLOYEE
WHERE DEPARTMENT = 'IT'
WITH CHECK OPTION;
```

Now an update through the view that changes the department from `IT` to `HR` is rejected because the row would no longer satisfy the view condition.

```text
View condition
      ↓
DEPARTMENT = 'IT'
      ↓
Update through view
      ↓
Still satisfies condition?
     / \
   YES  NO
    |    |
  Allow Reject
```

---

# 21. VIEW WITH DISTINCT

A view can contain `DISTINCT`.

```sql
CREATE VIEW Branch_List
AS
SELECT DISTINCT DEPARTMENT
FROM EMPLOYEE;
```

Use:

```sql
SELECT *
FROM Branch_List;
```

This returns each department only once.

---

# 22. VIEW WITH TOP

A view can also use `TOP`.

```sql
CREATE VIEW Top_Employees
AS
SELECT TOP 5
    EID,
    FIRSTNAME,
    SALARY
FROM EMPLOYEE
ORDER BY SALARY DESC;
```

This creates a view containing the top 5 employees according to salary.

---

# 23. View Naming Convention

Use meaningful names for views.

Examples:

```text
Employee_All
Employee_Basic
IT_Employees
HR_Employees
High_Salary_Employees
Salary_Between
Recent_Employees
Department_Salary
Employee_Department
Branch_List
```

A common naming style is:

```text
<Information>_<Purpose>
```

---

# 24. Why Use Views?

Views are useful for:

### 1. Simplicity

Instead of repeatedly writing a complex query:

```sql
SELECT ...
FROM ...
JOIN ...
WHERE ...
```

create a view once:

```sql
CREATE VIEW Employee_Details
AS
SELECT ...;
```

Then:

```sql
SELECT *
FROM Employee_Details;
```

### 2. Security

A view can expose only selected columns.

For example:

```sql
CREATE VIEW Employee_Public
AS
SELECT EID, FIRSTNAME, DEPARTMENT
FROM EMPLOYEE;
```

Sensitive columns such as salary or personal information can be excluded.

### 3. Reusability

The same query can be reused many times.

### 4. Abstraction

Users can work with the view without needing to know the complete underlying query.

---

# 25. View vs Table

| Feature | Table | View |
|---|---|---|
| Stores actual data | Yes | Normally no |
| Created using | `CREATE TABLE` | `CREATE VIEW` |
| Contains rows/columns | Yes | Yes, logically |
| Can contain SELECT query | No | Yes |
| Can use JOIN | Not applicable | Yes |
| Can use WHERE | Not applicable | Yes |
| Can use GROUP BY | Not applicable | Yes |
| Can be queried with SELECT | Yes | Yes |
| DROP removes data | Yes, table data | No base-table data |
| Purpose | Store data | Present/reuse data |

---

# 26. Table vs View Flow

### Table

```text
INSERT DATA
    ↓
TABLE
    ↓
DATA IS STORED
```

### View

```text
BASE TABLE
    ↓
SELECT QUERY
    ↓
VIEW
    ↓
DATA IS DISPLAYED FROM BASE TABLE
```

---

# 27. Simple Complete Example

### Step 1 – Create Table

```sql
CREATE TABLE EMPLOYEE
(
    EID INT PRIMARY KEY,
    FIRSTNAME VARCHAR(50),
    DEPARTMENT VARCHAR(50),
    SALARY DECIMAL(10,2),
    CITY VARCHAR(50)
);
```

### Step 2 – Insert Data

```sql
INSERT INTO EMPLOYEE
VALUES
(101, 'RAJU', 'IT', 15000, 'Rajkot'),
(102, 'AMIT', 'HR', 12000, 'Surat'),
(103, 'NEHA', 'IT', 18000, 'Ahmedabad'),
(104, 'PRIYA', 'ADMIN', 9000, 'Rajkot'),
(105, 'KARAN', 'IT', 22000, 'Ahmedabad');
```

### Step 3 – Create View

```sql
CREATE VIEW High_Salary_Employees
AS
SELECT
    EID,
    FIRSTNAME,
    DEPARTMENT,
    SALARY
FROM EMPLOYEE
WHERE SALARY > 12000;
```

### Step 4 – Use View

```sql
SELECT *
FROM High_Salary_Employees;
```

### Step 5 – Sort View Data

```sql
SELECT *
FROM High_Salary_Employees
ORDER BY SALARY DESC;
```

### Step 6 – Modify View

```sql
ALTER VIEW High_Salary_Employees
AS
SELECT
    EID,
    FIRSTNAME,
    DEPARTMENT,
    SALARY,
    CITY
FROM EMPLOYEE
WHERE SALARY > 15000;
```

### Step 7 – Remove View

```sql
DROP VIEW High_Salary_Employees;
```

---

# 28. Basic View Syntax Cheat Sheet

### Create

```sql
CREATE VIEW ViewName
AS
SELECT ...
FROM ...;
```

### Create or Alter

```sql
CREATE OR ALTER VIEW ViewName
AS
SELECT ...
FROM ...;
```

### Use

```sql
SELECT *
FROM ViewName;
```

### Alter

```sql
ALTER VIEW ViewName
AS
SELECT ...
FROM ...;
```

### Drop

```sql
DROP VIEW ViewName;
```

---

# 29. Important Concepts to Remember

```text
VIEW
↓
Virtual table based on a SELECT query

CREATE VIEW
↓
Create a new view

SELECT FROM VIEW
↓
Read data through the view

ALTER VIEW
↓
Change the view definition

DROP VIEW
↓
Remove the view

WITH CHECK OPTION
↓
Restrict modifications through the view

VIEW + JOIN
↓
Combine data from multiple tables

VIEW + GROUP BY
↓
Create summarized information

VIEW + WHERE
↓
Create filtered information
```

---

# 30. Final Revision

```text
                VIEW
                  |
        ----------------------
        |         |          |
      SELECT     JOIN      WHERE
        |         |          |
        ----------------------
                  |
            Virtual Table
                  |
       ---------------------
       |         |         |
     SELECT    UPDATE    DELETE
       |
     Result
```

### Easy Definition

> **A View is a virtual table based on a SELECT query that provides a reusable and simplified way to access data from one or more tables.**

### Most Important Commands

```sql
-- Create
CREATE VIEW ViewName
AS
SELECT ...;

-- Use
SELECT * FROM ViewName;

-- Modify
ALTER VIEW ViewName
AS
SELECT ...;

-- Create or Modify
CREATE OR ALTER VIEW ViewName
AS
SELECT ...;

-- Delete View
DROP VIEW ViewName;
```
