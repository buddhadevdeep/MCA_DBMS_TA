# Lab 27: Implement Cursors for Row-by-Row Data Processing in MS SQL Server

## 1. What Is a Cursor?

A **cursor** in SQL Server is a database object that allows us to process query results **one row at a time**.

Normally, SQL works with multiple rows together. A cursor lets us fetch one employee record, process it, move to the next employee, and repeat the process.

### Example

Suppose the `EMPLOYEE` table contains:

| EID | FIRSTNAME | SALARY |
|---:|---|---:|
| 101 | Hetvi | 14000 |
| 102 | Raj | 16000 |
| 103 | Deep | 12000 |

Using a cursor, we can process each employee separately:

```text
Fetch Hetvi → Display Hetvi
Fetch Raj   → Display Raj
Fetch Deep  → Display Deep
Finish
```

## 2. Why Do We Use Cursors?

Cursors are useful when a task requires row-by-row processing or individual actions for each record.

Examples:
- Display employee records one by one.
- Calculate information separately for each employee.
- Process employees according to specific conditions.
- Update or delete selected records one at a time.

**Note:** Whenever possible, prefer normal SQL statements such as `SELECT`, `UPDATE`, `DELETE`, and `GROUP BY`. They are usually more efficient than cursors.

## 3. Cursor Working Flow

A cursor generally follows these five steps:

```text
DECLARE Cursor
      ↓
OPEN Cursor
      ↓
FETCH First Row
      ↓
WHILE @@FETCH_STATUS = 0
      ↓
Process Current Row
      ↓
FETCH Next Row
      ↓
Repeat Until No Rows Remain
      ↓
CLOSE Cursor
      ↓
DEALLOCATE Cursor
```

### Explanation of Commands

| Command | Purpose |
|---|---|
| `DECLARE` | Defines the cursor and its SELECT query. |
| `OPEN` | Executes the cursor query and makes its result available for fetching. |
| `FETCH NEXT` | Retrieves the next row. |
| `@@FETCH_STATUS` | Checks whether the most recent fetch succeeded. |
| `CLOSE` | Closes the cursor and releases its active result set. |
| `DEALLOCATE` | Removes the cursor reference and releases its associated resources. |

`@@FETCH_STATUS = 0` means the last fetch succeeded.

When no more rows are available, the status becomes nonzero, and the loop stops.

# 4. Basic Cursor Syntax

```sql
DECLARE CursorName CURSOR FOR
SELECT ColumnName
FROM TableName;

OPEN CursorName;

FETCH NEXT FROM CursorName INTO @Variable;

WHILE @@FETCH_STATUS = 0
BEGIN
    -- Process the current row

    FETCH NEXT FROM CursorName INTO @Variable;
END;

CLOSE CursorName;
DEALLOCATE CursorName;
```

The variable used in `FETCH INTO` must match the selected column's data type.

# 5. Example 1: Display All Employees Using a Cursor

Assume the `EMPLOYEE` table contains `EID`, `FIRSTNAME`, and `LASTNAME`.

```sql
DECLARE @EID INT,
        @FIRSTNAME VARCHAR(50),
        @LASTNAME VARCHAR(50);

DECLARE Employee_Cursor CURSOR FOR
SELECT EID, FIRSTNAME, LASTNAME
FROM EMPLOYEE;

OPEN Employee_Cursor;

FETCH NEXT FROM Employee_Cursor
INTO @EID, @FIRSTNAME, @LASTNAME;

WHILE @@FETCH_STATUS = 0
BEGIN
    PRINT CAST(@EID AS VARCHAR(10)) + ' - '
          + @FIRSTNAME + ' ' + @LASTNAME;

    FETCH NEXT FROM Employee_Cursor
    INTO @EID, @FIRSTNAME, @LASTNAME;
END;

CLOSE Employee_Cursor;
DEALLOCATE Employee_Cursor;
```

### Explanation

1. Variables store the current employee's ID and name.
2. `DECLARE` defines a cursor for the employee query.
3. `OPEN` starts the cursor.
4. `FETCH NEXT` reads the first employee.
5. The `WHILE` loop processes each employee.
6. Another `FETCH NEXT` moves to the next employee.
7. `CLOSE` and `DEALLOCATE` clean up the cursor.

`PRINT` displays messages in the SQL Server Messages tab. Use `SELECT` if you want a result grid.

# 6. Example 2: Display Employees Whose Salary Is Greater Than 12000

