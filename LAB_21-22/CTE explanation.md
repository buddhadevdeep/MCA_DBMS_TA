# Lab 21,22 – Intermediate Common Table Expressions (CTE) in MS SQL Server

## 📌 Introduction

A **Common Table Expression (CTE)** is a temporary named result set that can be used inside a single SQL statement.

CTEs are mainly used to:

- Simplify complex queries
- Break a large query into smaller steps
- Perform calculations first and use the result later
- Work with aggregate functions
- Compare individual rows with group results
- Use ranking and row-number functions more clearly

### Basic Idea

```text
Main Table
    ↓
CTE
    ↓
Temporary Result
    ↓
Main Query
    ↓
Final Result
```

A CTE does **not permanently create a table**.

---

# 1. Basic CTE Syntax

The basic syntax is:

```sql
WITH CTE_Name AS
(
    SELECT ...
    FROM ...
)
SELECT *
FROM CTE_Name;
```

### Example

Suppose we have:

```text
STUDENT
--------------------------------
STDID | SNAME | BRANCH | SPI
--------------------------------
101   | RAJU  | CE     | 8.5
102   | AMIT  | IT     | 7.2
103   | NEHA  | CE     | 9.1
104   | PRIYA | ME     | 6.8
```

Create a CTE:

```sql
WITH StudentData AS
(
    SELECT *
    FROM STUDENT
)
SELECT *
FROM StudentData;
```

### Flow

```text
STUDENT
   ↓
WITH StudentData AS (...)
   ↓
Temporary Result
   ↓
SELECT FROM StudentData
```

---

# 2. CTE with WHERE

A CTE can first filter the records.

```sql
WITH HighSPI AS
(
    SELECT *
    FROM STUDENT
    WHERE SPI > 8
)
SELECT *
FROM HighSPI;
```

### Flow

```text
STUDENT
   ↓
WHERE SPI > 8
   ↓
HighSPI CTE
   ↓
SELECT
```

The CTE contains only students whose SPI is greater than 8.

---

# 3. CTE with Selected Columns

A CTE does not have to contain all columns.

```sql
WITH StudentBasic AS
(
    SELECT STDID, SNAME, BRANCH
    FROM STUDENT
)
SELECT *
FROM StudentBasic;
```

Only these columns are available in the CTE:

```text
STDID
SNAME
BRANCH
```

---

# 4. CTE with Aggregate Functions

A CTE can calculate aggregate values such as:

```text
COUNT()
SUM()
AVG()
MAX()
MIN()
```

Example:

```sql
WITH StudentAverage AS
(
    SELECT AVG(SPI) AS Average_SPI
    FROM STUDENT
)
SELECT *
FROM StudentAverage;
```

The CTE first calculates the average SPI.

Then the main query displays it.

### Flow

```text
STUDENT
   ↓
AVG(SPI)
   ↓
StudentAverage
   ↓
SELECT
```

---

# 5. CTE with GROUP BY

CTEs are very useful with `GROUP BY`.

Example:

```sql
WITH BranchCount AS
(
    SELECT
        BRANCH,
        COUNT(*) AS Total_Students
    FROM STUDENT
    GROUP BY BRANCH
)
SELECT *
FROM BranchCount;
```

Result concept:

```text
BRANCH     TOTAL_STUDENTS
-------------------------
CE         4
IT         3
ME         2
```

### Flow

```text
STUDENT
   ↓
GROUP BY BRANCH
   ↓
COUNT students
   ↓
BranchCount CTE
   ↓
SELECT
```

---

# 6. CTE for Branch Average

Suppose we want the average SPI of every branch.

```sql
WITH BranchAverage AS
(
    SELECT
        BRANCH,
        AVG(SPI) AS Average_SPI
    FROM STUDENT
    GROUP BY BRANCH
)
SELECT *
FROM BranchAverage;
```

The CTE creates one result for each branch.

```text
CE → Average SPI
IT → Average SPI
ME → Average SPI
```

---

# 7. Comparing Student SPI with Overall Average

One important use of a CTE is to calculate a value first and then compare individual records with that value.

Example:

