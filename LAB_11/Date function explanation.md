# 📘 DBMS Lab 11 — SQL In-Built Functions for Date and Time Handling

<p align="center">
  <img src="https://img.shields.io/badge/DBMS-Date%20%26%20Time%20Functions-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/SQL-Functions-green?style=for-the-badge">
  <img src="https://img.shields.io/badge/MS%20SQL%20Server-red?style=for-the-badge">
</p>

---

## 🎯 Objective

This lab focuses on **Date and Time Functions in MS SQL Server**.

The main concepts are:

- Getting the current date and time
- Adding and subtracting dates
- Finding the difference between dates
- Extracting day, month and year
- Formatting dates
- Finding the last date of a month
- Filtering records using dates
- Grouping records using dates
- Performing calculations using date and time values

> **Note:** This README explains the concepts required to solve the lab. It does not contain solutions to individual lab questions.

---

# 🧠 1. Date and Time Data Types

SQL Server provides different data types for storing date and time values.

| Data Type | Description | Example |
|---|---|---|
| `DATE` | Stores only date | `2026-08-23` |
| `TIME` | Stores only time | `18:30:00` |
| `DATETIME` | Stores date and time | `2026-08-23 18:30:00` |
| `DATETIME2` | Date and time with higher precision | `2026-08-23 18:30:00.1234567` |
| `DATETIMEOFFSET` | Date, time and timezone offset | `2026-08-23 18:30:00 +05:30` |

Example:

```sql
CREATE TABLE Employee
(
    EMP_ID INT,
    EMP_NAME VARCHAR(50),
    JOINING_DATE DATE
);
```

---

# 📅 2. GETDATE()

`GETDATE()` returns the **current date and time** of the SQL Server system.

### Syntax

```sql
GETDATE()
```

### Example

```sql
SELECT GETDATE() AS Today_Date;
```

Example output:

```text
2026-08-23 18:30:25.123
```

The exact value depends on the current date and time.

---

# 🕐 3. SYSDATETIME()

`SYSDATETIME()` also returns the current date and time, but with greater precision.

```sql
SELECT SYSDATETIME() AS Current_Date_Time;
```

### Difference

| Function | Purpose |
|---|---|
| `GETDATE()` | Current date and time |
| `SYSDATETIME()` | Current date and time with higher precision |

For basic queries, `GETDATE()` is commonly used.

---

# ➕ 4. DATEADD()

`DATEADD()` is used to **add or subtract a specific amount of time from a date**.

### Syntax

```sql
DATEADD(datepart, number, date)
```

### Example — Add 5 Years

```sql
SELECT DATEADD(YEAR, 5, GETDATE()) AS Future_Date;
```

### Add 10 Days

```sql
SELECT DATEADD(DAY, 10, GETDATE()) AS Future_Date;
```

### Add 3 Months

```sql
SELECT DATEADD(MONTH, 3, GETDATE()) AS Future_Date;
```

---

# ➖ 5. Subtracting Date Values

A negative number is used with `DATEADD()` to subtract time.

### Example

```sql
SELECT DATEADD(YEAR, -2, GETDATE()) AS Previous_Date;
```

This means:

```text
Current Date
     ↓
Subtract 2 Years
     ↓
Previous Date
```

Another example:

```sql
SELECT DATEADD(MONTH, -3, GETDATE());
```

This subtracts 3 months.

---

# 📌 6. Common DATEADD Date Parts

| Date Part | Meaning |
|---|---|
| `YEAR` | Year |
| `QUARTER` | Quarter |
| `MONTH` | Month |
| `WEEK` | Week |
| `DAY` | Day |
| `HOUR` | Hour |
| `MINUTE` | Minute |
| `SECOND` | Second |

Example:

```sql
SELECT DATEADD(DAY, 10, GETDATE());
```

---

# 🔍 7. DATEPART()

`DATEPART()` is used to **extract a particular part of a date**.

### Syntax

```sql
DATEPART(datepart, date)
```

### Example

```sql
SELECT DATEPART(YEAR, GETDATE()) AS Current_Year;
```

