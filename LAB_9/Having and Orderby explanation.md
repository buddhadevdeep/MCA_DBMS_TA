# 📘 DBMS Lab 9 — GROUP BY with HAVING and ORDER BY

<p align="center">
  <img src="https://img.shields.io/badge/DBMS-GROUP%20BY-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/SQL-HAVING-green?style=for-the-badge">
  <img src="https://img.shields.io/badge/SQL-ORDER%20BY-orange?style=for-the-badge">
  <img src="https://img.shields.io/badge/MS%20SQL%20Server-red?style=for-the-badge">
</p>

---

## 🎯 Objective

This lab focuses on:

- Aggregate Functions
- `GROUP BY`
- `HAVING`
- `ORDER BY`
- `WHERE` with `GROUP BY`
- Multiple conditions with `HAVING`
- Sorting grouped results

> **Note:** This README explains the concepts required to solve the lab questions. It does not contain individual lab solutions.

---

# 🧠 1. Aggregate Functions

Aggregate functions perform calculations on multiple rows and return a summary.

| Function | Purpose |
|---|---|
| `COUNT()` | Counts rows/values |
| `SUM()` | Calculates total |
| `AVG()` | Calculates average |
| `MAX()` | Finds highest value |
| `MIN()` | Finds lowest value |

Example:

```sql
SELECT
    COUNT(*) AS Total_Employees,
    SUM(SALARY) AS Total_Salary,
    AVG(SALARY) AS Average_Salary,
    MAX(SALARY) AS Maximum_Salary,
    MIN(SALARY) AS Minimum_Salary
FROM EMPLOYEE;
```

Without `GROUP BY`, the calculation is performed on the complete table.

---

# 📊 2. GROUP BY

`GROUP BY` divides rows into groups based on one or more columns.

Example:

```sql
SELECT
    DEPARTMENT,
    AVG(SALARY) AS Average_Salary
FROM EMPLOYEE
GROUP BY DEPARTMENT;
```

Concept:

```text
EMPLOYEE
    ↓
GROUP BY DEPARTMENT
    ↓
 ┌──────┬──────┬───────┐
 │  IT  │  HR  │ Admin │
 └──────┴──────┴───────┘
    ↓      ↓       ↓
   AVG    AVG     AVG
```

Instead of one overall average, SQL calculates an average for every department.

### Important idea

Words such as:

```text
department-wise
city-wise
gender-wise
branch-wise
```

usually indicate:

```sql
GROUP BY
```

---

# ⭐ 3. What is HAVING?

`HAVING` is used to **filter groups after `GROUP BY`**.

Example:

```sql
SELECT
    DEPARTMENT,
    AVG(SALARY) AS Average_Salary
FROM EMPLOYEE
GROUP BY DEPARTMENT
HAVING AVG(SALARY) > 30000;
```

Flow:

```text
EMPLOYEE
   ↓
GROUP BY DEPARTMENT
   ↓
Create department groups
   ↓
Calculate AVG(SALARY)
   ↓
HAVING AVG(SALARY) > 30000
   ↓
Keep only matching groups
```

---

# 🔥 4. WHERE vs HAVING

This is the most important difference.

| `WHERE` | `HAVING` |
|---|---|
| Filters individual rows | Filters groups |
| Applied before grouping | Applied after grouping |
| Used for row conditions | Commonly used for aggregate conditions |
| `SALARY > 10000` | `AVG(SALARY) > 10000` |

### Remember:

```text
WHERE  → Which rows?
HAVING → Which groups?
```

Example of `WHERE`:

```sql
SELECT *
FROM EMPLOYEE
WHERE CITY = 'Rajkot';
```

This filters individual employees.

Example of `HAVING`:

```sql
SELECT
    DEPARTMENT,
    COUNT(*) AS Total_Employees
FROM EMPLOYEE
GROUP BY DEPARTMENT
HAVING COUNT(*) > 2;
```

This filters departments based on the number of employees.

---

# 🧮 5. HAVING with Aggregate Functions

`HAVING` is commonly used with aggregate functions.

### COUNT()

```sql
HAVING COUNT(*) > 2
```

Meaning:

> Keep groups containing more than 2 records.

### SUM()

```sql
HAVING SUM(SALARY) > 50000
```

Meaning:

> Keep groups whose total salary is greater than 50000.

### AVG()

```sql
HAVING AVG(SALARY) > 30000
```

Meaning:

> Keep groups whose average salary is greater than 30000.

### MAX()

```sql
HAVING MAX(SALARY) > 40000
```

Meaning:

> Keep groups whose maximum salary is greater than 40000.

### MIN()

```sql
HAVING MIN(SALARY) > 20000
```

Meaning:

> Keep groups whose minimum salary is greater than 20000.

---

# 🔗 6. Multiple Conditions with HAVING

`AND` and `OR` can be used with `HAVING`.

Example:

```sql
SELECT
    DEPARTMENT,
    AVG(SALARY) AS Average_Salary
FROM EMPLOYEE
GROUP BY DEPARTMENT
HAVING AVG(SALARY) > 20000
   AND AVG(SALARY) < 50000;
```

Both conditions must be true.

Another example:

```sql
HAVING COUNT(*) > 2
    OR SUM(SALARY) > 50000;
```

At least one condition must be true.

---

# 🔎 7. WHERE + GROUP BY + HAVING

All three can be used together.

Example:

```sql
SELECT
    DEPARTMENT,
    AVG(SALARY) AS Average_Salary
FROM EMPLOYEE
WHERE CITY = 'Rajkot'
GROUP BY DEPARTMENT
HAVING AVG(SALARY) > 20000;
```

Understand the flow:

```text
1. FROM
   ↓
   Get EMPLOYEE records

2. WHERE
   ↓
   Keep Rajkot employees

3. GROUP BY
   ↓
   Create department groups

4. AVG()
   ↓
   Calculate average salary

5. HAVING
   ↓
   Keep groups with average > 20000
```

---

# 🔀 8. ORDER BY

`ORDER BY` is used to sort the final result.

### Ascending

```sql
ORDER BY SALARY ASC;
```

`ASC` means:

```text
Small → Large
A → Z
```

### Descending

```sql
ORDER BY SALARY DESC;
```

`DESC` means:

```text
Large → Small
Z → A
```

---

# 📈 9. ORDER BY with GROUP BY

Grouped results can also be sorted.

Example:

```sql
SELECT
    DEPARTMENT,
    SUM(SALARY) AS Total_Salary
FROM EMPLOYEE
GROUP BY DEPARTMENT
ORDER BY Total_Salary DESC;
```

Flow:

```text
GROUP BY
   ↓
Create department groups
   ↓
SUM(SALARY)
   ↓
Calculate total for each group
   ↓
ORDER BY
   ↓
Highest total first
```

---

# ⭐ 10. GROUP BY + HAVING + ORDER BY

These concepts can be combined.

Example:

```sql
SELECT
    DEPARTMENT,
    SUM(SALARY) AS Total_Salary
FROM EMPLOYEE
GROUP BY DEPARTMENT
HAVING SUM(SALARY) > 50000
ORDER BY Total_Salary DESC;
```

The query means:

```text
Group employees by department
        ↓
Calculate total salary
        ↓
Keep departments with total > 50000
        ↓
Sort by total salary
        ↓
Highest total first
```

---

# 🔄 11. SQL Logical Execution Flow

For queries containing all these clauses, understand the flow as:

```text
        FROM
          ↓
        WHERE
          ↓
      GROUP BY
          ↓
    Aggregate Functions
          ↓
       HAVING
          ↓
       SELECT
          ↓
      ORDER BY
```

### Meaning

```text
FROM
→ Select the source table

WHERE
→ Filter individual rows

GROUP BY
→ Create groups

Aggregate Functions
→ COUNT / SUM / AVG / MAX / MIN

HAVING
→ Filter the created groups

SELECT
→ Display required columns

ORDER BY
→ Sort the final result
```

---

# 🧠 12. How to Identify the Required Clause

When reading a question, break it into parts.

### Step 1 — What calculation is required?

```text
Number
   → COUNT()

Total
   → SUM()

Average
   → AVG()

Highest
   → MAX()

Lowest
   → MIN()
```

### Step 2 — Is it "per" something?

```text
City-wise
      → GROUP BY CITY

Department-wise
      → GROUP BY DEPARTMENT

Gender-wise
      → GROUP BY GENDER
```

### Step 3 — Is there a normal row condition?

```text
Salary > 10000
City = 'Rajkot'
Gender = 'Male'
      ↓
    WHERE
```

### Step 4 — Is the condition on an aggregate?

```text
Total > 50000
Average > 20000
Count > 2
Maximum > 30000
Minimum < 10000
      ↓
    HAVING
```

