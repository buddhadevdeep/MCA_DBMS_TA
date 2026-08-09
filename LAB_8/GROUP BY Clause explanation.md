# 📘 DBMS Lab 8 — Aggregate Functions & GROUP BY

<p align="center">
  <img src="https://img.shields.io/badge/DBMS-GROUP%20BY-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/SQL-Aggregate%20Functions-green?style=for-the-badge">
  <img src="https://img.shields.io/badge/MS%20SQL%20Server-orange?style=for-the-badge">
</p>

---

# 🎯 Objective

This lab introduces the concept of **Aggregate Functions** and the **GROUP BY clause** in SQL Server.

The main goal is to understand:

- What aggregate functions are
- Why aggregate functions are required
- `COUNT()`
- `SUM()`
- `AVG()`
- `MAX()`
- `MIN()`
- What `GROUP BY` does
- Why `GROUP BY` is used with aggregate functions
- How SQL creates groups
- Grouping by one column
- Grouping by multiple columns
- Using `WHERE` before `GROUP BY`
- Using `DISTINCT` with aggregate functions
- Understanding `NULL` with aggregate functions
- Understanding the difference between grouped and non-grouped results
- How to identify the required aggregate function from a question

> **Important:** This README explains the concepts required to solve the lab. It does **not** provide solutions to the individual lab questions.

---

# 🧠 1. Why Do We Need Aggregate Functions?

Suppose an `EMPLOYEE` table contains:

| EMPID | NAME | DEPARTMENT | CITY | SALARY |
|------:|------|------------|------|-------:|
| 101 | Rahul | IT | Rajkot | 30000 |
| 102 | Priya | HR | Rajkot | 35000 |
| 103 | Amit | IT | Surat | 40000 |
| 104 | Neha | HR | Surat | 45000 |
| 105 | Ravi | IT | Ahmedabad | 32000 |
| 106 | Pooja | Admin | Ahmedabad | 28000 |

Normally, SQL returns individual records:

```sql
SELECT *
FROM EMPLOYEE;
```

But sometimes we don't want individual records.

We may want information such as:

```text
How many employees are there?
What is the total salary?
What is the average salary?
What is the highest salary?
What is the lowest salary?
```

These are **summary calculations**.

SQL provides **aggregate functions** for this purpose.

---

# 🔢 2. What is an Aggregate Function?

An aggregate function performs a calculation on a **set of rows** and returns a summarized result.

The five most important aggregate functions are:

```text
COUNT()
SUM()
AVG()
MAX()
MIN()
```

Think of them as:

```text
COUNT → How many?
SUM   → How much in total?
AVG   → What is the average?
MAX   → What is the highest?
MIN   → What is the lowest?
```

---

# 3. COUNT()

`COUNT()` is used to count records or values.

## Example

```sql
SELECT COUNT(*)
FROM EMPLOYEE;
```

If the table contains 6 employees:

```text
COUNT
-----
6
```

---

## COUNT(*)

```sql
COUNT(*)
```

counts **all rows**.

---

## COUNT(column)

```sql
COUNT(CITY)
```

counts only rows where `CITY` is **not NULL**.

Example:

| NAME | CITY |
|------|------|
| Rahul | Rajkot |
| Priya | Surat |
| Amit | NULL |

```sql
SELECT COUNT(CITY)
FROM EMPLOYEE;
```

Result:

```text
2
```

because the NULL value is not counted.

---

# 4. SUM()

`SUM()` calculates the total of a numeric column.

Example:

```sql
SELECT SUM(SALARY)
FROM EMPLOYEE;
```

If salaries are:

```text
30000
35000
40000
```

then:

```text
SUM = 105000
```

`SUM()` is normally used with numeric columns.

---

# 5. AVG()

`AVG()` calculates the average of numeric values.

Example:

```sql
SELECT AVG(SALARY)
FROM EMPLOYEE;
```

Suppose:

```text
Salary:
30000
40000
50000
```