```sql
SELECT DATEPART(MONTH, GETDATE()) AS Current_Month;
```

```sql
SELECT DATEPART(DAY, GETDATE()) AS Current_Day;
```

---

# 📆 8. DAY(), MONTH() and YEAR()

SQL Server also provides simple functions for extracting date parts.

### DAY()

```sql
SELECT DAY(GETDATE()) AS Day_Number;
```

### MONTH()

```sql
SELECT MONTH(GETDATE()) AS Month_Number;
```

### YEAR()

```sql
SELECT YEAR(GETDATE()) AS Year_Number;
```

---

# 🔄 9. DATEPART() vs DAY(), MONTH(), YEAR()

For example:

```sql
SELECT DATEPART(MONTH, GETDATE());
```

and:

```sql
SELECT MONTH(GETDATE());
```

both return the month number.

### Simple Rule

```text
DAY()
    ↓
Day

MONTH()
    ↓
Month

YEAR()
    ↓
Year

DATEPART()
    ↓
Extract a particular date part
```

---

# ⏱️ 10. DATEDIFF()

`DATEDIFF()` is used to find the **difference between two dates**.

### Syntax

```sql
DATEDIFF(datepart, start_date, end_date)
```

### Example

```sql
SELECT
    DATEDIFF(DAY, '2025-01-01', '2025-01-10') AS Difference;
```

Output:

```text
9
```

---

# 📊 11. DATEDIFF() with Different Date Parts

### Difference in Years

```sql
SELECT DATEDIFF(YEAR, '2020-01-01', '2025-01-01');
```

### Difference in Months

```sql
SELECT DATEDIFF(MONTH, '2025-01-01', '2025-06-01');
```

### Difference in Days

```sql
SELECT DATEDIFF(DAY, '2025-01-01', '2025-06-01');
```

### Difference in Hours

```sql
SELECT DATEDIFF(HOUR,
                '2025-01-01 10:00',
                '2025-01-02 15:00');
```

---

# 🧠 12. DATEADD() vs DATEDIFF()

This is an important difference.

| Function | Purpose |
|---|---|
| `DATEADD()` | Add or subtract time |
| `DATEDIFF()` | Find difference between dates |

Example:

```sql
DATEADD(DAY, 10, GETDATE());
```

Means:

> Give me the date 10 days from today.

While:

```sql
DATEDIFF(DAY, '2025-01-01', '2025-01-10');
```

Means:

> Find the difference in days between two dates.

---

# 🗓️ 13. EOMONTH()

`EOMONTH()` returns the **last date of a month**.

### Example

```sql
SELECT EOMONTH(GETDATE()) AS Last_Day;
```

If the current month is August:

```text
2026-08-31
```

---

# 📅 14. EOMONTH() with a Specific Date

```sql
SELECT EOMONTH('2026-02-15') AS Last_Day;
```

Result:

```text
2026-02-28
```

For a leap year:

```sql
SELECT EOMONTH('2024-02-15') AS Last_Day;
```

Result:

```text
2024-02-29
```

---

# ➕ 15. EOMONTH() with Month Offset

You can also find the last date of another month.

### Next Month

```sql
SELECT EOMONTH(GETDATE(), 1);
```

### Previous Month

```sql
SELECT EOMONTH(GETDATE(), -1);
```

---

# 🎨 16. Formatting Dates

Sometimes a date needs to be displayed in a particular format.

SQL Server provides:

```text
FORMAT()
CONVERT()
```

---

# 🔤 17. FORMAT()

`FORMAT()` allows us to display a date in a custom format.

### Example

```sql
SELECT FORMAT(GETDATE(), 'dd MMM yyyy') AS Formatted_Date;
```

Example output:

```text
23 Aug 2026
```

Another example:

```sql
SELECT FORMAT(GETDATE(), 'dd MMMM yyyy');
```

Output:

```text
23 August 2026
```

---

# 📌 18. Common FORMAT() Patterns

| Pattern | Meaning |
|---|---|
| `dd` | Day |
| `MM` | Month number |
| `MMM` | Short month name |
| `MMMM` | Full month name |
| `yy` | 2-digit year |
| `yyyy` | 4-digit year |
| `HH` | Hour |
| `mm` | Minute |
| `ss` | Second |

