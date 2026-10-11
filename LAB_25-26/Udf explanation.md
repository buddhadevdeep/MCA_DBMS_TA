# Lab 25–26: User Defined Functions (UDF) in MS SQL Server

## 1. What Is a User Defined Function (UDF)?

A **User Defined Function (UDF)** is a function created by the user to perform a specific operation and return a result.

We can create a function once and reuse it whenever required.

### Types of UDF

| Scalar Function | Table-Valued Function |
|---|---|
| Returns one value | Returns a table |
| Returns an integer, string, date, decimal, etc. | Returns one or more rows and columns |
| Used for calculations and single results | Used to retrieve multiple records |
| Called inside `SELECT` or other expressions | Used in the `FROM` clause |

### Basic Flow

```text
Create Function
      ↓
Pass Parameters (if required)
      ↓
Perform Calculation or Query
      ↓
Return Result
      ↓
Use Function in SQL
```

# Lab 25: Scalar Function

## 2. What Is a Scalar Function?

A **Scalar Function** returns only one value.

Examples:
- Calculate simple interest.
- Calculate the square of a number.
- Find the maximum of three numbers.
- Count employees.
- Calculate the difference between two dates.

### Basic Syntax

```sql
CREATE FUNCTION FunctionName
(
    @Parameter INT
)
RETURNS INT
AS
BEGIN
    DECLARE @Result INT;

    -- Calculation

    RETURN @Result;
END;
```

- `CREATE FUNCTION`: Creates the function.
- `@Parameter`: Accepts an input value.
- `RETURNS INT`: Specifies the return data type.
- `DECLARE`: Creates a local variable.
- `RETURN`: Sends one value back to the caller.

## 3. Function Without Parameters

Example: Return a welcome message.

```sql
CREATE FUNCTION FN_Welcome()
RETURNS VARCHAR(100)
AS
BEGIN
    RETURN 'Welcome to DBMS Lab';
END;
```

Execute:

```sql
SELECT dbo.FN_Welcome() AS Message;
```

Output:

```text
Welcome to DBMS Lab
```

**Explanation:** The function takes no input and returns one string value.

## 4. Function with Parameters

Parameters allow the user to pass values into a function.

### Example: Simple Interest

Formula:

```text
Simple Interest = (Principal × Rate × Time) / 100
```

```sql
CREATE FUNCTION FN_SimpleInterest
(
    @Principal DECIMAL(10,2),
    @Rate DECIMAL(5,2),
    @Time DECIMAL(5,2)
)
RETURNS DECIMAL(10,2)
AS
BEGIN
    RETURN (@Principal * @Rate * @Time) / 100.0;
END;
```

Execute:

```sql
SELECT dbo.FN_SimpleInterest(10000, 5, 2) AS SimpleInterest;
```

Output:

```text
1000.00
```

**Flow:** Input values → Apply formula → Return one result.

## 5. Function to Find Difference Between Two Dates

`DATEDIFF()` calculates the difference between two dates using the specified date part.

```sql
CREATE FUNCTION FN_DateDifference
(
    @StartDate DATE,
    @EndDate DATE
)
RETURNS INT
AS
BEGIN
    RETURN DATEDIFF(DAY, @StartDate, @EndDate);
END;
```

Execute:

```sql
SELECT dbo.FN_DateDifference('2025-01-01', '2025-01-11')
AS DifferenceInDays;
```

Output:

```text
10
```

## 6. Function to Check Odd or Even

```sql
CREATE FUNCTION FN_OddEven
(
    @Number INT
)
RETURNS VARCHAR(10)
AS
BEGIN
    IF @Number % 2 = 0
        RETURN 'Even';

    RETURN 'Odd';
END;
```

Execute:

```sql
SELECT dbo.FN_OddEven(10) AS Result;
```

Output:

```text
Even
```

`%` returns the remainder after division. If a number divided by 2 has remainder 0, it is even.

## 7. Function to Calculate Factorial

Factorial of a number is the product of all positive integers from 1 to that number.

Example:

```text
5! = 5 × 4 × 3 × 2 × 1 = 120
0! = 1
```