```sql
DECLARE @EID INT,
        @FIRSTNAME VARCHAR(50),
        @SALARY DECIMAL(10,2);

DECLARE Salary_Cursor CURSOR FOR
SELECT EID, FIRSTNAME, SALARY
FROM EMPLOYEE
WHERE SALARY > 12000;

OPEN Salary_Cursor;

FETCH NEXT FROM Salary_Cursor
INTO @EID, @FIRSTNAME, @SALARY;

WHILE @@FETCH_STATUS = 0
BEGIN
    PRINT @FIRSTNAME + ' - '
          + CAST(@SALARY AS VARCHAR(20));

    FETCH NEXT FROM Salary_Cursor
    INTO @EID, @FIRSTNAME, @SALARY;
END;

CLOSE Salary_Cursor;
DEALLOCATE Salary_Cursor;
```

**Important:** The `WHERE` condition filters employees before the cursor processes the results.

# 7. Example 3: Display Employee Details in a Single String

Required format: `101_Hetvi_Patel`

```sql
DECLARE @EID INT,
        @FIRSTNAME VARCHAR(50),
        @LASTNAME VARCHAR(50);

DECLARE Employee_Cursor CURSOR FOR
SELECT EID, FIRSTNAME, LASTNAME
FROM EMPLOYEE;

OPEN Employee_Cursor;

FETCH NEXT FROM Employee_Cursor
INTO @EID, @FIRSTNAME, @LASTNAME;

WHILE @@FETCH_STATUS = 0
BEGIN
    SELECT
        CAST(@EID AS VARCHAR(10)) + '_'
        + @FIRSTNAME + '_'
        + @LASTNAME AS EmployeeDetails;

    FETCH NEXT FROM Employee_Cursor
    INTO @EID, @FIRSTNAME, @LASTNAME;
END;

CLOSE Employee_Cursor;
DEALLOCATE Employee_Cursor;
```

This produces one result row for each employee processed.

# 8. Example 4: Display Employees Who Joined in 2022 or Later

Assume the joining-date column is named `JOININGDATE`.

```sql
DECLARE @EID INT,
        @FIRSTNAME VARCHAR(50),
        @JOININGDATE DATE;

DECLARE Joining_Cursor CURSOR FOR
SELECT EID, FIRSTNAME, JOININGDATE
FROM EMPLOYEE
WHERE JOININGDATE >= '2022-01-01';

OPEN Joining_Cursor;

FETCH NEXT FROM Joining_Cursor
INTO @EID, @FIRSTNAME, @JOININGDATE;

WHILE @@FETCH_STATUS = 0
BEGIN
    SELECT @EID AS EID,
           @FIRSTNAME AS FIRSTNAME,
           @JOININGDATE AS JOININGDATE;

    FETCH NEXT FROM Joining_Cursor
    INTO @EID, @FIRSTNAME, @JOININGDATE;
END;

CLOSE Joining_Cursor;
DEALLOCATE Joining_Cursor;
```

The cursor processes only employees whose joining date is on or after January 1, 2022.

# 9. Example 5: Display Employee Name and Department

```sql
DECLARE @FIRSTNAME VARCHAR(50),
        @DEPARTMENT VARCHAR(50);

DECLARE Department_Cursor CURSOR FOR
SELECT FIRSTNAME, DEPARTMENT
FROM EMPLOYEE;

OPEN Department_Cursor;

FETCH NEXT FROM Department_Cursor
INTO @FIRSTNAME, @DEPARTMENT;

WHILE @@FETCH_STATUS = 0
BEGIN
    SELECT @FIRSTNAME AS EmployeeName,
           @DEPARTMENT AS Department;

    FETCH NEXT FROM Department_Cursor
    INTO @FIRSTNAME, @DEPARTMENT;
END;

CLOSE Department_Cursor;
DEALLOCATE Department_Cursor;
```

This example assumes that `DEPARTMENT` is a column in the `EMPLOYEE` table. If department details are stored in a separate table, use a `JOIN` in the cursor query.

# 10. Example 6: Update NULL City Values

Suppose employees whose `CITY` is `NULL` should be assigned the city `AHMEDABAD`.

```sql
DECLARE @EID INT;

DECLARE City_Cursor CURSOR FOR
SELECT EID
FROM EMPLOYEE
WHERE CITY IS NULL;

OPEN City_Cursor;

FETCH NEXT FROM City_Cursor INTO @EID;

WHILE @@FETCH_STATUS = 0
BEGIN
    UPDATE EMPLOYEE
    SET CITY = 'AHMEDABAD'
    WHERE EID = @EID;

    FETCH NEXT FROM City_Cursor INTO @EID;
END;

CLOSE City_Cursor;
DEALLOCATE City_Cursor;
```

