# 📘 DBMS Lab - ALTER TABLE Command

<p align="center">
  <img src="https://img.shields.io/badge/DBMS-ALTER_TABLE-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/SQL-DDL_Command-green?style=for-the-badge">
  <img src="https://img.shields.io/badge/Level-Beginner-orange?style=for-the-badge">
</p>

---

# 📖 Introduction

The **ALTER TABLE** command is a **Data Definition Language (DDL)** command used to modify the structure of an existing table without deleting the table or its data.

Using ALTER TABLE, we can:

- Add a new column
- Modify an existing column
- Change a column name
- Change a column datatype
- Rename a table
- Drop (delete) a column
- Add constraints
- Remove constraints

> **Note:** ALTER TABLE changes the table structure, **not the data** stored inside it.

---

# 🎯 Why Do We Use ALTER TABLE?

Suppose you created a table for students.

```sql
CREATE TABLE Student(
    StudentID INT,
    Name VARCHAR(50)
);
```

Later your college decides to store the student's email.

Instead of deleting and recreating the table, we simply use **ALTER TABLE**.

---

# 📌 Syntax

```sql
ALTER TABLE table_name
operation;
```

Example

```sql
ALTER TABLE Student
ADD Email VARCHAR(100);
```

---

# 📂 Sample Table

Before learning every ALTER command, consider this table.

| StudentID | Name | Age |
|-----------|------|-----|
|101|Rahul|20|
|102|Priya|19|
|103|Amit|21|

---

# 1️⃣ ALTER TABLE ADD COLUMN

## What is ADD?

The **ADD** keyword is used to insert one or more new columns into an existing table.

Existing data remains unchanged.

---

## Syntax

```sql
ALTER TABLE table_name
ADD column_name datatype;
```

---

## Example 1

```sql
ALTER TABLE Student
ADD Email VARCHAR(100);
```

### Before

|StudentID|Name|Age|
|---------|----|---|
|101|Rahul|20|

### After

|StudentID|Name|Age|Email|
|---------|----|---|------|
|101|Rahul|20|NULL|

Notice the new column contains **NULL** because no values are inserted yet.

---

## Example 2

Add Mobile Number

```sql
ALTER TABLE Student
ADD Mobile VARCHAR(15);
```

---

## Example 3

Add Address

```sql
ALTER TABLE Student
ADD Address VARCHAR(200);
```

---

## Adding Multiple Columns

Syntax

```sql
ALTER TABLE table_name
ADD column1 datatype,
ADD column2 datatype;
```

Example

```sql
ALTER TABLE Student
ADD Gender CHAR(1),
ADD City VARCHAR(50);
```

---

# 2️⃣ ALTER TABLE MODIFY COLUMN

## What is MODIFY?

The **MODIFY** command changes the datatype or size of an existing column.

It does **not** change the column name.

---

## Syntax

```sql
ALTER TABLE table_name
MODIFY column_name new_datatype;
```

---

## Example 1

Current column

```sql
Name VARCHAR(30)
```

Increase its size.

```sql
ALTER TABLE Student
MODIFY Name VARCHAR(100);
```

---

## Example 2

Change Mobile size

```sql
ALTER TABLE Student
MODIFY Mobile VARCHAR(20);
```

---

## Example 3

Increase Address size

```sql
ALTER TABLE Student
MODIFY Address VARCHAR(300);
```

---

# 3️⃣ ALTER TABLE CHANGE COLUMN

## What is CHANGE?

The **CHANGE** command is mainly used in MySQL.

It allows you to:

- Rename a column
- Change its datatype

Both can be done together.

---

## Syntax

```sql
ALTER TABLE table_name
CHANGE old_column new_column datatype;
```

---

## Example 1

Rename Name to FullName.

```sql
ALTER TABLE Student
CHANGE Name FullName VARCHAR(100);
```

---

## Before

|StudentID|Name|Age|

## After

|StudentID|FullName|Age|

---

## Example 2

Rename Mobile to PhoneNumber

```sql
ALTER TABLE Student
CHANGE Mobile PhoneNumber VARCHAR(15);
```

---

# 4️⃣ ALTER TABLE DROP COLUMN

## What is DROP COLUMN?