```sql
WITH OverallAverage AS
(
    SELECT AVG(SPI) AS Avg_SPI
    FROM STUDENT
)
SELECT S.*
FROM STUDENT AS S
CROSS JOIN OverallAverage AS A
WHERE S.SPI < A.Avg_SPI;
```

### Flow

```text
              STUDENT
                 |
                 ↓
            AVG(SPI)
                 |
                 ↓
         OverallAverage
                 |
                 ↓
       Compare each student
                 |
          SPI < Average
                 |
                 ↓
             Result
```

This is useful when we need to compare a row with an overall calculation.

---

# 8. Comparing Student SPI with Branch Average

This is another important CTE concept.

First calculate the average SPI of every branch:

```sql
WITH BranchAverage AS
(
    SELECT
        BRANCH,
        AVG(SPI) AS Avg_SPI
    FROM STUDENT
    GROUP BY BRANCH
)
SELECT
    S.STDID,
    S.SNAME,
    S.BRANCH,
    S.SPI,
    B.Avg_SPI
FROM STUDENT AS S
INNER JOIN BranchAverage AS B
    ON S.BRANCH = B.BRANCH
WHERE S.SPI > B.Avg_SPI;
```

### Flow

```text
                 STUDENT
                    |
                    | GROUP BY BRANCH
                    ↓
              Branch Average
                    |
                    ↓
              JOIN with Student
                    |
                    ↓
        Compare SPI with Branch Average
                    |
                    ↓
                  Result
```

### Important Concept

```text
Individual Student SPI
        ↓
Compare
        ↓
Average SPI of student's branch
```

---

# 9. CTE with HAVING

CTEs can also be used with `HAVING`.

Example:

```sql
WITH BranchStudents AS
(
    SELECT
        BRANCH,
        COUNT(*) AS Total_Students
    FROM STUDENT
    GROUP BY BRANCH
    HAVING COUNT(*) > 2
)
SELECT *
FROM BranchStudents;
```

Here:

```text
GROUP BY
→ Creates branch groups

COUNT()
→ Counts students

HAVING
→ Keeps branches having more than 2 students
```

---

# 10. CTE with ORDER BY

Usually, sorting is done in the final query.

Example:

```sql
WITH BranchAverage AS
(
    SELECT
        BRANCH,
        AVG(SPI) AS Average_SPI
    FROM STUDENT
    GROUP BY BRANCH
)
SELECT *
FROM BranchAverage
ORDER BY Average_SPI DESC;
```

### Flow

```text
STUDENT
   ↓
GROUP BY
   ↓
AVG(SPI)
   ↓
CTE
   ↓
ORDER BY
   ↓
Final Result
```

---

# 11. CTE with TOP

A CTE can be used to prepare data and then select the top records.

Example:

```sql
WITH StudentData AS
(
    SELECT *
    FROM STUDENT
)
SELECT TOP 3 *
FROM StudentData
ORDER BY SPI DESC;
```

### Concept

```text
STUDENT
   ↓
CTE
   ↓
ORDER BY SPI DESC
   ↓
TOP 3
   ↓
Highest 3 SPI students
```

---

# 12. CTE with ROW_NUMBER()

`ROW_NUMBER()` gives a unique sequential number to each row.

### Example

```sql
SELECT
    ROW_NUMBER() OVER (ORDER BY SPI DESC) AS Row_No,
    STDID,
    SNAME,
    SPI
FROM STUDENT;
```

Possible result:

```text
ROW_NO   STDID   SNAME   SPI
----------------------------
1        103     NEHA    9.1
2        101     RAJU    8.5
3        102     AMIT    7.2
4        104     PRIYA   6.8
```

---

# 13. ROW_NUMBER() with CTE

A CTE makes it easier to use the generated row number.

```sql
WITH StudentRanking AS
(
    SELECT
        ROW_NUMBER() OVER (ORDER BY SPI DESC) AS Row_No,
        STDID,
        SNAME,
        BRANCH,
        SPI
    FROM STUDENT
)
SELECT *
FROM StudentRanking;
```

### Flow

```text
STUDENT
   ↓
ROW_NUMBER()
   ↓
StudentRanking CTE
   ↓
SELECT
```

---

# 14. RANK()

`RANK()` gives the same rank to equal values.