Example:

```sql
SELECT FORMAT(
    GETDATE(),
    'dd MMM yyyy HH:mm:ss'
) AS Formatted_Date;
```

---

# ⚠️ 19. MM vs mm

This is a common mistake.

```text
MM → Month
mm → Minute
```

Example:

```sql
FORMAT(GETDATE(), 'dd-MM-yyyy');
```

Here `MM` represents the month.

Example:

```sql
FORMAT(GETDATE(), 'HH:mm:ss');
```

Here `mm` represents minutes.

---

# 🔄 20. CONVERT()

`CONVERT()` can convert a value to another data type and can also be used for date formatting.

### Example

```sql
SELECT CONVERT(VARCHAR(10), GETDATE(), 103) AS Formatted_Date;
```

A common output format is:

```text
23/08/2026
```

Another example:

```sql
SELECT CONVERT(VARCHAR(20), GETDATE(), 106);
```

This produces a format similar to:

```text
23 Aug 2026
```

---

# 📊 21. Filtering Records Using Dates

Date functions are useful with `WHERE`.

Suppose the `DEPOSIT` table contains:

```text
ADATE
```

We can filter records using:

```sql
SELECT *
FROM DEPOSIT
WHERE ADATE >= '2025-01-01';
```

This displays records from 1 January 2025 onwards.

---

# 📅 22. Filtering Records by Year

Use `YEAR()`:

```sql
SELECT *
FROM DEPOSIT
WHERE YEAR(ADATE) = 2025;
```

Meaning:

> Display records whose account date belongs to 2025.

---

# 📆 23. Filtering Records by Month

Use `MONTH()`:

```sql
SELECT *
FROM DEPOSIT
WHERE MONTH(ADATE) = 3;
```

Here:

```text
3 = March
```

To check both month and year:

```sql
SELECT *
FROM DEPOSIT
WHERE MONTH(ADATE) = 3
  AND YEAR(ADATE) = 2025;
```

---

# 🔢 24. Filtering Records by Day

Use `DAY()`:

```sql
SELECT *
FROM DEPOSIT
WHERE DAY(ADATE) = 1;
```

This finds records where the day of the month is `1`.

---

# 📊 25. Grouping Data by Year

Date functions can be combined with `GROUP BY`.

Example:

```sql
SELECT
    YEAR(ADATE) AS Account_Year,
    COUNT(*) AS Total_Accounts
FROM DEPOSIT
GROUP BY YEAR(ADATE);
```

Flow:

```text
DEPOSIT
   ↓
Extract YEAR(ADATE)
   ↓
GROUP BY Year
   ↓
COUNT Accounts
```

---

# 📅 26. Grouping Data by Month

Example:

```sql
SELECT
    MONTH(ADATE) AS Account_Month,
    COUNT(*) AS Total_Accounts
FROM DEPOSIT
GROUP BY MONTH(ADATE);
```

This calculates the number of accounts for each month.

---

# ⚠️ 27. Grouping by Month When Multiple Years Exist

If the table contains records from multiple years, this:

```sql
GROUP BY MONTH(ADATE)
```

will combine all January records together, all February records together, etc.

A better approach is:

```sql
SELECT
    YEAR(ADATE) AS Account_Year,
    MONTH(ADATE) AS Account_Month,
    COUNT(*) AS Total_Accounts
FROM DEPOSIT
GROUP BY
    YEAR(ADATE),
    MONTH(ADATE);
```

Now each year and month combination is treated as a separate group.

---

# 💰 28. Aggregate Functions with Dates

Date functions can be combined with aggregate functions.

Example:

```sql
SELECT
    YEAR(ADATE) AS Account_Year,
    SUM(AMOUNT) AS Total_Amount
FROM DEPOSIT
GROUP BY YEAR(ADATE);
```

This calculates the total amount for every year.

Another example:

```sql
SELECT
    MONTH(ADATE) AS Account_Month,
    MAX(AMOUNT) AS Maximum_Amount
FROM DEPOSIT
GROUP BY MONTH(ADATE);
```

