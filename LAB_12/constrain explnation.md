# Lab 12 – SQL Constraints in MS SQL Server

## 📌 Introduction

A **constraint** is a rule applied to a table or column to control the data stored in the database.

Constraints help maintain **data accuracy, consistency, and relationships**.

### Types of Constraints

1. `PRIMARY KEY`
2. `NOT NULL`
3. `UNIQUE`
4. `DEFAULT`
5. `CHECK`
6. `FOREIGN KEY`

---

## 1. PRIMARY KEY

A **PRIMARY KEY** uniquely identifies every record in a table.

### Rules

- Cannot contain `NULL`.
- Cannot contain duplicate values.
- A table can have only one primary key.

### Example

```sql
CREATE TABLE Student
(
    RNO INT PRIMARY KEY,
    NAME VARCHAR(20)
);
```

```sql
INSERT INTO Student VALUES (101, 'RAJU');
INSERT INTO Student VALUES (102, 'AMIT');
```

Duplicate value is not allowed:

```sql
INSERT INTO Student VALUES (101, 'RAHUL');
```

---

## 2. NOT NULL

`NOT NULL` means a value is compulsory.

```sql
CREATE TABLE Student
(
    RNO INT PRIMARY KEY,
    NAME VARCHAR(20) NOT NULL
);
```

Valid:

```sql
INSERT INTO Student VALUES (101, 'RAJU');
```

Invalid:

```sql
INSERT INTO Student VALUES (102, NULL);
```

---

## 3. UNIQUE

`UNIQUE` prevents duplicate values in a column.

```sql
CREATE TABLE Employee
(
    EMP_ID INT PRIMARY KEY,
    EMAIL VARCHAR(100) UNIQUE
);
```

Valid:

```sql
INSERT INTO Employee VALUES (1, 'abc@gmail.com');
INSERT INTO Employee VALUES (2, 'xyz@gmail.com');
```

Duplicate email is not allowed:

```sql
INSERT INTO Employee VALUES (3, 'abc@gmail.com');
```

### PRIMARY KEY vs UNIQUE

```text
PRIMARY KEY
→ Unique + NOT NULL
→ Identifies each record
→ Only one PRIMARY KEY per table

UNIQUE
→ Prevents duplicate values
→ Multiple UNIQUE constraints can be used
```

---

## 4. DEFAULT

`DEFAULT` automatically inserts a value when no value is provided.

```sql
CREATE TABLE Student
(
    RNO INT PRIMARY KEY,
    NAME VARCHAR(20) NOT NULL,
    BRANCH VARCHAR(20) DEFAULT 'CE'
);
```

```sql
INSERT INTO Student
(RNO, NAME)
VALUES
(101, 'RAJU');
```

Result:

```text
RNO     NAME     BRANCH
101     RAJU     CE
```

The value `CE` is automatically inserted.

You can also provide your own value:

```sql
INSERT INTO Student
VALUES (102, 'AMIT', 'IT');
```

---

## 5. CHECK

`CHECK` allows data only when a condition is true.

For example, SPI must be between `0` and `10`.

```sql
CREATE TABLE Result
(
    RESULTID INT PRIMARY KEY,

    SPI DECIMAL(4,2)
        CHECK (SPI >= 0 AND SPI <= 10)
);
```

Valid:

```sql
INSERT INTO Result VALUES (1, 8.5);
```

Invalid:

```sql
INSERT INTO Result VALUES (2, 15);
```

Because SPI cannot be greater than `10`.

Another example:

```sql
CREATE TABLE Employee
(
    EMP_ID INT PRIMARY KEY,
    SALARY INT CHECK (SALARY > 0)
);
```

---

## 6. FOREIGN KEY

A **FOREIGN KEY** creates a relationship between two tables.

It connects a column in one table to the `PRIMARY KEY` of another table.

### Parent Table

```sql
CREATE TABLE Student
(
    RNO INT PRIMARY KEY,
    NAME VARCHAR(20)
);
```

### Child Table

```sql
CREATE TABLE Result
(
    RESULTID INT PRIMARY KEY,
    SPI DECIMAL(4,2),
    RNO INT,

    FOREIGN KEY (RNO)
    REFERENCES Student(RNO)
);
```

Relationship:

```text
Student
   |
   | RNO
   ↓
Result
```

First insert the parent record:

```sql
INSERT INTO Student
VALUES (101, 'RAJU');
```

Then insert the child record:

```sql
INSERT INTO Result
VALUES (1, 8.5, 101);
```

This works because student `101` exists.

This fails:

```sql
INSERT INTO Result
VALUES (2, 9.0, 999);
```

Because student `999` does not exist in the `Student` table.

---

## 7. ON DELETE CASCADE

`ON DELETE CASCADE` automatically deletes related child records when the parent record is deleted.

```sql
CREATE TABLE Result
(
    RESULTID INT PRIMARY KEY,
    RNO INT,

    FOREIGN KEY (RNO)
    REFERENCES Student(RNO)
    ON DELETE CASCADE
);
```

If student `101` is deleted, its related result records are also deleted.

---

## 8. Multiple Constraints

A column can have more than one constraint.

```sql
CREATE TABLE Result
(
    RESULTID INT PRIMARY KEY,

    SPI DECIMAL(4,2)
        NOT NULL
        CHECK (SPI >= 0 AND SPI <= 10),

    RNO INT
);
```