### Explanation

- `IS NULL` finds employees without a city value.
- The cursor fetches each matching employee ID.
- `UPDATE` assigns the city to that employee.
- The loop repeats for every matching employee.

**Better approach:** This operation does not need a cursor. A single statement is simpler and faster:

```sql
UPDATE EMPLOYEE
SET CITY = 'AHMEDABAD'
WHERE CITY IS NULL;
```

# 11. Example 7: Delete Employees Whose Salary Is Below 5000

```sql
DECLARE @EID INT;

DECLARE Delete_Cursor CURSOR FOR
SELECT EID
FROM EMPLOYEE
WHERE SALARY < 5000;

OPEN Delete_Cursor;

FETCH NEXT FROM Delete_Cursor INTO @EID;

WHILE @@FETCH_STATUS = 0
BEGIN
    DELETE FROM EMPLOYEE
    WHERE EID = @EID;

    FETCH NEXT FROM Delete_Cursor INTO @EID;
END;

CLOSE Delete_Cursor;
DEALLOCATE Delete_Cursor;
```

**Better approach:**

```sql
DELETE FROM EMPLOYEE
WHERE SALARY < 5000;
```

Always verify the selected records before deleting data.

# 12. Example 8: Display Employees Department-Wise

```sql
DECLARE @FIRSTNAME VARCHAR(50),
        @DEPARTMENT VARCHAR(50);

DECLARE Dept_Cursor CURSOR FOR
SELECT FIRSTNAME, DEPARTMENT
FROM EMPLOYEE
ORDER BY DEPARTMENT, FIRSTNAME;

OPEN Dept_Cursor;

FETCH NEXT FROM Dept_Cursor
INTO @FIRSTNAME, @DEPARTMENT;

WHILE @@FETCH_STATUS = 0
BEGIN
    SELECT @DEPARTMENT AS Department,
           @FIRSTNAME AS EmployeeName;

    FETCH NEXT FROM Dept_Cursor
    INTO @FIRSTNAME, @DEPARTMENT;
END;

CLOSE Dept_Cursor;
DEALLOCATE Dept_Cursor;
```

`ORDER BY` controls the order in which the cursor receives records. It does not group or aggregate them.

# 13. Example 9: Find the Top 3 Highest-Paid Employees

The cursor can fetch the results of a query that already selects the top three employees.

```sql
DECLARE @FIRSTNAME VARCHAR(50),
        @SALARY DECIMAL(10,2);

DECLARE TopSalary_Cursor CURSOR FOR
SELECT TOP 3 FIRSTNAME, SALARY
FROM EMPLOYEE
ORDER BY SALARY DESC;

OPEN TopSalary_Cursor;

FETCH NEXT FROM TopSalary_Cursor
INTO @FIRSTNAME, @SALARY;

WHILE @@FETCH_STATUS = 0
BEGIN
    SELECT @FIRSTNAME AS EmployeeName,
           @SALARY AS Salary;

    FETCH NEXT FROM TopSalary_Cursor
    INTO @FIRSTNAME, @SALARY;
END;

CLOSE TopSalary_Cursor;
DEALLOCATE TopSalary_Cursor;
```

The query sorts salaries in descending order and selects the top three records before cursor processing begins.

# 14. Example 10: Calculate Department-Wise Total Salary

A cursor can iterate over departments, but `GROUP BY` is simpler for this calculation.

### Recommended SQL

```sql
SELECT
    DEPARTMENT,
    SUM(SALARY) AS TotalSalary
FROM EMPLOYEE
GROUP BY DEPARTMENT;
```

### Cursor-Based Alternative

```sql
DECLARE @DEPARTMENT VARCHAR(50),
        @TOTALSALARY DECIMAL(12,2);

DECLARE DepartmentSalary_Cursor CURSOR FOR
SELECT DISTINCT DEPARTMENT
FROM EMPLOYEE
WHERE DEPARTMENT IS NOT NULL;

OPEN DepartmentSalary_Cursor;

FETCH NEXT FROM DepartmentSalary_Cursor
INTO @DEPARTMENT;

WHILE @@FETCH_STATUS = 0
BEGIN
    SELECT @TOTALSALARY = SUM(SALARY)
    FROM EMPLOYEE
    WHERE DEPARTMENT = @DEPARTMENT;

    SELECT @DEPARTMENT AS Department,
           @TOTALSALARY AS TotalSalary;

    FETCH NEXT FROM DepartmentSalary_Cursor
    INTO @DEPARTMENT;
END;

CLOSE DepartmentSalary_Cursor;
DEALLOCATE DepartmentSalary_Cursor;
```

