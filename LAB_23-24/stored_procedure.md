# Lab 23–24: SQL Stored Procedures in MS SQL Server

## 1. What Is a Stored Procedure?

A **Stored Procedure** is a group of SQL statements saved in the database that can be executed whenever required.

Instead of writing the same query repeatedly, we create a procedure once and execute it whenever needed.

### Example

```sql
CREATE PROCEDURE SP_ShowStudents
AS
BEGIN
    SELECT * FROM STUDENT;
END;
```

Execute the procedure:

```sql
EXEC SP_ShowStudents;
```

### Working Flow

```text
Create Procedure
       ↓
Stored in Database
       ↓
Execute Using EXEC
       ↓
SQL Statements Execute
       ↓
Get Result
```

## 2. Basic Syntax

```sql
CREATE PROCEDURE ProcedureName
AS
BEGIN
    -- SQL statements
END;
```

Execute:

```sql
EXEC ProcedureName;
```

- `CREATE PROCEDURE`: Creates a stored procedure.
- `AS`: Begins the procedure definition.
- `BEGIN`: Starts the statement block.
- `END`: Ends the statement block.
- `EXEC`: Executes the procedure.

## 3. Procedure with Input Parameters

Parameters allow users to pass values to a procedure.

### Example: Find a Student by ID

```sql
CREATE PROCEDURE SP_GetStudent
    @StudentID INT
AS
BEGIN
    SELECT *
    FROM STUDENT
    WHERE STDID = @StudentID;
END;
```

Execute:

```sql
EXEC SP_GetStudent @StudentID = 101;
```

**Explanation:** The value `101` is passed to `@StudentID`. The procedure displays the matching student.

## 4. Procedure with Multiple Parameters

```sql
CREATE PROCEDURE SP_SearchStudent
    @StudentName VARCHAR(50),
    @StudentBranch VARCHAR(30)
AS
BEGIN
    SELECT *
    FROM STUDENT
    WHERE SNAME = @StudentName
      AND BRANCH = @StudentBranch;
END;
```

Execute:

```sql
EXEC SP_SearchStudent
    @StudentName = 'RAJU',
    @StudentBranch = 'CE';
```

Both conditions must be satisfied because we use `AND`.

## 5. Procedure with INSERT

Used to insert a new record into a table.

```sql
CREATE PROCEDURE SP_InsertStudent
    @StudentID INT,
    @StudentName VARCHAR(50),
    @Branch VARCHAR(30)
AS
BEGIN
    INSERT INTO STUDENT (STDID, SNAME, BRANCH)
    VALUES (@StudentID, @StudentName, @Branch);
END;
```

Execute:

```sql
EXEC SP_InsertStudent
    @StudentID = 110,
    @StudentName = 'KARAN',
    @Branch = 'CE';
```

## 6. Procedure with UPDATE

Used to modify existing records.

```sql
CREATE PROCEDURE SP_UPDATE_STUDENT
    @StudentID INT,
    @Branch VARCHAR(30)
AS
BEGIN
    UPDATE STUDENT
    SET BRANCH = @Branch
    WHERE STDID = @StudentID;
END;
```

Execute:

```sql
EXEC SP_UPDATE_STUDENT
    @StudentID = 115,
    @Branch = 'ELECTRICAL';
```

**Important:** Always use an appropriate `WHERE` condition. Without it, all records may be updated.

## 7. Procedure with DELETE

Used to delete selected records.

```sql
CREATE PROCEDURE SP_DELETE_STUDENT
    @StudentName VARCHAR(50)
AS
BEGIN
    DELETE FROM STUDENT
    WHERE SNAME = @StudentName;
END;
```

Execute:

```sql
EXEC SP_DELETE_STUDENT @StudentName = 'RAVI';
```

All records matching the specified name are deleted.

## 8. Procedure with IF-ELSE

`IF-ELSE` executes different statements depending on a condition.

```sql
CREATE PROCEDURE SP_CheckSalary
    @Salary DECIMAL(10,2)
AS
BEGIN
    IF @Salary >= 15000
        PRINT 'High Salary';
    ELSE
        PRINT 'Low Salary';
END;
```

Execute:

```sql
EXEC SP_CheckSalary @Salary = 20000;
```

Output:

```text
High Salary
```

## 9. Procedure with Aggregate Functions

Aggregate functions calculate values from multiple records.

| Function | Purpose |
|---|---|
| `SUM()` | Calculates total |
| `AVG()` | Calculates average |
| `MIN()` | Finds minimum |
| `MAX()` | Finds maximum |
| `COUNT()` | Counts records |

### Example: Department Salary Statistics

