# Lab 30: Exception Handling in MS SQL Server — TRY...CATCH, THROW and RAISERROR

## 1. What Is Exception Handling?

**Exception handling** is a mechanism used to handle errors that occur while executing SQL statements. It helps prevent unexpected failures and allows us to display meaningful error messages.

For example, dividing a number by zero causes an error. Instead of allowing the operation to fail without useful handling, we can catch the error and display a message.

### Real-Life Example

Suppose an application tries to update an employee's salary to `-5000`.

The database should reject the invalid salary and return an understandable error message.

SQL Server provides `TRY...CATCH`, `THROW`, and `RAISERROR` to handle such situations.

## 2. Types of Error Handling

| Concept | Purpose |
|---|---|
| `TRY...CATCH` | Catches and handles runtime errors. |
| `THROW` | Raises an exception or rethrows a caught error. |
| `RAISERROR` | Raises a user-defined error message with a specified severity and state. |
| `ERROR_MESSAGE()` | Returns the error message. |
| `ERROR_NUMBER()` | Returns the error number. |
| `ERROR_SEVERITY()` | Returns the error severity. |
| `ERROR_STATE()` | Returns the error state. |
| `ERROR_LINE()` | Returns the line number where the error occurred. |
| `ERROR_PROCEDURE()` | Returns the name of the stored procedure or trigger where the error occurred, if applicable. |

## 3. Basic TRY...CATCH Syntax

```sql
BEGIN TRY
    -- Statements that may cause an error
END TRY
BEGIN CATCH
    -- Handle the error
    SELECT ERROR_MESSAGE() AS ErrorMessage;
END CATCH;
```

### How It Works

1. SQL Server executes the statements inside `TRY`.
2. If a catchable error occurs, control moves to `CATCH`.
3. The `CATCH` block retrieves and handles the error.
4. If no error occurs, the `CATCH` block is skipped.

**Important:** Not every error is caught by `TRY...CATCH`. Some errors, such as certain compilation errors at the same execution level, are not caught.

## 4. Example 1: Handle Divide-by-Zero Error

```sql
BEGIN TRY
    DECLARE @A INT = 10;
    DECLARE @B INT = 0;

    SELECT @A / @B AS Result;
END TRY
BEGIN CATCH
    PRINT 'Error occurs that is - Divide by zero error.';

    SELECT ERROR_MESSAGE() AS ErrorMessage;
END CATCH;
```

**Explanation:** Dividing 10 by 0 causes an error. SQL Server transfers control to the `CATCH` block, which displays the message.

## 5. Example 2: Convert String to Integer

```sql
BEGIN TRY
    DECLARE @VALUE VARCHAR(20) = 'ABC';

    SELECT CAST(@VALUE AS INT) AS Result;
END TRY
BEGIN CATCH
    SELECT
        ERROR_NUMBER() AS ErrorNumber,
        ERROR_MESSAGE() AS ErrorMessage;
END CATCH;
```

**Explanation:** The value `'ABC'` cannot be converted into an integer, so the error is caught.

A safer alternative when conversion failure is expected is `TRY_CAST`:

```sql
SELECT TRY_CAST('ABC' AS INT) AS Result;
```

It returns `NULL` instead of raising a conversion error.

## 6. Example 3: Add Two Numbers and Handle Invalid Input

This stored procedure accepts two string inputs, converts them to integers, and calculates their sum.

```sql
CREATE OR ALTER PROCEDURE SP_ADD_NUMBERS
    @A VARCHAR(20),
    @B VARCHAR(20)
AS
BEGIN
    SET NOCOUNT ON;

    BEGIN TRY
        DECLARE @NUM1 INT = TRY_CAST(@A AS INT);
        DECLARE @NUM2 INT = TRY_CAST(@B AS INT);

        IF @NUM1 IS NULL OR @NUM2 IS NULL
        BEGIN
            THROW 50001, 'Both inputs must be valid integers.', 1;
        END;

        SELECT @NUM1 + @NUM2 AS Total;
    END TRY
    BEGIN CATCH
        SELECT
            ERROR_NUMBER() AS ErrorNumber,
            ERROR_MESSAGE() AS ErrorMessage,
            ERROR_SEVERITY() AS ErrorSeverity,
            ERROR_STATE() AS ErrorState;
    END CATCH;
END;
```