Then:

```text
AVG = (30000 + 40000 + 50000) / 3
    = 40000
```

---

# 6. MAX()

`MAX()` returns the highest value.

Example:

```sql
SELECT MAX(SALARY)
FROM EMPLOYEE;
```

If salaries are:

```text
30000
45000
38000
```

then:

```text
MAX = 45000
```

---

# 7. MIN()

`MIN()` returns the lowest value.

Example:

```sql
SELECT MIN(SALARY)
FROM EMPLOYEE;
```

If salaries are:

```text
30000
45000
38000
```

then:

```text
MIN = 30000
```

---

# 📊 8. Aggregate Functions Summary

| Function | Meaning | Example |
|----------|---------|---------|
| `COUNT()` | Number of records | `COUNT(*)` |
| `SUM()` | Total | `SUM(SALARY)` |
| `AVG()` | Average | `AVG(SALARY)` |
| `MAX()` | Highest value | `MAX(SALARY)` |
| `MIN()` | Lowest value | `MIN(SALARY)` |

---

# 🧠 9. Aggregate Function Without GROUP BY

This is very important.

Consider:

```sql
SELECT AVG(SALARY)
FROM EMPLOYEE;
```

SQL considers **all employees together**.

Conceptually:

```text
EMPLOYEE
────────────────────
Employee 1
Employee 2
Employee 3
Employee 4
Employee 5
Employee 6
────────────────────
        ↓
      AVG()
        ↓
 One overall result
```

The result is one summary value.

---

# ⭐ 10. What is GROUP BY?

`GROUP BY` is used to divide rows into **groups based on a column or columns**.

Instead of calculating one result for the entire table, SQL can calculate a separate result for every group.

---

# 🔥 The Main Idea of GROUP BY

Suppose we have:

| NAME | DEPARTMENT | SALARY |
|------|------------|-------:|
| Rahul | IT | 30000 |
| Amit | IT | 40000 |
| Ravi | IT | 32000 |
| Priya | HR | 35000 |
| Neha | HR | 45000 |
| Pooja | Admin | 28000 |

Without grouping:

```text
All employees
     ↓
One calculation
     ↓
One result
```

With grouping by department:

```text
             EMPLOYEE
                │
                ▼
        GROUP BY DEPARTMENT
                │
       ┌────────┼────────┐
       ▼        ▼        ▼
      IT        HR      Admin
       │        │        │
       ▼        ▼        ▼
    Calculate Calculate Calculate
    result     result    result
```

So instead of one result, we get:

```text
IT     → one result
HR     → one result
Admin  → one result
```

---

# 11. Simple GROUP BY Example

```sql
SELECT DEPARTMENT, AVG(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT;
```

The important part is:

```sql
GROUP BY DEPARTMENT
```

SQL creates groups:

```text
IT
├── Rahul
├── Amit
└── Ravi

HR
├── Priya
└── Neha

Admin
└── Pooja
```

Then `AVG(SALARY)` is calculated separately for each group.

---

# 12. GROUP BY Does Not Calculate Anything by Itself

This is an important concept.

`GROUP BY` itself does not calculate:

```text
Total
Average
Maximum
Minimum
Count
```

It only **creates groups**.

For example:

```sql
GROUP BY DEPARTMENT
```

means:

> "Put employees having the same department into the same group."

Then an aggregate function can calculate something for each group.

Example:

```sql
AVG(SALARY)
```

calculates the average salary of each group.

---

# 🧩 13. GROUP BY + Aggregate Function

The general pattern is:

```sql
SELECT group_column, aggregate_function(column)
FROM table_name
GROUP BY group_column;
```

Example:

```sql
SELECT
    DEPARTMENT,
    MAX(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT;
```

Here:

```text
DEPARTMENT → Creates groups
MAX()      → Performs calculation
SALARY     → Value being calculated
```

---

# 🔄 14. How GROUP BY Works Internally