```sql
CREATE PROCEDURE SP_SalaryStatistics
    @Department VARCHAR(50)
AS
BEGIN
    SELECT
        SUM(SALARY) AS TotalSalary,
        AVG(SALARY) AS AverageSalary,
        MIN(SALARY) AS MinimumSalary,
        MAX(SALARY) AS MaximumSalary
    FROM EMPLOYEE
    WHERE DEPARTMENT = @Department;
END;
```

Execute:

```sql
EXEC SP_SalaryStatistics @Department = 'IT';
```

This displays total, average, minimum, and maximum salary for the specified department.

## 10. Procedure with GROUP BY

`GROUP BY` creates groups based on a common column value.

### Example: Department-Wise Salary

```sql
CREATE PROCEDURE SP_DepartmentSalary
AS
BEGIN
    SELECT
        DEPARTMENT,
        SUM(SALARY) AS TotalSalary,
        AVG(SALARY) AS AverageSalary,
        MIN(SALARY) AS MinimumSalary,
        MAX(SALARY) AS MaximumSalary
    FROM EMPLOYEE
    GROUP BY DEPARTMENT;
END;
```

Execute:

```sql
EXEC SP_DepartmentSalary;
```

Each department gets its own salary statistics.

## 11. Procedure with LIKE

`LIKE` searches for records matching a text pattern.

```sql
CREATE PROCEDURE SP_SearchEmployee
    @Name VARCHAR(50)
AS
BEGIN
    SELECT *
    FROM EMPLOYEE
    WHERE FIRSTNAME LIKE @Name;
END;
```

Execute:

```sql
EXEC SP_SearchEmployee @Name = 'A%';
```

This displays employees whose first name starts with `A`.

Common patterns:

| Pattern | Meaning |
|---|---|
| `'A%'` | Starts with A |
| `'%A'` | Ends with A |
| `'%A%'` | Contains A |
| `'_A%'` | Second character is A |

## 12. Procedure with BETWEEN

`BETWEEN` checks whether a value falls within a range. Both endpoints are included.

```sql
CREATE PROCEDURE SP_SalaryRange
    @MinSalary DECIMAL(10,2),
    @MaxSalary DECIMAL(10,2)
AS
BEGIN
    SELECT *
    FROM EMPLOYEE
    WHERE SALARY BETWEEN @MinSalary AND @MaxSalary;
END;
```

Execute:

```sql
EXEC SP_SalaryRange
    @MinSalary = 10000,
    @MaxSalary = 15000;
```

This displays employees earning between 10,000 and 15,000, inclusive.

## 13. Procedure with Dynamic Search

Optional parameters allow users to search using different combinations of values.

```sql
CREATE PROCEDURE SP_DynamicSearch
    @Name VARCHAR(50) = NULL,
    @Department VARCHAR(50) = NULL
AS
BEGIN
    SELECT *
    FROM EMPLOYEE
    WHERE (@Name IS NULL OR FIRSTNAME LIKE '%' + @Name + '%')
      AND (@Department IS NULL OR DEPARTMENT = @Department);
END;
```

Execute:

```sql
EXEC SP_DynamicSearch @Name = 'RA';
```

Or:

```sql
EXEC SP_DynamicSearch @Department = 'IT';
```

Or:

```sql
EXEC SP_DynamicSearch
    @Name = 'RA',
    @Department = 'IT';
```

**Explanation:** If a parameter is `NULL`, that filter is ignored.

## 14. Procedure with TOP and Variable

A variable can specify how many records should be returned.

```sql
CREATE PROCEDURE SP_TopEmployees
    @N INT
AS
BEGIN
    SELECT TOP (@N) *
    FROM EMPLOYEE
    ORDER BY SALARY DESC;
END;
```

Execute:

```sql
EXEC SP_TopEmployees @N = 5;
```

This displays the five highest-paid employees.

## 15. Procedure with JOIN

A JOIN combines related records from multiple tables.

Assume `EMPLOYEE` has a `DEPARTMENTID` column and `DEPARTMENT` has `DEPARTMENTID` and `DEPARTMENTNAME`.

```sql
CREATE PROCEDURE SP_EmployeeDepartment
    @DepartmentName VARCHAR(100)
AS
BEGIN
    SELECT E.*
    FROM EMPLOYEE AS E
    INNER JOIN DEPARTMENT AS D
        ON E.DEPARTMENTID = D.DEPARTMENTID
    WHERE D.DEPARTMENTNAME = @DepartmentName;
END;
```

Execute:

```sql
EXEC SP_EmployeeDepartment @DepartmentName = 'IT';
```

This displays employees belonging to the specified department.

## 16. Procedure with Date Conditions

```sql
CREATE PROCEDURE SP_RecentEmployees
    @JoiningYear INT
AS
BEGIN
    SELECT *
    FROM EMPLOYEE
    WHERE YEAR(JOININGDATE) > @JoiningYear;
END;
```

