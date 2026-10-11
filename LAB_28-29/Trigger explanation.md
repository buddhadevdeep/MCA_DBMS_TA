# SQL Server Triggers — Lab 28 & Lab 29

## 1. What Is a Trigger?

A **trigger** is a special SQL object that automatically executes when a particular database event occurs, such as inserting, updating, or deleting a record.

For example, when a new employee is inserted into the `EMPLOYEE` table, a trigger can automatically display a message, update a value, or store the operation details in a log table.

### Real-Life Example

Suppose an employee's salary changes from ₹20,000 to ₹25,000.

A trigger can automatically save the old salary and new salary in an `EMPLOYEE_LOG` table.

This helps maintain an employee's history without requiring the user to insert a log record manually.

## 2. Types of Triggers in SQL Server

SQL Server supports two major categories of DML triggers.

| AFTER Trigger | INSTEAD OF Trigger |
|---|---|
| Executes after the `INSERT`, `UPDATE`, or `DELETE` operation succeeds. | Executes instead of the original `INSERT`, `UPDATE`, or `DELETE` operation. |
| The original operation happens first. | The trigger decides what action to perform. |
| Commonly used for logging and auditing. | Commonly used for validation, blocking, and custom processing. |
| Also called an `AFTER` trigger. | Also called an `INSTEAD OF` trigger. |

**Important:** SQL Server also supports DDL triggers for database-definition events and logon triggers for logon events. This lab focuses on DML triggers.

## 3. Basic Trigger Syntax

### AFTER Trigger

```sql
CREATE TRIGGER TriggerName
ON TableName
AFTER INSERT
AS
BEGIN
    -- Statements to execute after insertion
END;
```

### INSTEAD OF Trigger

```sql
CREATE TRIGGER TriggerName
ON TableName
INSTEAD OF INSERT
AS
BEGIN
    -- Statements executed instead of insertion
END;
```

The event can be `INSERT`, `UPDATE`, or `DELETE`. Multiple events can also be specified where supported.

## 4. Understanding INSERTED and DELETED

SQL Server provides two special logical tables inside DML triggers.

| Logical Table | Meaning |
|---|---|
| `INSERTED` | Contains the new row versions produced by an insert or update. |
| `DELETED` | Contains the old row versions removed by a delete or replaced by an update. |

### Example

Suppose an employee's salary changes from 20,000 to 25,000.

- `DELETED.SALARY` contains `20000`.
- `INSERTED.SALARY` contains `25000`.

For an `INSERT`, the new rows are available in `INSERTED`.

For a `DELETE`, the removed rows are available in `DELETED`.

**Important:** Triggers must support multiple rows. Do not assume `INSERTED` or `DELETED` contains only one record.

## 5. AFTER Triggers — Lab 28

### Example 1: Print a Message After Employee Insertion

```sql
CREATE TRIGGER TR_EMPLOYEE_INSERT
ON EMPLOYEE
AFTER INSERT
AS
BEGIN
    PRINT 'Employee inserted successfully.';
END;
```

**Explanation:** Whenever an employee is inserted successfully, the trigger executes automatically.

Test:

```sql
INSERT INTO EMPLOYEE (EID, FIRSTNAME)
VALUES (201, 'RAJ');
```

Use the actual required columns from your table if additional columns are mandatory.

### Example 2: Print a Message After Employee Update

```sql
CREATE TRIGGER TR_EMPLOYEE_UPDATE
ON EMPLOYEE
AFTER UPDATE
AS
BEGIN
    PRINT 'Employee updated successfully.';
END;
```

The trigger executes after an update succeeds.

### Example 3: Print a Message After Employee Deletion

```sql
CREATE TRIGGER TR_EMPLOYEE_DELETE
ON EMPLOYEE
AFTER DELETE
AS
BEGIN
    PRINT 'Employee deleted successfully.';
END;
```

The trigger executes after a delete succeeds.

### Example 4: Print a Message After a Salary Update

```sql
CREATE TRIGGER TR_SALARY_UPDATE
ON EMPLOYEE
AFTER UPDATE
AS
BEGIN
    IF UPDATE(SALARY)
    BEGIN
        PRINT 'Employee salary updated.';
    END;
END;
```

`UPDATE(SALARY)` checks whether the `SALARY` column was targeted by the update statement. It does not guarantee that the salary value actually changed.