Consider:

```sql
SELECT DEPARTMENT, SUM(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT;
```

Conceptually SQL performs:

### Step 1

Read the employee records.

```text
All Employees
```

### Step 2

Look at the `DEPARTMENT` value.

### Step 3

Put matching departments together.

```text
IT
IT
IT

HR
HR

Admin
```

### Step 4

Create logical groups.

```text
IT Group
HR Group
Admin Group
```

### Step 5

Apply the aggregate function separately.

```text
SUM(IT salaries)
SUM(HR salaries)
SUM(Admin salaries)
```

### Step 6

Return one result for each group.

---

# 📌 15. GROUP BY One Column

A table can be grouped using one column.

Example:

```sql
GROUP BY CITY
```

This creates:

```text
Ahmedabad Group
Rajkot Group
Surat Group
```

Then we can calculate something for every city.

For example:

```sql
SELECT CITY, COUNT(*)
FROM EMPLOYEE
GROUP BY CITY;
```

The important concept is:

```text
Same CITY → Same Group
```

---

# 📌 16. GROUP BY Multiple Columns

We can group using more than one column.

Example:

```sql
GROUP BY CITY, DEPARTMENT
```

This does **not** create separate groups independently.

It creates groups based on the **combination** of values.

For example:

```text
Ahmedabad + IT
Ahmedabad + HR
Rajkot + IT
Rajkot + HR
Surat + IT
Surat + HR
```

Each unique combination becomes a group.

---

# Example

```sql
SELECT
    CITY,
    DEPARTMENT,
    AVG(SALARY)
FROM EMPLOYEE
GROUP BY CITY, DEPARTMENT;
```

Think of it as:

```text
CITY + DEPARTMENT
        ↓
   Unique Group
        ↓
    AVG(SALARY)
```

---

# ⭐ 17. GROUP BY is About "Per"

A very useful trick for understanding questions:

Whenever you see:

```text
city-wise
department-wise
gender-wise
```

think:

```text
GROUP BY
```

For example:

```text
City-wise average
       ↓
GROUP BY CITY

Department-wise total
       ↓
GROUP BY DEPARTMENT

Gender-wise count
       ↓
GROUP BY GENDER
```

This is one of the easiest ways to identify when `GROUP BY` is required.

---

# 18. WHERE with GROUP BY

`WHERE` is used to filter rows **before grouping**.

Example:

```sql
SELECT DEPARTMENT, AVG(SALARY)
FROM EMPLOYEE
WHERE CITY = 'Rajkot'
GROUP BY DEPARTMENT;
```

Understand the flow:

```text
All Employees
      ↓
WHERE CITY = 'Rajkot'
      ↓
Only Rajkot Employees
      ↓
GROUP BY DEPARTMENT
      ↓
Department Groups
      ↓
AVG(SALARY)
```

So:

```text
WHERE → filters rows
GROUP BY → creates groups
Aggregate → calculates result
```

---

# 19. Important Difference: WHERE and GROUP BY

### WHERE

Answers:

> Which rows should participate?

Example:

```sql
WHERE CITY = 'Rajkot'
```

### GROUP BY

Answers:

> How should those rows be divided into groups?

Example:

```sql
GROUP BY DEPARTMENT
```

Together:

```text
WHERE
 ↓
Filter rows
 ↓
GROUP BY
 ↓
Create groups
 ↓
Aggregate function
 ↓
Calculate result
```

---

# 20. GROUP BY with Different Aggregate Functions

The same group can be used with different calculations.

For example:

```sql
SELECT
    DEPARTMENT,
    COUNT(*) AS Total_Employees,
    SUM(SALARY) AS Total_Salary,
    AVG(SALARY) AS Average_Salary,
    MAX(SALARY) AS Maximum_Salary,
    MIN(SALARY) AS Minimum_Salary
FROM EMPLOYEE
GROUP BY DEPARTMENT;
```

