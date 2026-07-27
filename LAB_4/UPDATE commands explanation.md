# 📘 SQL Lab 4 - UPDATE Queries

![SQL](https://img.shields.io/badge/SQL-Learning-blue)
![Database](https://img.shields.io/badge/Database-MySQL-orange)
![Lab](https://img.shields.io/badge/Lab-4-green)

---

# 📌 Objective

The objective of this lab is to learn how to modify existing data in a database using the **UPDATE** statement.

After completing this lab, students will be able to:

- Update a single column
- Update multiple columns
- Update selected rows
- Update all rows
- Use operators with UPDATE
- Perform calculations while updating values
- Work with NULL values

---

# 📋 STUDENT Table

| STID | SNAME | CITY | BRANCH | SPI |
|------|--------|---------|-----------|------|
|101|DEEP|RAJKOT|COMPUTER|8.50|
|102|RAJ|SURAT|CIVIL|7.20|
|103|HETVI|RAJKOT|COMPUTER|8.00|
|104|PARAG|SURAT|MECHANICAL|7.80|
|105|RIYA|AHMEDABAD|IT|6.90|

---

# What is UPDATE?

The `UPDATE` statement is used to modify existing records in a table.

Unlike INSERT, it does not create new rows.

It changes the values already stored in the table.

---

# Syntax

```sql
UPDATE table_name
SET column_name = value
WHERE condition;
```

---

# Updating a Single Column

A single column can be updated for one or more records.

### Example 1

```sql
UPDATE STUDENT
SET CITY='AHMEDABAD'
WHERE SNAME='HETVI';
```

### Example 2

```sql
UPDATE STUDENT
SET SPI=9.20
WHERE SNAME='DEEP';
```

---

# Updating Multiple Columns

Multiple columns can be updated in a single query.

### Syntax

```sql
UPDATE table_name
SET column1=value1,
    column2=value2
WHERE condition;
```

### Example 1

```sql
UPDATE STUDENT
SET SPI=8.50,
    CITY='VADODARA'
WHERE SNAME='DEEP';
```

### Example 2

```sql
UPDATE STUDENT
SET BRANCH='IT',
    CITY='SURAT'
WHERE STID=105;
```

---

# Updating All Rows

If the WHERE clause is omitted, every row in the table is updated.

### Example

```sql
UPDATE STUDENT
SET BRANCH='IT';
```

Every student's branch becomes IT.

⚠️ Be careful while omitting the WHERE clause.

---

# WHERE Clause

The WHERE clause specifies which rows should be updated.

### Example 1

```sql
UPDATE STUDENT
SET CITY='RAJKOT'
WHERE STID=101;
```

### Example 2

```sql
UPDATE STUDENT
SET SPI=8.00
WHERE BRANCH='CIVIL';
```

---

# Comparison Operators

Comparison operators help select rows.

| Operator | Meaning |
|----------|----------|
| = | Equal |
| > | Greater Than |
| < | Less Than |
| >= | Greater Than or Equal |
| <= | Less Than or Equal |
| <> | Not Equal |

---

## Equal (=)

```sql
UPDATE STUDENT
SET CITY='SURAT'
WHERE STID=101;
```

---

## Greater Than (>)

```sql
UPDATE STUDENT
SET CITY='RAJKOT'
WHERE SPI>8.0;
```

---

## Less Than (<)

```sql
UPDATE STUDENT
SET CITY='SURAT'
WHERE SPI<7.0;
```

---

## Greater Than or Equal (>=)

```sql
UPDATE STUDENT
SET BRANCH='IT'
WHERE SPI>=8.0;
```

---

## Less Than or Equal (<=)

```sql
UPDATE STUDENT
SET CITY='VADODARA'
WHERE SPI<=7.5;
```

---

## Not Equal (<>)

```sql
UPDATE STUDENT
SET CITY='RAJKOT'
WHERE BRANCH<>'COMPUTER';
```

---

# AND Operator

The AND operator updates rows only when all conditions are true.

### Example 1

```sql
UPDATE STUDENT
SET CITY='SURAT'
WHERE BRANCH='CIVIL'
AND SPI>7;
```

### Example 2

```sql
UPDATE STUDENT
SET SPI=8.50
WHERE CITY='RAJKOT'
AND BRANCH='COMPUTER';
```

---

# BETWEEN Operator

BETWEEN selects values within a range.

### Example 1

```sql
UPDATE STUDENT
SET SPI=7.50
WHERE STID BETWEEN 103 AND 107;
```

### Example 2

```sql
UPDATE STUDENT
SET CITY='SURAT'
WHERE SPI BETWEEN 6 AND 7;
```

---

# Arithmetic Operations

UPDATE can perform calculations.

---

## Increase by 10%

```sql
UPDATE STUDENT
SET SPI=SPI*1.10;
```

---

## Increase by 20%

```sql
UPDATE STUDENT
SET SPI=SPI*1.20;
```

---

## Add 0.50

```sql
UPDATE STUDENT
SET SPI=SPI+0.50;
```

---

## Subtract 1

```sql
UPDATE STUDENT
SET SPI=SPI-1;
```

---

# NULL Values

NULL means no value or unknown value.

It is different from zero.

---

# Updating NULL

### Example

```sql
UPDATE STUDENT
SET SPI=NULL
WHERE STID=110;
```

---

# IS NULL

Used to find NULL values.

### Example 1

```sql
SELECT *
FROM STUDENT
WHERE SPI IS NULL;
```

### Example 2

```sql
SELECT *
FROM STUDENT
WHERE BRANCH IS NULL;
```

---

# IS NOT NULL

Finds rows having values.

### Example 1

```sql
SELECT *
FROM STUDENT
WHERE SPI IS NOT NULL;
```

### Example 2

```sql
SELECT *
FROM STUDENT
WHERE BRANCH IS NOT NULL;
```

---

# SQL Execution Order

```
UPDATE
↓

SET
↓

WHERE
```

---

# Common Mistakes

## ❌ Forgetting WHERE

```sql
UPDATE STUDENT
SET CITY='SURAT';
```

This updates every row.

---

## ✅ Correct

```sql
UPDATE STUDENT
SET CITY='SURAT'
WHERE STID=101;
```

---

## ❌ Wrong NULL

```sql
WHERE SPI=NULL
```

---

## ✅ Correct

```sql
WHERE SPI IS NULL
```

---

# Best Practices

✅ Always check your WHERE condition.

✅ Use SELECT before UPDATE to verify affected rows.

✅ Backup important data.

✅ Update only required columns.

✅ Test queries on sample data first.

---

# Summary

| Concept | Purpose |
|----------|----------|
| UPDATE | Modify existing records |
| SET | Assign new values |
| WHERE | Select rows to update |
| AND | Multiple conditions |
| BETWEEN | Update range of rows |
| Arithmetic Operators | Increase or decrease values |
| NULL | Missing value |
| IS NULL | Find NULL values |
| IS NOT NULL | Find existing values |

---

# 🎯 Learning Outcome

After completing this lab, students will be able to:

- Update existing records
- Modify one or multiple columns
- Use conditions with UPDATE
- Perform mathematical updates
- Handle NULL values correctly
- Write safe and efficient UPDATE queries

---

⭐ Happy Learning SQL ⭐