```sql
CREATE FUNCTION FN_Factorial
(
    @Number INT
)
RETURNS BIGINT
AS
BEGIN
    DECLARE @Result BIGINT = 1;
    DECLARE @I INT = 1;

    IF @Number < 0 OR @Number > 20
        RETURN NULL;

    WHILE @I <= @Number
    BEGIN
        SET @Result = @Result * @I;
        SET @I = @I + 1;
    END;

    RETURN @Result;
END;
```

Execute:

```sql
SELECT dbo.FN_Factorial(5) AS Factorial;
```

Output:

```text
120
```

**Note:** This example restricts the input to 0–20 to keep the result within the supported `BIGINT` range.

## 8. Function to Find Maximum of Three Numbers

```sql
CREATE FUNCTION FN_Maximum
(
    @A INT,
    @B INT,
    @C INT
)
RETURNS INT
AS
BEGIN
    DECLARE @Max INT;

    SET @Max = @A;

    IF @B > @Max
        SET @Max = @B;

    IF @C > @Max
        SET @Max = @C;

    RETURN @Max;
END;
```

Execute:

```sql
SELECT dbo.FN_Maximum(10, 25, 15) AS MaximumNumber;
```

Output:

```text
25
```

## 9. Function to Calculate Square and Cube

A scalar function returns one value, so create separate functions for square and cube.

### Square

```sql
CREATE FUNCTION FN_Square
(
    @Number INT
)
RETURNS BIGINT
AS
BEGIN
    RETURN CONVERT(BIGINT, @Number) * @Number;
END;
```

### Cube

```sql
CREATE FUNCTION FN_Cube
(
    @Number INT
)
RETURNS BIGINT
AS
BEGIN
    RETURN CONVERT(BIGINT, @Number) * @Number * @Number;
END;
```

Execute:

```sql
SELECT
    dbo.FN_Square(4) AS Square,
    dbo.FN_Cube(4) AS Cube;
```

Output:

```text
Square    Cube
------    ----
16        64
```

## 10. Scalar Function Using an EMPLOYEE Table

A scalar function can query a table and return a single value.

Assume the `EMPLOYEE` table contains `EID`, `FIRSTNAME`, `DEPARTMENT`, `SALARY`, `CITY`, and `JOININGDATE`.

### A. Find Total Employees

```sql
CREATE FUNCTION FN_TotalEmployees()
RETURNS INT
AS
BEGIN
    DECLARE @Total INT;

    SELECT @Total = COUNT(*)
    FROM EMPLOYEE;

    RETURN @Total;
END;
```

Execute:

```sql
SELECT dbo.FN_TotalEmployees() AS TotalEmployees;
```

### B. Find Highest Salary in a Department

```sql
CREATE FUNCTION FN_HighestSalary
(
    @Department VARCHAR(50)
)
RETURNS DECIMAL(10,2)
AS
BEGIN
    DECLARE @HighestSalary DECIMAL(10,2);

    SELECT @HighestSalary = MAX(SALARY)
    FROM EMPLOYEE
    WHERE DEPARTMENT = @Department;

    RETURN @HighestSalary;
END;
```

Execute:

```sql
SELECT dbo.FN_HighestSalary('IT') AS HighestSalary;
```

### C. Count Employees in a City

```sql
CREATE FUNCTION FN_EmployeesByCity
(
    @City VARCHAR(50)
)
RETURNS INT
AS
BEGIN
    DECLARE @Total INT;

    SELECT @Total = COUNT(*)
    FROM EMPLOYEE
    WHERE CITY = @City;

    RETURN @Total;
END;
```

Execute:

```sql
SELECT dbo.FN_EmployeesByCity('RAJKOT') AS TotalEmployees;
```

### D. Calculate Employee Experience

```sql
CREATE FUNCTION FN_Experience
(
    @JoiningDate DATE
)
RETURNS INT
AS
BEGIN
    DECLARE @Years INT;

    SET @Years = DATEDIFF(YEAR, @JoiningDate, GETDATE());

    IF DATEADD(YEAR, @Years, @JoiningDate) > CAST(GETDATE() AS DATE)
        SET @Years = @Years - 1;

    RETURN @Years;
END;
```

Execute:

```sql
SELECT
    EID,
    FIRSTNAME,
    dbo.FN_Experience(JOININGDATE) AS ExperienceYears
FROM EMPLOYEE;
```

This calculates completed years of experience. Replace `JOININGDATE` with the actual column name if needed.

**Important:** A scalar function returns one value, not a complete row of employee details. For returning multiple columns, use a table-valued function.

# Lab 26: Table-Valued Function

## 11. What Is a Table-Valued Function?

A **Table-Valued Function (TVF)** returns a table containing rows and columns.

It is useful when we want to retrieve:
- All students.
- Students from a particular city.
- Students from a particular branch.
- Students above a specified SPI.
- Top students based on SPI.

### Basic Syntax

```sql
CREATE FUNCTION FunctionName
(
    @Parameter INT
)
RETURNS TABLE
AS
RETURN
(
    SELECT *
    FROM TableName
    WHERE ColumnName = @Parameter
);
```

Unlike a scalar function, a table-valued function returns a table that can be used in the `FROM` clause.

## 12. Inline Table-Valued Function

An inline TVF returns the result of a single `SELECT` statement.

### A. Display All Students

```sql
CREATE FUNCTION FN_AllStudents()
RETURNS TABLE
AS
RETURN
(
    SELECT *
    FROM STUDENT
);
```

Execute:

```sql
SELECT *
FROM dbo.FN_AllStudents();
```

### B. Display Students by City

```sql
CREATE FUNCTION FN_StudentsByCity
(
    @City VARCHAR(50)
)
RETURNS TABLE
AS
RETURN
(
    SELECT *
    FROM STUDENT
    WHERE CITY = @City
);
```

Execute:

```sql
SELECT *
FROM dbo.FN_StudentsByCity('RAJKOT');
```

### C. Display Students by Branch

```sql
CREATE FUNCTION FN_StudentsByBranch
(
    @Branch VARCHAR(30)
)
RETURNS TABLE
AS
RETURN
(
    SELECT *
    FROM STUDENT
    WHERE BRANCH = @Branch
);
```

Execute:

```sql
SELECT *
FROM dbo.FN_StudentsByBranch('CE');
```

### D. Students Whose SPI Is Greater Than a Given Value

```sql
CREATE FUNCTION FN_StudentsAboveSPI
(
    @SPI DECIMAL(4,2)
)
RETURNS TABLE
AS
RETURN
(
    SELECT *
    FROM STUDENT
    WHERE SPI > @SPI
);
```

Execute:

```sql
SELECT *
FROM dbo.FN_StudentsAboveSPI(8);
```

This returns all students whose SPI is greater than 8.

### E. Students Within an SPI Range

```sql
CREATE FUNCTION FN_StudentsBySPIRange
(
    @MinSPI DECIMAL(4,2),
    @MaxSPI DECIMAL(4,2)
)
RETURNS TABLE
AS
RETURN
(
    SELECT *
    FROM STUDENT
    WHERE SPI BETWEEN @MinSPI AND @MaxSPI
);
```

Execute:

```sql
SELECT *
FROM dbo.FN_StudentsBySPIRange(7, 9);
```

Both boundary values are included.

## 13. Multi-Statement Table-Valued Function

A multi-statement TVF allows multiple SQL statements to populate a returned table variable.

### Example

```sql
CREATE FUNCTION FN_StudentsAboveSeven
(
    @City VARCHAR(50)
)
RETURNS @StudentResult TABLE
(
    STDID INT,
    SNAME VARCHAR(50),
    CITY VARCHAR(50),
    SPI DECIMAL(4,2)
)
AS
BEGIN
    INSERT INTO @StudentResult
    SELECT STDID, SNAME, CITY, SPI
    FROM STUDENT
    WHERE CITY = @City
      AND SPI > 7;

    RETURN;
END;
```

Execute:

```sql
SELECT *
FROM dbo.FN_StudentsAboveSeven('RAJKOT');
```

**Explanation:**
- `RETURNS @StudentResult TABLE`: Defines the table structure.
- `INSERT INTO @StudentResult`: Inserts the query result into the returned table variable.
- `RETURN`: Returns the table.

## 14. TVF to Find Top N Students