```sql
SELECT
    RANK() OVER (ORDER BY SPI DESC) AS Student_Rank,
    SNAME,
    SPI
FROM STUDENT;
```

Example:

```text
SNAME     SPI     RANK
----------------------
RAJU      9.5      1
NEHA      9.5      1
AMIT      8.5      3
PRIYA     7.5      4
```

Notice that after two students get rank `1`, the next rank is `3`.

---

# 15. ROW_NUMBER vs RANK

| Function | Same values get same number? | Skips number? |
|---|---|---|
| `ROW_NUMBER()` | No | No |
| `RANK()` | Yes | Yes |
| `DENSE_RANK()` | Yes | No |

### Easy Example

For:

```text
SPI
9.5
9.5
8.5
```

`ROW_NUMBER()`:

```text
1
2
3
```

`RANK()`:

```text
1
1
3
```

`DENSE_RANK()`:

```text
1
1
2
```

---

# 16. Branch-wise Ranking

We can rank students separately inside each branch using `PARTITION BY`.

```sql
SELECT
    BRANCH,
    SNAME,
    SPI,
    RANK() OVER
    (
        PARTITION BY BRANCH
        ORDER BY SPI DESC
    ) AS Branch_Rank
FROM STUDENT;
```

### Important

```text
PARTITION BY BRANCH
        ↓
Create separate ranking groups
        ↓
Rank students inside each branch
```

Example concept:

```text
CE
 ├── Student A → Rank 1
 ├── Student B → Rank 2
 └── Student C → Rank 3

IT
 ├── Student D → Rank 1
 └── Student E → Rank 2
```

---

# 17. CTE for Branch-wise Ranking

```sql
WITH BranchRanking AS
(
    SELECT
        BRANCH,
        SNAME,
        SPI,
        RANK() OVER
        (
            PARTITION BY BRANCH
            ORDER BY SPI DESC
        ) AS Branch_Rank
    FROM STUDENT
)
SELECT *
FROM BranchRanking;
```

This makes a complex ranking query easier to understand.

---

# 18. Finding Maximum SPI

Aggregate function:

```sql
MAX(SPI)
```

Example:

```sql
WITH MaximumSPI AS
(
    SELECT MAX(SPI) AS Max_SPI
    FROM STUDENT
)
SELECT *
FROM MaximumSPI;
```

---

# 19. Finding Minimum SPI

```sql
WITH MinimumSPI AS
(
    SELECT MIN(SPI) AS Min_SPI
    FROM STUDENT
)
SELECT *
FROM MinimumSPI;
```

The CTE stores the calculated minimum and the main query displays it.

---

# 20. Finding Branch with Highest Average

First calculate the average of every branch:

```sql
WITH BranchAverage AS
(
    SELECT
        BRANCH,
        AVG(SPI) AS Average_SPI
    FROM STUDENT
    GROUP BY BRANCH
)
SELECT TOP 1 *
FROM BranchAverage
ORDER BY Average_SPI DESC;
```

### Flow

```text
STUDENT
   ↓
GROUP BY BRANCH
   ↓
AVG(SPI)
   ↓
BranchAverage
   ↓
ORDER BY Average_SPI DESC
   ↓
TOP 1
```

The important concept is not the exact query, but the sequence:

```text
Calculate
   ↓
Store temporarily in CTE
   ↓
Sort / Filter
   ↓
Get required result
```

---

# 21. Multiple CTEs

More than one CTE can be written in the same query.

```sql
WITH BranchAverage AS
(
    SELECT
        BRANCH,
        AVG(SPI) AS Avg_SPI
    FROM STUDENT
    GROUP BY BRANCH
),
BranchCount AS
(
    SELECT
        BRANCH,
        COUNT(*) AS Total_Students
    FROM STUDENT
    GROUP BY BRANCH
)
SELECT
    A.BRANCH,
    A.Avg_SPI,
    C.Total_Students
FROM BranchAverage AS A
INNER JOIN BranchCount AS C
    ON A.BRANCH = C.BRANCH;
```

### Flow

```text
                 STUDENT
                /       \
               /         \
              ↓           ↓
      BranchAverage   BranchCount
              \           /
               \         /
                  JOIN
                   ↓
                Result
```

