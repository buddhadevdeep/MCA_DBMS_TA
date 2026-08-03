# 📘 DBMS Lab 7 - SQL Pattern Searching Using LIKE Operator (MS SQL Server)

<p align="center">
  <img src="https://img.shields.io/badge/DBMS-LIKE%20Operator-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/MS%20SQL-Pattern%20Searching-green?style=for-the-badge">
  <img src="https://img.shields.io/badge/Level-Beginner-orange?style=for-the-badge">
</p>

---

# 📖 Introduction

The **LIKE** operator is used in SQL to search for data that matches a specific pattern.

It is mainly used with the **WHERE** clause to filter records based on text values.

The LIKE operator is useful when you don't know the exact value but know part of the text.

---

# Why Use LIKE?

The LIKE operator helps us to:

- Search names starting with a specific letter.
- Search names ending with a specific letter.
- Search words containing a specific text.
- Find records with a fixed number of characters.
- Perform flexible pattern matching.

---

# Syntax

```sql
SELECT column_name
FROM table_name
WHERE column_name LIKE 'pattern';
```

Example

```sql
SELECT *
FROM Employee
WHERE FirstName LIKE 'A%';
```

---

# Wildcards Used in MS SQL Server

|Wildcard|Meaning|
|----------|--------|
|%|Zero or more characters|
|_|Exactly one character|
|[ ]|Any one character inside brackets|
|[^ ]|Any one character NOT inside brackets|

---

# Sample Employee Table

|EmpID|FirstName|LastName|City|Department|
|------|---------|---------|---------|------------|
|101|Harsh|Patel|Rajkot|IT|
|102|Amit|Shah|Ahmedabad|HR|
|103|Riya|Joshi|Surat|Finance|
|104|Dhruv|Patel|Rajkot|IT|

---

# 1. Starts With (%)

Find employees whose name starts with **H**.

```sql
SELECT *
FROM Employee
WHERE FirstName LIKE 'H%';
```

Result

```
Harsh
```

---

# 2. Ends With (%)

Find employees whose last name ends with **EL**.

```sql
SELECT *
FROM Employee
WHERE LastName LIKE '%EL';
```

---

# 3. Contains (%)

Find employees whose first name contains **AR**.

```sql
SELECT *
FROM Employee
WHERE FirstName LIKE '%AR%';
```

---

# 4. Exactly One Character (_)

Find names having exactly 5 characters.

```sql
SELECT *
FROM Employee
WHERE FirstName LIKE '_____';
```

Each underscore (_) represents one character.

---

# 5. Starts and Ends With

Find names starting with **R** and ending with **A**.

```sql
SELECT *
FROM Employee
WHERE FirstName LIKE 'R%A';
```

---

# 6. Second Character

Find names whose second character is **A**.

```sql
SELECT *
FROM Employee
WHERE FirstName LIKE '_A%';
```

---

# 7. Third Character

Find names whose third character is **S**.

```sql
SELECT *
FROM Employee
WHERE FirstName LIKE '__S%';
```

---

# 8. Ends With Specific Character

Find cities ending with **T**.

```sql
SELECT *
FROM Employee
WHERE City LIKE '%T';
```

---

# 9. Starts With Multiple Letters

Find cities starting with **R** or **B**.

```sql
SELECT *
FROM Employee
WHERE City LIKE '[RB]%';
```

---

# 10. Starts With Range

Find names starting from A to H.

```sql
SELECT *
FROM Employee
WHERE FirstName LIKE '[A-H]%';
```

---

# 11. Does Not Start With

Find cities not starting with B.

```sql
SELECT *
FROM Employee
WHERE City LIKE '[^B]%';
```

---

# 12. Multiple Conditions

```sql
SELECT *
FROM Employee
WHERE FirstName LIKE '%A%'
AND Department IS NOT NULL;
```

---

# LIKE with WHERE Clause

```sql
SELECT *
FROM Employee
WHERE City LIKE 'R%';
```

---

# LIKE with ORDER BY

```sql
SELECT *
FROM Employee
WHERE FirstName LIKE '%A%'
ORDER BY FirstName;
```

---

# LIKE with NULL

NULL values cannot be searched using LIKE.

Wrong

```sql
WHERE City LIKE NULL
```

Correct

```sql
WHERE City IS NULL
```

---

# Wildcard Summary

|Pattern|Meaning|Example|
|---------|--------|---------|
|'A%'|Starts with A|Amit|
|'%A'|Ends with A|Riya|
|'%AR%'|Contains AR|Harsh|
|'_____'|Exactly 5 characters|Harsh|
|'_A%'|Second character A|Harsh|
|'__S%'|Third character S|Asha|
|'[ABC]%'|Starts with A, B or C|Amit|
|'[A-H]%'|Starts from A to H|Harsh|
|'[^A]%'|Does not start with A|Rahul|

---

# Difference Between % and _

|%|_|
|--|--|
|Matches zero or more characters|Matches exactly one character|
|Flexible length|Fixed length|
|'A%' → Amit, Anand, A|'A_' → An|

---

# Common Errors

❌ Wrong

```sql
WHERE Name = 'A%'
```

✅ Correct

```sql
WHERE Name LIKE 'A%'
```

---

❌ Wrong

```sql
LIKE '%'
```

without WHERE clause.

---

# Advantages

- Easy pattern searching.
- Flexible filtering.
- Supports multiple wildcards.
- Improves searching capability.
- Frequently used in reports and applications.

---

# Limitations

- Mainly used with character data.
- Searching with `%` at the beginning may reduce performance.
- Cannot be used to compare NULL values.

---

# Interview Questions

### 1. What is the LIKE operator?

The LIKE operator is used to search records matching a specific pattern.

---

### 2. Which wildcard matches any number of characters?

```
%
```

---

### 3. Which wildcard matches exactly one character?

```
_
```

---

### 4. Which wildcard matches characters between A and H?

```sql
[A-H]
```

---

### 5. Which operator is used for pattern searching?

```
LIKE
```

---

# Summary

|Pattern|Description|
|---------|------------|
|A%|Starts with A|
|%A|Ends with A|
|%AR%|Contains AR|
|_____|Exactly 5 characters|
|_A%|Second character A|
|__S%|Third character S|
|[ABC]%|Starts with A, B or C|
|[A-H]%|Starts between A and H|
|[^A]%|Does not start with A|

---

# Practice Questions

1. Find employees whose name starts with M.
2. Find employees whose city ends with T.
3. Find names containing AN.
4. Find names having exactly six characters.
5. Find cities starting with A or R.
6. Find names whose second character is E.
7. Find names whose third character is A.
8. Find cities not starting with S.
9. Find names starting from A to F.
10. Find employees whose department is not NULL.

---

# Key Takeaways

- **LIKE** is used for pattern matching.
- `%` represents **zero or more characters**.
- `_` represents **exactly one character**.
- `[ ]` matches any one character from a list or range.
- `[^ ]` matches any character **not** in the list.
- LIKE is always used with the **WHERE** clause.
- It is one of the most frequently asked SQL topics in interviews and practical exams.

---

# Conclusion

The **LIKE Operator** is one of the most powerful SQL filtering tools used to search text based on patterns. By combining **%**, **_**, **[]**, and **[^]** wildcards, users can perform flexible and efficient searches in SQL Server databases. Mastering the LIKE operator is essential for DBMS practicals, projects, and technical interviews.

⭐ If this README helped you, don't forget to give the repository a **Star**!