```sql
CREATE FUNCTION FN_TopStudents
(
    @TopN INT
)
RETURNS TABLE
AS
RETURN
(
    SELECT TOP (@TopN) *
    FROM STUDENT
    ORDER BY SPI DESC, STDID ASC
);
```

Execute:

```sql
SELECT *
FROM dbo.FN_TopStudents(3);
```

This returns the three students with the highest SPI. `STDID ASC` provides a secondary ordering when SPI values are equal.

## 15. TVF to Find the Highest SPI Student in a Branch

```sql
CREATE FUNCTION FN_HighestSPIStudent
(
    @Branch VARCHAR(30)
)
RETURNS TABLE
AS
RETURN
(
    SELECT TOP 1 *
    FROM STUDENT
    WHERE BRANCH = @Branch
    ORDER BY SPI DESC, STDID ASC
);
```

Execute:

```sql
SELECT *
FROM dbo.FN_HighestSPIStudent('CE');
```

This returns one student with the highest SPI in the specified branch.

## 16. TVF to Count Students in a City

A TVF can also return a table containing an aggregate result.

```sql
CREATE FUNCTION FN_StudentCountByCity
(
    @City VARCHAR(50)
)
RETURNS TABLE
AS
RETURN
(
    SELECT COUNT(*) AS TotalStudents
    FROM STUDENT
    WHERE CITY = @City
);
```

Execute:

```sql
SELECT *
FROM dbo.FN_StudentCountByCity('RAJKOT');
```

The function returns a one-row table containing `TotalStudents`.

Compare this with the scalar function that returns only the count value.

## 17. TVF to Display Students in Descending SPI Order

```sql
CREATE FUNCTION FN_BranchStudents
(
    @Branch VARCHAR(30)
)
RETURNS TABLE
AS
RETURN
(
    SELECT *
    FROM STUDENT
    WHERE BRANCH = @Branch
);
```

Execute:

```sql
SELECT *
FROM dbo.FN_BranchStudents('CE')
ORDER BY SPI DESC;
```

**Important:** For an inline TVF, use `ORDER BY` in the outer query when displaying sorted results. The order of rows in a table-valued function is not guaranteed unless the consuming query specifies an order.

## 18. TVF to Rank Students

```sql
CREATE FUNCTION FN_StudentRank
(
    @Branch VARCHAR(30)
)
RETURNS TABLE
AS
RETURN
(
    SELECT
        STDID,
        SNAME,
        BRANCH,
        SPI,
        RANK() OVER (ORDER BY SPI DESC) AS StudentRank
    FROM STUDENT
    WHERE BRANCH = @Branch
);
```

Execute:

```sql
SELECT *
FROM dbo.FN_StudentRank('CE')
ORDER BY StudentRank;
```

`RANK()` assigns the same rank to tied SPI values and skips the next rank where appropriate.

## 19. TVF to Find Students with the Second-Highest SPI

The second-highest *distinct* SPI is different from the second row after sorting.

```sql
CREATE FUNCTION FN_SecondHighestSPI
(
    @Branch VARCHAR(30)
)
RETURNS TABLE
AS
RETURN
(
    SELECT
        STDID,
        SNAME,
        BRANCH,
        SPI
    FROM
    (
        SELECT
            STDID,
            SNAME,
            BRANCH,
            SPI,
            DENSE_RANK() OVER (ORDER BY SPI DESC) AS SPI_Rank
        FROM STUDENT
        WHERE BRANCH = @Branch
    ) AS RankedStudents
    WHERE SPI_Rank = 2
);
```

Execute:

```sql
SELECT *
FROM dbo.FN_SecondHighestSPI('CE');
```

`DENSE_RANK()` gives the same rank to equal SPI values without skipping rank numbers. If multiple students share the second-highest distinct SPI, all of them are returned.

## 20. Using a TVF with WHERE and ORDER BY

The result of a TVF can be filtered and sorted just like a table.

```sql
SELECT *
FROM dbo.FN_AllStudents()
WHERE SPI > 8
ORDER BY SPI DESC;
```

### Flow

```text
Call Table-Valued Function
          ↓
Receive Table Result
          ↓
Apply WHERE
          ↓
Apply ORDER BY
          ↓
Display Final Result
```

