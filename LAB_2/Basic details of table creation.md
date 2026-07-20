# MS SQL Server - Table Creation Guide

# Table of Contents

1. What is a Table?
2. Rows and Columns
3. Data Types
4. Constraints
5. CREATE TABLE Syntax
6. Create a Table
7. Explanation of Each Column
8. View Table Structure
9. Insert Data (3 Methods)
10. View Data
11. Summary

---

# 1. What is a Table?

A **Table** is the basic object in SQL Server used to store data.

Data is organized into **Rows** and **Columns**, similar to an Excel spreadsheet.

Example

| StudentID | FirstName | LastName | Age | City |
|-----------|-----------|----------|-----|------|
| 1 | Rahul | Sharma | 20 | Mumbai |
| 2 | Priya | Patel | 21 | Ahmedabad |

Each table stores information about one type of entity.

Examples

- Students
- Employees
- Products
- Customers
- Orders

---

# 2. Rows and Columns

## Column

A **Column** defines what type of information will be stored.

Example

| StudentID | FirstName | LastName | Age | City |

Columns are

- StudentID
- FirstName
- LastName
- Age
- City

Each column has

- Name
- Data Type
- Size
- Constraints (Optional)

---

## Row

A **Row** represents one complete record.

Example

| StudentID | FirstName | LastName | Age | City |
|-----------|-----------|----------|-----|------|
| 1 | Rahul | Sharma | 20 | Mumbai |

This entire line is one row.

If the table has 100 students, then it contains 100 rows.

---

# 3. SQL Server Data Types

Each column must have a data type.

| Data Type | Description | Example |
|-----------|-------------|----------|
| INT | Whole numbers | 100 |
| BIGINT | Large whole numbers | 999999999 |
| DECIMAL(10,2) | Decimal numbers | 2500.75 |
| FLOAT | Floating point numbers | 45.87 |
| CHAR(10) | Fixed-length text | ABC |
| VARCHAR(50) | Variable-length text | Rahul |
| NVARCHAR(50) | Unicode text | भारत |
| DATE | Date only | 2026-07-20 |
| TIME | Time only | 10:30:00 |
| DATETIME | Date and time | 2026-07-20 10:30:00 |
| BIT | Boolean value | 1 or 0 |

---

# CHAR vs VARCHAR in DBMS

## Definition

### CHAR
- `CHAR` (Character) is a **fixed-length** data type.
- It always stores the specified number of characters.
- If the entered value is shorter, the remaining space is filled with blank spaces.

### VARCHAR
- `VARCHAR` (Variable Character) is a **variable-length** data type.
- It stores only the actual characters entered along with a small amount of extra space (1–2 bytes) to store the length.
- No blank spaces are added.

---

# Difference Between CHAR and VARCHAR

| Feature | CHAR | VARCHAR |
|---------|------|----------|
| Full Form | Character | Variable Character |
| Length | Fixed | Variable |
| Storage | Always reserves full size | Uses only required size |
| Extra Storage | No | Uses 1–2 bytes to store length |
| Padding | Adds blank spaces | No padding |
| Speed | Slightly faster | Slightly slower |
| Memory Usage | More | Less |
| Best For | Fixed-size data | Variable-size data |

---

# Example

```sql
CREATE TABLE Student (
    RollNo CHAR(5),
    Name VARCHAR(50)
);
```

Insert data:

```sql
INSERT INTO Student VALUES ('12', 'Rahul');
```

### Stored Data

**CHAR(5)**

```
'12   '
```

(3 spaces are automatically added)

**VARCHAR(50)**

```
'Rahul'
```

(Only actual characters are stored)

---

# Advantages of CHAR

- Faster retrieval for fixed-length data.
- Simple storage management.
- Good performance when all values have the same length.
- Predictable memory allocation.

## Disadvantages of CHAR

- Wastes storage space for short values.
- Blank spaces are added automatically.
- Not suitable for variable-length text.

---

# Advantages of VARCHAR

- Saves storage space.
- Stores only actual data.
- Ideal for variable-length values.
- Efficient for large text fields where lengths differ.

## Disadvantages of VARCHAR

- Slightly slower than `CHAR` because the database manages variable lengths.
- Uses 1–2 extra bytes to store the string length.
- Memory allocation is less predictable.

---

# Applications of CHAR

Use `CHAR` when data has a **fixed length**, such as:

- Gender (`M`, `F`)
- Country Code (`IN`, `US`)
- PAN Number (`ABCDE1234F`)
- Aadhaar Number (`123456789012`)
- PIN Code (if stored as text)
- Employee Code
- Blood Group
- Yes/No values (`Y`, `N`)

Example:

```sql
Gender CHAR(1),
CountryCode CHAR(2),
PAN CHAR(10)
```

---

# Applications of VARCHAR

Use `VARCHAR` when data length **varies**, such as:

- Name
- Email
- Address
- City
- Phone Number
- Product Name
- Description
- Comments
- Username