### Step 5 — Does it ask for sorting?

```text
Ordered by
Highest first
Lowest first
Ascending
Descending
      ↓
  ORDER BY
```

---

# 📌 13. General Query Pattern

A grouped query can follow this structure:

```sql
SELECT
    group_column,
    aggregate_function(column) AS alias
FROM table_name
WHERE row_condition
GROUP BY group_column
HAVING aggregate_condition
ORDER BY alias;
```

Not every query requires every clause.

For example:

```text
GROUP BY only

GROUP BY + HAVING

GROUP BY + ORDER BY

WHERE + GROUP BY + HAVING

WHERE + GROUP BY + HAVING + ORDER BY
```

---

# ⚠️ 14. Common Mistakes

### ❌ Mistake 1 — Using WHERE for Aggregate Conditions

Incorrect:

```sql
WHERE SUM(SALARY) > 50000
```

Correct:

```sql
HAVING SUM(SALARY) > 50000
```

Because `SUM()` is an aggregate result.

---

### ❌ Mistake 2 — Forgetting GROUP BY

If the requirement is:

```text
Department-wise average salary
```

you need:

```sql
GROUP BY DEPARTMENT
```

---

### ❌ Mistake 3 — Confusing WHERE and HAVING

```text
SALARY > 10000
```

→ `WHERE`

```text
AVG(SALARY) > 20000
```

→ `HAVING`

---

### ❌ Mistake 4 — Forgetting DESC

If the requirement says:

```text
Highest first
```

use:

```sql
ORDER BY column DESC;
```

If it says:

```text
Lowest first
```

use:

```sql
ORDER BY column ASC;
```

---

# 🧩 15. Simple Example

Suppose the requirement is:

> Find departments having more than 2 employees and display the departments with the highest employee count first.

Think:

```text
"departments"
      ↓
GROUP BY DEPARTMENT

"more than 2 employees"
      ↓
COUNT(*) > 2
      ↓
HAVING

"highest first"
      ↓
ORDER BY COUNT(*) DESC
```

General query:

```sql
SELECT
    DEPARTMENT,
    COUNT(*) AS Total_Employees
FROM EMPLOYEE
GROUP BY DEPARTMENT
HAVING COUNT(*) > 2
ORDER BY Total_Employees DESC;
```

The important thing is the **thinking process**, not memorizing the query.

---

# 📚 16. Quick Cheat Sheet

| Requirement | SQL Concept |
|---|---|
| Count employees | `COUNT()` |
| Total salary | `SUM()` |
| Average salary | `AVG()` |
| Highest salary | `MAX()` |
| Lowest salary | `MIN()` |
| City-wise | `GROUP BY CITY` |
| Department-wise | `GROUP BY DEPARTMENT` |
| Filter rows | `WHERE` |
| Filter aggregate/group result | `HAVING` |
| Highest first | `ORDER BY ... DESC` |
| Lowest first | `ORDER BY ... ASC` |

---

# 🎓 17. Final Concept

Remember this simple flow:

```text
┌───────────────┐
│     FROM      │
│ Get the table │
└───────┬───────┘
        ↓
┌───────────────┐
│     WHERE     │
│  Filter rows  │
└───────┬───────┘
        ↓
┌───────────────┐
│   GROUP BY    │
│ Create groups │
└───────┬───────┘
        ↓
┌───────────────┐
│   AGGREGATE   │
│ COUNT/SUM/AVG │
│ MAX/MIN       │
└───────┬───────┘
        ↓
┌───────────────┐
│    HAVING     │
│ Filter groups │
└───────┬───────┘
        ↓
┌───────────────┐
│   ORDER BY    │
│ Sort results  │
└───────────────┘
```

## ⭐ One-Line Memory Trick

> **WHERE filters rows → GROUP BY creates groups → HAVING filters groups → ORDER BY sorts the result.**

---

# 🚀 Final Revision

```text
COUNT() → How many?
SUM()   → Total?
AVG()   → Average?
MAX()   → Highest?
MIN()   → Lowest?

"Per / Each / Wise"
        ↓
    GROUP BY

"Normal row condition"
        ↓
      WHERE

"Condition on aggregate"
        ↓
      HAVING

"Sort / Order"
        ↓
    ORDER BY
```

> **Master these four concepts instead of memorizing individual queries. Once you can identify the group, aggregate function, row condition, group condition, and sorting requirement, you can solve the Lab 9 questions independently.**