Execute:

```sql
EXEC SP_ADD_NUMBERS '10', '20';

EXEC SP_ADD_NUMBERS '10', 'ABC';
```

The first call returns `30`. The second call reports an invalid integer input.

## 7. Example 4: Handle Primary Key Violation

Assume `STUDENT_INFO` has `RNO` as its primary key.

```sql
BEGIN TRY
    INSERT INTO STUDENT_INFO (RNO, NAME)
    VALUES (101, 'RAJ');
END TRY
BEGIN CATCH
    SELECT
        ERROR_NUMBER() AS ErrorNumber,
        ERROR_MESSAGE() AS ErrorMessage,
        ERROR_SEVERITY() AS ErrorSeverity,
        ERROR_STATE() AS ErrorState;
END CATCH;
```

If roll number `101` already exists, SQL Server raises a primary key violation and the `CATCH` block displays the error details.

Replace `RNO` and `NAME` with the actual column names and supply any other required columns in your table.

## 8. Example 5: THROW a Custom Error When an Employee Does Not Exist

```sql
CREATE OR ALTER PROCEDURE SP_CHECK_EMPLOYEE
    @EID INT
AS
BEGIN
    SET NOCOUNT ON;

    IF NOT EXISTS
    (
        SELECT 1
        FROM EMPLOYEE
        WHERE EID = @EID
    )
    BEGIN
        THROW 50002, 'No employee is available with this EID.', 1;
    END;

    SELECT *
    FROM EMPLOYEE
    WHERE EID = @EID;
END;
```

Execute:

```sql
EXEC SP_CHECK_EMPLOYEE 101;
```

If employee `101` exists, the procedure returns the employee details. Otherwise, it raises the custom error.

## 9. Example 6: Update Salary and Reject Negative or Zero Values

```sql
CREATE OR ALTER PROCEDURE SP_UPDATE_SALARY
    @EID INT,
    @SALARY DECIMAL(10,2)
AS
BEGIN
    SET NOCOUNT ON;

    BEGIN TRY
        IF @SALARY <= 0
        BEGIN
            THROW 50003, 'Salary must be greater than zero.', 1;
        END;

        IF NOT EXISTS
        (
            SELECT 1
            FROM EMPLOYEE
            WHERE EID = @EID
        )
        BEGIN
            THROW 50004, 'Employee does not exist.', 1;
        END;

        UPDATE EMPLOYEE
        SET SALARY = @SALARY
        WHERE EID = @EID;

        PRINT 'Salary updated successfully.';
    END TRY
    BEGIN CATCH
        SELECT ERROR_MESSAGE() AS ErrorMessage;
    END CATCH;
END;
```

Execute:

```sql
EXEC SP_UPDATE_SALARY 101, 25000;

EXEC SP_UPDATE_SALARY 101, -5000;
```

The first call updates the salary if the employee exists. The second call reports a validation error.

## 10. Example 7: Handle Foreign Key Violation

Suppose `RESULT.RNO` references `STUDENT_INFO.RNO`.

```sql
BEGIN TRY
    INSERT INTO RESULT (RESULTID, SPI, RNO)
    VALUES (1001, 8.5, 999);
END TRY
BEGIN CATCH
    SELECT
        ERROR_NUMBER() AS ErrorNumber,
        ERROR_MESSAGE() AS ErrorMessage;

    IF ERROR_NUMBER() = 547
        PRINT 'Foreign key violation: Student does not exist.';
END CATCH;
```

If roll number `999` does not exist in `STUDENT_INFO`, the foreign key constraint rejects the insertion.

**Note:** SQL Server error `547` can indicate other constraint violations too, so check the message to identify the exact problem.

## 11. Example 8: Handle Invalid Date Format