---

# 🔎 29. Date Range

A date range can be specified using `BETWEEN`.

Example:

```sql
SELECT *
FROM DEPOSIT
WHERE ADATE BETWEEN '2025-01-01' AND '2025-12-31';
```

This retrieves records within the specified date range.

---

# ⚠️ 30. Date Range with DateTime Columns

If the column contains both date and time, be careful with:

```sql
BETWEEN '2025-01-01' AND '2025-12-31'
```

The second value represents midnight at the start of that date.

A safer approach for a complete year is:

```sql
SELECT *
FROM DEPOSIT
WHERE ADATE >= '2025-01-01'
  AND ADATE < '2026-01-01';
```

This includes the complete year.

---

# ⏳ 31. Difference Between Today and a Stored Date

Suppose `ADATE` contains an account opening date.

We can calculate the number of days since that date:

```sql
SELECT
    ADATE,
    DATEDIFF(DAY, ADATE, GETDATE()) AS Days_Passed
FROM DEPOSIT;
```

Flow:

```text
Account Date
     ↓
GETDATE()
     ↓
DATEDIFF()
     ↓
Number of Days
```

---

# ➕ 32. Adding and Subtracting Time

### Add 5 Years

```sql
SELECT DATEADD(YEAR, 5, GETDATE());
```

### Add 6 Months

```sql
SELECT DATEADD(MONTH, 6, GETDATE());
```

### Add 30 Days

```sql
SELECT DATEADD(DAY, 30, GETDATE());
```

### Subtract 5 Years

```sql
SELECT DATEADD(YEAR, -5, GETDATE());
```

### Subtract 3 Months

```sql
SELECT DATEADD(MONTH, -3, GETDATE());
```

---

# 🧩 33. Common Date Functions Cheat Sheet

| Function | Purpose | Example |
|---|---|---|
| `GETDATE()` | Current date and time | `GETDATE()` |
| `SYSDATETIME()` | Current date/time with precision | `SYSDATETIME()` |
| `DATEADD()` | Add/subtract date part | `DATEADD(DAY, 5, date)` |
| `DATEDIFF()` | Difference between dates | `DATEDIFF(DAY, date1, date2)` |
| `DATEPART()` | Extract date part | `DATEPART(YEAR, date)` |
| `DAY()` | Extract day | `DAY(date)` |
| `MONTH()` | Extract month | `MONTH(date)` |
| `YEAR()` | Extract year | `YEAR(date)` |
| `EOMONTH()` | Last date of month | `EOMONTH(date)` |
| `FORMAT()` | Custom date formatting | `FORMAT(date, 'dd MMM yyyy')` |
| `CONVERT()` | Convert/format values | `CONVERT(VARCHAR, date, style)` |

---

# 🧠 34. How to Identify the Required Function

When reading a question, identify the keyword.

| Question Requirement | Function |
|---|---|
| Current date/time | `GETDATE()` |
| Add years/months/days | `DATEADD()` |
| Subtract years/months/days | `DATEADD()` with negative value |
| Difference between dates | `DATEDIFF()` |
| Extract year | `YEAR()` / `DATEPART()` |
| Extract month | `MONTH()` / `DATEPART()` |
| Extract day | `DAY()` / `DATEPART()` |
| Last date of month | `EOMONTH()` |
| Custom date format | `FORMAT()` |
| Date style conversion | `CONVERT()` |
| Filter by year | `WHERE YEAR(date)` |
| Filter by month | `WHERE MONTH(date)` |
| Group by year | `GROUP BY YEAR(date)` |
| Group by month | `GROUP BY MONTH(date)` |

---

# 🔄 35. Overall Concept Flow

```text
                 DATE / TIME
                     │
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
   Current        Modify        Extract
    Date           Date          Parts
       │             │             │
       ↓             ↓             ↓
  GETDATE()      DATEADD()      YEAR()
  SYSDATETIME()                  MONTH()
                                DAY()
                                DATEPART()
       │
       ↓
   Difference
       │
       ↓
   DATEDIFF()
       │
       ↓
  Month Ending
       │
       ↓
   EOMONTH()
       │
       ↓
   Formatting
       │
       ↓
 FORMAT() / CONVERT()
```