DROP COLUMN permanently removes a column from the table.

⚠ Once removed, the column and its data cannot be recovered.

---

## Syntax

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

---

## Example

```sql
ALTER TABLE Student
DROP COLUMN Address;
```

---

### Before

|StudentID|Name|Age|Address|

---

### After

|StudentID|Name|Age|

---

## Example 2

```sql
ALTER TABLE Student
DROP COLUMN Gender;
```

---

# 5️⃣ ALTER TABLE ADD CONSTRAINT

Constraints help maintain data integrity.

Common constraints are

- PRIMARY KEY
- FOREIGN KEY
- UNIQUE
- CHECK
- DEFAULT

---

## Syntax

```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name
constraint_type(column_name);
```

---

## Example

```sql
ALTER TABLE Student
ADD CONSTRAINT PK_Student
PRIMARY KEY(StudentID);
```

---

# 6️⃣ ALTER TABLE DROP CONSTRAINT

Used to remove an existing constraint.

---

## Syntax

```sql
ALTER TABLE table_name
DROP CONSTRAINT constraint_name;
```

Example

```sql
ALTER TABLE Student
DROP CONSTRAINT PK_Student;
```

---

# Real-Life Example

Imagine a school database.

Initially

```sql
CREATE TABLE Student(
StudentID INT,
Name VARCHAR(50)
);
```

Later school requirements change.

Step 1

Add Email

```sql
ALTER TABLE Student
ADD Email VARCHAR(100);
```

Step 2

Increase Name size

```sql
ALTER TABLE Student
MODIFY Name VARCHAR(100);
```

Step 3

Rename Name

```sql
ALTER TABLE Student
CHANGE Name FullName VARCHAR(100);
```

Step 4

Remove Email

```sql
ALTER TABLE Student
DROP COLUMN Email;
```

---

# Complete Example

```sql
CREATE TABLE Student(
StudentID INT,
Name VARCHAR(50),
Age INT
);

ALTER TABLE Student
ADD Email VARCHAR(100);

ALTER TABLE Student
ADD Mobile VARCHAR(15);

ALTER TABLE Student
MODIFY Name VARCHAR(100);

ALTER TABLE Student
CHANGE Mobile PhoneNumber VARCHAR(20);

ALTER TABLE Student
DROP COLUMN Age;
```

---

# ALTER TABLE Summary

|Command|Purpose|
|--------|--------|
|ADD|Add new column|
|MODIFY|Change datatype or size|
|CHANGE|Rename column and datatype|
|DROP COLUMN|Delete a column|
|ADD CONSTRAINT|Add constraint|
|DROP CONSTRAINT|Remove constraint|

---

# ALTER TABLE vs UPDATE

|ALTER TABLE|UPDATE|
|------------|------|
|Changes table structure|Changes table data|
|DDL Command|DML Command|
|Auto Commit|Can Rollback (depending on transaction)|
|No WHERE clause|Uses WHERE clause|

---

# Interview Questions

### Q1. What is ALTER TABLE?

It is a DDL command used to modify the structure of an existing table.

---

### Q2. Does ALTER TABLE delete existing data?

No. It changes only the table structure unless a column is dropped.

---

### Q3. Which command adds a new column?

```sql
ALTER TABLE Student
ADD Email VARCHAR(100);
```

---

### Q4. Which command changes the datatype?

```sql
ALTER TABLE Student
MODIFY Name VARCHAR(100);
```

---

### Q5. Which command removes a column?

```sql
ALTER TABLE Student
DROP COLUMN Address;
```

---

# Common Errors

❌ Wrong

```sql
ALTER Student
ADD Age INT;
```

✅ Correct

```sql
ALTER TABLE Student
ADD Age INT;
```

---

❌ Wrong

```sql
ALTER TABLE Student
ADD;
```

✅ Correct

```sql
ALTER TABLE Student
ADD Email VARCHAR(100);
```

---

# Key Points

- ALTER TABLE is a DDL command.
- Used to modify an existing table.
- Data remains safe while adding or modifying columns.
- DROP COLUMN permanently deletes a column.
- MODIFY changes datatype or size.
- CHANGE renames a column and can also change its datatype.
- Frequently asked in DBMS practical exams and interviews.

