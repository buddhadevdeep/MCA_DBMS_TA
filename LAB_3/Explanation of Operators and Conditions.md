# 📘 SQL Lab 3 - SELECT Queries Using Operators and Conditions

![SQL](https://img.shields.io/badge/SQL-Learning-blue)
![Database](https://img.shields.io/badge/Database-MySQL-orange)
![Lab](https://img.shields.io/badge/Lab-3-green)

---

# 📌 Objective

This lab helps students understand how to retrieve data from a database using:

- SELECT Statement
- WHERE Clause
- Comparison Operators
- Logical Operators
- IN / NOT IN
- BETWEEN
- NULL Values
- DISTINCT
- LIMIT / TOP

---

# 📋 STUDENT Table

Assume the following table:

| ID | NAME | CITY | BRANCH | SPI |
|----|-------|--------|----------|------|
| 101 | DEEP | RAJKOT | COMPUTER | 8.5 |
| 102 | RAHUL | SURAT | CIVIL | 7.8 |
| 103 | PRIYA | RAJKOT | CHEMICAL | 9.1 |
| 104 | AMIT | AHMEDABAD | COMPUTER | 8.9 |
| 105 | RIYA | SURAT | MECHANICAL | 7.2 |

---

# 1️⃣ SELECT Statement

## What is SELECT?

The `SELECT` statement is used to retrieve data from a table.

### Syntax

```sql
SELECT column_name
FROM table_name;
```

### Example 1

```sql
SELECT * FROM STUDENT;
```

Displays all columns and rows.

### Example 2

```sql
SELECT NAME, CITY
FROM STUDENT;
```

Displays only name and city.

---

# 2️⃣ WHERE Clause

## What is WHERE?

WHERE filters records based on a condition.

### Syntax

```sql
SELECT *
FROM table_name
WHERE condition;
```

### Example 1

```sql
SELECT *
FROM STUDENT
WHERE BRANCH='COMPUTER';
```

### Example 2

```sql
SELECT *
FROM STUDENT
WHERE SPI>8.0;
```

---

# 3️⃣ Comparison Operators

| Operator | Meaning |
|-----------|----------|
| = | Equal |
| > | Greater Than |
| < | Less Than |
| >= | Greater Than or Equal |
| <= | Less Than or Equal |
| <> | Not Equal |
| != | Not Equal |

---

## Equal (=)

### Example

```sql
SELECT *
FROM STUDENT
WHERE CITY='RAJKOT';
```

---

## Greater Than (>)

### Example

```sql
SELECT *
FROM STUDENT
WHERE SPI>8.0;
```

---

## Less Than (<)

### Example

```sql
SELECT *
FROM STUDENT
WHERE ID<104;
```

---

## Greater Than or Equal (>=)

### Example

```sql
SELECT *
FROM STUDENT
WHERE SPI>=7.0;
```

---

## Less Than or Equal (<=)

### Example

```sql
SELECT *
FROM STUDENT
WHERE SPI<=8.0;
```

---

## Not Equal (<>)

### Example

```sql
SELECT *
FROM STUDENT
WHERE BRANCH<>'COMPUTER';
```

---

## Not Equal (!=)

### Example

```sql
SELECT *
FROM STUDENT
WHERE CITY!='SURAT';
```

---

# 4️⃣ AND Operator

## What is AND?

Returns rows when all conditions are true.

### Syntax

```sql
condition1 AND condition2
```

### Example 1

```sql
SELECT *
FROM STUDENT
WHERE BRANCH='COMPUTER'
AND SPI>8.0;
```

### Example 2

```sql
SELECT *
FROM STUDENT
WHERE CITY='RAJKOT'
AND ID>101;
```

---

# 5️⃣ OR Operator

## What is OR?

Returns rows when at least one condition is true.

### Example 1

```sql
SELECT *
FROM STUDENT
WHERE CITY='RAJKOT'
OR CITY='SURAT';
```

### Example 2

```sql
SELECT *
FROM STUDENT
WHERE BRANCH='COMPUTER'
OR BRANCH='CIVIL';
```

---

# 6️⃣ NOT Operator

## What is NOT?

Reverses a condition.

### Example 1

```sql
SELECT *
FROM STUDENT
WHERE NOT BRANCH='COMPUTER';
```

### Example 2

```sql
SELECT *
FROM STUDENT
WHERE NOT CITY='RAJKOT';
```

---

# 7️⃣ IN Operator

## What is IN?

Checks multiple values.

### Syntax

```sql
column IN(value1,value2)
```

### Example 1

```sql
SELECT *
FROM STUDENT
WHERE CITY IN('RAJKOT','SURAT');
```

### Example 2

```sql
SELECT *
FROM STUDENT
WHERE BRANCH IN('COMPUTER','CIVIL');
```

---

# 8️⃣ NOT IN Operator

## What is NOT IN?

Excludes multiple values.

### Example 1

```sql
SELECT *
FROM STUDENT
WHERE CITY NOT IN('RAJKOT','SURAT');
```

### Example 2

```sql
SELECT *
FROM STUDENT
WHERE BRANCH NOT IN('COMPUTER','CIVIL');
```

---

# 9️⃣ BETWEEN Operator

## What is BETWEEN?

Checks values inside a range.

### Syntax

```sql
column BETWEEN value1 AND value2
```

### Example 1

```sql
SELECT *
FROM STUDENT
WHERE SPI BETWEEN 7 AND 9;
```

### Example 2

```sql
SELECT *
FROM STUDENT
WHERE ID BETWEEN 101 AND 104;
```

---

# 🔟 IS NULL

## What is NULL?

NULL means missing or unknown value.

### Example 1

```sql
SELECT *
FROM STUDENT
WHERE CITY IS NULL;
```

### Example 2

```sql
SELECT *
FROM STUDENT
WHERE BRANCH IS NULL;
```

---

# 1️⃣1️⃣ IS NOT NULL

### Example 1

```sql
SELECT *
FROM STUDENT
WHERE CITY IS NOT NULL;
```

### Example 2

```sql
SELECT *
FROM STUDENT
WHERE SPI IS NOT NULL;
```

---

# 1️⃣2️⃣ DISTINCT

## What is DISTINCT?

Removes duplicate values.

### Example 1

```sql
SELECT DISTINCT BRANCH
FROM STUDENT;
```

### Example 2

```sql
SELECT DISTINCT CITY
FROM STUDENT;
```

---

# 1️⃣3️⃣ LIMIT (MySQL)

Returns limited rows.

### Example 1

```sql
SELECT *
FROM STUDENT
LIMIT 5;
```

### Example 2

```sql
SELECT *
FROM STUDENT
LIMIT 3;
```

---

# 1️⃣4️⃣ TOP (SQL Server)

### Example 1

```sql
SELECT TOP 5 *
FROM STUDENT;
```

### Example 2

```sql
SELECT TOP 50 PERCENT *
FROM STUDENT;
```

---

# 1️⃣5️⃣ Combining Operators

### Example 1

```sql
SELECT *
FROM STUDENT
WHERE SPI>8
AND CITY='RAJKOT';
```

### Example 2

```sql
SELECT *
FROM STUDENT
WHERE BRANCH IN('COMPUTER','CIVIL')
AND SPI>7;
```

---

# SQL Execution Order

SQL executes in this order:

```
FROM
↓
WHERE
↓
SELECT
↓
ORDER BY
↓
LIMIT
```

---

# Common Mistakes

❌ Wrong

```sql
WHERE CITY = NULL
```

✅ Correct

```sql
WHERE CITY IS NULL
```

---

❌ Wrong

```sql
CITY='RAJKOT'
OR CITY='SURAT'
OR CITY='AHMEDABAD'
```

✅ Better

```sql
CITY IN('RAJKOT','SURAT','AHMEDABAD')
```

---

# Best Practices

✅ Use specific columns instead of `*`

✅ Use IN instead of multiple OR

✅ Use BETWEEN for ranges

✅ Handle NULL properly

✅ Write SQL keywords in uppercase

---

# Summary Table

| Concept | Purpose |
|----------|----------|
| SELECT | Retrieve data |
| WHERE | Filter rows |
| = | Equal |
| > | Greater than |
| < | Less than |
| >= | Greater than equal |
| <= | Less than equal |
| <> | Not equal |
| AND | All conditions true |
| OR | Any condition true |
| NOT | Reverse condition |
| IN | Multiple values |
| NOT IN | Exclude values |
| BETWEEN | Range |
| IS NULL | Missing value |
| IS NOT NULL | Existing value |
| DISTINCT | Remove duplicates |
| LIMIT | Limit rows |
| TOP | Limit rows (SQL Server) |

---

# 🎯 Learning Outcome

After completing this lab, students will be able to:

✔ Retrieve data

✔ Filter records

✔ Use operators

✔ Work with conditions

✔ Handle NULL values

✔ Remove duplicate data

✔ Limit results

✔ Write efficient SQL queries

---

⭐ Happy Learning SQL ⭐