Here the department groups are created only once conceptually, but several calculations are performed for each group.

---

# 🧠 21. Choosing the Correct Aggregate Function

When reading a question, look for the keyword.

| Question asks for | Use |
|-------------------|-----|
| Number of employees | `COUNT()` |
| Total salary | `SUM()` |
| Average salary | `AVG()` |
| Highest salary | `MAX()` |
| Lowest salary | `MIN()` |

Example:

```text
"highest salary"
        ↓
      MAX()

"lowest salary"
        ↓
      MIN()

"total salary"
        ↓
      SUM()

"average salary"
        ↓
      AVG()

"number of employees"
        ↓
      COUNT()
```

---

# 22. Choosing the GROUP BY Column

Look for words such as:

```text
city-wise
department-wise
gender-wise
branch-wise
category-wise
```

These indicate the grouping column.

Examples:

```text
City-wise
    ↓
GROUP BY CITY
```

```text
Department-wise
    ↓
GROUP BY DEPARTMENT
```

```text
Gender-wise
    ↓
GROUP BY GENDER
```

---

# 23. DISTINCT with Aggregate Functions

`DISTINCT` removes duplicate values.

Suppose:

```text
CITY
---------
Rajkot
Rajkot
Surat
Surat
Ahmedabad
```

Without `DISTINCT`:

```text
Rajkot
Rajkot
Surat
Surat
Ahmedabad
```

With:

```sql
SELECT DISTINCT CITY
FROM EMPLOYEE;
```

Result:

```text
Rajkot
Surat
Ahmedabad
```

---

# COUNT(DISTINCT column)

We can combine `COUNT()` and `DISTINCT`.

```sql
SELECT COUNT(DISTINCT CITY)
FROM EMPLOYEE;
```

Meaning:

```text
1. Find unique cities
2. Count those cities
```

This is useful when the question asks:

```text
How many different cities?
How many unique departments?
```

---

# 24. GROUP BY vs DISTINCT

These two concepts are related but have different purposes.

## DISTINCT

Used to remove duplicate values.

```sql
SELECT DISTINCT CITY
FROM EMPLOYEE;
```

Purpose:

```text
Show unique cities
```

---

## GROUP BY

Used to create groups, usually for aggregate calculations.

```sql
SELECT CITY, COUNT(*)
FROM EMPLOYEE
GROUP BY CITY;
```

Purpose:

```text
Create city groups
+
Calculate something for every city
```

---

# 25. NULL and Aggregate Functions

`NULL` means that a value is missing or unknown.

Most aggregate functions ignore `NULL` values.

For example:

```text
SALARY
------
30000
40000
NULL
50000
```

For:

```sql
AVG(SALARY)
```

SQL considers:

```text
30000
40000
50000
```

The `NULL` value is ignored.

---

# 26. COUNT(*) vs COUNT(column)

This is an important concept.

Suppose:

| EMPID | CITY |
|------:|------|
| 101 | Rajkot |
| 102 | Surat |
| 103 | NULL |

### COUNT(*)

```sql
SELECT COUNT(*)
FROM EMPLOYEE;
```

Counts all rows:

```text
3
```

### COUNT(CITY)

```sql
SELECT COUNT(CITY)
FROM EMPLOYEE;
```

Counts only non-NULL CITY values:

```text
2
```

Therefore:

```text
COUNT(*)       → Counts rows
COUNT(column)  → Counts non-NULL values
```

---

# 27. Column Alias

An alias gives a meaningful name to the calculated result.

Without alias:

```sql
SELECT AVG(SALARY)
FROM EMPLOYEE;
```

With alias:

```sql
SELECT AVG(SALARY) AS Average_Salary
FROM EMPLOYEE;
```

Aliases improve readability.

Common aliases:

```text
COUNT(*)  → Total_Employees
SUM()     → Total_Salary
AVG()     → Average_Salary
MAX()     → Maximum_Salary
MIN()     → Minimum_Salary
```

---