```sql
BEGIN TRY
    DECLARE @DATEVALUE DATE;

    SET @DATEVALUE = CONVERT(DATE, '31-02-2025', 105);

    INSERT INTO DEPOSIT (ADATE)
    VALUES (@DATEVALUE);
END TRY
BEGIN CATCH
    SELECT
        ERROR_NUMBER() AS ErrorNumber,
        ERROR_MESSAGE() AS ErrorMessage;
END CATCH;
```

The date is invalid because February 2025 does not have 31 days. SQL Server catches the conversion error.

This example assumes `DEPOSIT.ADATE` is a date column and that other required columns have suitable defaults or are not required.

For user-provided dates, you can also use `TRY_CONVERT` and validate the returned value before inserting.

## 12. Example 9: Validate Gender in a Stored Procedure

```sql
CREATE OR ALTER PROCEDURE SP_VALIDATE_GENDER
    @EID INT,
    @GENDER VARCHAR(10)
AS
BEGIN
    SET NOCOUNT ON;

    IF LOWER(@GENDER) NOT IN ('male', 'female')
       OR @GENDER IS NULL
    BEGIN
        THROW 50005, 'Gender must be Male or Female.', 1;
    END;

    UPDATE EMPLOYEE
    SET GENDER = CASE
        WHEN LOWER(@GENDER) = 'male' THEN 'Male'
        ELSE 'Female'
    END
    WHERE EID = @EID;

    IF @@ROWCOUNT = 0
    BEGIN
        THROW 50006, 'Employee does not exist.', 1;
    END;

    PRINT 'Gender updated successfully.';
END;
```

The procedure accepts only `Male` or `Female` and updates the matching employee.

This example assumes the `EMPLOYEE` table contains `EID` and `GENDER` columns.

## 13. Example 10: Reject a Joining Year Greater Than the Current Year

```sql
CREATE OR ALTER PROCEDURE SP_VALIDATE_JOINING_YEAR
    @EID INT,
    @JOININGYEAR INT
AS
BEGIN
    SET NOCOUNT ON;

    IF @JOININGYEAR > YEAR(GETDATE())
    BEGIN
        THROW 50007, 'Joining year cannot be greater than the current year.', 1;
    END;

    UPDATE EMPLOYEE
    SET JOININGYEAR = @JOININGYEAR
    WHERE EID = @EID;

    IF @@ROWCOUNT = 0
    BEGIN
        THROW 50008, 'Employee does not exist.', 1;
    END;

    PRINT 'Joining year updated successfully.';
END;
```

This validates the joining year before updating the employee record.

## 14. Example 11: Delete Employee and Handle Missing Employee

```sql
CREATE OR ALTER PROCEDURE SP_DELETE_EMPLOYEE
    @EID INT
AS
BEGIN
    SET NOCOUNT ON;

    BEGIN TRY
        IF NOT EXISTS
        (
            SELECT 1
            FROM EMPLOYEE
            WHERE EID = @EID
        )
        BEGIN
            THROW 50009, 'Cannot delete: Employee does not exist.', 1;
        END;

        DELETE FROM EMPLOYEE
        WHERE EID = @EID;

        PRINT 'Employee deleted successfully.';
    END TRY
    BEGIN CATCH
        SELECT
            ERROR_NUMBER() AS ErrorNumber,
            ERROR_MESSAGE() AS ErrorMessage;
    END CATCH;
END;
```

If the employee does not exist, the procedure raises a custom error. A delete may also fail if other tables reference that employee through foreign keys.

## 15. Example 12: Reject a NULL Department During Insertion

```sql
CREATE OR ALTER PROCEDURE SP_INSERT_EMPLOYEE
    @EID INT,
    @FIRSTNAME VARCHAR(50),
    @DEPARTMENT VARCHAR(50)
AS
BEGIN
    SET NOCOUNT ON;

    BEGIN TRY
        IF @DEPARTMENT IS NULL
        BEGIN
            THROW 50010, 'Department cannot be NULL.', 1;
        END;

        INSERT INTO EMPLOYEE
        (
            EID,
            FIRSTNAME,
            DEPARTMENT
        )
        VALUES
        (
            @EID,
            @FIRSTNAME,
            @DEPARTMENT
        );

        PRINT 'Employee inserted successfully.';
    END TRY
    BEGIN CATCH
        SELECT
            ERROR_NUMBER() AS ErrorNumber,
            ERROR_MESSAGE() AS ErrorMessage;
    END CATCH;
END;
```