The cursor processes each department, and the aggregate query calculates the total salary for that department.

# 15. Example 11: Count Male and Female Employees Separately

This calculation can be done without a cursor:

```sql
SELECT
    SUM(CASE WHEN GENDER = 'Male' THEN 1 ELSE 0 END)
        AS MaleEmployees,
    SUM(CASE WHEN GENDER = 'Female' THEN 1 ELSE 0 END)
        AS FemaleEmployees
FROM EMPLOYEE;
```

This assumes the table has a `GENDER` column with values `Male` and `Female`.

The `CASE` expression counts employees matching each condition.

# 16. Example 12: Find Employees Earning More Than Their Department's Average

```sql
SELECT E.*
FROM EMPLOYEE AS E
WHERE E.SALARY >
(
    SELECT AVG(E2.SALARY)
    FROM EMPLOYEE AS E2
    WHERE E2.DEPARTMENT = E.DEPARTMENT
);
```

This is the recommended set-based solution. It compares each employee's salary with the average salary of that employee's department without requiring a cursor.

# 17. Cursor Declaration Options

SQL Server supports different cursor options.

| Option | Meaning |
|---|---|
| `LOCAL` | Cursor is limited to its local scope. |
| `GLOBAL` | Cursor is available at the connection's global scope. |
| `FAST_FORWARD` | Forward-only, read-only cursor optimized for simple sequential reading. |
| `STATIC` | Uses a static result set that does not reflect later changes to the underlying data. |
| `KEYSET` | Tracks the keys of the result rows; changes to non-key values can be visible depending on the cursor operation. |
| `DYNAMIC` | Can reflect changes to the result set as it is navigated. |

For simple read-only processing, `LOCAL FAST_FORWARD` is often a good choice.

### Example

```sql
DECLARE Employee_Cursor CURSOR LOCAL FAST_FORWARD FOR
SELECT EID, FIRSTNAME
FROM EMPLOYEE;
```

The remaining cursor commands (`OPEN`, `FETCH`, `CLOSE`, and `DEALLOCATE`) follow the same pattern.

# 18. Common Cursor Mistakes

1. Forgetting to open the cursor before fetching.
2. Forgetting to fetch the next row inside the `WHILE` loop, which can cause an infinite loop.
3. Using a different number of variables from the number of selected columns.
4. Using incompatible variable data types in `FETCH INTO`.
5. Forgetting to close and deallocate the cursor.
6. Using a cursor for operations that a single `UPDATE`, `DELETE`, or aggregate query can perform.
7. Assuming `PRINT` produces a result grid; use `SELECT` for grid output.

# 19. Cursor vs Normal SQL Query

| Cursor | Normal SQL Query |
|---|---|
| Processes rows one at a time | Usually processes a set of rows together |
| Requires declaration, opening, fetching, closing, and deallocation | Often requires only one statement |
| Can be slower for large datasets | Usually more efficient for bulk operations |
| Useful for sequential row-by-row tasks | Best for filtering, updating, deleting, joining, and aggregation |
| Uses a loop to process rows | Uses set-based operations |

# 20. Final Revision

Remember the basic cursor sequence:

```sql
DECLARE MyCursor CURSOR FOR
SELECT EID FROM EMPLOYEE;

OPEN MyCursor;

FETCH NEXT FROM MyCursor INTO @EID;

WHILE @@FETCH_STATUS = 0
BEGIN
    -- Process current employee

    FETCH NEXT FROM MyCursor INTO @EID;
END;

CLOSE MyCursor;
DEALLOCATE MyCursor;
```

Before executing this template, declare `@EID` with a data type compatible with `EMPLOYEE.EID`.

**Key definitions:**

- **Cursor:** A SQL Server object for processing query results row by row.
- **FETCH:** Retrieves a row from the cursor.
- **`@@FETCH_STATUS`:** Indicates whether the most recent fetch succeeded.
- **CLOSE:** Closes the cursor.
- **DEALLOCATE:** Releases the cursor reference and associated resources.

**Best practice:** Learn cursor syntax for your DBMS lab and exams, but prefer set-based SQL for normal database applications whenever possible.