# 28. Multiple Aggregate Functions

We can use multiple aggregate functions in one query.

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

This produces an overall summary.

With `GROUP BY`:

```sql
SELECT
    DEPARTMENT,
    COUNT(*) AS Total_Employees,
    AVG(SALARY) AS Average_Salary
FROM EMPLOYEE
GROUP BY DEPARTMENT;
```

Now the summary is produced **for each department**.

---

# ⚠️ 29. Important GROUP BY Rule

If a column is selected and it is **not an aggregate function**, it normally needs to be present in `GROUP BY`.

### Correct

```sql
SELECT
    DEPARTMENT,
    AVG(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT;
```

Why?

```text
DEPARTMENT → GROUP BY
SALARY     → AVG()
```

---

### Multiple Columns

```sql
SELECT
    CITY,
    DEPARTMENT,
    AVG(SALARY)
FROM EMPLOYEE
GROUP BY CITY, DEPARTMENT;
```

Why?

```text
CITY       → GROUP BY
DEPARTMENT → GROUP BY
SALARY     → AVG()
```

---

# 30. Query Structure

The basic structure of a grouped query is:

```sql
SELECT
    group_column,
    aggregate_function(column)
FROM table_name
WHERE condition
GROUP BY group_column;
```

Not every query needs `WHERE`.

So the basic form can also be:

```sql
SELECT
    group_column,
    aggregate_function(column)
FROM table_name
GROUP BY group_column;
```

---

# 🔄 31. Logical Execution Flow

For a query containing `WHERE` and `GROUP BY`:

```text
┌──────────────┐
│    FROM      │
│ Get table    │
└──────┬───────┘
       ↓
┌──────────────┐
│    WHERE     │
│ Filter rows  │
└──────┬───────┘
       ↓
┌──────────────┐
│   GROUP BY   │
│ Create groups│
└──────┬───────┘
       ↓
┌──────────────┐
│  AGGREGATE   │
│ COUNT/SUM/   │
│ AVG/MAX/MIN  │
└──────┬───────┘
       ↓
┌──────────────┐
│    SELECT    │
│ Show result  │
└──────────────┘
```

Remember:

```text
FROM
 ↓
WHERE
 ↓
GROUP BY
 ↓
AGGREGATE
 ↓
SELECT
```

---

# 🧩 32. How to Think About GROUP BY

Imagine a classroom.

There are 30 students.

Students belong to:

```text
CSE
IT
CE
ME
```

If you ask:

```text
How many students are there?
```

You need:

```sql
COUNT(*)
```

You get one answer:

```text
30
```

But if you ask:

```text
How many students are there in each branch?
```

You need:

```sql
GROUP BY BRANCH
```

Now SQL creates:

```text
CSE Group
IT Group
CE Group
ME Group
```

Then:

```sql
COUNT(*)
```

is calculated for each group.

This is the basic idea behind `GROUP BY`.

---

# 🎯 33. Overall Result vs Grouped Result

## Without GROUP BY

```sql
SELECT AVG(SALARY)
FROM EMPLOYEE;
```

Concept:

```text
All Employees
      ↓
One Average
```

Result:

```text
One row
```

---

## With GROUP BY

```sql
SELECT DEPARTMENT, AVG(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT;
```

Concept:

```text
Employees
    ↓
Department Groups
    ↓
Average for each group
```

Result:

```text
One row per department
```

---

# 📊 34. One Column vs Multiple Columns

### One-column grouping

```sql
GROUP BY CITY
```

Groups by:

```text
CITY
```

### Two-column grouping

```sql
GROUP BY CITY, DEPARTMENT
```

Groups by:

```text
CITY + DEPARTMENT
```

### Three-column grouping

```sql
GROUP BY CITY, DEPARTMENT, GENDER
```

Groups by:

```text
CITY + DEPARTMENT + GENDER
```

The more columns you add, the more specific the groups become.

---

# 🚫 35. Common Mistakes

