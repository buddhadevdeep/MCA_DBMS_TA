# Lab – SQL JOINs in MS SQL Server

## 📌 Introduction

A **JOIN** is used to combine data from two or more tables based on a related column.

For example, suppose we have two tables:

### Student

| RNO | NAME | BRANCH |
|---:|---|---|
| 101 | RAJU | CE |
| 102 | AMIT | CE |
| 103 | SANIYA | ME |
| 104 | NEHA | EC |

### Result

| RESULTID | RNO | SPI |
|---:|---:|---:|
| 1 | 101 | 8.8 |
| 2 | 102 | 9.2 |
| 3 | 103 | 7.6 |
| 5 | 105 | 8.5 |

Here, `RNO` is the common column.

```text
Student.RNO  ←→  Result.RNO
```

JOIN allows us to combine information from these tables.

---

# 1. INNER JOIN

`INNER JOIN` returns only the records that have a match in **both tables**.

### Syntax

```sql
SELECT columns
FROM Table1
INNER JOIN Table2
    ON Table1.column = Table2.column;
```

### Example

```sql
SELECT
    Student.RNO,
    Student.NAME,
    Student.BRANCH,
    Result.SPI
FROM Student
INNER JOIN Result
    ON Student.RNO = Result.RNO;
```

### Flow

```text
Student
   |
   | Match RNO
   ↓
Result
   |
   ↓
Only matching records
```

If `RNO = 101` exists in both tables, it is displayed.

If a record exists only in one table, it is not displayed.

### Remember

```text
INNER JOIN
→ Matching records from both tables
```

---

# 2. LEFT JOIN

`LEFT JOIN` returns:

- All records from the **left table**
- Matching records from the right table
- If there is no match, right-side columns become `NULL`

### Syntax

```sql
SELECT columns
FROM Table1
LEFT JOIN Table2
    ON Table1.column = Table2.column;
```

### Example

```sql
SELECT
    Student.RNO,
    Student.NAME,
    Result.SPI
FROM Student
LEFT JOIN Result
    ON Student.RNO = Result.RNO;
```

### Flow

```text
LEFT TABLE
   ↓
All records are kept
   ↓
Check matching records
   ↓
Match → Show data
No Match → NULL
```

### Remember

```text
LEFT JOIN
→ Everything from LEFT table
→ Matching data from RIGHT table
```

---

# 3. RIGHT JOIN

`RIGHT JOIN` is the opposite of `LEFT JOIN`.

It returns:

- All records from the **right table**
- Matching records from the left table
- If there is no match, left-side columns become `NULL`

### Syntax

```sql
SELECT columns
FROM Table1
RIGHT JOIN Table2
    ON Table1.column = Table2.column;
```

### Example

```sql
SELECT
    Student.RNO,
    Student.NAME,
    Result.SPI
FROM Student
RIGHT JOIN Result
    ON Student.RNO = Result.RNO;
```

### Flow

```text
RIGHT TABLE
   ↓
All records are kept
   ↓
Check matching records
   ↓
Match → Show data
No Match → NULL
```

### Remember

```text
RIGHT JOIN
→ Everything from RIGHT table
→ Matching data from LEFT table
```

---

# 4. FULL OUTER JOIN

`FULL OUTER JOIN` returns **all records from both tables**.

It includes:

- Matching records
- Unmatched records from left table
- Unmatched records from right table

Unmatched columns contain `NULL`.

### Syntax

```sql
SELECT columns
FROM Table1
FULL OUTER JOIN Table2
    ON Table1.column = Table2.column;
```

### Example

```sql
SELECT
    Student.RNO,
    Student.NAME,
    Result.SPI
FROM Student
FULL OUTER JOIN Result
    ON Student.RNO = Result.RNO;
```

### Flow

```text
        Student
       /       \
   Matching   Unmatched
       \       /
        Result
           |
           ↓
      Everything
```

### Remember

```text
FULL JOIN
→ Everything from LEFT + Everything from RIGHT
```

---

# 5. CROSS JOIN

`CROSS JOIN` creates a **Cartesian Product**.

Every row of the first table is combined with every row of the second table.

### Syntax

```sql
SELECT *
FROM Student
CROSS JOIN Result;
```

If:

```text
Student = 4 rows
Result  = 4 rows
```

Then:

```text
4 × 4 = 16 rows
```

### Important

`CROSS JOIN` does not require an `ON` condition.

```sql
SELECT *
FROM Student
CROSS JOIN Result;
```

### Remember

```text
CROSS JOIN
→ Every row × Every row
```

---

# 6. JOIN Comparison

Assume:

```text
Student = Left Table
Result  = Right Table
```

| JOIN | What it returns |
|---|---|
| `INNER JOIN` | Matching records only |
| `LEFT JOIN` | All left + matching right |
| `RIGHT JOIN` | All right + matching left |
| `FULL OUTER JOIN` | All records from both tables |
| `CROSS JOIN` | Every possible combination |

---

# 7. Easy JOIN Diagram

```text
INNER JOIN

    LEFT       RIGHT
      \         /
       \       /
        MATCH
         ↓
      Result
```


```text
LEFT JOIN

    LEFT
   █████
   █████ ← All kept
      \
       MATCH
        |
      RIGHT
```

```text
RIGHT JOIN

     LEFT
       \
      MATCH
        |
    ███████
    RIGHT
    ███████ ← All kept
```

```text
FULL JOIN

    LEFT          RIGHT
   ███████        ███████
      \             /
       \           /
        \         /
         ALL
          ↓
       Result
```

```text
CROSS JOIN

A1 ── B1
A1 ── B2
A1 ── B3

A2 ── B1
A2 ── B2
A2 ── B3

A3 ── B1
A3 ── B2
A3 ── B3
```

---