---

# Practice Questions

1. Create a Student table.
2. Add a Phone column.
3. Add an Address column.
4. Increase the size of Name to VARCHAR(100).
5. Rename Name to FullName.
6. Drop the Address column.
7. Add a PRIMARY KEY.
8. Drop the PRIMARY KEY.

---

# Conclusion

The **ALTER TABLE** command is one of the most important SQL DDL commands. It allows developers to change the structure of an existing table without recreating it. Learning all ALTER operations—such as **ADD**, **MODIFY**, **CHANGE**, **DROP COLUMN**, and **Constraints**—is essential for database management, practical labs, and technical interviews.

# 📘 DBMS Lab - RENAME Command

<p align="center">
  <img src="https://img.shields.io/badge/DBMS-RENAME-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/SQL-DDL_Command-green?style=for-the-badge">
  <img src="https://img.shields.io/badge/Level-Beginner-orange?style=for-the-badge">
</p>

---

# 📖 Introduction

The **RENAME** command is a **Data Definition Language (DDL)** command used to change the name of an existing **table** or **column** without affecting the data stored in it.

The RENAME operation only changes the name. The structure and records inside the table remain the same.

---

# 🎯 Why Do We Use RENAME?

Sometimes while designing a database, we may give a table or column an incorrect or unclear name.

For example:

- `Stud` → `Student`
- `Name` → `FullName`
- `Mob` → `MobileNumber`

Instead of creating a new table, we simply rename the existing one.

---

# 📌 Types of Rename

There are two common rename operations.

1. Rename Table
2. Rename Column

---

# Sample Table

```sql
CREATE TABLE Student(
    StudentID INT,
    Name VARCHAR(50),
    Age INT
);
```

Current Table

| StudentID | Name | Age |
|-----------|------|-----|
|101|Rahul|20|
|102|Priya|19|
|103|Amit|21|

---

# 1️⃣ Rename Table

## What is Rename Table?

Rename Table changes the name of an existing table.

Only the table name changes.

The data inside the table remains unchanged.

---

## Syntax (MySQL)

```sql
RENAME TABLE old_table_name
TO new_table_name;
```

---

## Example 1

Rename Student to Students.

```sql
RENAME TABLE Student
TO Students;
```

---

### Before

```
Student
```

### After

```
Students
```

The records inside the table remain exactly the same.

---

## Example 2

Rename Employee to Staff.

```sql
RENAME TABLE Employee
TO Staff;
```

---

## Example 3

Rename Product to Products.

```sql
RENAME TABLE Product
TO Products;
```

---

# Alternative Syntax (SQL Server / PostgreSQL)

Some databases use ALTER TABLE.

```sql
ALTER TABLE Student
RENAME TO Students;
```

---

# 2️⃣ Rename Column

## What is Rename Column?

Rename Column changes the name of a column.

The data inside the column is not deleted.

Only the column name changes.

---

## Syntax (MySQL)

```sql
ALTER TABLE table_name
CHANGE old_column_name
new_column_name datatype;
```

Notice that MySQL requires the datatype while renaming.

---

## Example

Rename Name to FullName.

```sql
ALTER TABLE Student
CHANGE Name FullName VARCHAR(50);
```

---

### Before

|StudentID|Name|Age|

---

### After

|StudentID|FullName|Age|

---

## Example 2

Rename Age to StudentAge.

```sql
ALTER TABLE Student
CHANGE Age StudentAge INT;
```

---

## Example 3

Rename Mobile to PhoneNumber.

```sql
ALTER TABLE Student
CHANGE Mobile PhoneNumber VARCHAR(15);
```

---

# Rename Column (SQL Server)

SQL Server uses

```sql
EXEC sp_rename
'Student.Name',
'FullName',
'COLUMN';
```

---

# Rename Column (PostgreSQL)

```sql
ALTER TABLE Student
RENAME COLUMN Name
TO FullName;
```

---

# Complete Example

Create Table

```sql
CREATE TABLE Student(
StudentID INT,
Name VARCHAR(50),
Age INT
);
```

Rename Table

```sql
RENAME TABLE Student
TO Students;
```

Rename Column

