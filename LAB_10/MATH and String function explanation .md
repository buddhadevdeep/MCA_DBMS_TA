# 📘 SQL Lab 10 – In-Built Functions for Mathematical and String Operations

![SQL](https://img.shields.io/badge/SQL-Learning-blue)
![Database](https://img.shields.io/badge/Database-SQL-orange)
![Lab](https://img.shields.io/badge/Lab-10-green)

---

# 🎯 Objective

The objective of this lab is to understand and use SQL **built-in functions** for:

- Mathematical operations
- Numeric calculations
- Rounding numbers
- Finding absolute values
- Finding powers and square roots
- Logarithmic calculations
- Trigonometric calculations
- Random number generation
- String manipulation
- String length
- Uppercase and lowercase conversion
- Extracting characters
- Replacing characters
- Removing spaces
- Combining strings
- Reversing strings
- Repeating strings
- Type conversion

---

# 📚 Prerequisites

Before starting this lab, students should know:

- Basic SQL
- `SELECT`
- `FROM`
- `WHERE`
- Basic operators
- Tables and columns
- Basic numeric and string data types

---

# 📖 What are SQL Built-In Functions?

SQL provides many predefined functions that perform common operations.

For example:

```sql
SELECT ABS(-25);
```

Output:

```text
25
```

The function performs the calculation automatically.

---

# 🧩 Types of Functions in This Lab

This lab mainly covers:

```text
SQL Built-In Functions
│
├── Mathematical Functions
│   ├── ABS()
│   ├── CEILING()
│   ├── FLOOR()
│   ├── POWER()
│   ├── SQRT()
│   ├── PI()
│   ├── ROUND()
│   ├── EXP()
│   ├── LOG()
│   ├── LOG10()
│   ├── SIN()
│   ├── COS()
│   ├── TAN()
│   ├── SIGN()
│   └── RAND()
│
└── String Functions
    ├── LEN()
    ├── LOWER()
    ├── UPPER()
    ├── LEFT()
    ├── RIGHT()
    ├── SUBSTRING()
    ├── REPLACE()
    ├── ASCII()
    ├── CHAR()
    ├── LTRIM()
    ├── RTRIM()
    ├── SPACE()
    ├── CONCAT()
    ├── REVERSE()
    └── REPLICATE()
```

> **Note:** Examples in this README primarily use **SQL Server syntax**, because functions such as `LEN()`, `CHAR()`, `REPLICATE()`, and `CONVERT()` are commonly used in SQL Server.

---

# 🔢 PART A – MATHEMATICAL FUNCTIONS

Mathematical functions are used to perform calculations on numeric values.

---

# 1. ABS()

## What is ABS()?

`ABS()` returns the **absolute value** of a number.

An absolute value removes the negative sign.

### Syntax

```sql
ABS(number)
```

### Example 1

```sql
SELECT ABS(-25);
```

Output:

```text
25
```

### Example 2

```sql
SELECT ABS(50);
```

Output:

```text
50
```

### Simple Rule

```text
ABS(-10) → 10
ABS(10)  → 10
ABS(0)   → 0
```

---

# 2. CEILING()

## What is CEILING()?

`CEILING()` returns the **smallest integer greater than or equal to the given number**.

In simple words:

> It rounds a decimal number upward.

### Example 1

```sql
SELECT CEILING(25.2);
```

Output:

```text
26
```

### Example 2

```sql
SELECT CEILING(25.7);
```

Output:

```text
26
```

### Example 3

```sql
SELECT CEILING(-25.2);
```

Output:

```text
-25
```

### Remember

```text
CEILING(25.2) → 26
CEILING(25.7) → 26
```

---

# 3. FLOOR()

## What is FLOOR()?

`FLOOR()` returns the **largest integer less than or equal to the given number**.

In simple words:

> It rounds a decimal number downward.

### Example 1

```sql
SELECT FLOOR(25.2);
```

Output:

```text
25
```

### Example 2

```sql
SELECT FLOOR(25.7);
```

Output:

```text
25
```

### Example 3

```sql
SELECT FLOOR(-25.2);
```

Output:

```text
-26
```

---

# CEILING() vs FLOOR()

| Function | Purpose |
|---|---|
| `CEILING()` | Rounds upward |
| `FLOOR()` | Rounds downward |

Example:

```sql
SELECT CEILING(25.7);
```

Result:

```text
26
```

```sql
SELECT FLOOR(25.7);
```

Result:

```text
25
```

---

# 4. % Modulus Operator

The `%` operator returns the **remainder** after division.

### Syntax

```sql
number1 % number2
```

### Example 1

```sql
SELECT 5 % 2;
```

Output:

```text
1
```

Because:

```text
5 ÷ 2

Quotient = 2
Remainder = 1
```

### Example 2

```sql
SELECT 5 % 3;
```

Output:

```text
2
```

### Example 3

```sql
SELECT 10 % 5;
```

Output:

```text
0
```

---

# 5. POWER()

## What is POWER()?

`POWER()` calculates the power of a number.

### Syntax

```sql
POWER(number, power)
```

### Example 1

Find:

```text
2³
```

```sql
SELECT POWER(2, 3);
```

Output:

```text
8
```

### Example 2

```sql
SELECT POWER(5, 2);
```

Output:

```text
25
```

---

# 6. SQRT()

## What is SQRT()?

`SQRT()` returns the square root of a number.

### Example 1

```sql
SELECT SQRT(25);
```

Output:

```text
5
```

### Example 2

```sql
SELECT SQRT(100);
```

Output:

```text
10
```

---

# 7. PI()

## What is PI()?

`PI()` returns the mathematical value of π.

Approximately:

```text
3.141592653589793
```

### Example

```sql
SELECT PI();
```

---

# 8. ROUND()

## What is ROUND()?

`ROUND()` rounds a number to a specified number of decimal places.

### Syntax

```sql
ROUND(number, decimal_places)
```

### Example 1

```sql
SELECT ROUND(157.732, 2);
```

Output:

```text
157.73
```

### Example 2

```sql
SELECT ROUND(157.732, 1);
```

Output:

```text
157.7
```

### Example 3

```sql
SELECT ROUND(157.732, 0);
```

Output:

```text
158
```

---

# ROUND() – Easy Understanding

```text
157.732

ROUND(..., 2) → 157.73
ROUND(..., 1) → 157.7
ROUND(..., 0) → 158
```

---

# 9. EXP()

## What is EXP()?

`EXP()` returns:

```text
e^number
```

where `e` is approximately:

```text
2.71828
```

### Example

```sql
SELECT EXP(2);
```

This calculates:

```text
e²
```

---

# 10. LOG()

## What is LOG()?

`LOG()` calculates the natural logarithm by default.

### Example

```sql
SELECT LOG(10);
```

---

## LOG() with a Base

In SQL Server, a base can also be supplied.

```sql
SELECT LOG(8, 2);
```

This means:

```text
log₂(8)
```

Result:

```text
3
```

---

# 11. LOG10()

## What is LOG10()?

`LOG10()` calculates the base-10 logarithm.

### Example

```sql
SELECT LOG10(100);
```

Output:

```text
2
```

Because:

```text
10² = 100
```

---

# LOG() vs LOG10()

| Function | Meaning |
|---|---|
| `LOG()` | Natural logarithm by default |
| `LOG10()` | Base-10 logarithm |

---

# 12. SIN()

## What is SIN()?

`SIN()` returns the sine of an angle.

The angle must be supplied in **radians**.

### Example

```sql
SELECT SIN(PI()/2);
```

Output is approximately:

```text
1
```

---

# 13. COS()

## What is COS()?

`COS()` returns the cosine of an angle in radians.

### Example

```sql
SELECT COS(0);
```

Output:

```text
1
```

---

# 14. TAN()

## What is TAN()?

`TAN()` returns the tangent of an angle in radians.

### Example

```sql
SELECT TAN(0);
```

Output:

```text
0
```

---

# SIN(), COS(), TAN()

| Function | Purpose |
|---|---|
| `SIN()` | Sine |
| `COS()` | Cosine |
| `TAN()` | Tangent |

---

# 15. SIGN()

## What is SIGN()?

`SIGN()` tells whether a number is:

- Positive
- Negative
- Zero

### Example 1

```sql
SELECT SIGN(25);
```

Output:

```text
1
```

### Example 2

```sql
SELECT SIGN(-25);
```

Output:

```text
-1
```

### Example 3

```sql
SELECT SIGN(0);
```

Output:

```text
0
```

### Easy Rule

```text
Positive → 1
Negative → -1
Zero     → 0
```

---

# 16. RAND()

## What is RAND()?

`RAND()` generates a pseudo-random decimal number between `0` and `1`.

### Example

```sql
SELECT RAND();
```

Possible output:

```text
0.684523
```

The exact result changes.

---

## Generate a Random Integer

For example, generate a random number from 1 to 100:

```sql
SELECT FLOOR(RAND() * 100) + 1;
```

---

# 🧮 Mathematical Functions – Quick Revision

| Function | Purpose | Example |
|---|---|---|
| `ABS()` | Absolute value | `ABS(-25)` |
| `CEILING()` | Round upward | `CEILING(25.7)` |
| `FLOOR()` | Round downward | `FLOOR(25.7)` |
| `%` | Remainder | `5 % 2` |
| `POWER()` | Power | `POWER(2,3)` |
| `SQRT()` | Square root | `SQRT(25)` |
| `PI()` | π value | `PI()` |
| `ROUND()` | Round decimal | `ROUND(157.732,2)` |
| `EXP()` | e^x | `EXP(2)` |
| `LOG()` | Logarithm | `LOG(10)` |
| `LOG10()` | Base-10 log | `LOG10(100)` |
| `SIN()` | Sine | `SIN(0)` |
| `COS()` | Cosine | `COS(0)` |
| `TAN()` | Tangent | `TAN(0)` |
| `SIGN()` | Sign of number | `SIGN(-10)` |
| `RAND()` | Random number | `RAND()` |

---

# 🔤 PART B – STRING FUNCTIONS

String functions are used to manipulate text.

For example:

```text
"Deep"
"Darshan University"
"Computer Science"
```

SQL provides functions to:

- Find string length
- Convert uppercase/lowercase
- Extract characters
- Replace characters
- Remove spaces
- Combine strings
- Reverse strings
- Repeat strings

---

# 17. LEN()

## What is LEN()?

`LEN()` returns the number of characters in a string.

### Syntax

```sql
LEN(string)
```

### Example 1

```sql
SELECT LEN('hello');
```

Output:

```text
5
```

### Example 2

```sql
SELECT LEN('Darshan');
```

Output:

```text
7
```

---

## LEN() and Spaces

In SQL Server, `LEN()` does not count trailing spaces.

Example:

```sql
SELECT LEN('Hello   ');
```

The trailing spaces are not counted.

---

# 18. LOWER()

## What is LOWER()?

`LOWER()` converts text into lowercase.

### Example 1

```sql
SELECT LOWER('DARSHAN');
```

Output:

```text
darshan
```

### Example 2

```sql
SELECT LOWER('HELLO WORLD');
```

Output:

```text
hello world
```

---

# 19. UPPER()

## What is UPPER()?

`UPPER()` converts text into uppercase.

### Example 1

```sql
SELECT UPPER('darshan');
```

Output:

```text
DARSHAN
```

### Example 2

```sql
SELECT UPPER('hello world');
```

Output:

```text
HELLO WORLD
```

---

# LOWER() vs UPPER()

| Function | Result |
|---|---|
| `LOWER()` | Lowercase |
| `UPPER()` | Uppercase |

Example:

```sql
SELECT LOWER('HELLO');
```

```text
hello
```

```sql
SELECT UPPER('hello');
```

```text
HELLO
```

---

# 20. LEFT()

## What is LEFT()?

`LEFT()` returns a specified number of characters from the **left side** of a string.

### Syntax

```sql
LEFT(string, number_of_characters)
```

### Example 1

```sql
SELECT LEFT('DARSHAN', 3);
```

Output:

```text
DAR
```

### Example 2

```sql
SELECT LEFT('COMPUTER', 4);
```

Output:

```text
COMP
```

---

# 21. RIGHT()

## What is RIGHT()?

`RIGHT()` returns a specified number of characters from the **right side**.

### Example 1

```sql
SELECT RIGHT('DARSHAN', 3);
```

Output:

```text
HAN
```

### Example 2

```sql
SELECT RIGHT('COMPUTER', 4);
```

Output:

```text
UTER
```

---

# LEFT() vs RIGHT()

For:

```text
DARSHAN
```

```sql
LEFT('DARSHAN', 3)
```

returns:

```text
DAR
```

while:

```sql
RIGHT('DARSHAN', 3)
```

returns:

```text
HAN
```

---

# 22. SUBSTRING()

## What is SUBSTRING()?

`SUBSTRING()` extracts characters from a string starting from a specified position.

### Syntax

```sql
SUBSTRING(string, start_position, length)
```

### Example

```sql
SELECT SUBSTRING('DARSHAN', 3, 3);
```

Output:

```text
RSH
```

Explanation:

```text
D A R S H A N
1 2 3 4 5 6 7
```

Starting from position `3`:

```text
RSH
```

---

# 23. REPLACE()

## What is REPLACE()?

`REPLACE()` replaces one string with another string.

### Syntax

```sql
REPLACE(string, old_value, new_value)
```

### Example 1

```sql
SELECT REPLACE('abc123def', '123', 'XYZ');
```

Output:

```text
abcXYZdef
```

### Example 2

Replace `abc` with `xyz`:

```sql
SELECT REPLACE('abcabc', 'abc', 'xyz');
```

Output:

```text
xyzxyz
```

---

# 24. ASCII()

## What is ASCII()?

`ASCII()` returns the ASCII code of the first character.

### Example

```sql
SELECT ASCII('A');
```

Output:

```text
65
```

Another example:

```sql
SELECT ASCII('a');
```

Output:

```text
97
```

---

# 25. CHAR()

## What is CHAR()?

`CHAR()` converts an ASCII code into a character.

### Example

```sql
SELECT CHAR(65);
```

Output:

```text
A
```

### Example

```sql
SELECT CHAR(97);
```

Output:

```text
a
```

---

# ASCII() vs CHAR()

These functions work in opposite directions.

```text
ASCII()
Character → Number
```

Example:

```sql
SELECT ASCII('A');
```

```text
65
```

And:

```text
CHAR()
Number → Character
```

Example:

```sql
SELECT CHAR(65);
```

```text
A
```

---

# 26. LTRIM()

## What is LTRIM()?

`LTRIM()` removes spaces from the **left side** of a string.

### Example

```sql
SELECT LTRIM('     Hello');
```

Output:

```text
Hello
```

---

# 27. RTRIM()

## What is RTRIM()?

`RTRIM()` removes spaces from the **right side** of a string.

### Example

```sql
SELECT RTRIM('Hello     ');
```

Output:

```text
Hello
```

---

# LTRIM() vs RTRIM()

| Function | Removes |
|---|---|
| `LTRIM()` | Left-side spaces |
| `RTRIM()` | Right-side spaces |

---

# 28. SPACE()

## What is SPACE()?

`SPACE()` generates a specified number of spaces.

### Syntax

```sql
SPACE(number)
```

### Example

```sql
SELECT 'Hello' + SPACE(5) + 'World';
```

Result conceptually:

```text
Hello     World
```

There are five spaces between the words.

---

# 29. CONCAT()

## What is CONCAT()?

`CONCAT()` combines two or more strings.

### Syntax

```sql
CONCAT(value1, value2, value3, ...)
```

### Example 1

```sql
SELECT CONCAT('Hello', 'World');
```

Output:

```text
HelloWorld
```

### Example 2

```sql
SELECT CONCAT('Hello', ' ', 'World');
```

Output:

```text
Hello World
```

---

# CONCAT() with Employee Names

Suppose the table contains:

```text
FIRSTNAME = DEEP
LASTNAME  = PATEL
```

We can combine them:

```sql
SELECT CONCAT(FIRSTNAME, ' ', LASTNAME) AS FULLNAME
FROM EMPLOYEE;
```

Result:

```text
DEEP PATEL
```

---

# 30. REVERSE()

## What is REVERSE()?

`REVERSE()` reverses the characters in a string.

### Example

```sql
SELECT REVERSE('DARSHAN');
```

Output:

```text
NAHSRAD
```

---

# 31. REPLICATE()

## What is REPLICATE()?

`REPLICATE()` repeats a string a specified number of times.

### Syntax

```sql
REPLICATE(string, number)
```

### Example 1

```sql
SELECT REPLICATE('A', 3);
```

Output:

```text
AAA
```

### Example 2

```sql
SELECT REPLICATE('SQL ', 3);
```

Output:

```text
SQL SQL SQL
```

---

# 🔤 String Functions – Quick Revision

| Function | Purpose | Example |
|---|---|---|
| `LEN()` | Find length | `LEN('Hello')` |
| `LOWER()` | Convert lowercase | `LOWER('HELLO')` |
| `UPPER()` | Convert uppercase | `UPPER('hello')` |
| `LEFT()` | Characters from left | `LEFT('DARSHAN',3)` |
| `RIGHT()` | Characters from right | `RIGHT('DARSHAN',3)` |
| `SUBSTRING()` | Extract part | `SUBSTRING('DARSHAN',3,3)` |
| `REPLACE()` | Replace text | `REPLACE('ABC','A','X')` |
| `ASCII()` | Character → ASCII | `ASCII('A')` |
| `CHAR()` | ASCII → Character | `CHAR(65)` |
| `LTRIM()` | Remove left spaces | `LTRIM(' Hello')` |
| `RTRIM()` | Remove right spaces | `RTRIM('Hello ')` |
| `SPACE()` | Generate spaces | `SPACE(5)` |
| `CONCAT()` | Combine strings | `CONCAT('A','B')` |
| `REVERSE()` | Reverse string | `REVERSE('SQL')` |
| `REPLICATE()` | Repeat string | `REPLICATE('A',3)` |

---

# 🔄 PART C – TYPE CONVERSION FUNCTIONS

Sometimes data needs to be converted from one data type to another.

For example:

```text
String → Integer
String → Decimal
Integer → String
```

SQL Server provides:

```text
CAST()
CONVERT()
```

---

# 32. CAST()

## What is CAST()?

`CAST()` converts a value from one data type to another.

### Syntax

```sql
CAST(value AS datatype)
```

---

## Example 1

Convert string to integer:

```sql
SELECT CAST('123' AS INT);
```

Output:

```text
123
```

---

## Example 2

Convert string to decimal:

```sql
SELECT CAST('1234.56' AS DECIMAL(10,2));
```

Output:

```text
1234.56
```

---

## Example 3

Convert decimal to integer:

```sql
SELECT CAST(10.58 AS INT);
```

Result:

```text
10
```

---

# 33. CONVERT()

## What is CONVERT()?

`CONVERT()` also changes one data type into another.

### Syntax

```sql
CONVERT(data_type, value)
```

### Example 1

```sql
SELECT CONVERT(INT, '123');
```

Output:

```text
123
```

### Example 2

```sql
SELECT CONVERT(DECIMAL(10,2), '1234.56');
```

Output:

```text
1234.56
```

---

# CAST() vs CONVERT()

| CAST() | CONVERT() |
|---|---|
| Standard SQL style | SQL Server-specific feature |
| Simple syntax | Provides additional SQL Server options |
| `CAST(value AS type)` | `CONVERT(type, value)` |

### CAST

```sql
SELECT CAST('100' AS INT);
```

### CONVERT

```sql
SELECT CONVERT(INT, '100');
```

---

# 👨‍💼 PART D – FUNCTIONS WITH EMPLOYEE TABLE

Suppose our `EMPLOYEE` table contains:

| EID | FIRSTNAME | LASTNAME | CITY | SALARY |
|---:|---|---|---|---:|
| 101 | DEEP | PATEL | RAJKOT | 50000 |
| 102 | RAHUL | SHAH | SURAT | 45000 |
| 103 | PRIYA | MEHTA | AHMEDABAD | 55000 |
| 104 | RIYA | JOSHI | RAJKOT | 48000 |

---

# 34. FIRSTNAME in Lowercase

```sql
SELECT LOWER(FIRSTNAME)
FROM EMPLOYEE;
```

Example result:

```text
deep
rahul
priya
riya
```

---

# 35. LASTNAME in Uppercase

```sql
SELECT UPPER(LASTNAME)
FROM EMPLOYEE;
```

---

# 36. FIRSTNAME in Uppercase

```sql
SELECT UPPER(FIRSTNAME)
FROM EMPLOYEE;
```

---

# 37. FIRST Three Characters of FIRSTNAME

```sql
SELECT LEFT(FIRSTNAME, 3)
FROM EMPLOYEE;
```

For:

```text
DEEP
```

result:

```text
DEE
```

---

# 38. Last Three Characters of FIRSTNAME

```sql
SELECT RIGHT(FIRSTNAME, 3)
FROM EMPLOYEE;
```

For:

```text
DEEP
```

result:

```text
EEP
```

---

# 39. First Two Characters of LASTNAME

```sql
SELECT LEFT(LASTNAME, 2)
FROM EMPLOYEE;
```

---

# 40. Last Two Characters of LASTNAME

```sql
SELECT RIGHT(LASTNAME, 2)
FROM EMPLOYEE;
```

---

# 41. Length of FIRSTNAME

```sql
SELECT FIRSTNAME, LEN(FIRSTNAME) AS NAME_LENGTH
FROM EMPLOYEE;
```

Example:

```text
DEEP → 4
RAHUL → 5
PRIYA → 5
```

---

# 42. Replace 'A' with '@'

```sql
SELECT REPLACE(FIRSTNAME, 'A', '@')
FROM EMPLOYEE;
```

Example:

```text
RAHUL
```

becomes:

```text
R@HUL
```

---

# 43. Combine FIRSTNAME and LASTNAME

```sql
SELECT CONCAT(FIRSTNAME, ' ', LASTNAME) AS FULLNAME
FROM EMPLOYEE;
```

Example:

```text
DEEP PATEL
RAHUL SHAH
PRIYA MEHTA
```

---

# 44. Reverse Employee Name

```sql
SELECT REVERSE(FIRSTNAME)
FROM EMPLOYEE;
```

Example:

```text
DEEP
```

becomes:

```text
PEED
```

---

# 45. Display FIRSTNAME and LASTNAME in Lowercase

```sql
SELECT
    LOWER(FIRSTNAME) AS FIRSTNAME,
    LOWER(LASTNAME) AS LASTNAME
FROM EMPLOYEE;
```

---

# 46. Display FIRSTNAME and LASTNAME in Uppercase

```sql
SELECT
    UPPER(FIRSTNAME) AS FIRSTNAME,
    UPPER(LASTNAME) AS LASTNAME
FROM EMPLOYEE;
```

---

# 47. Display Full Name

```sql
SELECT
    CONCAT(FIRSTNAME, ' ', LASTNAME) AS FULLNAME
FROM EMPLOYEE;
```

---

# 48. Display Names Having More Than 10 Characters

We can combine `LEN()` with `WHERE`.

```sql
SELECT FIRSTNAME, LASTNAME
FROM EMPLOYEE
WHERE LEN(CONCAT(FIRSTNAME, LASTNAME)) > 10;
```

---

# 49. Employees Whose FIRSTNAME and LASTNAME Start With Same Character

We can use `LEFT()`.

```sql
SELECT *
FROM EMPLOYEE
WHERE LEFT(FIRSTNAME, 1) = LEFT(LASTNAME, 1);
```

Example:

```text
FIRSTNAME = RAHUL
LASTNAME  = RANA
```

Both start with:

```text
R
```

Therefore, the employee is selected.

---

# 50. Employees Whose FIRSTNAME and LASTNAME Are the Same

```sql
SELECT *
FROM EMPLOYEE
WHERE FIRSTNAME = LASTNAME;
```

---

# 51. Employee Name in Reverse

```sql
SELECT
    REVERSE(FIRSTNAME) AS REVERSED_NAME
FROM EMPLOYEE;
```

---

# 52. Display First Character

```sql
SELECT LEFT(FIRSTNAME, 1) AS FIRST_CHARACTER
FROM EMPLOYEE;
```

---

# 53. Display Last Character

```sql
SELECT RIGHT(FIRSTNAME, 1) AS LAST_CHARACTER
FROM EMPLOYEE;
```

---

# 🧠 Combining Multiple Functions

SQL functions can be combined.

For example:

```sql
SELECT UPPER(LEFT(FIRSTNAME, 3))
FROM EMPLOYEE;
```

If:

```text
FIRSTNAME = darshan
```

First:

```sql
LEFT('darshan', 3)
```

gives:

```text
dar
```

Then:

```sql
UPPER('dar')
```

gives:

```text
DAR
```

Final result:

```text
DAR
```

---

# 🔥 More Function Combinations

## Full Name in Uppercase

```sql
SELECT UPPER(
    CONCAT(FIRSTNAME, ' ', LASTNAME)
) AS FULLNAME
FROM EMPLOYEE;
```

---

## First Character in Uppercase

```sql
SELECT UPPER(LEFT(FIRSTNAME, 1))
FROM EMPLOYEE;
```

---

## Last Character in Lowercase

```sql
SELECT LOWER(RIGHT(FIRSTNAME, 1))
FROM EMPLOYEE;
```

---

## Reverse Full Name

```sql
SELECT REVERSE(
    CONCAT(FIRSTNAME, ' ', LASTNAME)
) AS REVERSED_NAME
FROM EMPLOYEE;
```

---

# 🧩 Function Nesting

A function inside another function is called **function nesting**.

Example:

```sql
UPPER(
    LEFT(FIRSTNAME, 3)
)
```

Execution:

```text
FIRSTNAME
   ↓
LEFT()
   ↓
UPPER()
   ↓
Final Result
```

---

# 📌 Important Function Categories

## Mathematical

```text
ABS()
CEILING()
FLOOR()
POWER()
SQRT()
PI()
ROUND()
EXP()
LOG()
LOG10()
SIN()
COS()
TAN()
SIGN()
RAND()
```

## String

```text
LEN()
LOWER()
UPPER()
LEFT()
RIGHT()
SUBSTRING()
REPLACE()
ASCII()
CHAR()
LTRIM()
RTRIM()
SPACE()
CONCAT()
REVERSE()
REPLICATE()
```

## Conversion

```text
CAST()
CONVERT()
```

---

# ⚠️ Common Mistakes

## Mistake 1 – Confusing LEFT() and RIGHT()

```sql
LEFT('DARSHAN', 3)
```

returns:

```text
DAR
```

while:

```sql
RIGHT('DARSHAN', 3)
```

returns:

```text
HAN
```

---

## Mistake 2 – Confusing CEILING() and FLOOR()

```sql
CEILING(10.2)
```

returns:

```text
11
```

while:

```sql
FLOOR(10.2)
```

returns:

```text
10
```

---

## Mistake 3 – Confusing ASCII() and CHAR()

```sql
ASCII('A')
```

returns:

```text
65
```

while:

```sql
CHAR(65)
```

returns:

```text
A
```

---

## Mistake 4 – Forgetting the Third Argument of SUBSTRING()

Correct:

```sql
SUBSTRING('DARSHAN', 2, 3)
```

The three values represent:

```text
String
Start Position
Length
```

---

## Mistake 5 – Using + for String Concatenation Without Considering NULL

For reliable string concatenation in SQL Server, `CONCAT()` is often easier:

```sql
SELECT CONCAT(FIRSTNAME, ' ', LASTNAME)
FROM EMPLOYEE;
```

---

# 🎯 Quick Revision

```text
ABS()
↓
Absolute value

CEILING()
↓
Round upward

FLOOR()
↓
Round downward

POWER()
↓
Calculate power

SQRT()
↓
Square root

ROUND()
↓
Round decimal

LEN()
↓
String length

LOWER()
↓
Lowercase

UPPER()
↓
Uppercase

LEFT()
↓
Characters from left

RIGHT()
↓
Characters from right

SUBSTRING()
↓
Extract part of string

REPLACE()
↓
Replace text

LTRIM()
↓
Remove left spaces

RTRIM()
↓
Remove right spaces

CONCAT()
↓
Combine strings

REVERSE()
↓
Reverse string

REPLICATE()
↓
Repeat string

CAST()
↓
Convert data type

CONVERT()
↓
Convert data type
```

---

# 📝 Practice Questions

Try solving these without looking at the examples above.

## Mathematical Functions

1. Find the absolute value of `-50`.
2. Find the ceiling value of `25.7`.
3. Find the floor value of `25.7`.
4. Find the remainder of `17 / 5`.
5. Find `3⁴`.
6. Find the square root of `144`.
7. Display the value of π.
8. Round `157.732` to 2 decimal places.
9. Find `LOG10(1000)`.
10. Find the sign of `-100`.
11. Generate a random number.

---

## String Functions

12. Find the length of `DARSHAN`.
13. Convert `DATABASE` to lowercase.
14. Convert `database` to uppercase.
15. Display first 3 characters of `DARSHAN`.
16. Display last 3 characters of `DARSHAN`.
17. Replace `A` with `@`.
18. Find ASCII value of `A`.
19. Convert ASCII `65` into a character.
20. Remove spaces from the left of a string.
21. Remove spaces from the right of a string.
22. Generate 10 spaces.
23. Combine first name and last name.
24. Reverse `DARSHAN`.
25. Repeat `SQL` three times.

---

# 🎤 Interview Questions

### 1. What is a built-in function in SQL?

A built-in function is a predefined SQL function that performs a specific operation.

---

### 2. What is the use of ABS()?

It returns the absolute value of a number.

---

### 3. Difference between CEILING() and FLOOR()?

`CEILING()` rounds upward while `FLOOR()` rounds downward.

---

### 4. What does POWER() do?

It calculates a number raised to a specified power.

---

### 5. What is the difference between LEN() and LEFT()?

`LEN()` returns the length of a string.

`LEFT()` extracts characters from the beginning of a string.

---

### 6. What does CONCAT() do?

It combines multiple values into one string.

---

### 7. What does REPLACE() do?

It replaces occurrences of one string with another.

---

### 8. Difference between LTRIM() and RTRIM()?

`LTRIM()` removes spaces from the left.

`RTRIM()` removes spaces from the right.

---

### 9. What is the difference between ASCII() and CHAR()?

```text
ASCII()
Character → ASCII number

CHAR()
ASCII number → Character
```

---

### 10. Difference between CAST() and CONVERT()?

Both convert data types.

`CAST()` follows standard SQL syntax, while `CONVERT()` is commonly associated with SQL Server and provides additional formatting options.

---

# 📊 Final Summary

| Category | Function | Main Purpose |
|---|---|---|
| Mathematical | `ABS()` | Absolute value |
| Mathematical | `CEILING()` | Round upward |
| Mathematical | `FLOOR()` | Round downward |
| Mathematical | `%` | Remainder |
| Mathematical | `POWER()` | Power |
| Mathematical | `SQRT()` | Square root |
| Mathematical | `PI()` | π |
| Mathematical | `ROUND()` | Rounding |
| Mathematical | `EXP()` | Exponential |
| Mathematical | `LOG()` | Logarithm |
| Mathematical | `LOG10()` | Base-10 logarithm |
| Mathematical | `SIN()` | Sine |
| Mathematical | `COS()` | Cosine |
| Mathematical | `TAN()` | Tangent |
| Mathematical | `SIGN()` | Sign |
| Mathematical | `RAND()` | Random number |
| String | `LEN()` | String length |
| String | `LOWER()` | Lowercase |
| String | `UPPER()` | Uppercase |
| String | `LEFT()` | Extract left characters |
| String | `RIGHT()` | Extract right characters |
| String | `SUBSTRING()` | Extract part of string |
| String | `REPLACE()` | Replace text |
| String | `ASCII()` | Character to ASCII |
| String | `CHAR()` | ASCII to character |
| String | `LTRIM()` | Remove left spaces |
| String | `RTRIM()` | Remove right spaces |
| String | `SPACE()` | Generate spaces |
| String | `CONCAT()` | Combine strings |
| String | `REVERSE()` | Reverse text |
| String | `REPLICATE()` | Repeat text |
| Conversion | `CAST()` | Convert data type |
| Conversion | `CONVERT()` | Convert data type |

---

# 🎯 Learning Outcome

After completing this lab, students should be able to:

- Use SQL mathematical functions.
- Perform calculations using numeric functions.
- Round numeric values.
- Work with powers and square roots.
- Use logarithmic and trigonometric functions.
- Generate random numbers.
- Manipulate strings using SQL functions.
- Extract characters from strings.
- Change string case.
- Replace and remove characters.
- Combine multiple strings.
- Reverse and repeat strings.
- Convert values between different data types.
- Apply built-in functions directly to table columns.
- Combine multiple functions in a single SQL query.

---

# ⭐ Key Takeaway

SQL built-in functions make it easy to perform common operations without writing complex logic.

The most important functions from this lab are:

```text
MATHEMATICAL
────────────
ABS()
CEILING()
FLOOR()
POWER()
SQRT()
ROUND()
SIGN()
RAND()

STRING
──────
LEN()
LOWER()
UPPER()
LEFT()
RIGHT()
SUBSTRING()
REPLACE()
LTRIM()
RTRIM()
CONCAT()
REVERSE()
REPLICATE()

CONVERSION
──────────
CAST()
CONVERT()
```

The most important idea to remember is:

```text
SQL Query
   ↓
Built-In Function
   ↓
Input Value
   ↓
Processed Result
```

For example:

```sql
SELECT UPPER(FIRSTNAME)
FROM EMPLOYEE;
```

means:

```text
FIRSTNAME
    ↓
UPPER()
    ↓
UPPERCASE NAME
```

---

# ⭐ Happy Learning SQL! ⭐