This is useful when a query requires multiple intermediate calculations.

---

# 22. CTE vs Temporary Table

A CTE and temporary table are not the same.

| CTE | Temporary Table |
|---|---|
| Temporary query result | Temporary table |
| Exists for one statement | Can be used for multiple statements |
| Starts with `WITH` | Starts with `#` |
| Mainly for query simplification | Useful for storing intermediate data |
| Does not need manual cleanup | Automatically removed when session ends, depending on type |

### CTE

```sql
WITH StudentData AS
(
    SELECT *
    FROM STUDENT
)
SELECT *
FROM StudentData;
```

### Temporary Table

```sql
SELECT *
INTO #StudentData
FROM STUDENT;

SELECT *
FROM #StudentData;
```

---

# 23. CTE vs View

| CTE | View |
|---|---|
| Temporary for one statement | Stored database object |
| Uses `WITH` | Uses `CREATE VIEW` |
| Not permanently stored as a view | Permanently stored definition |
| Useful for complex queries | Useful for reusable queries |
| Disappears after the statement | Can be used later |

### CTE

```sql
WITH StudentData AS
(
    SELECT *
    FROM STUDENT
)
SELECT *
FROM StudentData;
```

### View

```sql
CREATE VIEW StudentData
AS
SELECT *
FROM STUDENT;
```

---

# 24. Why Use CTE?

### Without CTE

A complex query may become difficult to read:

```text
Large Query
   ↓
Nested Query
   ↓
Another Calculation
   ↓
Another Filter
   ↓
Final Result
```

### With CTE

```text
Step 1 → Calculate
          ↓
Step 2 → CTE
          ↓
Step 3 → Filter / Join
          ↓
Step 4 → Final Result
```

CTEs make the query more **organized, readable, and easier to understand**.

---

# 25. Important CTE Rules

### Rule 1 – CTE starts with WITH

```sql
WITH CTE_Name AS
(
    SELECT ...
)
```

### Rule 2 – Main query must use the CTE

```sql
WITH StudentData AS
(
    SELECT *
    FROM STUDENT
)
SELECT *
FROM StudentData;
```

### Rule 3 – CTE exists only for the current statement

```sql
WITH StudentData AS
(
    SELECT *
    FROM STUDENT
)
SELECT *
FROM StudentData;
```

After this statement, `StudentData` is not available as a permanent table.

### Rule 4 – CTE does not permanently store data

It is a query definition used for the statement.

---

# 26. CTE Query Flow

The most important flow to remember:

```text
WITH
 ↓
Define CTE
 ↓
SELECT / WHERE / GROUP BY / Aggregate
 ↓
Temporary Result
 ↓
Main SELECT
 ↓
JOIN / WHERE / ORDER BY / TOP
 ↓
Final Result
```

Example concept:

```text
STUDENT
   ↓
Calculate branch average
   ↓
BranchAverage CTE
   ↓
JOIN with STUDENT
   ↓
Compare SPI
   ↓
Filter
   ↓
Final Result
```

---

# 27. General CTE Template

Use this template while learning:

```sql
WITH CTE_Name AS
(
    SELECT
        column1,
        column2,
        AGGREGATE(column3) AS Result
    FROM TableName
    WHERE condition
    GROUP BY column1
)
SELECT *
FROM CTE_Name;
```

---

# 28. Final Revision

```text
CTE
↓
Common Table Expression
↓
Temporary named result
↓
Created using WITH
↓
Used by the main query
```

### Common Uses

```text
CTE
 ├── Filtering
 ├── Aggregation
 ├── GROUP BY
 ├── JOIN
 ├── Comparing values
 ├── ROW_NUMBER()
 ├── RANK()
 ├── DENSE_RANK()
 ├── TOP
 └── Complex query simplification
```

### Easy Definition

> **A CTE is a temporary named result set created using `WITH` that helps break a complex SQL query into simple and readable steps.**

### Most Important Syntax

```sql
WITH CTE_Name AS
(
    SELECT ...
    FROM ...
)
SELECT *
FROM CTE_Name;
```

### Remember

```text
CTE = Calculate first → Name the result → Use it in the main query
```