```sql
ALTER TABLE Students
CHANGE Name FullName VARCHAR(50);
```

Rename Age

```sql
ALTER TABLE Students
CHANGE Age StudentAge INT;
```

---

# Before and After

### Before

|StudentID|Name|Age|
|----------|----|---|
|101|Rahul|20|

---

### After

|StudentID|FullName|StudentAge|
|----------|---------|----------|
|101|Rahul|20|

---

# Real-Life Example

Suppose a college database contains

```sql
Student
```

Later the college decides to store both school and college students.

So the table name is changed.

```sql
RENAME TABLE Student
TO Students;
```

Later the administrator wants a more descriptive column name.

```sql
ALTER TABLE Students
CHANGE Name FullName VARCHAR(50);
```

Now the database is easier to understand.

---

# Difference Between Rename Table and Rename Column

|Rename Table|Rename Column|
|-------------|-------------|
|Changes table name|Changes column name|
|Table remains the same|Column data remains the same|
|Uses RENAME TABLE|Uses ALTER TABLE|

---

# RENAME vs ALTER

|RENAME|ALTER|
|------|------|
|Changes only the name|Changes table structure|
|Can rename table or column|Can add, modify, drop, rename|
|Does not affect data|Does not affect data unless dropping columns|

---

# Common Errors

## Wrong

```sql
RENAME Student TO Students;
```

## Correct

```sql
RENAME TABLE Student
TO Students;
```

---

## Wrong

```sql
ALTER TABLE Student
CHANGE Name FullName;
```

Datatype is missing.

---

## Correct

```sql
ALTER TABLE Student
CHANGE Name FullName VARCHAR(50);
```

---

# Interview Questions

### Q1. What is the RENAME command?

It is a DDL command used to change the name of a table or column.

---

### Q2. Does RENAME delete data?

No.

Only the name changes.

---

### Q3. Which command renames a table?

```sql
RENAME TABLE Student
TO Students;
```

---

### Q4. Which command renames a column in MySQL?

```sql
ALTER TABLE Student
CHANGE Name FullName VARCHAR(50);
```

---

### Q5. Which command renames a column in PostgreSQL?

```sql
ALTER TABLE Student
RENAME COLUMN Name
TO FullName;
```

---

# Practice Questions

1. Create a Student table.
2. Rename Student to Students.
3. Rename Name to FullName.
4. Rename Age to StudentAge.
5. Rename Employee to Staff.
6. Rename Product to Products.
7. Rename Mobile to PhoneNumber.

---

# Summary

|Command|Purpose|
|--------|--------|
|RENAME TABLE|Rename an existing table|
|ALTER TABLE CHANGE|Rename a column in MySQL|
|ALTER TABLE RENAME COLUMN|Rename a column in PostgreSQL|
|EXEC sp_rename|Rename a column in SQL Server|

---

# Key Points

- RENAME is a **DDL command**.
- It changes only the **name**, not the data.
- Tables and columns can both be renamed.
- In **MySQL**, use `CHANGE` to rename a column (datatype must be specified).
- In **PostgreSQL**, use `RENAME COLUMN`.
- In **SQL Server**, use `sp_rename`.
- Renaming improves database readability and maintainability.

---

# Conclusion

The **RENAME** command helps developers change the names of tables and columns without recreating them or losing data. It is commonly used when database requirements change or when better naming conventions are adopted. Understanding table and column renaming is an essential DBMS concept for practical exams, projects, and interviews.

# 📘 DBMS Lab - DELETE, TRUNCATE & DROP

<p align="center">
  <img src="https://img.shields.io/badge/DBMS-DDL%20%26%20DML-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/SQL-Commands-green?style=for-the-badge">
</p>

---

# 📖 Introduction

SQL provides different commands to remove data or database objects. The three most commonly used commands are:

- DELETE
- TRUNCATE
- DROP

Although all three remove something, they work differently.

---

# 1️⃣ DELETE Command

## What is DELETE?

The **DELETE** command removes one or more rows from a table.

It is a **DML (Data Manipulation Language)** command because it modifies the data stored in the table, not the table structure.

---

## Syntax

Delete specific rows

```sql
DELETE FROM table_name
WHERE condition;
```