This example assumes the listed columns exist and other required columns are handled appropriately.

## 16. THROW vs RAISERROR

| THROW | RAISERROR |
|---|---|
| Modern recommended method for raising exceptions. | Older error-raising method still supported in SQL Server. |
| Can raise a custom error or rethrow the current error. | Can specify a message, severity, and state. |
| Custom error numbers must be at least `50000`. | Supports custom message formatting and configurable severity. |
| A new error is generally raised with severity 16. | Severity can be explicitly specified. |
| Does not require `sys.messages` for a custom message. | Can use a message string or a registered message ID. |

### THROW Syntax

```sql
THROW 50011, 'Invalid salary value.', 1;
```

The three values represent the error number, message, and state.

### RAISERROR Syntax

```sql
RAISERROR('Invalid salary value.', 16, 1);
```

Here, `16` is the severity and `1` is the state.

**Important:** When using `THROW` to rethrow an existing exception inside a `CATCH` block, use `THROW;` without arguments to preserve the original error.

## 17. SQL Server Error Functions

These functions provide details about the error being handled inside a `CATCH` block.

```sql
BEGIN TRY
    SELECT 10 / 0 AS Result;
END TRY
BEGIN CATCH
    SELECT
        ERROR_NUMBER() AS ErrorNumber,
        ERROR_MESSAGE() AS ErrorMessage,
        ERROR_SEVERITY() AS ErrorSeverity,
        ERROR_STATE() AS ErrorState,
        ERROR_LINE() AS ErrorLine,
        ERROR_PROCEDURE() AS ErrorProcedure;
END CATCH;
```

| Function | Returns |
|---|---|
| `ERROR_NUMBER()` | SQL Server error number |
| `ERROR_MESSAGE()` | Error description |
| `ERROR_SEVERITY()` | Error severity level |
| `ERROR_STATE()` | Error state code |
| `ERROR_LINE()` | Line number where the error occurred |
| `ERROR_PROCEDURE()` | Procedure or trigger name, if applicable |

These functions return the current error details when called inside a `CATCH` block.

## 18. Important Rules to Remember

1. Put potentially failing statements inside `BEGIN TRY` and `END TRY`.
2. Handle catchable errors inside `BEGIN CATCH` and `END CATCH`.
3. Use `THROW` to raise custom errors with meaningful messages.
4. Use `ERROR_MESSAGE()` to display the error description.
5. Use `ERROR_NUMBER()` to identify specific SQL Server errors.
6. Validate input before inserting or updating data.
7. Primary key violations usually occur when a duplicate key is inserted.
8. Foreign key violations occur when a referenced parent record does not exist or a referenced key is changed or deleted in a prohibited way.
9. `TRY_CAST` and `TRY_CONVERT` can return `NULL` for failed conversions instead of raising conversion errors.
10. `TRY...CATCH` does not automatically guarantee that every earlier change in a transaction is rolled back. Use suitable transaction handling when multiple changes must succeed or fail together.

## 19. Quick Revision

| Concept | Meaning |
|---|---|
| Exception handling | Handling errors during SQL execution |
| `TRY` | Contains statements to execute |
| `CATCH` | Contains error-handling statements |
| `THROW` | Raises or rethrows an exception |
| `RAISERROR` | Raises a custom SQL Server error |
| `ERROR_MESSAGE()` | Returns the error description |
| `ERROR_NUMBER()` | Returns the error code |
| `ERROR_SEVERITY()` | Returns the error severity |
| `ERROR_STATE()` | Returns the error state |
| `TRY_CAST()` | Attempts conversion and returns `NULL` if it fails |
| Stored procedure | A named collection of SQL statements that can accept parameters |

**Final takeaway:** Use `TRY...CATCH` to handle errors, `THROW` to report invalid operations, and SQL Server error functions to understand what went wrong.