# 8. JOIN with WHERE

After joining tables, we can filter the result using `WHERE`.

### Example

Display students whose branch is `CE`:

```sql
SELECT
    Student.RNO,
    Student.NAME,
    Student.BRANCH,
    Result.SPI
FROM Student
INNER JOIN Result
    ON Student.RNO = Result.RNO
WHERE Student.BRANCH = 'CE';
```

### Flow

```text
Student + Result
       ↓
     JOIN
       ↓
   Matching rows
       ↓
     WHERE
       ↓
   Filter rows
       ↓
    Final Result
```

---

# 9. JOIN with Aggregate Functions

JOIN can also be combined with:

- `COUNT()`
- `SUM()`
- `AVG()`
- `MAX()`
- `MIN()`

Example:

```sql
SELECT
    Student.BRANCH,
    AVG(Result.SPI) AS Average_SPI
FROM Student
INNER JOIN Result
    ON Student.RNO = Result.RNO
GROUP BY Student.BRANCH;
```

### Flow

```text
Student
   +
Result
   ↓
JOIN
   ↓
Matching records
   ↓
GROUP BY BRANCH
   ↓
AVG(SPI)
   ↓
Result
```

---

# 10. JOIN with GROUP BY

When we want results **branch-wise, city-wise, department-wise, etc.**, we can use `GROUP BY`.

Example:

```sql
SELECT
    Student.BRANCH,
    COUNT(*) AS Total_Students
FROM Student
INNER JOIN Result
    ON Student.RNO = Result.RNO
GROUP BY Student.BRANCH;
```

The important idea is:

```text
JOIN
→ Combine tables

GROUP BY
→ Create groups

Aggregate Function
→ Calculate something for each group
```

---

# 11. JOIN with ORDER BY

After joining tables, we can sort the result.

Example:

```sql
SELECT
    Student.RNO,
    Student.NAME,
    Result.SPI
FROM Student
INNER JOIN Result
    ON Student.RNO = Result.RNO
ORDER BY Result.SPI DESC;
```

```text
JOIN
 ↓
Combine data
 ↓
ORDER BY
 ↓
Sort result
```

---

# 12. Table Aliases

Aliases make JOIN queries shorter and easier to read.

Instead of:

```sql
Student.RNO
Student.NAME
Result.SPI
```

We can use:

```sql
S.RNO
S.NAME
R.SPI
```

### Example

```sql
SELECT
    S.RNO,
    S.NAME,
    S.BRANCH,
    R.SPI
FROM Student AS S
INNER JOIN Result AS R
    ON S.RNO = R.RNO;
```

Here:

```text
S → Student
R → Result
```

---

# 13. Why ON Condition Is Important

The `ON` condition tells SQL **how two tables are related**.

Example:

```sql
ON Student.RNO = Result.RNO
```

It means:

```text
Student.RNO
     =
Result.RNO
```

SQL searches for rows where these values match.

Without a proper relationship condition, you may get incorrect results.

---

# 14. JOIN Query Flow

A simple way to understand a JOIN query:

```text
FROM
 ↓
Choose first table
 ↓
JOIN
 ↓
Choose second table
 ↓
ON
 ↓
Define relationship
 ↓
WHERE
 ↓
Filter rows
 ↓
GROUP BY
 ↓
Create groups
 ↓
HAVING
 ↓
Filter groups
 ↓
ORDER BY
 ↓
Sort result
 ↓
SELECT
 ↓
Display required columns
```

For learning JOINs, remember the basic flow first:

```text
FROM
 ↓
JOIN
 ↓
ON
 ↓
WHERE
 ↓
SELECT
```

---

# 15. Difference Between JOIN Types

### INNER JOIN

```text
Only matching data
```

### LEFT JOIN

```text
Everything from left
+ matching right
```

### RIGHT JOIN

```text
Everything from right
+ matching left
```

### FULL OUTER JOIN

```text
Everything from both tables
```

### CROSS JOIN

```text
Every possible combination
```

---

# 16. Quick Memory Trick

```text
INNER
→ INTERSECTION
→ Only matching

LEFT
→ LEFT is important
→ Keep all LEFT rows

RIGHT
→ RIGHT is important
→ Keep all RIGHT rows

FULL
→ FULL data
→ Keep everything

CROSS
→ CROSS combinations
→ Every row with every row
```

---

# 17. Basic Syntax Cheat Sheet

```sql
-- INNER JOIN
SELECT *
FROM A
INNER JOIN B
ON A.ID = B.ID;
```

```sql
-- LEFT JOIN
SELECT *
FROM A
LEFT JOIN B
ON A.ID = B.ID;
```

```sql
-- RIGHT JOIN
SELECT *
FROM A
RIGHT JOIN B
ON A.ID = B.ID;
```

```sql
-- FULL OUTER JOIN
SELECT *
FROM A
FULL OUTER JOIN B
ON A.ID = B.ID;
```

```sql
-- CROSS JOIN
SELECT *
FROM A
CROSS JOIN B;
```

---

# 18. Final Revision

```text
JOIN = Combine tables

INNER JOIN
→ Matching records

LEFT JOIN
→ All LEFT + matching RIGHT

RIGHT JOIN
→ All RIGHT + matching LEFT

FULL OUTER JOIN
→ All LEFT + all RIGHT

CROSS JOIN
→ Every possible combination

ON
→ Defines how tables are related

WHERE
→ Filters individual rows

GROUP BY
→ Creates groups

HAVING
→ Filters groups

ORDER BY
→ Sorts the final result
```

### Most Important Concept

```text
Two Tables
    ↓
Common / Related Column
    ↓
JOIN
    ↓
ON condition
    ↓
Combined Data
    ↓
WHERE / GROUP BY / HAVING / ORDER BY
    ↓
Final Result
```