Example:

```sql
Name VARCHAR(100),
Email VARCHAR(255),
Address VARCHAR(500)
```

---

# Real-World Example

```sql
CREATE TABLE Employee
(
    EmployeeID INT PRIMARY KEY,
    EmployeeCode CHAR(6),
    Gender CHAR(1),
    CountryCode CHAR(2),
    Name VARCHAR(100),
    Email VARCHAR(255),
    Address VARCHAR(500),
    Department VARCHAR(50)
);
```

---

# Summary

| CHAR | VARCHAR |
|------|----------|
| Fixed-length data type | Variable-length data type |
| May waste storage | Saves storage |
| Faster for fixed-size data | Flexible for different lengths |
| Pads with spaces | No padding |
| Best for IDs, codes, gender | Best for names, emails, addresses |

## Quick Rule

- ✅ Use **CHAR** for **fixed-length** values.
- ✅ Use **VARCHAR** for **variable-length** text.

# 4. Constraints

Constraints define rules for the data stored in a table.

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | Uniquely identifies each row |
| NOT NULL | Value cannot be empty |
| UNIQUE | Duplicate values are not allowed |
| DEFAULT | Assigns a default value if none is provided |
| CHECK | Restricts values based on a condition |
| FOREIGN KEY | Creates a relationship with another table |

Example

```sql
StudentID INT PRIMARY KEY
```

```sql
FirstName VARCHAR(50) NOT NULL
```

```sql
Age INT CHECK (Age >= 18)
```

---

# 5. CREATE TABLE Syntax

```sql
CREATE TABLE TableName
(
    ColumnName DataType Constraint,
    ColumnName DataType Constraint,
    ColumnName DataType Constraint
);
```

General Format

```sql
CREATE TABLE Employees
(
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    Salary DECIMAL(10,2)
);
```

---

# 6. Create a Table

```sql
CREATE TABLE Students
(
    StudentID INT PRIMARY KEY,
    FirstName VARCHAR(50) NOT NULL,
    LastName VARCHAR(50),
    Age INT,
    City VARCHAR(50)
);
```

---

# 7. Explanation of Each Column

```sql
StudentID INT PRIMARY KEY
```

- Column Name: StudentID
- Data Type: INT
- Constraint: PRIMARY KEY
- Stores a unique ID for every student.

---

```sql
FirstName VARCHAR(50) NOT NULL
```

- Stores student's first name.
- Maximum 50 characters.
- Cannot be empty.

---

```sql
LastName VARCHAR(50)
```

- Stores student's last name.
- Maximum 50 characters.
- NULL values are allowed.

---

```sql
Age INT
```

- Stores age.
- Accepts whole numbers only.

---

```sql
City VARCHAR(50)
```

- Stores city name.
- Maximum 50 characters.

---

# 8. View Table Structure

To see information about the table:

```sql
EXEC sp_help Students;
```

Or

```sql
sp_help Students;
```

---

# 9. Insert Data

## Method 1 — Insert Without Column Names

```sql
INSERT INTO Students
VALUES
(
    1,
    'Rahul',
    'Sharma',
    20,
    'Mumbai'
);
```

**Note:** Values must be in the exact same order as the columns were defined in the table.

---

## Method 2 — Insert With Column Names (Recommended)

```sql
INSERT INTO Students
(
    StudentID,
    FirstName,
    LastName,
    Age,
    City
)
VALUES
(
    2,
    'Priya',
    'Patel',
    21,
    'Ahmedabad'
);
```

### Advantages

- Easier to read
- Safer
- Column order can be changed
- Best practice

---

## Method 3 — Insert Multiple Rows

```sql
INSERT INTO Students
(
    StudentID,
    FirstName,
    LastName,
    Age,
    City
)
VALUES
(3,'Amit','Shah',23,'Delhi'),
(4,'Sneha','Joshi',20,'Pune'),
(5,'Neha','Patel',21,'Rajkot');
```

This inserts multiple records with a single query.

## Method 4 — Insert Multiple Rows without columns

```sql
INSERT INTO TableName
VALUES
(3,'Amit','Shah',23,'Delhi'),
(4,'Sneha','Joshi',20,'Pune'),
(5,'Neha','Patel',21,'Rajkot');
```

This inserts multiple records with a single query.

---

# 10. View Data

Display all rows and columns.

```sql
SELECT * FROM Students;
```

Display selected columns only.

```sql
SELECT
StudentID,
FirstName,
City
FROM Students;
```

---

# Summary

- A **Table** stores related data in SQL Server.
- A **Column** defines the type of information to store.
- A **Row** represents one complete record.
- Every column must have a **Data Type**.
- **Constraints** enforce rules on the data.
- `CREATE TABLE` is used to create a new table.
- Data can be inserted in **three ways**:
  1. Without column names
  2. With column names (recommended)
  3. Multiple rows in a single query
- `SELECT` is used to retrieve data from a table.