Here `SPI`:

```text
NOT NULL
→ SPI cannot be NULL

CHECK
→ SPI must be between 0 and 10
```

---

## 9. Complete Example

### Student Table

```sql
CREATE TABLE STUDENT_INFO
(
    RNO INT PRIMARY KEY,
    NAME VARCHAR(20) NOT NULL,
    BRANCH VARCHAR(20) DEFAULT 'CE'
);
```

### Result Table

```sql
CREATE TABLE RESULT
(
    RESULTID INT PRIMARY KEY,

    SPI DECIMAL(4,2)
        CHECK (SPI >= 0 AND SPI <= 10),

    RNO INT,

    FOREIGN KEY (RNO)
    REFERENCES STUDENT_INFO(RNO)
);
```

### Insert Student Data

```sql
INSERT INTO STUDENT_INFO
VALUES
(101, 'RAJU', 'CE'),
(102, 'AMIT', 'CE'),
(103, 'SANIYA', 'ME'),
(104, 'NEHA', 'EC');
```

### Insert Result Data

```sql
INSERT INTO RESULT
VALUES
(11, 8.8, 101),
(12, 9.2, 102),
(13, 7.6, 103),
(14, 8.2, 104);
```

---

## 10. Testing Constraints

### PRIMARY KEY

```sql
INSERT INTO STUDENT_INFO
VALUES (101, 'RAHUL', 'IT');
```

❌ Error because `101` already exists.

### NOT NULL

```sql
INSERT INTO STUDENT_INFO
VALUES (105, NULL, 'CE');
```

❌ Error because `NAME` cannot be `NULL`.

### DEFAULT

```sql
INSERT INTO STUDENT_INFO
(RNO, NAME)
VALUES (105, 'MEERA');
```

`BRANCH` automatically becomes `CE`.

### CHECK

```sql
INSERT INTO RESULT
VALUES (15, 12.5, 101);
```

❌ Error because SPI must be between `0` and `10`.

### FOREIGN KEY

```sql
INSERT INTO RESULT
VALUES (16, 8.5, 999);
```

❌ Error because `999` does not exist in `STUDENT_INFO`.

---

## 11. Adding Constraints Using ALTER TABLE

Constraints can also be added after creating a table.

### PRIMARY KEY

```sql
ALTER TABLE Student
ADD CONSTRAINT PK_Student
PRIMARY KEY (RNO);
```

### UNIQUE

```sql
ALTER TABLE Student
ADD CONSTRAINT UQ_Student_Name
UNIQUE (NAME);
```

### CHECK

```sql
ALTER TABLE Result
ADD CONSTRAINT CK_Result_SPI
CHECK (SPI >= 0 AND SPI <= 10);
```

### FOREIGN KEY

```sql
ALTER TABLE Result
ADD CONSTRAINT FK_Result_Student
FOREIGN KEY (RNO)
REFERENCES Student(RNO);
```

### DEFAULT

```sql
ALTER TABLE Student
ADD CONSTRAINT DF_Student_Branch
DEFAULT 'CE' FOR BRANCH;
```

### NOT NULL

```sql
ALTER TABLE Student
ALTER COLUMN NAME VARCHAR(20) NOT NULL;
```

---

## 12. Naming Constraints

Giving constraints a name makes them easier to identify and manage.

```sql
CREATE TABLE Student
(
    RNO INT
        CONSTRAINT PK_Student PRIMARY KEY,

    NAME VARCHAR(20)
        CONSTRAINT UQ_Student_Name UNIQUE,

    BRANCH VARCHAR(20)
        CONSTRAINT DF_Student_Branch DEFAULT 'CE'
);
```

### Common Naming Convention

```text
PK_ → Primary Key
FK_ → Foreign Key
UQ_ → Unique
CK_ → Check
DF_ → Default
```

Examples:

```text
PK_Student
FK_Result_Student
UQ_Student_Email
CK_Result_SPI
DF_Student_Branch
```

---

## 13. Constraint Flow

```text
INSERT / UPDATE DATA
        |
        ↓
PRIMARY KEY CHECK
        |
        ↓
NOT NULL CHECK
        |
        ↓
UNIQUE CHECK
        |
        ↓
CHECK CONDITION
        |
        ↓
FOREIGN KEY CHECK
        |
        ↓
     VALID?
      /   \
    YES    NO
     |      |
     ↓      ↓
   SAVE    ERROR
```

---

## 14. Quick Revision

| Constraint | Purpose |
|---|---|
| `PRIMARY KEY` | Uniquely identifies each record |
| `NOT NULL` | Value is compulsory |
| `UNIQUE` | Prevents duplicate values |
| `DEFAULT` | Automatically provides a value |
| `CHECK` | Validates a condition |
| `FOREIGN KEY` | Creates a relationship between tables |

### Easy Way to Remember

```text
PRIMARY KEY
→ Who is this record?

NOT NULL
→ Is the value compulsory?

UNIQUE
→ Can duplicate values exist?

DEFAULT
→ What value should be inserted automatically?

CHECK
→ Is the value valid?

FOREIGN KEY
→ Does this value exist in another table?
```

---

## Final Summary

```text
PRIMARY KEY → Identity
NOT NULL    → Required value
UNIQUE      → No duplicates
DEFAULT     → Automatic value
CHECK       → Condition validation
FOREIGN KEY → Table relationship
```