Execute:

```sql
EXEC SP_RecentEmployees @JoiningYear = 2023;
```

This displays employees who joined after 2023.

**Note:** Use the actual date-column name from your table.

## 17. Procedure to Display Last N Employees

```sql
CREATE PROCEDURE SP_LastEmployees
    @N INT
AS
BEGIN
    SELECT TOP (@N) *
    FROM EMPLOYEE
    ORDER BY EID DESC;
END;
```

Execute:

```sql
EXEC SP_LastEmployees @N = 5;
```

This displays the five records with the highest `EID` values. It represents the latest employees only if `EID` follows the order in which employees were added.

## 18. Procedure with OUTPUT Parameter

An `OUTPUT` parameter returns a calculated value to the caller.

```sql
CREATE PROCEDURE SP_TotalEmployees
    @Total INT OUTPUT
AS
BEGIN
    SELECT @Total = COUNT(*)
    FROM EMPLOYEE;
END;
```

Execute:

```sql
DECLARE @EmployeeCount INT;

EXEC SP_TotalEmployees
    @Total = @EmployeeCount OUTPUT;

SELECT @EmployeeCount AS TotalEmployees;
```

**Difference:** An input parameter sends a value into a procedure. An output parameter returns a value from the procedure.

## 19. Alter an Existing Procedure

Use `ALTER PROCEDURE` to modify a procedure that already exists.

```sql
ALTER PROCEDURE SP_ShowStudents
AS
BEGIN
    SELECT STDID, SNAME, BRANCH
    FROM STUDENT;
END;
```

Execute:

```sql
EXEC SP_ShowStudents;
```

## 20. Delete a Stored Procedure

Use `DROP PROCEDURE` to remove a procedure definition from the database.

```sql
DROP PROCEDURE SP_ShowStudents;
```

To avoid an error if the procedure does not exist:

```sql
DROP PROCEDURE IF EXISTS SP_ShowStudents;
```

**Note:** Dropping a procedure does not delete the table or its records.

## 21. View Stored Procedures

To list stored procedures in the current database:

```sql
SELECT name
FROM sys.procedures
ORDER BY name;
```

To view a procedure's definition:

```sql
EXEC sp_helptext 'SP_ShowStudents';
```

## 22. Important Rules

1. Procedure names commonly begin with `SP_` in college lab exercises. This is a naming convention, not a requirement.
2. Use `CREATE PROCEDURE` to create a new procedure.
3. Use `ALTER PROCEDURE` to modify an existing procedure.
4. Use `EXEC` or `EXECUTE` to run a procedure.
5. Use `@` before parameter and local variable names.
6. Use `BEGIN` and `END` to group multiple statements.
7. Use `WHERE` carefully in `UPDATE` and `DELETE`.
8. Input parameters can have default values.
9. Use `OUTPUT` when a procedure needs to return a parameter value.
10. Use `DROP PROCEDURE` to remove a stored procedure.

## 23. Stored Procedure vs Function

| Stored Procedure | Function |
|---|---|
| Executed using `EXEC` | Commonly used inside a `SELECT` or expression |
| Can perform data modifications | User-defined functions have restrictions on side effects and data modifications |
| Can return result sets | Returns a scalar value or a table |
| Supports input and output parameters | Supports parameters and returns a value |
| Useful for database operations | Useful for calculations and reusable expressions |

## 24. Stored Procedure Execution Flow

```text
User Calls EXEC
       ↓
Procedure Receives Parameters
       ↓
Conditions Are Checked
       ↓
SQL Queries Execute
       ↓
Data Is Selected / Inserted / Updated / Deleted
       ↓
Result Is Returned
```

## 25. Final Revision

| Concept | SQL Keyword |
|---|---|
| Create procedure | `CREATE PROCEDURE` |
| Execute procedure | `EXEC` |
| Modify procedure | `ALTER PROCEDURE` |
| Remove procedure | `DROP PROCEDURE` |
| Input parameter | `@ParameterName` |
| Output parameter | `OUTPUT` |
| Conditional logic | `IF...ELSE` |
| Group records | `GROUP BY` |
| Filter matching text | `LIKE` |
| Filter a range | `BETWEEN` |
| Return limited rows | `TOP` |
| Combine tables | `JOIN` |
| Calculate values | `SUM`, `AVG`, `MIN`, `MAX`, `COUNT` |

### Easy Definition to Remember

> A stored procedure is a named collection of SQL statements stored in a database that can be executed repeatedly, with or without parameters, to perform database operations.

**Important:** The examples use illustrative table and column names. Adjust them to match your actual `STUDENT`, `EMPLOYEE`, `AUTHOR`, `PUBLISHER`, and `BOOK` table structures.