---

# ⭐ 36. Simple Complete Example

Suppose we have an `EMPLOYEE` table containing:

```text
EMP_ID
EMP_NAME
JOINING_DATE
```

We want to display the employee name, joining date, and number of days since joining.

```sql
SELECT
    EMP_NAME,
    JOINING_DATE,
    DATEDIFF(DAY, JOINING_DATE, GETDATE()) AS Days_Passed
FROM EMPLOYEE;
```

### Flow

```text
JOINING_DATE
      ↓
DATEDIFF()
      ↓
Compare with current date
      ↓
Calculate difference
      ↓
Display result
```

---

# ⚠️ 37. Common Mistakes

### Mistake 1 — Confusing DATEADD and DATEDIFF

```text
DATEADD
→ Changes a date

DATEDIFF
→ Calculates difference
```

---

### Mistake 2 — Confusing Month and Minute

```text
MM → Month
mm → Minute
```

---

### Mistake 3 — Using the Wrong DATEADD Part

```sql
DATEADD(DAY, 5, GETDATE())
```

adds 5 days.

```sql
DATEADD(MONTH, 5, GETDATE())
```

adds 5 months.

---

### Mistake 4 — Grouping Only by Month

This:

```sql
GROUP BY MONTH(ADATE)
```

can combine January from different years.

For year + month:

```sql
GROUP BY
    YEAR(ADATE),
    MONTH(ADATE);
```

---

# 🎯 38. Final Revision

Remember:

```text
GETDATE()
→ Current date and time

DATEADD()
→ Add / subtract date or time

DATEDIFF()
→ Difference between dates

DATEPART()
→ Extract a specific date part

DAY()
→ Day

MONTH()
→ Month

YEAR()
→ Year

EOMONTH()
→ Last day of month

FORMAT()
→ Custom date formatting

CONVERT()
→ Convert / format date values
```

---

# 🧠 One-Line Memory Trick

> **GETDATE gets the date → DATEADD changes the date → DATEDIFF compares dates → DATEPART/DAY/MONTH/YEAR extract information → EOMONTH finds month-end → FORMAT/CONVERT controls display.**

---

# 🚀 Quick Practice

```sql
-- Current date and time
SELECT GETDATE();

-- Current date with higher precision
SELECT SYSDATETIME();

-- Add 5 years
SELECT DATEADD(YEAR, 5, GETDATE());

-- Subtract 3 months
SELECT DATEADD(MONTH, -3, GETDATE());

-- Extract year
SELECT YEAR(GETDATE());

-- Extract month
SELECT MONTH(GETDATE());

-- Extract day
SELECT DAY(GETDATE());

-- Difference between two dates
SELECT DATEDIFF(DAY, '2025-01-01', '2025-01-10');

-- Last date of current month
SELECT EOMONTH(GETDATE());

-- Format current date
SELECT FORMAT(GETDATE(), 'dd MMM yyyy');

-- Format date using CONVERT
SELECT CONVERT(VARCHAR(10), GETDATE(), 103);
```

---

# 🎓 Key Takeaway

Date and Time functions allow SQL Server to:

```text
Retrieve
   ↓
Modify
   ↓
Compare
   ↓
Extract
   ↓
Format
   ↓
Filter
   ↓
Group
```

Before solving the lab questions, identify what the question is asking:

```text
Current Date
    ↓
GETDATE()

Add / Subtract
    ↓
DATEADD()

Difference
    ↓
DATEDIFF()

Day / Month / Year
    ↓
DAY() / MONTH() / YEAR()

Extract Date Part
    ↓
DATEPART()

Last Day of Month
    ↓
EOMONTH()

Format Date
    ↓
FORMAT() / CONVERT()

Filter by Date
    ↓
WHERE

Group by Date
    ↓
GROUP BY + YEAR() / MONTH()
```

> **Understand the purpose of each function instead of memorizing individual queries.**
