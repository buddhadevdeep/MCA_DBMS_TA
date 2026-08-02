# 📘 DBMS Lab - SELECT INTO (Data Copy)

<p align="center">
  <img src="https://img.shields.io/badge/DBMS-SELECT_INTO-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/SQL-Data_Copy-green?style=for-the-badge">
  <img src="https://img.shields.io/badge/DDL%20%26%20DML-Lab-orange?style=for-the-badge">
</p>

---

# 📖 Introduction

The **SELECT INTO** statement is used to **create a new table** and **copy data** from an existing table into it.

The new table is created automatically with the selected columns and copied records.

It is commonly used for:

- Creating backup tables
- Copying selected records
- Copying specific columns
- Creating temporary tables
- Filtering records into another table

---

# What is SELECT INTO?

`SELECT INTO` creates a **new table** and inserts data into it in a single statement.

Unlike **INSERT INTO**, the destination table **does not need to exist**.

---

# Syntax

## Copy All Columns

```sql
SELECT *
INTO new_table
FROM old_table;
```

---

## Copy Selected Columns

```sql
SELECT column1, column2
INTO new_table
FROM old_table;
```

---

## Copy Records Using Condition

```sql
SELECT *
INTO new_table
FROM old_table
WHERE condition;
```

---

# Sample Table

## Student

|STDID|SNAME|CITY|BRANCH|SPI|
|------|------|------|---------|----|
|101|Rahul|Ahmedabad|Computer|8.5|
|102|Priya|Rajkot|Civil|9.2|
|103|Amit|Surat|Computer|8.9|
|104|Neha|Rajkot|Mechanical|7.8|

---

# Example 1 - Copy Entire Table

```sql
SELECT *
INTO Student_Backup
FROM Student;
```

### Result

A new table **Student_Backup** is created containing all records.

---

# Example 2 - Copy Selected Columns

```sql
SELECT SNAME, CITY
INTO Student_Address
FROM Student;
```

Only **SNAME** and **CITY** columns are copied.

---

# Example 3 - Copy Using WHERE

```sql
SELECT *
INTO Computer_Students
FROM Student
WHERE BRANCH='Computer';
```

Only Computer branch students are copied.

---

# Example 4 - Copy Distinct Values

```sql
SELECT DISTINCT CITY
INTO City_List
FROM Student;
```

Duplicate cities are removed.

---

# Example 5 - Copy Top Records

```sql
SELECT TOP 3 *
INTO Topper_List
FROM Student
ORDER BY SPI DESC;
```

Copies top three students.

---

# Example 6 - Copy Without Data

Create only table structure.

```sql
SELECT *
INTO Student_Backup
FROM Student
WHERE 1=0;
```

Result

- Table is created
- No records copied

---

# Example 7 - Rename Column While Copying

```sql
SELECT
STDID,
SNAME,
SPI AS Percentage
INTO Student_Result
FROM Student;
```

New table column name becomes

```
Percentage
```

instead of

```
SPI
```

---

# Example 8 - Copy Between Range

```sql
SELECT *
INTO Mid_Students
FROM Student
WHERE STDID BETWEEN 103 AND 108;
```

---

# Common Clauses Used with SELECT INTO

|Clause|Purpose|
|--------|--------|
|WHERE|Copy selected rows|
|DISTINCT|Remove duplicate values|
|TOP|Copy limited records|
|ORDER BY|Sort records (used with TOP)|
|AS|Rename column|

---

# Real-Life Example

Suppose a company has an **Employee** table.

Before making major updates, the administrator creates a backup.

```sql
SELECT *
INTO Employee_Backup
FROM Employee;
```

Now all employee records are safely copied.

---

# SELECT INTO vs INSERT INTO

|SELECT INTO|INSERT INTO|
|-------------|------------|
|Creates new table|Uses existing table|
|Copies structure and data|Copies only data|
|Destination table must not exist|Destination table must exist|
|Used for backup|Used to insert records|

---

# Advantages

- Creates table automatically
- Easy backup
- Faster than creating table manually
- Copies selected columns
- Copies filtered records
- Supports DISTINCT and TOP

---

# Limitations

- Cannot copy into an existing table.
- Constraints like Primary Key and Foreign Key are not copied automatically.
- Indexes and triggers are not copied.

---

# Common Errors

### Wrong

```sql
SELECT *
INTO Student
FROM Student;
```

Table already exists.

---

### Correct

```sql
SELECT *
INTO Student_Backup
FROM Student;
```

---

### Wrong

```sql
SELECT
INTO Backup
FROM Student;
```

Columns are missing.

---

### Correct

```sql
SELECT *
INTO Backup
FROM Student;
```

---

# Interview Questions

### 1. What is SELECT INTO?

It creates a new table and copies data from another table.

---

### 2. Does SELECT INTO create a new table?

Yes.

---

### 3. Can SELECT INTO copy selected columns?

Yes.

---

### 4. Can WHERE be used with SELECT INTO?

Yes.

---

### 5. What is the difference between SELECT INTO and INSERT INTO?

SELECT INTO creates a new table, whereas INSERT INTO inserts data into an existing table.

---

# Summary

|Operation|Example|
|----------|--------|
|Copy Entire Table|`SELECT * INTO Backup FROM Student;`|
|Copy Selected Columns|`SELECT Name, City INTO Student_Address FROM Student;`|
|Copy Using WHERE|`SELECT * INTO CS_Students FROM Student WHERE Branch='Computer';`|
|Copy Distinct Values|`SELECT DISTINCT City INTO City_List FROM Student;`|
|Copy Top Records|`SELECT TOP 5 * INTO Topper FROM Student;`|
|Copy Without Data|`SELECT * INTO Student_Backup FROM Student WHERE 1=0;`|
|Rename Column|`SELECT SPI AS Percentage INTO Result FROM Student;`|

---

# Practice Questions

1. Create a backup of the Student table.
2. Copy only Name and City into Student_Address.
3. Copy Computer branch students.
4. Copy the top 5 students based on SPI.
5. Copy all distinct cities.
6. Create an empty backup table.
7. Rename SPI as Percentage while copying.
8. Copy students whose IDs are between 103 and 108.

---

# Key Takeaways

- **SELECT INTO** creates a **new table** and copies data.
- It is widely used for **backup** and **data migration**.
- It supports **WHERE**, **DISTINCT**, **TOP**, and **AS**.
- The destination table **must not already exist**.
- Constraints and indexes are **not copied automatically**.

---

# Conclusion

The **SELECT INTO** statement is one of the easiest ways to create a new table from an existing one. It is useful for backups, filtering records, creating reports, and copying selected data without manually creating the destination table. Mastering **SELECT INTO** is essential for DBMS practicals, projects, and interviews.

⭐ If this README helped you, consider giving the repository a **Star**!