Delete all rows

```sql
DELETE FROM table_name;
```

---

## Example

Delete the student whose ID is 101.

```sql
DELETE FROM Student
WHERE StudentID = 101;
```

Delete all records.

```sql
DELETE FROM Student;
```

---

## Key Points

- Removes data only.
- Table structure remains unchanged.
- WHERE clause can delete selected rows.
- Can be rolled back (before COMMIT).
- AUTO_INCREMENT value is generally not reset.

---

# 2️⃣ TRUNCATE Command

## What is TRUNCATE?

The **TRUNCATE** command removes **all rows** from a table at once.

It is a **DDL (Data Definition Language)** command.

The table structure remains, but all records are deleted.

---

## Syntax

```sql
TRUNCATE TABLE table_name;
```

---

## Example

```sql
TRUNCATE TABLE Student;
```

---

## Key Points

- Deletes all rows.
- WHERE clause is not allowed.
- Faster than DELETE.
- Usually cannot be rolled back.
- Resets AUTO_INCREMENT in MySQL.

---

# 3️⃣ DROP Command

## What is DROP?

The **DROP** command permanently removes the entire database object.

It deletes:

- Table
- Structure
- Data
- Constraints
- Indexes

Everything is removed permanently.

It is a **DDL command**.

---

## Syntax

Drop Table

```sql
DROP TABLE table_name;
```

Drop Database

```sql
DROP DATABASE database_name;
```

---

## Example

```sql
DROP TABLE Student;
```

---

## Key Points

- Deletes table completely.
- Table no longer exists.
- Structure and data are removed.
- Cannot be recovered easily.

---

# Real-Life Example

Suppose a table contains:

|ID|Name|
|--|----|
|1|Rahul|
|2|Priya|
|3|Amit|

### DELETE

```sql
DELETE FROM Student
WHERE ID=2;
```

Result

|ID|Name|
|--|----|
|1|Rahul|
|3|Amit|

---

### TRUNCATE

```sql
TRUNCATE TABLE Student;
```

Result

Table exists, but contains **0 rows**.

---

### DROP

```sql
DROP TABLE Student;
```

Result

The **Student** table is completely removed from the database.

---

# DELETE vs TRUNCATE vs DROP

|Feature|DELETE|TRUNCATE|DROP|
|--------|-------|---------|-----|
|Command Type|DML|DDL|DDL|
|Removes|Selected or all rows|All rows|Entire table|
|WHERE Clause|✅ Yes|❌ No|❌ No|
|Table Structure|Remains|Remains|Deleted|
|Data Removed|Yes|Yes|Yes|
|Table Exists After Command|✅ Yes|✅ Yes|❌ No|
|Can Rollback|✅ Yes (before COMMIT)|❌ Usually No|❌ No|
|AUTO_INCREMENT Reset|❌ No|✅ Yes (MySQL)|N/A|
|Speed|Slowest|Faster|Fastest|

---

# When to Use

### Use DELETE

- Remove specific records.
- Keep remaining data.

### Use TRUNCATE

- Remove all records quickly.
- Keep the table structure.

### Use DROP

- Remove the table permanently.
- Table is no longer needed.

---

# Interview Questions

### Q1. Which command deletes selected rows?

**Answer:** DELETE

---

### Q2. Which command deletes all rows but keeps the table?

**Answer:** TRUNCATE

---

### Q3. Which command deletes the entire table?

**Answer:** DROP

---

### Q4. Which command supports the WHERE clause?

**Answer:** DELETE

---

### Q5. Which command is fastest?

**Answer:** DROP (removes the object) and TRUNCATE (for clearing all rows) are much faster than DELETE.

---

# Summary

|Command|Purpose|
|--------|--------|
|DELETE|Delete selected or all rows|
|TRUNCATE|Delete all rows, keep table|
|DROP|Delete the entire table|

---

# Key Takeaways

- **DELETE** removes data and supports the `WHERE` clause.
- **TRUNCATE** removes all rows quickly but keeps the table.
- **DROP** removes both the table and its data permanently.
- Choose the command based on whether you want to delete **rows**, **all data**, or the **entire table**.

---

⭐ **If this README helped you, consider giving the repository a Star!**