## Mistake 1 — Forgetting GROUP BY

Incorrect:

```sql
SELECT DEPARTMENT, AVG(SALARY)
FROM EMPLOYEE;
```

Correct:

```sql
SELECT DEPARTMENT, AVG(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT;
```

---

## Mistake 2 — Grouping by the Wrong Column

If the question asks for:

```text
City-wise
```

the grouping column should be:

```sql
GROUP BY CITY
```

not:

```sql
GROUP BY DEPARTMENT
```

---

## Mistake 3 — Using COUNT Instead of SUM

Remember:

```text
How many? → COUNT()
Total?    → SUM()
```

---

## Mistake 4 — Using MAX Instead of MIN

Remember:

```text
Highest → MAX()
Lowest  → MIN()
```

---

## Mistake 5 — Forgetting DISTINCT

If the requirement is:

```text
unique cities
```

think:

```sql
DISTINCT
```

---

# 🧠 36. Quick Learning Formula

When solving a GROUP BY problem, mentally break the question into three parts:

```text
1. WHAT calculation?
2. PER WHAT group?
3. WHICH rows?
```

### WHAT?

```text
Highest → MAX()
Lowest  → MIN()
Total   → SUM()
Average → AVG()
Count   → COUNT()
```

### PER WHAT?

```text
City       → GROUP BY CITY
Department → GROUP BY DEPARTMENT
Gender     → GROUP BY GENDER
```

### WHICH ROWS?

If a condition is given:

```sql
WHERE condition
```

This gives the basic thinking process:

```text
Question
   ↓
What calculation?
   ↓
What grouping?
   ↓
Any condition?
   ↓
Build GROUP BY query
```

---

# 📚 37. Concept Cheat Sheet

```text
COUNT()
    → Number of rows/values

SUM()
    → Total of numeric values

AVG()
    → Average of numeric values

MAX()
    → Highest value

MIN()
    → Lowest value

GROUP BY
    → Creates groups

WHERE
    → Filters rows before grouping

DISTINCT
    → Removes duplicate values

AS
    → Gives an alias to output

COUNT(DISTINCT column)
    → Counts unique non-NULL values
```

---

# 🎓 38. Final Concept Example

Suppose the requirement is:

> Find the average salary for every department.

Think step-by-step:

```text
"average"
     ↓
AVG()

"every department"
     ↓
GROUP BY DEPARTMENT
```

Therefore the general structure becomes:

```sql
SELECT
    DEPARTMENT,
    AVG(SALARY)
FROM EMPLOYEE
GROUP BY DEPARTMENT;
```

The important thing is not memorizing this query.

The important concept is:

```text
AVERAGE
   +
PER DEPARTMENT
   =
AVG() + GROUP BY DEPARTMENT
```

---

# 🚀 Final Takeaways

The most important concepts from this lab are:

### Aggregate Functions

```text
COUNT()
SUM()
AVG()
MAX()
MIN()
```

### GROUP BY

```text
GROUP BY = Divide rows into groups
```

### WHERE

```text
WHERE = Filter rows before grouping
```

### DISTINCT

```text
DISTINCT = Remove duplicate values
```

### Main Pattern

```text
                   GROUP BY
                       ↓
              ┌────────────────┐
              │ Create Groups   │
              └───────┬────────┘
                      ↓
              ┌────────────────┐
              │ Aggregate      │
              │ COUNT / SUM    │
              │ AVG / MAX / MIN│
              └───────┬────────┘
                      ↓
                  Result
```

### Remember

```text
COUNT → How many?
SUM   → Total?
AVG   → Average?
MAX   → Highest?
MIN   → Lowest?

"Per / Each / Wise"
        ↓
    GROUP BY

"Only / Where / Whose"
        ↓
      WHERE
```

> **Master the concept instead of memorizing queries. Once you understand how rows become groups and how aggregate functions operate on each group, you can solve all the questions in this lab yourself.**
