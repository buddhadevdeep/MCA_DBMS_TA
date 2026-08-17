# DBMS – Microsoft SQL Server
# Lab 1 to Lab 9 – Complete Revision Notes

> **Purpose:** Fast but complete revision for the college DBMS-MSSQL MCQ/practical exam.
>
> **Scope:** This revision covers **only Lab 1 to Lab 9** from the supplied DBMS Lab Manual. Later labs such as mathematical/string/date functions, joins, views, window functions, CTEs, stored procedures, UDFs, triggers, and exception handling are intentionally excluded.

---

# Table of Contents

1. [Lab 1 – SQL Server Management Studio](#lab-1--sql-server-management-studio)
2. [Lab 2 – CREATE and INSERT](#lab-2--create-and-insert)
3. [Lab 3 – SELECT, Operators and Conditions](#lab-3--select-operators-and-conditions)
4. [Lab 4 – UPDATE](#lab-4--update)
5. [Lab 5 – ALTER, RENAME, DELETE, TRUNCATE and DROP](#lab-5--alter-rename-delete-truncate-and-drop)
6. [Lab 6 – SELECT INTO](#lab-6--select-into)
7. [Lab 7 – LIKE and Pattern Searching](#lab-7--like-and-pattern-searching)
8. [Lab 8 – Aggregate Functions and GROUP BY](#lab-8--aggregate-functions-and-group-by)
9. [Lab 9 – GROUP BY, HAVING and ORDER BY](#lab-9--group-by-having-and-order-by)
10. [Most Important Syntax](#most-important-syntax)
11. [Most Important Differences](#most-important-differences)
12. [MCQ Exam Traps](#mcq-exam-traps)
13. [Last-Minute Revision Checklist](#last-minute-revision-checklist)

---

# Lab 1 – SQL Server Management Studio

## 1. What is SSMS?

**SQL Server Management Studio (SSMS)** is the graphical environment used to work with Microsoft SQL Server.

For these labs, the important idea is:

```text
SQL Server
    ↓
SSMS
    ↓
Query Editor
    ↓
Write + Execute T-SQL
    ↓
View Result
```

## 2. Important SSMS Areas

### Query Editor

Used to:

- Write SQL/T-SQL statements
- Execute queries
- Test commands
- View query results and messages

### Object Explorer

Used to navigate database objects such as:

- Databases
- Tables
- Views
- Programmability objects
- Other SQL Server objects

## 3. Basic Query Workflow

```text
Connect to SQL Server
        ↓
Open SSMS
        ↓
Open Query Editor
        ↓
Select/use the required database
        ↓
Write T-SQL
        ↓
Execute
        ↓
Check Results / Messages
```

## 4. Exam Points

Remember:

- SSMS is a **tool/environment**, not a SQL data type.
- T-SQL statements are written/executed in the query editor.
- SQL Server is the database platform; SSMS is the management interface.

---

# Lab 2 – CREATE and INSERT

Lab 2 focuses on creating tables and inserting records.

Typical tables used in the manual include:

- `STUDENT`
- `DEPOSIT`
- `EMPLOYEE`

---

## 1. CREATE TABLE

Basic syntax:

```sql
CREATE TABLE table_name
(
    column1 datatype,
    column2 datatype,
    column3 datatype
);
```

Example:

```sql
CREATE TABLE STUDENT
(
    STDID INT,
    SNAME VARCHAR(50),
    CITY VARCHAR(50),
    SPI DECIMAL(4,2),
    BRANCH VARCHAR(30)
);
```

---

## 2. Important Data Types

### INT

Used for whole numbers.

Example:

```sql
STDID INT
```

### VARCHAR(n)

Used for variable-length text.

Example:

```sql
SNAME VARCHAR(50)
```

### DECIMAL(p,s)

Used for numeric values with precision and scale.

Example:

```sql
SPI DECIMAL(4,2)
```

Meaning:

- `4` = total number of digits
- `2` = digits after decimal

### DATETIME

Used for date/time values.

Example:

```sql
ADATE DATETIME
```

---

# DEPOSIT Table

Important columns:

```text
ACTNO
CNAME
BNAME
AMOUNT
ADATE
```

Example structure:

```sql
CREATE TABLE DEPOSIT
(
    ACTNO INT,
    CNAME VARCHAR(50),
    BNAME VARCHAR(50),
    AMOUNT DECIMAL(10,2),
    ADATE DATETIME
);
```

---

# STUDENT Table

Important columns:

```text
STDID
SNAME
CITY
SPI
BRANCH
```

---

# EMPLOYEE Table

Important columns used throughout Labs 7–9 include:

```text
EID
FIRSTNAME
LASTNAME
DEPARTMENT
SALARY
CITY
GENDER
JOININGYEAR
```

---

# 3. INSERT INTO

Basic syntax:

```sql
INSERT INTO table_name
VALUES
(value1, value2, value3);
```

Example:

```sql
INSERT INTO STUDENT
VALUES
(101, 'HETVI', 'RAJKOT', 7.40, 'COMPUTER');
```

## Safer form

Specify the columns explicitly:

```sql
INSERT INTO STUDENT
(STDID, SNAME, CITY, SPI, BRANCH)
VALUES
(101, 'HETVI', 'RAJKOT', 7.40, 'COMPUTER');
```

This makes the value-to-column mapping explicit.

---

# 4. String Values

String literals normally use single quotes:

```sql
'RAJKOT'
'COMPUTER'
'HETVI'
```

Do not confuse:

```text
'COMPUTER'  → string value
COMPUTER    → identifier/name in a normal SQL expression
```

---

# 5. NULL

`NULL` represents an unknown/missing value.

It is NOT:

```text
0
''
'NULL'
```

For example:

```sql
INSERT INTO STUDENT
VALUES
(111, 'HARSH', 'RAJKOT', 4.00, NULL);
```

---

# Lab 2 – Quick Exam Checklist

- `CREATE TABLE`
- Column names
- Data types
- `INT`
- `VARCHAR`
- `DECIMAL(p,s)`
- `DATETIME`
- `INSERT INTO`
- `VALUES`
- String literals
- NULL values
- Column order

---

# Lab 3 – SELECT, Operators and Conditions

The supplied manual explicitly covers retrieving all data, selecting particular columns, filtering with conditions, `OR`, `IN`, `AND`, `BETWEEN`, `NOT`, `NOT IN`, NULL, `DISTINCT`, `TOP 50%`, and `TOP 5`. fileciteturn3file6L354-L390

---

# 1. SELECT

All columns:

```sql
SELECT *
FROM STUDENT;
```

Specific columns:

```sql
SELECT SNAME, CITY
FROM STUDENT;
```

## Remember

```text
SELECT *       → all columns
SELECT A, B    → only A and B
```

---

# 2. WHERE

`WHERE` filters rows.

Example:

```sql
SELECT *
FROM STUDENT
WHERE SPI > 8.0;
```

Only rows satisfying the condition are returned.

---

# 3. Comparison Operators

| Operator | Meaning |
|---|---|
| `=` | Equal |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal |
| `<=` | Less than or equal |
| `<>` | Not equal |
| `!=` | Not equal |

Example:

```sql
WHERE SPI >= 7.0
```

---

# 4. AND

Both conditions must be true.

```sql
SELECT *
FROM STUDENT
WHERE SPI > 8.0
AND STDID < 105;
```

Meaning:

```text
SPI > 8.0
AND
STDID < 105
```

---

# 5. OR

At least one condition must be true.

```sql
SELECT *
FROM STUDENT
WHERE CITY = 'RAJKOT'
OR CITY = 'SURAT';
```

---

# 6. AND + OR

Use parentheses when you need explicit grouping.

```sql
WHERE SPI > 7.5
AND
(CITY = 'RAJKOT' OR CITY = 'SURAT');
```

This is much safer and clearer than relying on precedence.

---

# 7. IN

Instead of:

```sql
WHERE CITY = 'RAJKOT'
OR CITY = 'SURAT';
```

you can write:

```sql
WHERE CITY IN ('RAJKOT', 'SURAT');
```

For branches:

```sql
WHERE BRANCH IN
('COMPUTER', 'CIVIL', 'CHEMICAL');
```

---

# 8. NOT IN

Excludes values.

```sql
WHERE BRANCH NOT IN
('COMPUTER', 'CIVIL');
```

Meaning:

```text
Branch is neither COMPUTER nor CIVIL
```

---

# 9. BETWEEN

Example:

```sql
WHERE SPI BETWEEN 7.0 AND 9.0;
```

**Very important:**

`BETWEEN` is inclusive.

So:

```text
7.0 → included
9.0 → included
```

---

# 10. NOT

Negates a condition.

Example:

```sql
WHERE NOT SNAME = 'DEEP';
```

---

# 11. NOT EQUAL

Both are commonly used:

```sql
WHERE SNAME <> 'DEEP';
```

or:

```sql
WHERE SNAME != 'DEEP';
```

---

# 12. NULL

Never normally write:

```sql
WHERE BRANCH = NULL
```

Correct:

```sql
WHERE BRANCH IS NULL;
```

For non-NULL:

```sql
WHERE BRANCH IS NOT NULL;
```

### MCQ Trap

```sql
NULL = NULL
```

does NOT behave like ordinary equality.

Remember:

```text
IS NULL
IS NOT NULL
```

---

# 13. DISTINCT

Returns unique values.

```sql
SELECT DISTINCT BRANCH
FROM STUDENT;
```

If the data contains:

```text
COMPUTER
COMPUTER
CIVIL
CIVIL
MECHANICAL
```

result:

```text
COMPUTER
CIVIL
MECHANICAL
```

---

# 14. TOP

SQL Server uses `TOP`.

First five rows:

```sql
SELECT TOP 5 *
FROM STUDENT;
```

First 50 percent:

```sql
SELECT TOP 50 PERCENT *
FROM STUDENT;
```

### Important

Do not use MySQL's:

```sql
LIMIT 5
```

for a SQL Server question.

---

# 15. TOP + WHERE

Example:

```sql
SELECT TOP 3 *
FROM STUDENT
WHERE SPI > 8.0;
```

This means:

1. Consider students satisfying `SPI > 8.0`
2. Return TOP 3 from that result

---

# Lab 3 – Important Practice Patterns

### Pattern 1

```sql
SELECT SNAME, CITY, SPI
FROM STUDENT
WHERE SPI > 6.50;
```

### Pattern 2

```sql
SELECT SNAME
FROM STUDENT
WHERE BRANCH = 'COMPUTER'
AND SPI > 8.0;
```

### Pattern 3

```sql
SELECT SNAME
FROM STUDENT
WHERE CITY IN ('RAJKOT', 'SURAT');
```

### Pattern 4

```sql
SELECT *
FROM STUDENT
WHERE SPI BETWEEN 7.0 AND 9.0;
```

### Pattern 5

```sql
SELECT SNAME
FROM STUDENT
WHERE BRANCH NOT IN ('COMPUTER', 'CIVIL');
```

### Pattern 6

```sql
SELECT SNAME
FROM STUDENT
WHERE BRANCH IS NULL;
```

---

# Lab 3 – MCQ Traps

| Trap | Correct idea |
|---|---|
| `= NULL` | Use `IS NULL` |
| `!= NULL` | Use `IS NOT NULL` |
| `BETWEEN 7 AND 9` | Includes 7 and 9 |
| `%` | Not used for normal equality |
| `IN` | Checks a list |
| `NOT IN` | Excludes a list |
| `TOP` | SQL Server row limiting |
| `LIMIT` | Not SQL Server TOP syntax |
| `DISTINCT` | Removes duplicate result values |

---

# Lab 4 – UPDATE

The key concept of Lab 4 is modifying existing records.

---

# 1. Basic UPDATE

```sql
UPDATE STUDENT
SET SPI = 8.00
WHERE STDID = 101;
```

Meaning:

```text
Find STDID 101
        ↓
Change SPI to 8.00
```

---

# 2. Update Multiple Columns

```sql
UPDATE STUDENT
SET SPI = 8.00,
    CITY = 'SURAT'
WHERE STDID = 101;
```

### Important

Assignments in `SET` are separated by commas:

```text
SET A = value,
    B = value
```

Not:

```text
SET A = value AND B = value
```

---

# 3. UPDATE with Condition

```sql
UPDATE STUDENT
SET CITY = 'SURAT'
WHERE SPI < 7.0;
```

Only matching rows change.

---

# 4. UPDATE Without WHERE

```sql
UPDATE STUDENT
SET CITY = 'SURAT';
```

**Very dangerous:**

Every row may be updated.

### Exam trap

```text
UPDATE + WHERE       → selected rows
UPDATE without WHERE → all rows
```

---

# 5. Arithmetic UPDATE

Increase SPI by 0.50:

```sql
UPDATE STUDENT
SET SPI = SPI + 0.50;
```

Decrease:

```sql
SET SPI = SPI - 0.50
```

Multiply:

```sql
SET SPI = SPI * 1.10
```

A 10% increase:

```sql
SET SALARY = SALARY * 1.10
```

---

# 6. UPDATE with BETWEEN

```sql
UPDATE STUDENT
SET SPI = 7.50
WHERE STDID BETWEEN 103 AND 107;
```

Remember:

`BETWEEN` includes both boundaries.

---

# 7. UPDATE NULL

To set a column to SQL NULL:

```sql
UPDATE STUDENT
SET BRANCH = NULL
WHERE STDID = 111;
```

Do not write:

```sql
SET BRANCH = 'NULL'
```

because that is a text value.

---

# Lab 4 – Exam Traps

### Trap 1

```sql
UPDATE STUDENT
SET SPI = 8.0;
```

All rows can change.

### Trap 2

```sql
SET SPI = 8.0,
    CITY = 'SURAT'
```

Correct multiple-column syntax.

### Trap 3

```sql
SET SPI = SPI + 0.5
```

Uses the existing value.

### Trap 4

```sql
SET SPI = NULL
```

Stores SQL NULL.

---

# Lab 5 – ALTER, RENAME, DELETE, TRUNCATE and DROP

The supplied manual covers changing column data types, deleting columns, renaming columns, adding columns, changing a table name, conditional DELETE, TRUNCATE, and DROP. fileciteturn4file7L433-L458

This is one of the **most important MCQ labs**.

---

# 1. ALTER TABLE

General form:

```sql
ALTER TABLE table_name
...
```

---

# 2. ADD COLUMN

Example:

```sql
ALTER TABLE DEPOSIT
ADD STATUS VARCHAR(10);
```

---

# 3. DROP COLUMN

Example:

```sql
ALTER TABLE DEPOSIT
DROP COLUMN ACCOUNT_TYPE;
```

---

# 4. ALTER COLUMN

In SQL Server, changing a column definition uses:

```sql
ALTER TABLE table_name
ALTER COLUMN column_name datatype;
```

Example:

```sql
ALTER TABLE DEPOSIT
ALTER COLUMN PINCODE BIGINT;
```

---

# 5. RENAME COLUMN – SQL Server

The lab uses `sp_rename`.

Example:

```sql
EXEC sp_rename
'DEPOSIT.AMOUNT',
'BALANCE',
'COLUMN';
```

Breakdown:

```text
DEPOSIT.AMOUNT → old column
BALANCE        → new column
COLUMN         → object type
```

---

# 6. Rename Table

SQL Server can also use `sp_rename` for a table.

General form:

```sql
EXEC sp_rename
'old_table_name',
'new_table_name';
```

Example:

```sql
EXEC sp_rename
'deposit_detail',
'bank_deposit';
```

---

# 7. DELETE

Delete selected rows:

```sql
DELETE FROM DEPOSIT
WHERE AMOUNT <= 3000;
```

Delete by branch:

```sql
DELETE FROM DEPOSIT
WHERE BNAME = 'BEDI';
```

Multiple conditions:

```sql
DELETE FROM DEPOSIT
WHERE AMOUNT = 7000
AND CNAME = 'CHARMI'
AND BNAME = 'SHITAL PARK';
```

---

# 8. DELETE with OR

```sql
DELETE FROM DEPOSIT
WHERE BNAME = 'BEDI'
OR BNAME = 'MADHAPAR';
```

Better list form:

```sql
DELETE FROM DEPOSIT
WHERE BNAME IN ('BEDI', 'MADHAPAR');
```

---

# 9. DELETE NULL Rows

Correct:

```sql
DELETE FROM DEPOSIT
WHERE BNAME IS NULL;
```

Wrong:

```sql
DELETE FROM DEPOSIT
WHERE BNAME = NULL;
```

---

# 10. DELETE All Rows

```sql
DELETE FROM DEPOSIT;
```

This removes all rows but leaves the table object.

---

# 11. TRUNCATE

```sql
TRUNCATE TABLE DEPOSIT;
```

Removes all rows and keeps the table definition.

---

# 12. DROP

```sql
DROP TABLE DEPOSIT;
```

Removes the table object.

---

# 13. DELETE vs TRUNCATE vs DROP

| Command | Removes Rows | Removes Table Structure | WHERE |
|---|---:|---:|---|
| `DELETE` | Yes | No | Yes |
| `TRUNCATE` | All rows | No | No |
| `DROP TABLE` | Yes, with object | Yes | No |

### Memory Trick

```text
DELETE    → Data
TRUNCATE  → All Data
DROP      → Table itself
```

---

# Lab 5 – High-Probability MCQs

## Question type

**Which removes all rows but keeps the table?**

Answer:

```sql
TRUNCATE TABLE
```

## Question type

**Which removes the table itself?**

Answer:

```sql
DROP TABLE
```

## Question type

**Which supports WHERE?**

Answer:

```sql
DELETE
```

## Question type

**Which SQL Server procedure renames an object?**

Answer:

```sql
sp_rename
```

---

# Lab 6 – SELECT INTO

The manual's Lab 6 specifically covers copying filtered DEPOSIT records, selected columns, dates, distinct branches, TOP records, BETWEEN, NULL records, aliases, IN, and creating a structure without copying data. fileciteturn3file0L41-L60

---

# 1. Basic SELECT INTO

```sql
SELECT *
INTO HIGH_AMOUNT
FROM DEPOSIT
WHERE AMOUNT > 3000;
```

Meaning:

```text
DEPOSIT
   ↓
Filter AMOUNT > 3000
   ↓
Create HIGH_AMOUNT
   ↓
Copy result
```

---

# 2. Copy Selected Columns

```sql
SELECT CNAME, AMOUNT
INTO MAVDI_CUSTOMERS
FROM DEPOSIT
WHERE BNAME = 'MAVDI';
```

The new table contains only:

```text
CNAME
AMOUNT
```

---

# 3. SELECT INTO + DISTINCT

```sql
SELECT DISTINCT BNAME
INTO BRANCH_LIST
FROM DEPOSIT;
```

Creates a new table containing unique branch values.

---

# 4. SELECT INTO + TOP

```sql
SELECT TOP 5 *
INTO TOP_DEPOSITS
FROM DEPOSIT;
```

Creates a new table using TOP 5 rows from the SELECT result.

---

# 5. SELECT INTO + BETWEEN

```sql
SELECT *
INTO MID_RANGE
FROM DEPOSIT
WHERE AMOUNT BETWEEN 2000 AND 6000;
```

Both boundaries are included.

---

# 6. SELECT INTO + NULL

```sql
SELECT *
INTO NO_BRANCH_ASSIGNED
FROM DEPOSIT
WHERE BNAME IS NULL;
```

---

# 7. SELECT INTO + IN

```sql
SELECT *
INTO SELECTED_BRANCH
FROM DEPOSIT
WHERE BNAME IN ('MAVDI','BEDI');
```

---

# 8. Rename Result Column with Alias

```sql
SELECT AMOUNT AS BALANCE
INTO DEPOSIT_COPY
FROM DEPOSIT;
```

The new table gets the resulting column name `BALANCE`.

---

# 9. Create Table Structure Without Data

A common SQL Server pattern:

```sql
SELECT *
INTO STUDENT_BACKUP
FROM STUDENT
WHERE 1 = 0;
```

Since:

```text
1 = 0 → FALSE
```

no rows are copied, but the SELECT INTO operation creates the destination table from the result definition.

---

# 10. SELECT INTO – Important Facts

### Source table

Remains available.

### Destination table

Is created by the SELECT INTO operation.

### Existing destination

Normally, the destination table should not already exist for ordinary SELECT INTO use.

---

# Lab 6 – Exam Traps

```text
SELECT INTO → creates a new table
INSERT INTO → inserts into an existing table
```

Do not confuse:

```sql
SELECT INTO
```

with:

```sql
INSERT INTO ... SELECT
```

---

# Lab 7 – LIKE and Pattern Searching

Lab 7 focuses heavily on pattern matching with `LIKE`, including first/last characters, character positions, vowels, and combinations with other conditions. The manual also includes patterns such as a second-character vowel and conditions using NULL/department filters. fileciteturn1file6L370-L375

---

# 1. LIKE

Used for pattern matching.

Basic form:

```sql
WHERE column_name LIKE 'pattern';
```

---

# 2. `%`

`%` represents:

```text
Zero or more characters
```

Example:

```sql
WHERE FIRSTNAME LIKE 'H%';
```

Means:

```text
Starts with H
```

Possible matches:

```text
HETVI
HARSH
H...
```

---

# 3. `%` at the Beginning

```sql
WHERE FIRSTNAME LIKE '%A';
```

Means:

```text
Ends with A
```

---

# 4. `%` on Both Sides

```sql
WHERE FIRSTNAME LIKE '%AR%';
```

Means:

```text
Contains AR anywhere
```

---

# 5. `_`

Underscore represents:

```text
Exactly one character
```

Example:

```sql
WHERE FIRSTNAME LIKE '_A%';
```

Meaning:

```text
First character = anything
Second character = A
Remaining characters = anything
```

---

# 6. Exactly Five Characters

```sql
WHERE FIRSTNAME LIKE '_____';
```

Five underscores:

```text
_ _ _ _ _
```

means exactly five character positions.

---

# 7. First + Last Pattern

Starts with R and ends with A:

```sql
WHERE FIRSTNAME LIKE 'R%A';
```

---

# 8. Specific Character Position

Suppose the second character must be a vowel:

```sql
WHERE FIRSTNAME LIKE '_[AEIOU]%';
```

Breakdown:

```text
_          → first character
[AEIOU]    → second character is a vowel
%          → remaining characters
```

---

# 9. Character Range / Character List

SQL Server LIKE patterns can use bracket expressions.

Example:

```sql
LIKE '[AEIOU]%'
```

Means first character is one of A, E, I, O, U.

---

# 10. NOT LIKE

Example:

```sql
WHERE FIRSTNAME NOT LIKE 'A%';
```

Means:

```text
FIRSTNAME does not start with A
```

---

# 11. LIKE + AND

Example:

```sql
WHERE FIRSTNAME LIKE 'V%'
AND SALARY < 12000;
```

Both conditions must hold.

---

# 12. LIKE + NULL

Important:

```sql
CITY LIKE '%RAJ%'
```

does not replace:

```sql
CITY IS NULL
```

NULL must be handled separately.

---

# LIKE Cheat Sheet

| Requirement | Pattern |
|---|---|
| Starts with H | `'H%'` |
| Ends with A | `'%A'` |
| Contains AR | `'%AR%'` |
| Exactly 5 characters | `'_____'` |
| Starts R, ends A | `'R%A'` |
| Second character is A | `'_A%'` |
| Second character vowel | `'_[AEIOU]%'` |
| Does not start A | `NOT LIKE 'A%'` |

---

# Lab 7 – Biggest MCQ Trap

Do not confuse:

```text
% → zero or more characters
_ → exactly one character
```

Example:

```sql
LIKE 'A%'
```

can match:

```text
A
AMIT
AMIT...
```

But:

```sql
LIKE 'A_'
```

requires exactly two character positions:

```text
A + one character
```

---

# Lab 8 – Aggregate Functions and GROUP BY

The manual's Lab 8 covers highest/lowest salary, total/average salary, employee counts, distinct cities/departments, city-wise and department-wise aggregation, gender-based aggregation, and multi-column grouping. fileciteturn1file6L376-L412

---

# 1. Aggregate Functions

Main functions:

```text
COUNT()
SUM()
AVG()
MIN()
MAX()
```

---

# 2. MAX

Highest value:

```sql
SELECT MAX(SALARY)
FROM EMPLOYEE;
```

---

# 3. MIN

Lowest value:

```sql
SELECT MIN(SALARY)
FROM EMPLOYEE;
```

---

# 4. SUM

Total:

```sql
SELECT SUM(SALARY)
FROM EMPLOYEE;
```

---

# 5. AVG

Average:

```sql
SELECT AVG(SALARY)
FROM EMPLOYEE;
```

---

# 6. COUNT

Total number of rows:

```sql
SELECT COUNT(*)
FROM EMPLOYEE;
```

---

# 7. COUNT(column)

```sql
SELECT COUNT(CITY)
FROM EMPLOYEE;
```

Important:

`COUNT(column)` counts non-NULL values of that column.

---

# 8. COUNT(DISTINCT column)

```sql
SELECT COUNT(DISTINCT CITY)
FROM EMPLOYEE;
```

Counts unique non-NULL city values.

---

# 9. GROUP BY

Used to divide rows into groups.

Example:

```sql
SELECT DEPARTMENT, MAX(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT;
```

Result concept:

```text
DEPARTMENT    MAX(SALARY)
-------------------------
ADMIN         ...
COMPUTER      ...
HR            ...
IT            ...
```

---

# 10. City-Wise Count

```sql
SELECT CITY, COUNT(*)
FROM EMPLOYEE
GROUP BY CITY;
```

---

# 11. Department-Wise Total Salary

```sql
SELECT DEPARTMENT, SUM(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT;
```

---

# 12. Department-Wise Average

```sql
SELECT DEPARTMENT, AVG(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT;
```

---

# 13. Gender-Wise Salary

```sql
SELECT GENDER, SUM(SALARY)
FROM EMPLOYEE
GROUP BY GENDER;
```

---

# 14. Multiple GROUP BY Columns

Example:

```sql
SELECT DEPARTMENT, CITY, GENDER, AVG(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT, CITY, GENDER;
```

Groups by the combination:

```text
DEPARTMENT + CITY + GENDER
```

---

# 15. WHERE with GROUP BY

`WHERE` filters rows before grouping.

Example:

```sql
SELECT DEPARTMENT, MAX(SALARY)
FROM EMPLOYEE
WHERE CITY <> 'AHMEDABAD'
GROUP BY DEPARTMENT;
```

Concept:

```text
EMPLOYEE rows
     ↓
WHERE
     ↓
GROUP BY
     ↓
MAX
```

---

# 16. Aggregate Difference

Highest minus lowest:

```sql
SELECT MAX(SALARY) - MIN(SALARY)
FROM EMPLOYEE;
```

With alias:

```sql
SELECT
    MAX(SALARY) - MIN(SALARY) AS DIFFERENCE
FROM EMPLOYEE;
```

---

# 17. NULL and Aggregate Functions

Important exam rule:

```text
COUNT(*)        → counts rows
COUNT(column)   → counts non-NULL values
SUM(column)     → ignores NULL values in aggregation
AVG(column)     → ignores NULL values in aggregation
MIN/MAX          → operate on available non-NULL values
```

For MCQs, always inspect whether a column contains NULL.

---

# Lab 8 – Common Exam Patterns

### Maximum salary

```sql
SELECT MAX(SALARY)
FROM EMPLOYEE;
```

### Minimum salary

```sql
SELECT MIN(SALARY)
FROM EMPLOYEE;
```

### Total salary

```sql
SELECT SUM(SALARY)
FROM EMPLOYEE;
```

### Average salary

```sql
SELECT AVG(SALARY)
FROM EMPLOYEE;
```

### Employee count

```sql
SELECT COUNT(*)
FROM EMPLOYEE;
```

### Unique city count

```sql
SELECT COUNT(DISTINCT CITY)
FROM EMPLOYEE;
```

### City-wise count

```sql
SELECT CITY, COUNT(*)
FROM EMPLOYEE
GROUP BY CITY;
```

---

# Lab 9 – GROUP BY, HAVING and ORDER BY

The manual's Lab 9 specifically asks for aggregate conditions such as total salary, average salary, minimum/maximum salary, employee counts, gender-based groups, and ordered department/city results. fileciteturn1file2L130-L164

---

# 1. HAVING

`HAVING` filters groups after grouping.

Example:

```sql
SELECT DEPARTMENT, SUM(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT
HAVING SUM(SALARY) > 20000;
```

Meaning:

```text
Create department groups
        ↓
Calculate SUM(SALARY)
        ↓
Keep groups whose SUM > 20000
```

---

# 2. WHERE vs HAVING

This is one of the **highest-priority exam topics**.

## WHERE

Filters individual rows.

```sql
WHERE SALARY > 10000
```

## HAVING

Filters grouped results.

```sql
HAVING AVG(SALARY) > 10000
```

### Memory Trick

```text
WHERE  → Rows
HAVING → Groups
```

---

# 3. HAVING COUNT

Departments having more than 2 employees:

```sql
SELECT DEPARTMENT, COUNT(*)
FROM EMPLOYEE
GROUP BY DEPARTMENT
HAVING COUNT(*) > 2;
```

---

# 4. HAVING SUM

```sql
SELECT DEPARTMENT, SUM(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT
HAVING SUM(SALARY) > 20000;
```

---

# 5. HAVING AVG

```sql
SELECT DEPARTMENT, AVG(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT
HAVING AVG(SALARY) > 12000;
```

---

# 6. HAVING MIN

```sql
SELECT CITY, MIN(SALARY)
FROM EMPLOYEE
GROUP BY CITY
HAVING MIN(SALARY) < 7000;
```

---

# 7. HAVING MAX

```sql
SELECT DEPARTMENT, MAX(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT
HAVING MAX(SALARY) > 14000;
```

---

# 8. Multiple HAVING Conditions

Example:

```sql
SELECT DEPARTMENT, AVG(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT
HAVING AVG(SALARY) > 10000
AND AVG(SALARY) < 14000;
```

---

# 9. ORDER BY

Sort ascending:

```sql
ORDER BY SALARY ASC;
```

Sort descending:

```sql
ORDER BY SALARY DESC;
```

---

# 10. Highest to Lowest

```sql
ORDER BY MAX(SALARY) DESC;
```

`DESC` = descending.

---

# 11. Lowest to Highest

```sql
ORDER BY MIN(SALARY) ASC;
```

`ASC` = ascending.

---

# 12. Complete GROUP BY + HAVING + ORDER BY

Example:

```sql
SELECT DEPARTMENT, MAX(SALARY) AS MAX_SALARY
FROM EMPLOYEE
GROUP BY DEPARTMENT
HAVING MAX(SALARY) > 13000
ORDER BY MAX(SALARY) DESC;
```

Understand the purpose of each:

```text
SELECT    → what to display
FROM      → source
GROUP BY  → make groups
HAVING    → filter groups
ORDER BY  → sort final result
```

---

# 13. WHERE + GROUP BY + HAVING

Example:

```sql
SELECT DEPARTMENT, COUNT(*) AS EMP_COUNT
FROM EMPLOYEE
WHERE JOININGYEAR > 2022
GROUP BY DEPARTMENT
HAVING COUNT(*) > 1;
```

Interpretation:

```text
1. Take EMPLOYEE
2. Keep employees who joined after 2022
3. Group remaining rows by department
4. Count employees in each group
5. Keep groups whose count > 1
```

---

# 14. Logical Query Processing Order

For the concepts in Labs 3, 8 and 9, remember this exam sequence:

```text
FROM
  ↓
WHERE
  ↓
GROUP BY
  ↓
HAVING
  ↓
SELECT
  ↓
ORDER BY
```

Do not confuse this with the written syntax order.

Written query usually appears as:

```sql
SELECT ...
FROM ...
WHERE ...
GROUP BY ...
HAVING ...
ORDER BY ...;
```

---

# Lab 9 – High-Probability Patterns

## Departments with total salary > 20000

```sql
SELECT DEPARTMENT, SUM(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT
HAVING SUM(SALARY) > 20000;
```

## Departments with average salary > 12000

```sql
SELECT DEPARTMENT, AVG(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT
HAVING AVG(SALARY) > 12000;
```

## Departments with more than 2 employees

```sql
SELECT DEPARTMENT, COUNT(*)
FROM EMPLOYEE
GROUP BY DEPARTMENT
HAVING COUNT(*) > 2;
```

## Departments ordered by maximum salary

```sql
SELECT DEPARTMENT, MAX(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT
ORDER BY MAX(SALARY) DESC;
```

---

# Most Important Syntax

## SELECT

```sql
SELECT column1, column2
FROM table_name;
```

## SELECT *

```sql
SELECT *
FROM table_name;
```

## WHERE

```sql
SELECT *
FROM table_name
WHERE condition;
```

## IN

```sql
WHERE column IN ('A', 'B');
```

## NOT IN

```sql
WHERE column NOT IN ('A', 'B');
```

## BETWEEN

```sql
WHERE column BETWEEN value1 AND value2;
```

## NULL

```sql
WHERE column IS NULL;
```

```sql
WHERE column IS NOT NULL;
```

## DISTINCT

```sql
SELECT DISTINCT column
FROM table_name;
```

## TOP

```sql
SELECT TOP 5 *
FROM table_name;
```

## TOP PERCENT

```sql
SELECT TOP 50 PERCENT *
FROM table_name;
```

## UPDATE

```sql
UPDATE table_name
SET column = value
WHERE condition;
```

## UPDATE Multiple Columns

```sql
UPDATE table_name
SET column1 = value1,
    column2 = value2
WHERE condition;
```

## ALTER ADD

```sql
ALTER TABLE table_name
ADD column_name datatype;
```

## ALTER COLUMN

```sql
ALTER TABLE table_name
ALTER COLUMN column_name datatype;
```

## DROP COLUMN

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

## RENAME COLUMN

```sql
EXEC sp_rename
'table_name.old_column',
'new_column',
'COLUMN';
```

## DELETE

```sql
DELETE FROM table_name
WHERE condition;
```

## DELETE ALL ROWS

```sql
DELETE FROM table_name;
```

## TRUNCATE

```sql
TRUNCATE TABLE table_name;
```

## DROP TABLE

```sql
DROP TABLE table_name;
```

## SELECT INTO

```sql
SELECT column1, column2
INTO new_table
FROM old_table
WHERE condition;
```

## LIKE

```sql
WHERE column LIKE 'A%';
```

## Aggregate

```sql
SELECT MAX(SALARY)
FROM EMPLOYEE;
```

## GROUP BY

```sql
SELECT DEPARTMENT, AVG(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT;
```

## HAVING

```sql
SELECT DEPARTMENT, AVG(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT
HAVING AVG(SALARY) > 10000;
```

## ORDER BY

```sql
ORDER BY SALARY ASC;
```

```sql
ORDER BY SALARY DESC;
```

---

# Most Important Differences

## DELETE vs TRUNCATE vs DROP

| Feature | DELETE | TRUNCATE | DROP |
|---|---|---|---|
| Removes rows | Yes | Yes, all | Yes, with object |
| Keeps table | Yes | Yes | No |
| WHERE | Yes | No | No |
| Purpose | Selective/all row deletion | Remove all rows | Remove table |

---

# WHERE vs HAVING

| WHERE | HAVING |
|---|---|
| Filters rows | Filters groups |
| Used before GROUP BY | Used after GROUP BY |
| Can use normal row conditions | Commonly used with aggregates |
| Example: `SALARY > 10000` | Example: `AVG(SALARY) > 10000` |

---

# `%` vs `_`

| `%` | `_` |
|---|---|
| Zero or more characters | Exactly one character |
| `H%` | `H_` |
| Starts with H | H + exactly one character |

---

# COUNT(*) vs COUNT(column)

| Expression | Meaning |
|---|---|
| `COUNT(*)` | Counts rows |
| `COUNT(column)` | Counts non-NULL column values |
| `COUNT(DISTINCT column)` | Counts unique non-NULL values |

---

# SELECT INTO vs INSERT INTO

## SELECT INTO

Creates a new table:

```sql
SELECT *
INTO NEW_TABLE
FROM OLD_TABLE;
```

## INSERT INTO

Adds rows to an existing table:

```sql
INSERT INTO EXISTING_TABLE
VALUES (...);
```

---

# ALTER vs UPDATE

## ALTER

Changes table structure.

Examples:

```text
ADD column
DROP column
ALTER COLUMN
```

## UPDATE

Changes data stored in rows.

Example:

```sql
UPDATE STUDENT
SET SPI = 8.5
WHERE STDID = 101;
```

---

# DROP vs DELETE

```text
DELETE → rows
DROP   → table object
```

---

# Lab-by-Lab One-Minute Revision

## Lab 1

Remember:

```text
SSMS
Query Editor
Object Explorer
Execute T-SQL
Results
```

## Lab 2

Remember:

```text
CREATE TABLE
INT
VARCHAR
DECIMAL
DATETIME
INSERT INTO
VALUES
NULL
```

## Lab 3

Remember:

```text
SELECT
WHERE
=
>
<
>=
<=
<>
!=
AND
OR
NOT
IN
NOT IN
BETWEEN
IS NULL
IS NOT NULL
DISTINCT
TOP
TOP PERCENT
```

## Lab 4

Remember:

```text
UPDATE
SET
WHERE
Multiple-column UPDATE
Arithmetic UPDATE
UPDATE + NULL
Danger of UPDATE without WHERE
```

## Lab 5

Remember:

```text
ALTER TABLE
ADD
ALTER COLUMN
DROP COLUMN
sp_rename
DELETE
TRUNCATE
DROP TABLE
```

## Lab 6

Remember:

```text
SELECT INTO
WHERE
DISTINCT
TOP
BETWEEN
IN
IS NULL
Column alias
Empty destination using false WHERE
```

## Lab 7

Remember:

```text
LIKE
%
_
NOT LIKE
[AEIOU]
Prefix
Suffix
Contains
Character position
```

## Lab 8

Remember:

```text
COUNT
SUM
AVG
MIN
MAX
COUNT(*)
COUNT(column)
COUNT(DISTINCT column)
GROUP BY
Multiple GROUP BY columns
```

## Lab 9

Remember:

```text
GROUP BY
HAVING
WHERE vs HAVING
COUNT in HAVING
SUM in HAVING
AVG in HAVING
MIN in HAVING
MAX in HAVING
ORDER BY
ASC
DESC
```

---

# MCQ Exam Traps

## Trap 1

```sql
WHERE BRANCH = NULL
```

Wrong.

Use:

```sql
WHERE BRANCH IS NULL
```

---

## Trap 2

```sql
BETWEEN 7 AND 9
```

Includes:

```text
7
9
```

---

## Trap 3

```text
% ≠ _
```

Remember:

```text
% = zero or more
_ = one
```

---

## Trap 4

```sql
UPDATE STUDENT
SET SPI = 8;
```

Can update every row.

---

## Trap 5

```sql
DELETE FROM STUDENT;
```

Deletes all rows but keeps the table.

---

## Trap 6

```sql
TRUNCATE TABLE STUDENT;
```

Deletes all rows but keeps the table definition.

---

## Trap 7

```sql
DROP TABLE STUDENT;
```

Removes the table object.

---

## Trap 8

SQL Server uses:

```sql
SELECT TOP 5 *
FROM STUDENT;
```

not:

```sql
SELECT LIMIT 5 ...
```

---

## Trap 9

Aggregate condition:

```sql
HAVING SUM(SALARY) > 20000
```

not normally:

```sql
WHERE SUM(SALARY) > 20000
```

---

## Trap 10

`COUNT(column)` ignores NULL values.

`COUNT(*)` counts rows.

---

## Trap 11

Correct GROUP BY:

```sql
SELECT DEPARTMENT, MAX(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT;
```

---

## Trap 12

Correct ORDER BY:

```sql
ORDER BY SALARY DESC
```

means:

```text
Highest → Lowest
```

---

# 25 Most Important Things to Memorize

1. `SELECT *` = all columns.
2. `WHERE` = row filtering.
3. `AND` = both conditions.
4. `OR` = either condition.
5. `IN` = match a list.
6. `NOT IN` = exclude a list.
7. `BETWEEN` = inclusive range.
8. `IS NULL` = test NULL.
9. `IS NOT NULL` = test non-NULL.
10. `DISTINCT` = unique results.
11. `TOP` = SQL Server row limiting.
12. `UPDATE` = modify existing data.
13. `UPDATE` without WHERE can modify every row.
14. `ALTER TABLE` = change table structure.
15. `sp_rename` = SQL Server object renaming.
16. `DELETE` = remove rows.
17. `TRUNCATE` = remove all rows, keep table.
18. `DROP TABLE` = remove table object.
19. `SELECT INTO` = create a new table from a SELECT result.
20. `%` = zero or more characters.
21. `_` = one character.
22. `COUNT(*)` = count rows.
23. `COUNT(column)` = count non-NULL values.
24. `GROUP BY` = create groups.
25. `HAVING` = filter groups.

---

# Last-Minute Revision Checklist

Before the exam, make sure you can answer YES to all of these:

## Lab 1

- [ ] What is SSMS?
- [ ] What is Query Editor?
- [ ] What is Object Explorer?
- [ ] How is a T-SQL query executed?

## Lab 2

- [ ] Can I write CREATE TABLE?
- [ ] Do I know INT?
- [ ] Do I know VARCHAR?
- [ ] Do I know DECIMAL(p,s)?
- [ ] Do I know DATETIME?
- [ ] Can I write INSERT INTO?
- [ ] Do I understand NULL?

## Lab 3

- [ ] Can I write SELECT?
- [ ] Can I use WHERE?
- [ ] Do I know all comparison operators?
- [ ] Do I know AND/OR/NOT?
- [ ] Do I know IN/NOT IN?
- [ ] Do I know BETWEEN?
- [ ] Do I know IS NULL?
- [ ] Do I know IS NOT NULL?
- [ ] Do I know DISTINCT?
- [ ] Do I know TOP?
- [ ] Do I know TOP 50 PERCENT?
- [ ] Can I combine multiple conditions?

## Lab 4

- [ ] Can I write UPDATE?
- [ ] Can I update multiple columns?
- [ ] Can I update using conditions?
- [ ] Can I perform arithmetic updates?
- [ ] Do I understand the danger of UPDATE without WHERE?

## Lab 5

- [ ] Can I ADD a column?
- [ ] Can I ALTER COLUMN?
- [ ] Can I DROP a column?
- [ ] Can I rename a column?
- [ ] Do I know sp_rename?
- [ ] Can I write DELETE with WHERE?
- [ ] Do I understand DELETE without WHERE?
- [ ] Do I understand TRUNCATE?
- [ ] Do I understand DROP?
- [ ] Can I distinguish DELETE/TRUNCATE/DROP?

## Lab 6

- [ ] Can I write SELECT INTO?
- [ ] Can I copy selected columns?
- [ ] Can I use WHERE?
- [ ] Can I use DISTINCT?
- [ ] Can I use TOP?
- [ ] Can I use BETWEEN?
- [ ] Can I use IN?
- [ ] Can I copy NULL records?
- [ ] Can I rename a copied column using an alias?
- [ ] Can I create an empty table structure using SELECT INTO?

## Lab 7

- [ ] Do I know LIKE?
- [ ] Do I know `%`?
- [ ] Do I know `_`?
- [ ] Can I find prefix?
- [ ] Can I find suffix?
- [ ] Can I find substring?
- [ ] Can I find an exact character count?
- [ ] Can I search a specific character position?
- [ ] Do I know NOT LIKE?
- [ ] Can I combine LIKE with AND/OR?

## Lab 8

- [ ] Do I know COUNT?
- [ ] Do I know SUM?
- [ ] Do I know AVG?
- [ ] Do I know MIN?
- [ ] Do I know MAX?
- [ ] Do I understand COUNT(*)?
- [ ] Do I understand COUNT(column)?
- [ ] Do I understand COUNT(DISTINCT column)?
- [ ] Can I write GROUP BY?
- [ ] Can I group by multiple columns?
- [ ] Do I understand NULL in aggregate functions?

## Lab 9

- [ ] Do I understand HAVING?
- [ ] Do I know WHERE vs HAVING?
- [ ] Can I use HAVING with COUNT?
- [ ] Can I use HAVING with SUM?
- [ ] Can I use HAVING with AVG?
- [ ] Can I use HAVING with MIN/MAX?
- [ ] Can I use ORDER BY?
- [ ] Do I know ASC?
- [ ] Do I know DESC?
- [ ] Can I combine WHERE + GROUP BY + HAVING + ORDER BY?

---

# Final Super-Short Memory Map

```text
LAB 1
SSMS
  ↓
LAB 2
CREATE + INSERT
  ↓
LAB 3
SELECT + WHERE + CONDITIONS
  ↓
LAB 4
UPDATE
  ↓
LAB 5
ALTER + RENAME + DELETE + TRUNCATE + DROP
  ↓
LAB 6
SELECT INTO
  ↓
LAB 7
LIKE + % + _
  ↓
LAB 8
COUNT + SUM + AVG + MIN + MAX + GROUP BY
  ↓
LAB 9
GROUP BY + HAVING + ORDER BY
```

## The Most Important Exam Comparisons

```text
WHERE       → rows
HAVING      → groups

%           → zero or more characters
_           → exactly one character

DELETE      → rows
TRUNCATE    → all rows
DROP        → table

UPDATE      → existing data
ALTER       → table structure

SELECT INTO → creates new table
INSERT INTO → inserts into existing table

COUNT(*)              → rows
COUNT(column)         → non-NULL values
COUNT(DISTINCT col)   → unique non-NULL values

ASC         → low to high / A to Z
DESC        → high to low / Z to A
```

# End of Lab 1–9 Revision