### Example 5: Convert City Names to Uppercase During Insertion

```sql
CREATE TRIGGER TR_CITY_UPPERCASE
ON EMPLOYEE
AFTER INSERT
AS
BEGIN
    UPDATE E
    SET CITY = UPPER(E.CITY)
    FROM EMPLOYEE AS E
    INNER JOIN INSERTED AS I
        ON E.EID = I.EID;
END;
```

**Explanation:**

1. The employee is inserted.
2. The trigger reads the newly inserted rows.
3. `UPPER()` converts city names to uppercase.
4. The matching employee records are updated.

This example assumes `EID` uniquely identifies each employee and `CITY` exists in the table.

In practice, input normalization can also be handled in the application or with suitable database constraints.

### Example 6: Assign a Default City When City Is NULL

```sql
CREATE TRIGGER TR_DEFAULT_CITY
ON EMPLOYEE
AFTER INSERT
AS
BEGIN
    UPDATE E
    SET CITY = 'RAJKOT'
    FROM EMPLOYEE AS E
    INNER JOIN INSERTED AS I
        ON E.EID = I.EID
    WHERE E.CITY IS NULL;
END;
```

This assigns `RAJKOT` to inserted employees whose city is `NULL`.

A `DEFAULT` constraint is usually preferable when the requirement is simply to provide a default value.

### Example 7: Increase Salary by 10% During Insertion

```sql
CREATE TRIGGER TR_SALARY_INCREMENT
ON EMPLOYEE
AFTER INSERT
AS
BEGIN
    UPDATE E
    SET SALARY = SALARY * 1.10
    FROM EMPLOYEE AS E
    INNER JOIN INSERTED AS I
        ON E.EID = I.EID;
END;
```

**Explanation:** The trigger increases the salary of each newly inserted employee by 10%.

Use this only when the business requirement explicitly says to increase salary after insertion.

### Example 8: Create an Employee Audit Log

Create the log table first:

```sql
CREATE TABLE EMPLOYEE_LOG
(
    LOGID INT IDENTITY(1,1) PRIMARY KEY,
    EID INT,
    OLDVALUE VARCHAR(100),
    NEWVALUE VARCHAR(100),
    OPERATIONTYPE VARCHAR(20),
    LOGDATE DATETIME DEFAULT GETDATE()
);
```

Create the trigger:

```sql
CREATE TRIGGER TR_EMPLOYEE_AUDIT
ON EMPLOYEE
AFTER UPDATE
AS
BEGIN
    INSERT INTO EMPLOYEE_LOG
    (
        EID,
        OLDVALUE,
        NEWVALUE,
        OPERATIONTYPE
    )
    SELECT
        I.EID,
        CAST(D.SALARY AS VARCHAR(100)),
        CAST(I.SALARY AS VARCHAR(100)),
        'UPDATE'
    FROM INSERTED AS I
    INNER JOIN DELETED AS D
        ON I.EID = D.EID;
END;
```

**Explanation:**

- `DELETED` supplies the old salary.
- `INSERTED` supplies the new salary.
- `EMPLOYEE_LOG` stores both values and the operation type.
- Multiple updated employees are handled by the same trigger.

This example logs salary values for every updated row. To log only salary changes, add an appropriate comparison between old and new values.

### Example 9: Store Newly Inserted Employee Details

```sql
CREATE TABLE EMPLOYEE_INSERT_LOG
(
    LOGID INT IDENTITY(1,1) PRIMARY KEY,
    EID INT,
    FIRSTNAME VARCHAR(50),
    OPERATIONTYPE VARCHAR(20),
    LOGDATE DATETIME DEFAULT GETDATE()
);
```

```sql
CREATE TRIGGER TR_INSERT_EMPLOYEE_LOG
ON EMPLOYEE
AFTER INSERT
AS
BEGIN
    INSERT INTO EMPLOYEE_INSERT_LOG
    (
        EID,
        FIRSTNAME,
        OPERATIONTYPE
    )
    SELECT
        EID,
        FIRSTNAME,
        'INSERT'
    FROM INSERTED;
END;
```

This automatically records inserted employee IDs and names in a separate table.

### Example 10: Store Old and New First Names

```sql
CREATE TABLE NAME_CHANGE_LOG
(
    LOGID INT IDENTITY(1,1) PRIMARY KEY,
    EID INT,
    OLDNAME VARCHAR(50),
    NEWNAME VARCHAR(50),
    LOGDATE DATETIME DEFAULT GETDATE()
);
```