# 21. Scalar Function vs Table-Valued Function

| Feature | Scalar Function | Table-Valued Function |
|---|---|---|
| Return type | One scalar value | A table |
| Syntax | `RETURNS INT`, `RETURNS VARCHAR`, etc. | `RETURNS TABLE` or a table variable |
| Main use | Calculation or single result | Retrieving multiple records |
| Example | Calculate factorial | Display students from a city |
| How to call | `SELECT dbo.FN_Name(...)` | `SELECT * FROM dbo.FN_Name(...)` |
| Use in `FROM` | Not as a table result | Yes |
| Example output | `120` | Multiple rows and columns |

### Easy Example

Scalar function:

```sql
SELECT dbo.FN_Factorial(5) AS Result;
```

Output:

```text
Result
------
120
```

Table-valued function:

```sql
SELECT *
FROM dbo.FN_StudentsByCity('RAJKOT');
```

Output concept:

```text
STDID    SNAME    CITY      SPI
101      RAJU     RAJKOT    8.5
103      NEHA     RAJKOT    9.1
```

The rows shown are illustrative.

# 22. Function vs Stored Procedure

| Function | Stored Procedure |
|---|---|
| Must return a scalar value or table | Can return result sets, output parameters, or status codes |
| Can be used in expressions or the `FROM` clause, depending on type | Normally executed using `EXEC` |
| User-defined functions have restrictions on side effects | Can perform INSERT, UPDATE, and DELETE operations |
| Useful for calculations and reusable query results | Useful for database operations and business logic |

# 23. ALTER and DROP Functions

### Modify an Existing Scalar Function

```sql
ALTER FUNCTION FN_Welcome()
RETURNS VARCHAR(100)
AS
BEGIN
    RETURN 'Welcome to SQL Lab';
END;
```

### Remove a Function

```sql
DROP FUNCTION IF EXISTS FN_Welcome;
```

### Remove a Table-Valued Function

```sql
DROP FUNCTION IF EXISTS FN_AllStudents;
```

**Note:** Dropping a function removes the function definition, not the underlying table or its records.

# 24. Important Rules for SQL Server UDFs

1. Use `CREATE FUNCTION` to create a function.
2. Use `ALTER FUNCTION` to modify an existing function.
3. Use `DROP FUNCTION` to remove a function.
4. Use `RETURN` to return a scalar value or finish a multi-statement TVF.
5. Use `dbo.FunctionName()` when calling a function in the `dbo` schema.
6. Scalar functions return one value; TVFs return tables.
7. Call scalar functions in expressions such as `SELECT dbo.FN_Name(...)`.
8. Use `FROM dbo.FN_Name(...)` to retrieve rows from a TVF.
9. SQL Server UDFs have restrictions on side effects and data modification. Use a stored procedure when you need to insert, update, or delete data.
10. The return type of a scalar function must match the value it returns.

# 25. Final Revision

```text
User Defined Function (UDF)
          |
          +-- Scalar Function
          |      |
          |      +-- Returns one value
          |      +-- Calculations
          |      +-- Factorial
          |      +-- Date difference
          |      +-- Employee count
          |
          +-- Table-Valued Function
                 |
                 +-- Returns a table
                 +-- Filter students
                 +-- Search by city or branch
                 +-- Top N students
                 +-- Ranking
```

### Most Important Syntax

Scalar function:

```sql
CREATE FUNCTION dbo.FN_Name(@Number INT)
RETURNS INT
AS
BEGIN
    RETURN @Number * @Number;
END;
```

Execute:

```sql
SELECT dbo.FN_Name(5) AS Result;
```

Table-valued function:

```sql
CREATE FUNCTION dbo.FN_Students()
RETURNS TABLE
AS
RETURN
(
    SELECT *
    FROM STUDENT
);
```

Execute:

```sql
SELECT *
FROM dbo.FN_Students();
```

### Easy Definitions to Remember

**Scalar Function:** A user-defined function that returns a single value.

**Table-Valued Function:** A user-defined function that returns a table containing rows and columns.

**Key Difference:** Scalar functions return one value, while table-valued functions return a table that can be queried using `SELECT` and `FROM`.