```sql
CREATE TRIGGER TR_NAME_CHANGE
ON EMPLOYEE
AFTER UPDATE
AS
BEGIN
    INSERT INTO NAME_CHANGE_LOG
    (
        EID,
        OLDNAME,
        NEWNAME
    )
    SELECT
        I.EID,
        D.FIRSTNAME,
        I.FIRSTNAME
    FROM INSERTED AS I
    INNER JOIN DELETED AS D
        ON I.EID = D.EID
    WHERE ISNULL(I.FIRSTNAME, '') <>
          ISNULL(D.FIRSTNAME, '');
END;
```

This stores the old and new first names only when the first name actually changes.

### Example 11: Assign a Default Department When NULL

```sql
CREATE TRIGGER TR_DEFAULT_DEPARTMENT
ON EMPLOYEE
AFTER INSERT
AS
BEGIN
    UPDATE E
    SET DEPARTMENT = 'ADMIN'
    FROM EMPLOYEE AS E
    INNER JOIN INSERTED AS I
        ON E.EID = I.EID
    WHERE E.DEPARTMENT IS NULL;
END;
```

This assigns `ADMIN` to newly inserted employees without a department.

A `DEFAULT` constraint or `NOT NULL` constraint may be more appropriate, depending on the requirement.

## 6. INSTEAD OF Triggers — Lab 29

An `INSTEAD OF` trigger executes instead of the original DML operation.

For example, if an `INSTEAD OF DELETE` trigger is created to block deletion, the trigger executes but the original delete does not happen unless the trigger explicitly performs a delete.

### Example 1: Prevent Employee Deletion

```sql
CREATE TRIGGER TR_PREVENT_DELETE
ON EMPLOYEE
INSTEAD OF DELETE
AS
BEGIN
    PRINT 'Employee deletion is not allowed.';
END;
```

**Explanation:** When a delete is attempted, the trigger displays a message and does not delete the employee records.

### Example 2: Prevent Employee Insertion

```sql
CREATE TRIGGER TR_PREVENT_INSERT
ON EMPLOYEE
INSTEAD OF INSERT
AS
BEGIN
    PRINT 'Employee insertion is not allowed.';
END;
```

The attempted insertion is not performed because the trigger does not insert the rows into `EMPLOYEE`.

### Example 3: Prevent Employee Updates

```sql
CREATE TRIGGER TR_PREVENT_UPDATE
ON EMPLOYEE
INSTEAD OF UPDATE
AS
BEGIN
    PRINT 'Employee updates are not allowed.';
END;
```

The original update does not occur.

### Example 4: Prevent Updates to Joining Year

```sql
CREATE TRIGGER TR_PREVENT_JOININGYEAR_UPDATE
ON EMPLOYEE
INSTEAD OF UPDATE
AS
BEGIN
    IF UPDATE(JOININGYEAR)
    BEGIN
        PRINT 'Employees are not allowed to update their joining year.';
        RETURN;
    END;

    UPDATE E
    SET
        FIRSTNAME = I.FIRSTNAME,
        LASTNAME = I.LASTNAME,
        SALARY = I.SALARY,
        CITY = I.CITY,
        DEPARTMENT = I.DEPARTMENT,
        JOININGYEAR = I.JOININGYEAR
    FROM EMPLOYEE AS E
    INNER JOIN INSERTED AS I
        ON E.EID = I.EID;
END;
```

**Explanation:** If the statement targets `JOININGYEAR`, the trigger stops processing. Otherwise, it updates the listed columns.

This example assumes the listed columns exist and that `EID` is the primary key. Every updatable column that must be preserved needs to be handled correctly. For real applications, column-specific permissions or other controls may be simpler.

### Example 5: Prevent Duplicate Employee Records

Assume an employee is considered a duplicate when `FIRSTNAME`, `LASTNAME`, and `CITY` all match an existing record.

```sql
CREATE TRIGGER TR_PREVENT_DUPLICATE_EMPLOYEE
ON EMPLOYEE
INSTEAD OF INSERT
AS
BEGIN
    IF EXISTS
    (
        SELECT 1
        FROM INSERTED AS I
        INNER JOIN EMPLOYEE AS E
            ON E.FIRSTNAME = I.FIRSTNAME
            AND E.LASTNAME = I.LASTNAME
            AND E.CITY = I.CITY
    )
    BEGIN
        PRINT 'Duplicate employee record is not allowed.';
        RETURN;
    END;

    INSERT INTO EMPLOYEE
    (
        EID,
        FIRSTNAME,
        LASTNAME,
        CITY
    )
    SELECT
        EID,
        FIRSTNAME,
        LASTNAME,
        CITY
    FROM INSERTED;
END;
```

**Explanation:**

1. The trigger checks whether any incoming employee matches an existing employee.
2. If a duplicate exists, it stops without inserting the incoming rows.
3. Otherwise, it inserts the incoming records.

This is an educational example. It assumes these columns exist and that `EID` is supplied by the caller. It does not handle every possible duplicate within the same multi-row insert. For reliable duplicate prevention, use a suitable `UNIQUE` constraint or unique index, with an appropriate key definition.

### Example 6: Prevent Insertion of Employees With NULL Department

```sql
CREATE TRIGGER TR_CHECK_DEPARTMENT
ON EMPLOYEE
INSTEAD OF INSERT
AS
BEGIN
    IF EXISTS
    (
        SELECT 1
        FROM INSERTED
        WHERE DEPARTMENT IS NULL
    )
    BEGIN
        PRINT 'Department cannot be NULL.';
        RETURN;
    END;

    INSERT INTO EMPLOYEE
    (
        EID,
        FIRSTNAME,
        LASTNAME,
        DEPARTMENT
    )
    SELECT
        EID,
        FIRSTNAME,
        LASTNAME,
        DEPARTMENT
    FROM INSERTED;
END;
```

The trigger rejects the entire incoming batch if any inserted row has a `NULL` department. Otherwise, it inserts the incoming rows.

For ordinary required-column validation, a `NOT NULL` constraint is generally the better solution.

## 7. Student Triggers — Lab 29

The same concepts can be applied to the `STUDENT` table.

Assume the table contains `STDID`, `SNAME`, `BRANCH`, and `SPI`.

### Example 1: Prevent Insertion When SPI Is Outside 0–10

```sql
CREATE TRIGGER TR_CHECK_STUDENT_SPI
ON STUDENT
INSTEAD OF INSERT
AS
BEGIN
    IF EXISTS
    (
        SELECT 1
        FROM INSERTED
        WHERE SPI < 0 OR SPI > 10
    )
    BEGIN
        PRINT 'SPI must be between 0 and 10.';
        RETURN;
    END;

    INSERT INTO STUDENT
    (
        STDID,
        SNAME,
        BRANCH,
        SPI
    )
    SELECT
        STDID,
        SNAME,
        BRANCH,
        SPI
    FROM INSERTED;
END;
```

The trigger rejects the incoming batch if any SPI value is outside the permitted range.

A `CHECK` constraint is normally preferable for this rule:

```sql
ALTER TABLE STUDENT
ADD CONSTRAINT CK_STUDENT_SPI
CHECK (SPI >= 0 AND SPI <= 10);
```

### Example 2: Prevent Branch Changes After Admission

```sql
CREATE TRIGGER TR_PREVENT_BRANCH_UPDATE
ON STUDENT
INSTEAD OF UPDATE
AS
BEGIN
    IF UPDATE(BRANCH)
    BEGIN
        PRINT 'Branch cannot be changed after admission.';
        RETURN;
    END;

    UPDATE S
    SET
        SNAME = I.SNAME,
        SPI = I.SPI
    FROM STUDENT AS S
    INNER JOIN INSERTED AS I
        ON S.STDID = I.STDID;
END;
```

This example blocks update statements that target `BRANCH`. Other permitted columns are updated explicitly. Add every other updatable column that your actual `STUDENT` table requires.

### Example 3: Prevent Student Deletion

```sql
CREATE TRIGGER TR_PREVENT_STUDENT_DELETE
ON STUDENT
INSTEAD OF DELETE
AS
BEGIN
    PRINT 'Student deletion is not allowed.';
END;
```

The trigger stops the original delete operation.

## 8. AFTER vs INSTEAD OF: Final Difference

| Feature | AFTER | INSTEAD OF |
|---|---|---|
| Execution | After the original operation succeeds | In place of the original operation |
| Original operation | Already performed, subject to transaction success | Not performed automatically |
| Logging | Common use | Possible, if explicitly implemented |
| Blocking an operation | Can raise an error and roll back the transaction | Can omit the original operation |
| Custom insertion/update/delete | Usually supplements the original operation | Must explicitly perform permitted operations |
| Common example | Save salary changes to a log | Reject a delete request |

## 9. Other Important Trigger Concepts

### A. DML Triggers

DML means Data Manipulation Language.

Examples of DML statements:

- `INSERT`
- `UPDATE`
- `DELETE`

DML triggers execute when the configured table or view operation occurs.

### B. DDL Triggers

DDL means Data Definition Language.

Examples include:

- `CREATE TABLE`
- `ALTER TABLE`
- `DROP TABLE`

DDL triggers can be used to audit or restrict changes to database objects.

Example:

```sql
CREATE TRIGGER TR_DATABASE_DDL
ON DATABASE
FOR CREATE_TABLE
AS
BEGIN
    PRINT 'A table was created.';
END;
```

This database-scoped trigger fires when a table is created. It is separate from the `EMPLOYEE` DML triggers.

### C. Logon Triggers

Logon triggers execute in response to a SQL Server logon event. They can be used for connection auditing or carefully designed access controls.

They require special care because an incorrect logon trigger can prevent legitimate connections.

### D. Trigger Conditions

`IF`, `EXISTS`, `UPDATE(column)`, and comparisons can be used inside a trigger to decide which actions should occur.

Remember that `UPDATE(column)` indicates whether a column was targeted by the statement, not whether its value necessarily changed.

### E. Nested and Recursive Triggers

A trigger can cause another trigger to execute by modifying another table or by causing another applicable operation. SQL Server has settings that affect recursive trigger behavior. Avoid unnecessary trigger chains because they make database behavior harder to understand and debug.

## 10. View Trigger Definitions and Manage Triggers

### View Existing Triggers

```sql
SELECT
    name,
    object_id,
    type_desc
FROM sys.triggers;
```

### View a Trigger's Definition

```sql
EXEC sp_helptext 'TR_EMPLOYEE_AUDIT';
```

### Disable a Trigger

```sql
DISABLE TRIGGER TR_EMPLOYEE_AUDIT
ON EMPLOYEE;
```

### Enable a Trigger

```sql
ENABLE TRIGGER TR_EMPLOYEE_AUDIT
ON EMPLOYEE;
```

### Delete a Trigger

```sql
DROP TRIGGER TR_EMPLOYEE_AUDIT;
```

Use the actual trigger name in each command.

## 11. Best Practices

1. Write triggers that support multiple inserted, updated, or deleted rows.
2. Use `INSERTED` and `DELETED` instead of assuming a single affected record.
3. Avoid unnecessary cursors and row-by-row loops inside triggers.
4. Keep trigger logic short, clear, and easy to test.
5. Prefer constraints for rules such as `NOT NULL`, `CHECK`, and `UNIQUE` when appropriate.
6. Be careful with `INSTEAD OF` triggers: they must explicitly perform any permitted operation.
7. Remember that trigger work normally runs within the transaction of the original statement; a trigger error can cause the transaction to fail or roll back.
8. Test insert, update, and delete statements involving multiple rows.
9. Avoid using `PRINT` as the only production error-handling mechanism. Use appropriate errors and transaction handling where needed.
10. Do not create multiple overlapping triggers without understanding their behavior and execution order.

## 12. Quick Revision

- **Trigger:** A database object that executes automatically in response to a configured event.
- **AFTER:** Executes after the original DML operation succeeds.
- **INSTEAD OF:** Executes instead of the original DML operation.
- **INSERTED:** Contains new row versions from an insert or update.
- **DELETED:** Contains deleted row versions or old row versions from an update.
- **DML trigger:** Responds to `INSERT`, `UPDATE`, or `DELETE`.
- **DDL trigger:** Responds to database-definition events such as `CREATE_TABLE`.
- **Logon trigger:** Responds to SQL Server logon events.
- **Audit trigger:** Records changes or operations for auditing.
- **`UPDATE(column)`:** Checks whether the column was targeted by an update statement.
- **Constraint:** Often the simplest and most reliable way to enforce basic data rules.

**Remember:** AFTER triggers are commonly used to react to completed operations, while INSTEAD OF triggers let you replace the normal operation with custom logic.
