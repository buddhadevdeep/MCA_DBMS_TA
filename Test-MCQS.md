# DBMS-MSSQL Lab 1–9 MCQ Question Bank

**Source:** Darshan University MCA DBMS Lab Manual (A.Y. 2026, Semester I) — Labs 1 to 9 only
**Target System:** Microsoft SQL Server / T-SQL

---

## Exam Coverage

* Lab 1 — Introduction to SQL Server Management Studio (SSMS)
* Lab 2 — CREATE and INSERT
* Lab 3 — SELECT, Operators and Conditions
* Lab 4 — UPDATE
* Lab 5 — ALTER, RENAME, DELETE, TRUNCATE, DROP
* Lab 6 — SELECT INTO
* Lab 7 — LIKE / Pattern Searching
* Lab 8 — Aggregate Functions + GROUP BY
* Lab 9 — GROUP BY + HAVING + ORDER BY

## Difficulty Distribution

| Difficulty | Count |
| ---------- | ----: |
| Easy       |    25 |
| Medium     |    40 |
| Hard       |    25 |
| Very Hard  |    10 |
| **Total**  | **100** |

## Reference Data Used (from Lab Manual)

**STUDENT:** 101 HETVI/RAJKOT/7.40/COMPUTER, 102 RAJ/MORBI/9.50/MECHANICAL, 103 VISHAL/RAJKOT/9.00/CIVIL, 104 DEEP/SURAT/8.80/COMPUTER, 105 DHARMIK/BARODA/8.80/CHEMICAL, 106 KRUNAL/VAPI/9.00/CIVIL, 107 RIYA/NAVSARI/5.50/COMPUTER, 108 VRUNDA/KUTCH/7.60/ELECTRICAL, 109 SMAIR/JAMNAGAR/6.80/EC, 110 PARAG/SURAT/7.00/CHEMICAL, 111 HARSH/RAJKOT/4.00/NULL

**DEPOSIT:** 101 MEET/MAVDI/10000, 102 JAY/MADHAPAR/5000, 103 RAHUL/BEDI/3500, 104 RIYA/MAVDI/1200, 105 MANSI/KKV HALL/3000, 106 DIYA/MADHAPAR/2000, 107 MIRAL/BEDI/1000, 108 UDAY/UMIYA CHOWK/5000, 109 CHARMI/SHITAL PARK/7000, 110 BHAVIN/RING ROAD/8000, 111 BANSI/NULL/9000

**EMPLOYEE:** 101 HETVI PATEL/ADMIN/12000/RAJKOT, 102 RAJ MEHTA/IT/14000/AHMEDABAD, 103 VISHAL SHARMA/HR/15000/BARODA, 104 DEEP PATEL/ADMIN/12500/RAJKOT, 105 DHAVAL SHAH/IT/14000/JAMNAGAR, 106 RIYA KAUR/IT/5000/AHMEDABAD, 107 PARAG PANDYA/HR/7000/RAJKOT, 108 VRUNDA VYAS/SERVER/10000/BARODA, 109 MEHUL SINGH/HR/12000/MORBI, 110 MUBIN PARMAR/TRANSPORT/12000/SURAT, 111 MAYANK PUROHIT/ACCOUNT/13000/NULL

---

## MCQs

### Q1. What does SSMS stand for?

**Difficulty:** Easy
**Lab:** Lab 1 — SSMS
**Topic:** SSMS Basics

A. SQL Server Management Studio
B. SQL Server Master Studio
C. Structured Server Management System
D. SQL Server Monitoring Software

**Answer:** A

**Explanation:** SSMS is the official Microsoft tool for managing SQL Server, standing for SQL Server Management Studio.

---

### Q2. Which window in SSMS is used to write and execute SQL queries?

**Difficulty:** Easy
**Lab:** Lab 1 — SSMS
**Topic:** SSMS Interface

A. Object Explorer
B. Query Editor
C. Solution Explorer
D. Results Grid

**Answer:** B

**Explanation:** The Query Editor window is where T-SQL statements are typed and executed.

---

### Q3. Which SSMS pane displays the hierarchical list of databases, tables, and other server objects?

**Difficulty:** Easy
**Lab:** Lab 1 — SSMS
**Topic:** SSMS Interface

A. Query Editor
B. Object Explorer
C. Results Pane
D. Template Explorer

**Answer:** B

**Explanation:** Object Explorer shows a tree view of the connected server's databases, tables, views, and other objects.

---

### Q4. In SSMS, which key is commonly used to execute a query?

**Difficulty:** Medium
**Lab:** Lab 1 — SSMS
**Topic:** SSMS Shortcuts

A. F5
B. F2
C. Ctrl+S
D. Ctrl+N

**Answer:** A

**Explanation:** F5 (or the Execute button) runs the query currently open in the Query Editor.

---

### Q5. To connect to a SQL Server instance in SSMS, which authentication mode allows login using the OS login credentials?

**Difficulty:** Medium
**Lab:** Lab 1 — SSMS
**Topic:** Authentication

A. SQL Server Authentication
B. Windows Authentication
C. Mixed Authentication
D. Guest Authentication

**Answer:** B

**Explanation:** Windows Authentication uses the credentials of the currently logged-in Windows user to connect to SQL Server.

---

### Q6. Which SQL Server data type is appropriate for storing values like SPI with fixed precision and scale?

**Difficulty:** Easy
**Lab:** Lab 2 — CREATE/INSERT
**Topic:** Data Types

A. INT
B. VARCHAR
C. DECIMAL
D. DATETIME

**Answer:** C

**Explanation:** DECIMAL(p,s) stores exact numeric values with a defined number of digits and decimal places, ideal for SPI values like 7.40.

---

### Q7. Which statement correctly declares the ACTNO column of DEPOSIT as an integer?

**Difficulty:** Easy
**Lab:** Lab 2 — CREATE/INSERT
**Topic:** CREATE TABLE

A. ACTNO INTEGER(10)
B. ACTNO INT
C. ACTNO NUMBER
D. ACTNO DIGIT

**Answer:** B

**Explanation:** INT is the valid SQL Server data type for whole numbers; INTEGER(10), NUMBER and DIGIT are not valid T-SQL syntax here.

---

### Q8. Which command is used to add a new row of data into a table?

**Difficulty:** Easy
**Lab:** Lab 2 — CREATE/INSERT
**Topic:** INSERT

A. ADD INTO
B. INSERT INTO
C. CREATE INTO
D. NEW ROW

**Answer:** B

**Explanation:** INSERT INTO is the standard T-SQL statement used to add rows into a table.

---

### Q9. Given STUDENT(STDID INT, SNAME VARCHAR(50), CITY VARCHAR(50), SPI DECIMAL(4,2), BRANCH VARCHAR(50)), which INSERT is syntactically correct?

**Difficulty:** Easy
**Lab:** Lab 2 — CREATE/INSERT
**Topic:** INSERT Syntax

A. INSERT INTO STUDENT VALUES (101, HETVI, RAJKOT, 7.40, COMPUTER);
B. INSERT INTO STUDENT VALUES (101, 'HETVI', 'RAJKOT', 7.40, 'COMPUTER');
C. INSERT STUDENT SET STDID=101;
D. INSERT INTO STUDENT (101,'HETVI','RAJKOT',7.40,'COMPUTER');

**Answer:** B

**Explanation:** String/character values must be enclosed in single quotes, and the VALUES keyword is required; option A omits quotes and C/D use invalid syntax.

---

### Q10. DECIMAL(8,2) for the AMOUNT column means:

**Difficulty:** Medium
**Lab:** Lab 2 — CREATE/INSERT
**Topic:** Data Types

A. 8 digits total, 2 of which are after the decimal point
B. 8 digits after the decimal, 2 total
C. Maximum value is 8.2
D. 8 rows, 2 columns

**Answer:** A

**Explanation:** In DECIMAL(precision, scale), precision is the total number of digits and scale is the number of digits to the right of the decimal point.

---

### Q11. Which data type correctly stores the ADATE column, which must hold both date and time?

**Difficulty:** Medium
**Lab:** Lab 2 — CREATE/INSERT
**Topic:** Data Types

A. DATE
B. DATETIME
C. TIME
D. VARCHAR(20)

**Answer:** B

**Explanation:** DATETIME stores both date and time components, matching the manual's ADATE column definition.

---

### Q12. Which statement correctly inserts a NULL value into the BRANCH column for HARSH?

**Difficulty:** Medium
**Lab:** Lab 2 — CREATE/INSERT
**Topic:** NULL Handling

A. INSERT INTO STUDENT VALUES (111,'HARSH','RAJKOT',4.00,'NULL');
B. INSERT INTO STUDENT VALUES (111,'HARSH','RAJKOT',4.00,NULL);
C. INSERT INTO STUDENT VALUES (111,'HARSH','RAJKOT',4.00,'');
D. INSERT INTO STUDENT VALUES (111,'HARSH','RAJKOT',4.00,0);

**Answer:** B

**Explanation:** NULL without quotes represents the absence of a value; 'NULL' in quotes is treated as the literal string "NULL", which is a common trap.

---

### Q13. Which of the following is NOT a valid SQL Server data type?

**Difficulty:** Medium
**Lab:** Lab 2 — CREATE/INSERT
**Topic:** Data Types

A. VARCHAR
B. DECIMAL
C. DATETIME
D. LIMIT

**Answer:** D

**Explanation:** LIMIT is a MySQL clause used for row limiting, not a SQL Server data type at all.

---

### Q14. A student runs: INSERT INTO STUDENT VALUES (101,'HETVI','RAJKOT',COMPUTER,7.40); This fails because:

**Difficulty:** Hard
**Lab:** Lab 2 — CREATE/INSERT
**Topic:** INSERT Errors

A. The string COMPUTER is unquoted and the values are in the wrong column order
B. STDID cannot be 101
C. RAJKOT is misspelled
D. SPI cannot be a decimal

**Answer:** A

**Explanation:** COMPUTER needs quotes as a string, and its position doesn't match the BRANCH/SPI column order defined in the table.

---

### Q15. Which statement is TRUE about INSERT INTO using an explicit column list?

**Difficulty:** Hard
**Lab:** Lab 2 — CREATE/INSERT
**Topic:** INSERT Syntax

A. Values must always follow the exact order of the table definition, never the listed columns
B. Values can be provided in any order, as long as they match the order of the explicitly listed column names
C. An explicit column list is invalid syntax in SQL Server
D. VALUES-only insert (no column list) allows skipping any column

**Answer:** B

**Explanation:** When column names are explicitly listed, SQL Server matches values positionally to that list, not the table's original definition order.

---

### Q16. Which query retrieves all columns from the STUDENT table?

**Difficulty:** Easy
**Lab:** Lab 3 — SELECT Queries
**Topic:** SELECT

A. `SELECT ALL FROM STUDENT;`
B. `SELECT * FROM STUDENT;`
C. `GET * FROM STUDENT;`
D. `DISPLAY * FROM STUDENT;`

**Answer:** B

**Explanation:** `SELECT * FROM STUDENT;` retrieves all columns and rows from the STUDENT table.

---

### Q17. Which clause is used to filter rows based on a condition?

**Difficulty:** Easy
**Lab:** Lab 3 — SELECT Queries
**Topic:** WHERE

A. GROUP BY
B. WHERE
C. ORDER BY
D. HAVING

**Answer:** B

**Explanation:** WHERE filters individual rows before any grouping or sorting occurs.

---

### Q18. Which operator checks whether a value matches any value within a specified set?

**Difficulty:** Easy
**Lab:** Lab 3 — SELECT Queries
**Topic:** IN Operator

A. BETWEEN
B. IN
C. LIKE
D. IS

**Answer:** B

**Explanation:** IN allows matching a column against a list of possible values, e.g., `BRANCH IN ('COMPUTER','CIVIL')`.

---

### Q19. Which operator correctly tests for NULL values in a WHERE clause?

**Difficulty:** Easy
**Lab:** Lab 3 — SELECT Queries
**Topic:** NULL Handling

A. `= NULL`
B. `IS NULL`
C. `== NULL`
D. `<> NULL`

**Answer:** B

**Explanation:** NULL represents an unknown value, so `=` cannot be used to compare it; `IS NULL` is the correct SQL Server syntax.

---

### Q20. The DISTINCT keyword is used to:

**Difficulty:** Easy
**Lab:** Lab 3 — SELECT Queries
**Topic:** DISTINCT

A. Sort records
B. Remove duplicate rows from the result set
C. Filter NULL values
D. Combine two tables

**Answer:** B

**Explanation:** DISTINCT eliminates duplicate rows from the query's output, keeping only unique combinations of the selected columns.

---

### Q21. How many rows are returned by: `SELECT * FROM STUDENT WHERE CITY = 'RAJKOT';`

**Difficulty:** Medium
**Lab:** Lab 3 — SELECT Queries
**Topic:** Output Prediction

A. 2
B. 3
C. 4
D. 5

**Answer:** B

**Explanation:** Students in RAJKOT are HETVI (101), VISHAL (103), and HARSH (111) — a total of 3 rows.

---

### Q22. How many rows are returned by: `SELECT * FROM STUDENT WHERE SPI > 8.0;`

**Difficulty:** Medium
**Lab:** Lab 3 — SELECT Queries
**Topic:** Output Prediction

A. 4
B. 5
C. 6
D. 7

**Answer:** B

**Explanation:** RAJ(9.50), VISHAL(9.00), DEEP(8.80), DHARMIK(8.80), and KRUNAL(9.00) all have SPI strictly greater than 8.0 — 5 rows.

---

### Q23. Which query correctly displays names of students belonging to either 'RAJKOT' or 'SURAT' using IN?

**Difficulty:** Medium
**Lab:** Lab 3 — SELECT Queries
**Topic:** IN Operator

A. `SELECT SNAME FROM STUDENT WHERE CITY IN ('RAJKOT','SURAT');`
B. `SELECT SNAME FROM STUDENT WHERE CITY = 'RAJKOT' AND CITY='SURAT';`
C. `SELECT SNAME FROM STUDENT WHERE CITY LIKE 'RAJKOT','SURAT';`
D. `SELECT SNAME FROM STUDENT WHERE CITY BETWEEN 'RAJKOT' AND 'SURAT';`

**Answer:** A

**Explanation:** IN provides a clean way to check membership in a list of values, equivalent to multiple OR conditions.

---

### Q24. How many rows satisfy: `SELECT * FROM STUDENT WHERE SPI BETWEEN 7.0 AND 9.0;`

**Difficulty:** Medium
**Lab:** Lab 3 — SELECT Queries
**Topic:** BETWEEN

A. 5
B. 6
C. 7
D. 8

**Answer:** C

**Explanation:** Matching rows (inclusive): HETVI(7.40), VISHAL(9.00), DEEP(8.80), DHARMIK(8.80), KRUNAL(9.00), VRUNDA(7.60), PARAG(7.00) — 7 rows. RAJ(9.50), RIYA(5.50), SMAIR(6.80), and HARSH(4.00) are excluded.

---

### Q25. Which query displays student names whose branch is NULL?

**Difficulty:** Medium
**Lab:** Lab 3 — SELECT Queries
**Topic:** NULL Handling

A. `SELECT SNAME FROM STUDENT WHERE BRANCH = NULL;`
B. `SELECT SNAME FROM STUDENT WHERE BRANCH IS NULL;`
C. `SELECT SNAME FROM STUDENT WHERE BRANCH = 'NULL';`
D. `SELECT SNAME FROM STUDENT WHERE ISNULL(BRANCH);`

**Answer:** B

**Explanation:** `IS NULL` is the only correct way to test for NULL; `= NULL` always evaluates to UNKNOWN and returns no rows.

---

### Q26. TOP 50 PERCENT is used to:

**Difficulty:** Medium
**Lab:** Lab 3 — SELECT Queries
**Topic:** TOP

A. Retrieve exactly 50 rows
B. Retrieve the first half of the rows based on the total row count
C. Retrieve rows where a column equals 50
D. Retrieve rows with 50% NULL values

**Answer:** B

**Explanation:** TOP 50 PERCENT dynamically calculates the row count as half of the total rows in the result set.

---

### Q27. Which query returns students NOT belonging to the 'COMPUTER' branch using NOT IN?

**Difficulty:** Medium
**Lab:** Lab 3 — SELECT Queries
**Topic:** NOT IN

A. `SELECT * FROM STUDENT WHERE BRANCH NOT IN ('COMPUTER');`
B. `SELECT * FROM STUDENT WHERE BRANCH != IN ('COMPUTER');`
C. `SELECT * FROM STUDENT WHERE NOT BRANCH = ('COMPUTER');`
D. `SELECT * FROM STUDENT WHERE BRANCH OUT ('COMPUTER');`

**Answer:** A

**Explanation:** NOT IN is the correct syntax for excluding rows matching any value in a list.

---

### Q28. How many rows are returned by: `SELECT * FROM STUDENT WHERE BRANCH IN ('COMPUTER','CIVIL','CHEMICAL') AND STDID < 104;`

**Difficulty:** Hard
**Lab:** Lab 3 — SELECT Queries
**Topic:** Output Prediction

A. 1
B. 2
C. 3
D. 4

**Answer:** B

**Explanation:** STDID < 104 gives rows 101, 102, 103. Of these, 101 HETVI (COMPUTER) and 103 VISHAL (CIVIL) match the branch list; 102 RAJ (MECHANICAL) does not — 2 rows.

---

### Q29. In SQL Server (default settings), what does `NULL = NULL` evaluate to?

**Difficulty:** Hard
**Lab:** Lab 3 — SELECT Queries
**Topic:** NULL Trap

A. TRUE
B. FALSE
C. UNKNOWN, so the row is not returned
D. It causes a syntax error

**Answer:** C

**Explanation:** NULL represents an unknown value, so comparing NULL to NULL with `=` yields UNKNOWN, not TRUE — a common misconception.

---

### Q30. For `SELECT * FROM STUDENT WHERE CITY = 'RAJKOT' OR CITY = 'SURAT' AND SPI > 8.0;`, how many rows are returned? (Recall: AND has higher precedence than OR)

**Difficulty:** Hard
**Lab:** Lab 3 — SELECT Queries
**Topic:** Operator Precedence

A. 3
B. 4
C. 5
D. 6

**Answer:** B

**Explanation:** The condition evaluates as `CITY='RAJKOT' OR (CITY='SURAT' AND SPI>8.0)`. RAJKOT rows: HETVI, VISHAL, HARSH (3). SURAT AND SPI>8.0: only DEEP (8.80) qualifies. Total = 4 rows.

---

### Q31. Which query correctly retrieves STDID and SNAME for students whose ID is NOT in the range 105 to 109?

**Difficulty:** Hard
**Lab:** Lab 3 — SELECT Queries
**Topic:** NOT BETWEEN

A. `SELECT STDID, SNAME FROM STUDENT WHERE STDID NOT BETWEEN 105 AND 109;`
B. `SELECT STDID, SNAME FROM STUDENT WHERE STDID <> BETWEEN 105 AND 109;`
C. `SELECT STDID, SNAME FROM STUDENT WHERE NOT STDID IN (105,109);`
D. `SELECT STDID, SNAME FROM STUDENT WHERE STDID != 105 TO 109;`

**Answer:** A

**Explanation:** NOT BETWEEN excludes all values within the inclusive range 105–109; the other options are syntactically invalid.

---

### Q32. For `SELECT * FROM STUDENT WHERE BRANCH <> 'COMPUTER';`, which student is unexpectedly EXCLUDED even though their branch is genuinely not 'COMPUTER'?

**Difficulty:** Very Hard
**Lab:** Lab 3 — SELECT Queries
**Topic:** NULL Trap

A. VISHAL (CIVIL)
B. HARSH (NULL branch)
C. DEEP (COMPUTER)
D. None are excluded

**Answer:** B

**Explanation:** `BRANCH <> 'COMPUTER'` compares against NULL for HARSH, which evaluates to UNKNOWN rather than TRUE, so that row is silently dropped from the result — a classic NULL trap.

---

### Q33. How many rows are returned by: `SELECT * FROM STUDENT WHERE NOT (BRANCH = 'CIVIL');`

**Difficulty:** Very Hard
**Lab:** Lab 3 — SELECT Queries
**Topic:** NULL Trap

A. 2
B. 8
C. 9
D. 10

**Answer:** B

**Explanation:** Out of 11 rows, 2 have BRANCH='CIVIL' (VISHAL, KRUNAL) and are excluded, and HARSH's NULL branch makes `BRANCH='CIVIL'` UNKNOWN — so NOT(UNKNOWN) is also UNKNOWN, excluding that row too. Result: 11 − 2 − 1 = 8 rows.

---

### Q34. Which command is used to modify existing data in a table?

**Difficulty:** Easy
**Lab:** Lab 4 — UPDATE
**Topic:** UPDATE Basics

A. ALTER
B. UPDATE
C. MODIFY
D. CHANGE

**Answer:** B

**Explanation:** UPDATE is the T-SQL command used to change the values of existing rows.

---

### Q35. Which clause should always accompany UPDATE to avoid modifying all rows unintentionally?

**Difficulty:** Easy
**Lab:** Lab 4 — UPDATE
**Topic:** UPDATE Basics

A. GROUP BY
B. WHERE
C. ORDER BY
D. HAVING

**Answer:** B

**Explanation:** WHERE restricts which rows are affected by the UPDATE; without it, every row in the table is updated.

---

### Q36. Which is the correct syntax to update SPI of HETVI to 8.00?

**Difficulty:** Easy
**Lab:** Lab 4 — UPDATE
**Topic:** UPDATE Syntax

A. `UPDATE STUDENT SET SPI = 8.00 WHERE SNAME = 'HETVI';`
B. `UPDATE STUDENT SPI = 8.00 WHERE SNAME = 'HETVI';`
C. `SET STUDENT SPI = 8.00 WHERE SNAME='HETVI';`
D. `UPDATE SPI = 8.00 IN STUDENT WHERE SNAME='HETVI';`

**Answer:** A

**Explanation:** The correct syntax requires the SET keyword after specifying the table name in UPDATE.

---

### Q37. Which statement updates both SPI and CITY of the student with STDID 101 in one query?

**Difficulty:** Medium
**Lab:** Lab 4 — UPDATE
**Topic:** Multiple Column Update

A. `UPDATE STUDENT SET SPI = 8.00; SET CITY='SURAT' WHERE STDID=101;`
B. `UPDATE STUDENT SET SPI = 8.00, CITY = 'SURAT' WHERE STDID = 101;`
C. `UPDATE STUDENT SET SPI = 8.00 AND CITY = 'SURAT' WHERE STDID=101;`
D. `UPDATE STUDENT SET (SPI, CITY) = (8.00,'SURAT') WHERE STDID=101;`

**Answer:** B

**Explanation:** Multiple columns are updated in a single SET clause separated by commas, not AND or tuple syntax.

---

### Q38. The query `UPDATE STUDENT SET SPI = SPI + 0.50;` without a WHERE clause will:

**Difficulty:** Medium
**Lab:** Lab 4 — UPDATE
**Topic:** Risk of Missing WHERE

A. Give an error
B. Increase SPI of only the first row
C. Increase SPI of every row in the table by 0.50
D. Do nothing

**Answer:** C

**Explanation:** Without a WHERE clause, UPDATE applies to all rows in the table.

---

### Q39. To give a 10% increment in SPI for all students, which expression is correct?

**Difficulty:** Medium
**Lab:** Lab 4 — UPDATE
**Topic:** Percentage Update

A. `SET SPI = SPI + 10`
B. `SET SPI = SPI * 0.10`
C. `SET SPI = SPI + (SPI * 0.10)`
D. `SET SPI = 10`

**Answer:** C

**Explanation:** A 10% increment means adding 10% of the current value to itself, i.e., `SPI + (SPI * 0.10)`.

---

### Q40. Which query sets the BRANCH of VISHAL to NULL?

**Difficulty:** Medium
**Lab:** Lab 4 — UPDATE
**Topic:** NULL Update

A. `UPDATE STUDENT SET BRANCH = 'NULL' WHERE SNAME = 'VISHAL';`
B. `UPDATE STUDENT SET BRANCH = NULL WHERE SNAME = 'VISHAL';`
C. `UPDATE STUDENT SET BRANCH = '' WHERE SNAME='VISHAL';`
D. `UPDATE STUDENT REMOVE BRANCH WHERE SNAME='VISHAL';`

**Answer:** B

**Explanation:** Assigning the unquoted keyword NULL sets the column to a true NULL value; option A sets it to the literal string "NULL".

---

### Q41. What is the primary risk of executing `UPDATE STUDENT SET CITY = 'RAJKOT';` without a WHERE clause?

**Difficulty:** Hard
**Lab:** Lab 4 — UPDATE
**Topic:** UPDATE Risk

A. It will throw a syntax error
B. Only NULL city values will be updated
C. It updates the CITY column for every row, overwriting all cities to 'RAJKOT'
D. It only affects the first row

**Answer:** C

**Explanation:** Omitting WHERE means the SET clause applies to every row in the table, a common and costly mistake.

---

### Q42. `UPDATE STUDENT SET SPI = 7.50 WHERE STDID BETWEEN 103 AND 107;` — how many rows are affected?

**Difficulty:** Hard
**Lab:** Lab 4 — UPDATE
**Topic:** Output Prediction

A. 3
B. 4
C. 5
D. 6

**Answer:** C

**Explanation:** STDID 103, 104, 105, 106, and 107 fall within the inclusive range — 5 rows.

---

### Q43. After `UPDATE STUDENT SET SPI = SPI + 0.50 WHERE BRANCH = 'CIVIL' OR BRANCH IS NULL;`, how many rows have their SPI updated?

**Difficulty:** Very Hard
**Lab:** Lab 4 — UPDATE
**Topic:** Multi-Condition Update

A. 2
B. 3
C. 4
D. 5

**Answer:** B

**Explanation:** CIVIL branch: VISHAL and KRUNAL (2 rows). BRANCH IS NULL: HARSH (1 row). Total = 3 rows updated.

---

### Q44. Which command changes the structure of an existing table, such as adding a column?

**Difficulty:** Easy
**Lab:** Lab 5 — ALTER/RENAME/DELETE/TRUNCATE/DROP
**Topic:** ALTER TABLE

A. UPDATE
B. ALTER TABLE
C. MODIFY TABLE
D. CREATE TABLE

**Answer:** B

**Explanation:** ALTER TABLE is used to add, modify, or drop columns and constraints of an existing table.

---

### Q45. Which command removes all rows from a table while keeping the table structure intact?

**Difficulty:** Easy
**Lab:** Lab 5 — ALTER/RENAME/DELETE/TRUNCATE/DROP
**Topic:** TRUNCATE

A. DELETE
B. DROP
C. TRUNCATE TABLE
D. REMOVE

**Answer:** C

**Explanation:** TRUNCATE TABLE quickly removes all rows but preserves the table's schema for future use.

---

### Q46. Which command permanently removes a table, including its structure, from the database?

**Difficulty:** Easy
**Lab:** Lab 5 — ALTER/RENAME/DELETE/TRUNCATE/DROP
**Topic:** DROP

A. DELETE TABLE
B. TRUNCATE TABLE
C. DROP TABLE
D. REMOVE TABLE

**Answer:** C

**Explanation:** DROP TABLE deletes the table object itself, including its data, structure, and associated indexes/constraints.

---

### Q47. Correct syntax to add a column 'state' of type varchar(20) to the DEPOSIT table:

**Difficulty:** Medium
**Lab:** Lab 5 — ALTER/RENAME/DELETE/TRUNCATE/DROP
**Topic:** ALTER TABLE ADD

A. `ALTER TABLE DEPOSIT ADD COLUMN state VARCHAR(20);`
B. `ALTER TABLE DEPOSIT ADD state VARCHAR(20);`
C. `ADD COLUMN state VARCHAR(20) TO DEPOSIT;`
D. `UPDATE DEPOSIT ADD state VARCHAR(20);`

**Answer:** B

**Explanation:** SQL Server's ALTER TABLE ADD syntax does not use the word COLUMN (unlike some other databases).

---

### Q48. Correct syntax to change the size of the CNAME column from varchar(50) to varchar(35) in SQL Server:

**Difficulty:** Medium
**Lab:** Lab 5 — ALTER/RENAME/DELETE/TRUNCATE/DROP
**Topic:** ALTER COLUMN

A. `ALTER TABLE DEPOSIT MODIFY CNAME VARCHAR(35);`
B. `ALTER TABLE DEPOSIT ALTER COLUMN CNAME VARCHAR(35);`
C. `ALTER TABLE DEPOSIT CHANGE CNAME VARCHAR(35);`
D. `UPDATE TABLE DEPOSIT SET CNAME VARCHAR(35);`

**Answer:** B

**Explanation:** SQL Server uses `ALTER COLUMN`; `MODIFY` and `CHANGE` are MySQL syntax and are invalid in T-SQL.

---

### Q49. Which system stored procedure is used in SQL Server to rename a column or table?

**Difficulty:** Medium
**Lab:** Lab 5 — ALTER/RENAME/DELETE/TRUNCATE/DROP
**Topic:** sp_rename

A. sp_change
B. sp_rename
C. sp_alter
D. sp_columnrename

**Answer:** B

**Explanation:** sp_rename is the built-in SQL Server system procedure used to rename database objects such as tables and columns.

---

### Q50. Which is the correct syntax to rename the ACTNO column of DEPOSIT to ANO using sp_rename?

**Difficulty:** Medium
**Lab:** Lab 5 — ALTER/RENAME/DELETE/TRUNCATE/DROP
**Topic:** sp_rename Syntax

A. `EXEC sp_rename 'DEPOSIT.ACTNO', 'ANO', 'COLUMN';`
B. `EXEC sp_rename 'ANO', 'DEPOSIT.ACTNO', 'COLUMN';`
C. `EXEC sp_rename 'DEPOSIT', 'ACTNO', 'ANO';`
D. `EXEC sp_rename COLUMN 'DEPOSIT.ACTNO' TO 'ANO';`

**Answer:** A

**Explanation:** The correct argument order for sp_rename is: old_name (qualified with table name for columns), new_name, and object type ('COLUMN').

---

### Q51. Which command deletes only the rows where AMOUNT is less than or equal to 3000, keeping the table structure?

**Difficulty:** Medium
**Lab:** Lab 5 — ALTER/RENAME/DELETE/TRUNCATE/DROP
**Topic:** DELETE with WHERE

A. `TRUNCATE TABLE DEPOSIT WHERE AMOUNT <= 3000;`
B. `DELETE FROM DEPOSIT WHERE AMOUNT <= 3000;`
C. `DROP FROM DEPOSIT WHERE AMOUNT <= 3000;`
D. `DELETE DEPOSIT WHERE AMOUNT <= 3000 ONLY;`

**Answer:** B

**Explanation:** DELETE FROM with a WHERE clause removes only the rows matching the condition.

---

### Q52. Which statement about TRUNCATE TABLE compared to DELETE without WHERE is TRUE?

**Difficulty:** Medium
**Lab:** Lab 5 — ALTER/RENAME/DELETE/TRUNCATE/DROP
**Topic:** DELETE vs TRUNCATE

A. TRUNCATE removes the table structure while DELETE does not
B. TRUNCATE is generally faster and does not log individual row deletions the way DELETE does, but both remove all rows and keep the table structure
C. DELETE removes the table while TRUNCATE keeps only column names
D. There is no difference at all

**Answer:** B

**Explanation:** Both remove all data and keep the table structure, but TRUNCATE is a minimally logged, faster operation compared to row-by-row DELETE logging.

---

### Q53. Which SQL Server statement correctly renames the DEPOSIT table to DEPOSIT_DETAIL?

**Difficulty:** Hard
**Lab:** Lab 5 — ALTER/RENAME/DELETE/TRUNCATE/DROP
**Topic:** Table Rename

A. `RENAME TABLE DEPOSIT TO DEPOSIT_DETAIL;`
B. `ALTER TABLE DEPOSIT RENAME TO DEPOSIT_DETAIL;`
C. `EXEC sp_rename 'DEPOSIT', 'DEPOSIT_DETAIL';`
D. `EXEC sp_rename 'DEPOSIT', 'DEPOSIT_DETAIL', 'TABLE';`

**Answer:** C

**Explanation:** For renaming a table (not a column), sp_rename only needs the old name and new name; `RENAME TABLE` (MySQL) is not valid SQL Server syntax.

---

### Q54. Which statement correctly distinguishes DELETE FROM table (no WHERE) from TRUNCATE TABLE?

**Difficulty:** Hard
**Lab:** Lab 5 — ALTER/RENAME/DELETE/TRUNCATE/DROP
**Topic:** DELETE vs TRUNCATE

A. DELETE cannot be rolled back, TRUNCATE can always be rolled back
B. DELETE fires row-level triggers and can be used with WHERE; TRUNCATE cannot use WHERE and typically does not fire row-level DELETE triggers
C. TRUNCATE removes the table permanently while DELETE does not remove any rows
D. There is no functional difference between them

**Answer:** B

**Explanation:** DELETE operates row-by-row (allowing WHERE and firing triggers), while TRUNCATE deallocates data pages as a whole and cannot be conditioned with WHERE.

---

### Q55. Which of the following will result in an ERROR in SQL Server?

**Difficulty:** Hard
**Lab:** Lab 5 — ALTER/RENAME/DELETE/TRUNCATE/DROP
**Topic:** TRUNCATE Restrictions

A. `TRUNCATE TABLE DEPOSIT;`
B. `DELETE FROM DEPOSIT WHERE AMOUNT > 5000;`
C. `TRUNCATE TABLE DEPOSIT WHERE AMOUNT > 5000;`
D. `DROP TABLE DEPOSIT;`

**Answer:** C

**Explanation:** TRUNCATE TABLE does not support a WHERE clause, making option C a syntax error.

---

### Q56. What happens to DEPOSIT's column definitions and constraints after `TRUNCATE TABLE DEPOSIT;`?

**Difficulty:** Hard
**Lab:** Lab 5 — ALTER/RENAME/DELETE/TRUNCATE/DROP
**Topic:** TRUNCATE Effects

A. All columns and constraints are removed
B. The table structure, columns, and constraints remain unchanged; only data rows are removed
C. The table is deleted entirely
D. Only the constraints are removed

**Answer:** B

**Explanation:** TRUNCATE only clears the data; the table definition (columns, data types, constraints) is untouched.

---

### Q57. Which query correctly changes the data type of the AMOUNT column from decimal to int?

**Difficulty:** Hard
**Lab:** Lab 5 — ALTER/RENAME/DELETE/TRUNCATE/DROP
**Topic:** ALTER COLUMN Data Type

A. `ALTER TABLE DEPOSIT ALTER COLUMN AMOUNT INT;`
B. `ALTER TABLE DEPOSIT MODIFY AMOUNT INT;`
C. `UPDATE DEPOSIT SET AMOUNT AS INT;`
D. `ALTER COLUMN DEPOSIT AMOUNT INT;`

**Answer:** A

**Explanation:** `ALTER TABLE ... ALTER COLUMN ...` is the correct T-SQL syntax for changing a column's data type.

---

### Q58. Which sequence correctly orders DELETE (with WHERE), TRUNCATE, and DROP from LEAST to MOST destructive?

**Difficulty:** Very Hard
**Lab:** Lab 5 — ALTER/RENAME/DELETE/TRUNCATE/DROP
**Topic:** DELETE vs TRUNCATE vs DROP

A. DROP TABLE → TRUNCATE TABLE → DELETE FROM table WHERE condition
B. DELETE FROM table WHERE condition → TRUNCATE TABLE → DROP TABLE
C. TRUNCATE TABLE → DELETE FROM table WHERE condition → DROP TABLE
D. DROP TABLE → DELETE FROM table WHERE condition → TRUNCATE TABLE

**Answer:** B

**Explanation:** Conditional DELETE removes only some rows (least destructive), TRUNCATE removes all rows but keeps the structure, and DROP removes the entire table object (most destructive).

---

### Q59. A student runs `DROP TABLE DEPOSIT;` and then `EXEC sp_rename 'DEPOSIT.ACTNO', 'ANO', 'COLUMN';`. What is the most likely outcome?

**Difficulty:** Very Hard
**Lab:** Lab 5 — ALTER/RENAME/DELETE/TRUNCATE/DROP
**Topic:** DROP Consequences

A. The rename succeeds because DROP only hides the table
B. The rename fails because the DEPOSIT table no longer exists in the database
C. The rename creates a new DEPOSIT table automatically
D. The rename executes successfully but only for the ACTNO column

**Answer:** B

**Explanation:** DROP TABLE permanently removes the table object, so any subsequent reference to DEPOSIT.ACTNO fails since the object no longer exists.

---

### Q60. Which of these correctly deletes all accounts whose branch is 'BEDI' or 'MADHAPAR'?

**Difficulty:** Medium
**Lab:** Lab 5 — ALTER/RENAME/DELETE/TRUNCATE/DROP
**Topic:** DELETE with OR

A. `DELETE FROM DEPOSIT WHERE BNAME = 'BEDI' AND BNAME = 'MADHAPAR';`
B. `DELETE FROM DEPOSIT WHERE BNAME = 'BEDI' OR BNAME = 'MADHAPAR';`
C. `DELETE FROM DEPOSIT WHERE BNAME IN 'BEDI','MADHAPAR';`
D. `DELETE DEPOSIT SET BNAME = 'BEDI' OR 'MADHAPAR';`

**Answer:** B

**Explanation:** A row's BNAME cannot equal two different values at once, so AND (option A) would match nothing; OR is correct here.

---

### Q61. `DELETE FROM DEPOSIT WHERE BNAME IS NULL;` — how many rows are deleted from the original 11-row DEPOSIT table?

**Difficulty:** Hard
**Lab:** Lab 5 — ALTER/RENAME/DELETE/TRUNCATE/DROP
**Topic:** Output Prediction

A. 0
B. 1
C. 2
D. 11

**Answer:** B

**Explanation:** Only BANSI (ACTNO 111) has a NULL BNAME, so exactly 1 row is deleted.

---

### Q62. Which clause is used with SELECT to create a new table and copy data into it in a single statement?

**Difficulty:** Easy
**Lab:** Lab 6 — SELECT INTO
**Topic:** SELECT INTO Basics

A. INTO
B. COPY
C. CREATE FROM
D. IMPORT

**Answer:** A

**Explanation:** SELECT INTO combines table creation and data copying, e.g., `SELECT * INTO NewTable FROM OldTable;`.

---

### Q63. `SELECT * INTO HIGH_AMOUNT FROM DEPOSIT WHERE AMOUNT > 3000;` does what?

**Difficulty:** Easy
**Lab:** Lab 6 — SELECT INTO
**Topic:** SELECT INTO Behavior

A. Updates the existing HIGH_AMOUNT table
B. Creates a new table HIGH_AMOUNT and copies matching rows into it
C. Deletes rows from DEPOSIT
D. Throws an error because HIGH_AMOUNT does not exist

**Answer:** B

**Explanation:** SELECT INTO automatically creates the destination table with a matching structure and populates it with the query's result rows.

---

### Q64. After running the SELECT INTO query in Q63, what happens to the original DEPOSIT table?

**Difficulty:** Easy
**Lab:** Lab 6 — SELECT INTO
**Topic:** Source Table Impact

A. It is dropped
B. It remains completely unchanged
C. All matching rows are removed from it
D. It is renamed to HIGH_AMOUNT

**Answer:** B

**Explanation:** SELECT INTO only reads from the source table; it never modifies or deletes data in the source.

---

### Q65. Which query copies only distinct branch names from DEPOSIT into a new table BRANCH_LIST?

**Difficulty:** Medium
**Lab:** Lab 6 — SELECT INTO
**Topic:** SELECT INTO with DISTINCT

A. `SELECT DISTINCT BNAME INTO BRANCH_LIST FROM DEPOSIT;`
B. `SELECT BNAME INTO DISTINCT BRANCH_LIST FROM DEPOSIT;`
C. `CREATE TABLE BRANCH_LIST AS SELECT DISTINCT BNAME;`
D. `SELECT DISTINCT INTO BRANCH_LIST BNAME FROM DEPOSIT;`

**Answer:** A

**Explanation:** DISTINCT immediately follows SELECT, and INTO comes right after the selected column list.

---

### Q66. Which query copies the top 5 records from DEPOSIT into TOP_DEPOSITS?

**Difficulty:** Medium
**Lab:** Lab 6 — SELECT INTO
**Topic:** SELECT INTO with TOP

A. `SELECT TOP 5 * INTO TOP_DEPOSITS FROM DEPOSIT;`
B. `SELECT * INTO TOP_DEPOSITS TOP 5 FROM DEPOSIT;`
C. `SELECT * INTO TOP 5 TOP_DEPOSITS FROM DEPOSIT;`
D. `SELECT TOP(5) INTO * TOP_DEPOSITS FROM DEPOSIT;`

**Answer:** A

**Explanation:** TOP 5 must directly follow SELECT, before the column list, and INTO comes after the columns.

---

### Q67. Which statement about SELECT INTO vs INSERT INTO ... SELECT is TRUE?

**Difficulty:** Medium
**Lab:** Lab 6 — SELECT INTO
**Topic:** Comparison

A. SELECT INTO requires the destination table to already exist, while INSERT INTO ... SELECT creates it
B. SELECT INTO creates a new destination table automatically, while INSERT INTO ... SELECT requires the destination table to already exist
C. Both require the destination table to already exist
D. Both automatically create the destination table

**Answer:** B

**Explanation:** SELECT INTO is used specifically to create a new table on the fly; INSERT INTO ... SELECT copies rows into a pre-existing table.

---

### Q68. How many columns will the new table have after: `SELECT CNAME, AMOUNT INTO MAVDI_CUSTOMERS FROM DEPOSIT WHERE BNAME = 'MAVDI';`?

**Difficulty:** Medium
**Lab:** Lab 6 — SELECT INTO
**Topic:** Output Prediction

A. 1
B. 2
C. 5
D. It depends on the WHERE clause

**Answer:** B

**Explanation:** The new table's columns match exactly the columns listed in SELECT — CNAME and AMOUNT — regardless of the WHERE filter.

---

### Q69. How many rows will exist in MAVDI_CUSTOMERS after the query in Q68?

**Difficulty:** Hard
**Lab:** Lab 6 — SELECT INTO
**Topic:** Output Prediction

A. 1
B. 2
C. 3
D. 0

**Answer:** B

**Explanation:** Two DEPOSIT rows have BNAME = 'MAVDI': MEET (ACTNO 101) and RIYA (ACTNO 104) — 2 rows copied.

---

### Q70. Which query creates an empty table STUDENT_BACKUP with the same structure as STUDENT but with no rows?

**Difficulty:** Hard
**Lab:** Lab 6 — SELECT INTO
**Topic:** Empty Table via SELECT INTO

A. `SELECT * INTO STUDENT_BACKUP FROM STUDENT WHERE 1 = 0;`
B. `SELECT * INTO STUDENT_BACKUP FROM STUDENT WHERE 1 = 1;`
C. `CREATE TABLE STUDENT_BACKUP LIKE STUDENT;`
D. `SELECT * INTO STUDENT_BACKUP FROM STUDENT LIMIT 0;`

**Answer:** A

**Explanation:** An impossible WHERE condition (1=0) ensures no rows match, so only the table structure is created; LIMIT is not valid SQL Server syntax.

---

### Q71. `SELECT AMOUNT AS BALANCE INTO DEPOSIT_COPY FROM DEPOSIT;` is executed. Which statement about DEPOSIT_COPY is TRUE?

**Difficulty:** Very Hard
**Lab:** Lab 6 — SELECT INTO
**Topic:** Column Alias in SELECT INTO

A. It has a column named AMOUNT
B. It has a column named BALANCE, since the alias becomes the new table's column name
C. It fails because SELECT INTO does not support aliases
D. It copies all columns of DEPOSIT, not just AMOUNT

**Answer:** B

**Explanation:** In SELECT INTO, any column alias defined in the SELECT list becomes the actual column name in the newly created table.

---

### Q72. Which wildcard character represents zero or more characters in a LIKE pattern?

**Difficulty:** Easy
**Lab:** Lab 7 — LIKE / Pattern Searching
**Topic:** Wildcards

A. `_`
B. `%`
C. `*`
D. `?`

**Answer:** B

**Explanation:** `%` matches any sequence of zero or more characters in SQL Server pattern matching.

---

### Q73. Which wildcard character represents exactly one character in a LIKE pattern?

**Difficulty:** Easy
**Lab:** Lab 7 — LIKE / Pattern Searching
**Topic:** Wildcards

A. `%`
B. `_`
C. `#`
D. `^`

**Answer:** B

**Explanation:** The underscore `_` matches exactly one character in a LIKE pattern.

---

### Q74. Which pattern finds FIRSTNAME values that start with 'H'?

**Difficulty:** Medium
**Lab:** Lab 7 — LIKE / Pattern Searching
**Topic:** Prefix Search

A. `LIKE '%H'`
B. `LIKE 'H%'`
C. `LIKE '_H%'`
D. `LIKE '%H%'`

**Answer:** B

**Explanation:** `'H%'` matches any string starting with H, followed by zero or more characters.

---

### Q75. Which pattern finds FIRSTNAME values containing 'AR' anywhere in the name?

**Difficulty:** Medium
**Lab:** Lab 7 — LIKE / Pattern Searching
**Topic:** Contains Search

A. `LIKE 'AR%'`
B. `LIKE '%AR'`
C. `LIKE '%AR%'`
D. `LIKE '_AR_'`

**Answer:** C

**Explanation:** Placing `%` on both sides of 'AR' matches names that contain 'AR' anywhere within them.

---

### Q76. Which pattern finds FIRSTNAME values consisting of EXACTLY 5 characters?

**Difficulty:** Medium
**Lab:** Lab 7 — LIKE / Pattern Searching
**Topic:** Exact Character Count

A. `LIKE '%%%%%'`
B. `LIKE '_____'`
C. `LIKE '5%'`
D. `LIKE '%5'`

**Answer:** B

**Explanation:** Five underscores each represent exactly one character, so the pattern matches strings of precisely 5 characters.

---

### Q77. Which pattern finds FIRSTNAME values where the third character is 'S'?

**Difficulty:** Medium
**Lab:** Lab 7 — LIKE / Pattern Searching
**Topic:** Specific Character Position

A. `LIKE '__S%'`
B. `LIKE 'S__%'`
C. `LIKE '%S__'`
D. `LIKE '_S_%'`

**Answer:** A

**Explanation:** Two underscores match the first two (any) characters, then S must appear as the third character, followed by anything.

---

### Q78. Which pattern is used to find FIRSTNAME values that start with 'R' and end with 'A'?

**Difficulty:** Medium
**Lab:** Lab 7 — LIKE / Pattern Searching
**Topic:** Prefix and Suffix Search

A. `LIKE 'R%A'`
B. `LIKE '%R_A%'`
C. `LIKE 'RA%'`
D. `LIKE '%RA'`

**Answer:** A

**Explanation:** `'R%A'` requires the string to start with R and end with A, with any number of characters in between.

---

### Q79. Applying the pattern `LIKE 'V_S%'` to a FIRSTNAME column, which name would MATCH?

**Difficulty:** Hard
**Lab:** Lab 7 — LIKE / Pattern Searching
**Topic:** Pattern Matching

A. VISHAL
B. VRUNDA
C. VYAS
D. VAS

**Answer:** A

**Explanation:** VISHAL breaks down as V-I-S-HAL: V matches, I matches the single `_`, S matches literally, and HAL matches `%` — so it fits `V_S%`.

---

### Q80. How many EMPLOYEE rows match `FIRSTNAME LIKE '%A%'` given first names HETVI, RAJ, VISHAL, DEEP, DHAVAL, RIYA, PARAG, VRUNDA, MEHUL, MUBIN, MAYANK?

**Difficulty:** Hard
**Lab:** Lab 7 — LIKE / Pattern Searching
**Topic:** Output Prediction

A. 5
B. 6
C. 7
D. 8

**Answer:** C

**Explanation:** Names containing 'A': RAJ, VISHAL, DHAVAL, RIYA, PARAG, VRUNDA, MAYANK — 7 matches (HETVI, DEEP, MEHUL, MUBIN do not contain 'A').

---

### Q81. A student writes `WHERE FIRSTNAME LIKE 'H_'` intending to find names starting with H having exactly 2 characters. Testing on FIRSTNAME = 'HETVI', which is TRUE?

**Difficulty:** Hard
**Lab:** Lab 7 — LIKE / Pattern Searching
**Topic:** % vs _ Trap

A. It matches, because % is implied
B. It does not match, because `_` represents only one character and HETVI has 5 characters
C. It matches because H is the first character
D. It causes a syntax error

**Answer:** B

**Explanation:** `'H_'` requires exactly 2 characters total (H followed by exactly one more); HETVI has 5 characters, so it does not match — a classic `%` vs `_` confusion trap.

---

### Q82. Which query correctly displays employees whose FIRSTNAME does NOT start with 'B'?

**Difficulty:** Hard
**Lab:** Lab 7 — LIKE / Pattern Searching
**Topic:** NOT LIKE

A. `SELECT * FROM EMPLOYEE WHERE FIRSTNAME NOT LIKE 'B%';`
B. `SELECT * FROM EMPLOYEE WHERE FIRSTNAME <> 'B%';`
C. `SELECT * FROM EMPLOYEE WHERE FIRSTNAME LIKE NOT 'B%';`
D. `SELECT * FROM EMPLOYEE WHERE NOT FIRSTNAME = 'B%';`

**Answer:** A

**Explanation:** NOT LIKE is required for pattern-based negation; `<>` performs literal string comparison and would not treat '%' as a wildcard.

---

### Q83. Which pattern correctly matches CITY values that end with 'T' and are exactly 6 characters long (e.g., 'RAJKOT')?

**Difficulty:** Very Hard
**Lab:** Lab 7 — LIKE / Pattern Searching
**Topic:** Combined Length and Suffix

A. `LIKE '%T'`
B. `LIKE '_____T'`
C. `LIKE 'T_____'`
D. `LIKE '%_T'`

**Answer:** B

**Explanation:** Five underscores plus a literal T equal exactly 6 characters, with the last one fixed as T — matching 'RAJKOT' precisely.

---

### Q84. Which function returns the total number of rows in a result set?

**Difficulty:** Easy
**Lab:** Lab 8 — Aggregate Functions + GROUP BY
**Topic:** COUNT

A. SUM()
B. COUNT()
C. TOTAL()
D. ADD()

**Answer:** B

**Explanation:** COUNT() is the aggregate function used to count rows.

---

### Q85. Which clause groups rows sharing a common value so aggregate functions can be applied per group?

**Difficulty:** Easy
**Lab:** Lab 8 — Aggregate Functions + GROUP BY
**Topic:** GROUP BY

A. WHERE
B. ORDER BY
C. GROUP BY
D. HAVING

**Answer:** C

**Explanation:** GROUP BY organizes rows into groups based on one or more columns, enabling per-group aggregate calculations.

---

### Q86. What is the difference between COUNT(*) and COUNT(column_name)?

**Difficulty:** Medium
**Lab:** Lab 8 — Aggregate Functions + GROUP BY
**Topic:** COUNT(*) vs COUNT(column)

A. COUNT(*) counts only non-NULL rows of the whole table, COUNT(column_name) counts all rows
B. COUNT(*) counts all rows including those with NULLs, COUNT(column_name) counts only rows where that column is NOT NULL
C. Both always return the same value
D. COUNT(*) is invalid in SQL Server

**Answer:** B

**Explanation:** COUNT(*) counts every row regardless of NULLs, while COUNT(column_name) excludes rows where that specific column is NULL.

---

### Q87. Given EMPLOYEE.CITY has one NULL value (EID 111), what does `SELECT COUNT(CITY) FROM EMPLOYEE;` return, out of 11 total rows?

**Difficulty:** Medium
**Lab:** Lab 8 — Aggregate Functions + GROUP BY
**Topic:** NULL in Aggregates

A. 11
B. 10
C. 0
D. NULL

**Answer:** B

**Explanation:** COUNT(CITY) ignores the one row with a NULL city, so it returns 10.

---

### Q88. Which query correctly finds the maximum salary in the IT department?

**Difficulty:** Medium
**Lab:** Lab 8 — Aggregate Functions + GROUP BY
**Topic:** MAX with WHERE

A. `SELECT MAX(SALARY) FROM EMPLOYEE WHERE DEPARTMENT = 'IT';`
B. `SELECT MAX(SALARY) FROM EMPLOYEE GROUP BY 'IT';`
C. `SELECT SALARY FROM EMPLOYEE WHERE DEPARTMENT='IT' HAVING MAX(SALARY);`
D. `SELECT MAX(DEPARTMENT) FROM EMPLOYEE WHERE SALARY='IT';`

**Answer:** A

**Explanation:** Filtering by department first with WHERE, then applying MAX(SALARY), correctly returns the highest IT salary.

---

### Q89. Which query displays each department along with its maximum salary?

**Difficulty:** Medium
**Lab:** Lab 8 — Aggregate Functions + GROUP BY
**Topic:** GROUP BY with Aggregate

A. `SELECT DEPARTMENT, MAX(SALARY) FROM EMPLOYEE GROUP BY DEPARTMENT;`
B. `SELECT DEPARTMENT, MAX(SALARY) FROM EMPLOYEE;`
C. `SELECT MAX(SALARY) FROM EMPLOYEE GROUP BY DEPARTMENT WHERE DEPARTMENT IS NOT NULL;`
D. `SELECT DEPARTMENT, MAX(SALARY) FROM EMPLOYEE ORDER BY DEPARTMENT;`

**Answer:** A

**Explanation:** GROUP BY DEPARTMENT is required whenever a non-aggregated column (DEPARTMENT) is selected alongside an aggregate function; option B would cause an error in SQL Server.

---

### Q90. Based on EMPLOYEE data, what is the total salary of ADMIN department employees (HETVI 12000, DEEP 12500)?

**Difficulty:** Hard
**Lab:** Lab 8 — Aggregate Functions + GROUP BY
**Topic:** Output Prediction

A. 12000
B. 12500
C. 24500
D. 25000

**Answer:** C

**Explanation:** SUM(SALARY) for ADMIN = 12000 + 12500 = 24500.

---

### Q91. Which query is INVALID in SQL Server due to mixing an aggregate and non-aggregate column without GROUP BY?

**Difficulty:** Hard
**Lab:** Lab 8 — Aggregate Functions + GROUP BY
**Topic:** Aggregate vs Non-Aggregate Columns

A. `SELECT DEPARTMENT, COUNT(*) FROM EMPLOYEE GROUP BY DEPARTMENT;`
B. `SELECT DEPARTMENT, AVG(SALARY) FROM EMPLOYEE;`
C. `SELECT COUNT(*) FROM EMPLOYEE;`
D. `SELECT AVG(SALARY) FROM EMPLOYEE WHERE DEPARTMENT = 'HR';`

**Answer:** B

**Explanation:** Selecting DEPARTMENT alongside AVG(SALARY) without a GROUP BY clause causes a SQL Server error, since DEPARTMENT is not aggregated or grouped.

---

### Q92. What does `SELECT COUNT(DISTINCT CITY) FROM EMPLOYEE;` count?

**Difficulty:** Hard
**Lab:** Lab 8 — Aggregate Functions + GROUP BY
**Topic:** COUNT(DISTINCT column)

A. Total number of employees
B. Total number of rows including duplicates and NULLs
C. Number of unique non-NULL CITY values
D. Number of departments

**Answer:** C

**Explanation:** COUNT(DISTINCT CITY) counts each unique CITY value only once and automatically excludes NULLs.

---

### Q93. Which clause filters groups AFTER aggregation, unlike WHERE which filters rows BEFORE grouping?

**Difficulty:** Medium
**Lab:** Lab 9 — GROUP BY + HAVING + ORDER BY
**Topic:** WHERE vs HAVING

A. WHERE
B. HAVING
C. ORDER BY
D. GROUP BY

**Answer:** B

**Explanation:** HAVING is applied after GROUP BY has formed groups and aggregates have been computed, allowing conditions on aggregate results.

---

### Q94. Which query displays departments having a total salary greater than 20000?

**Difficulty:** Medium
**Lab:** Lab 9 — GROUP BY + HAVING + ORDER BY
**Topic:** HAVING with SUM

A. `SELECT DEPARTMENT, SUM(SALARY) FROM EMPLOYEE WHERE SUM(SALARY) > 20000 GROUP BY DEPARTMENT;`
B. `SELECT DEPARTMENT, SUM(SALARY) FROM EMPLOYEE GROUP BY DEPARTMENT HAVING SUM(SALARY) > 20000;`
C. `SELECT DEPARTMENT, SUM(SALARY) FROM EMPLOYEE HAVING SUM(SALARY) > 20000;`
D. `SELECT DEPARTMENT, SUM(SALARY) FROM EMPLOYEE GROUP BY DEPARTMENT WHERE SUM(SALARY) > 20000;`

**Answer:** B

**Explanation:** WHERE cannot contain aggregate functions like SUM(); the correct approach uses GROUP BY followed by HAVING.

---

### Q95. To sort results by an aggregate value in descending order, which clause is used at the end of the query?

**Difficulty:** Medium
**Lab:** Lab 9 — GROUP BY + HAVING + ORDER BY
**Topic:** ORDER BY Aggregate

A. `GROUP BY SUM(SALARY) DESC`
B. `ORDER BY SUM(SALARY) DESC`
C. `HAVING SUM(SALARY) DESC`
D. `WHERE SUM(SALARY) DESC`

**Answer:** B

**Explanation:** ORDER BY can reference an aggregate expression directly to sort the final grouped result set.

---

### Q96. Fill the blank: `SELECT DEPARTMENT, AVG(SALARY) FROM EMPLOYEE _____ DEPARTMENT HAVING AVG(SALARY) > 12000;`

**Difficulty:** Hard
**Lab:** Lab 9 — GROUP BY + HAVING + ORDER BY
**Topic:** Fill-the-Syntax

A. WHERE
B. GROUP BY
C. ORDER BY
D. HAVING

**Answer:** B

**Explanation:** GROUP BY DEPARTMENT must precede HAVING to define the groups over which AVG(SALARY) is calculated.

---

### Q97. What is the correct logical order of execution of SQL clauses when a query contains SELECT, FROM, WHERE, GROUP BY, HAVING, and ORDER BY?

**Difficulty:** Hard
**Lab:** Lab 9 — GROUP BY + HAVING + ORDER BY
**Topic:** Clause Execution Order

A. SELECT → FROM → WHERE → GROUP BY → HAVING → ORDER BY
B. FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY
C. FROM → GROUP BY → WHERE → HAVING → SELECT → ORDER BY
D. SELECT → FROM → GROUP BY → WHERE → HAVING → ORDER BY

**Answer:** B

**Explanation:** SQL Server logically processes FROM first, then WHERE (row filtering), GROUP BY (grouping), HAVING (group filtering), SELECT (column projection), and finally ORDER BY (sorting) — even though it is written differently.

---

### Q98. Which pair of conditions would generally produce DIFFERENT results when applied to the EMPLOYEE table?

**Difficulty:** Very Hard
**Lab:** Lab 9 — GROUP BY + HAVING + ORDER BY
**Topic:** WHERE vs HAVING Trap

A. `WHERE SALARY > 10000` (filters individual employee rows before grouping) vs. `HAVING AVG(SALARY) > 10000` (filters entire groups based on their average salary)
B. `GROUP BY DEPARTMENT` vs. `GROUP BY DEPARTMENT, CITY` when only one column is selected
C. `ORDER BY SALARY ASC` vs. `ORDER BY SALARY DESC` on a single-row result
D. `SELECT *` vs. `SELECT * with DISTINCT` on a table with no duplicate rows

**Answer:** A

**Explanation:** WHERE removes individual rows before grouping occurs, while HAVING evaluates the aggregated result of a group — these operate on fundamentally different things and typically yield different result sets.

---

### Q99. For `SELECT DEPARTMENT, MAX(SALARY) FROM EMPLOYEE GROUP BY DEPARTMENT HAVING MAX(SALARY) > 13000 ORDER BY MAX(SALARY) DESC;`, which department appears FIRST in the output? (Department max salaries: HR=15000, IT=14000, ADMIN=12500, SERVER=10000, TRANSPORT=12000, ACCOUNT=13000)

**Difficulty:** Very Hard
**Lab:** Lab 9 — GROUP BY + HAVING + ORDER BY
**Topic:** GROUP BY + HAVING + ORDER BY Output

A. IT
B. HR
C. ACCOUNT
D. ADMIN

**Answer:** B

**Explanation:** Only HR (15000) and IT (14000) exceed 13000; sorted by MAX(SALARY) DESC, HR (the highest) appears first.

---

### Q100. A student writes: `SELECT DEPARTMENT, COUNT(*) FROM EMPLOYEE WHERE JOININGYEAR > 2022 GROUP BY DEPARTMENT HAVING COUNT(*) > 1;` to find departments with more than one employee who joined after 2022. Is this query logically correct?

**Difficulty:** Very Hard
**Lab:** Lab 9 — GROUP BY + HAVING + ORDER BY
**Topic:** Combined WHERE + GROUP BY + HAVING Trap

A. No, because WHERE cannot be combined with GROUP BY in SQL Server
B. No, because COUNT(*) cannot appear in HAVING
C. Yes — WHERE correctly filters rows (employees joined after 2022) before grouping, and HAVING correctly filters the resulting groups by count
D. No, because JOININGYEAR cannot be used in WHERE

**Answer:** C

**Explanation:** This is valid and correct SQL Server syntax: WHERE filters rows before aggregation, GROUP BY forms department groups from the filtered rows, and HAVING filters those groups by their row count.

---

# Answer Key

| Q | Answer | Difficulty | Lab |
|---|--------|------------|-----|
| 1 | A | Easy | Lab 1 |
| 2 | B | Easy | Lab 1 |
| 3 | B | Easy | Lab 1 |
| 4 | A | Medium | Lab 1 |
| 5 | B | Medium | Lab 1 |
| 6 | C | Easy | Lab 2 |
| 7 | B | Easy | Lab 2 |
| 8 | B | Easy | Lab 2 |
| 9 | B | Easy | Lab 2 |
| 10 | A | Medium | Lab 2 |
| 11 | B | Medium | Lab 2 |
| 12 | B | Medium | Lab 2 |
| 13 | D | Medium | Lab 2 |
| 14 | A | Hard | Lab 2 |
| 15 | B | Hard | Lab 2 |
| 16 | B | Easy | Lab 3 |
| 17 | B | Easy | Lab 3 |
| 18 | B | Easy | Lab 3 |
| 19 | B | Easy | Lab 3 |
| 20 | B | Easy | Lab 3 |
| 21 | B | Medium | Lab 3 |
| 22 | B | Medium | Lab 3 |
| 23 | A | Medium | Lab 3 |
| 24 | C | Medium | Lab 3 |
| 25 | B | Medium | Lab 3 |
| 26 | B | Medium | Lab 3 |
| 27 | A | Medium | Lab 3 |
| 28 | B | Hard | Lab 3 |
| 29 | C | Hard | Lab 3 |
| 30 | B | Hard | Lab 3 |
| 31 | A | Hard | Lab 3 |
| 32 | B | Very Hard | Lab 3 |
| 33 | B | Very Hard | Lab 3 |
| 34 | B | Easy | Lab 4 |
| 35 | B | Easy | Lab 4 |
| 36 | A | Easy | Lab 4 |
| 37 | B | Medium | Lab 4 |
| 38 | C | Medium | Lab 4 |
| 39 | C | Medium | Lab 4 |
| 40 | B | Medium | Lab 4 |
| 41 | C | Hard | Lab 4 |
| 42 | C | Hard | Lab 4 |
| 43 | B | Very Hard | Lab 4 |
| 44 | B | Easy | Lab 5 |
| 45 | C | Easy | Lab 5 |
| 46 | C | Easy | Lab 5 |
| 47 | B | Medium | Lab 5 |
| 48 | B | Medium | Lab 5 |
| 49 | B | Medium | Lab 5 |
| 50 | A | Medium | Lab 5 |
| 51 | B | Medium | Lab 5 |
| 52 | B | Medium | Lab 5 |
| 53 | C | Hard | Lab 5 |
| 54 | B | Hard | Lab 5 |
| 55 | C | Hard | Lab 5 |
| 56 | B | Hard | Lab 5 |
| 57 | A | Hard | Lab 5 |
| 58 | B | Very Hard | Lab 5 |
| 59 | B | Very Hard | Lab 5 |
| 60 | B | Medium | Lab 5 |
| 61 | B | Hard | Lab 5 |
| 62 | A | Easy | Lab 6 |
| 63 | B | Easy | Lab 6 |
| 64 | B | Easy | Lab 6 |
| 65 | A | Medium | Lab 6 |
| 66 | A | Medium | Lab 6 |
| 67 | B | Medium | Lab 6 |
| 68 | B | Medium | Lab 6 |
| 69 | B | Hard | Lab 6 |
| 70 | A | Hard | Lab 6 |
| 71 | B | Very Hard | Lab 6 |
| 72 | B | Easy | Lab 7 |
| 73 | B | Easy | Lab 7 |
| 74 | B | Medium | Lab 7 |
| 75 | C | Medium | Lab 7 |
| 76 | B | Medium | Lab 7 |
| 77 | A | Medium | Lab 7 |
| 78 | A | Medium | Lab 7 |
| 79 | A | Hard | Lab 7 |
| 80 | C | Hard | Lab 7 |
| 81 | B | Hard | Lab 7 |
| 82 | A | Hard | Lab 7 |
| 83 | B | Very Hard | Lab 7 |
| 84 | B | Easy | Lab 8 |
| 85 | C | Easy | Lab 8 |
| 86 | B | Medium | Lab 8 |
| 87 | B | Medium | Lab 8 |
| 88 | A | Medium | Lab 8 |
| 89 | A | Medium | Lab 8 |
| 90 | C | Hard | Lab 8 |
| 91 | B | Hard | Lab 8 |
| 92 | C | Hard | Lab 8 |
| 93 | B | Medium | Lab 9 |
| 94 | B | Medium | Lab 9 |
| 95 | B | Medium | Lab 9 |
| 96 | B | Hard | Lab 9 |
| 97 | B | Hard | Lab 9 |
| 98 | A | Very Hard | Lab 9 |
| 99 | B | Very Hard | Lab 9 |
| 100 | C | Very Hard | Lab 9 |

---

# Quick Revision — Important Traps

**NULL handling**
- `NULL = NULL` is never TRUE — it evaluates to UNKNOWN. Always use `IS NULL` / `IS NOT NULL`, never `= NULL`.
- `<>` and `<> 'value'` silently exclude rows where the column is NULL, since the comparison result is UNKNOWN, not TRUE.
- Aggregate functions like SUM, AVG, MIN, MAX, COUNT(column) all ignore NULL values; only COUNT(*) counts NULL rows too.

**BETWEEN / IN**
- `BETWEEN a AND b` is inclusive of both endpoints.
- `IN (...)` is shorthand for multiple OR conditions; `NOT IN (...)` excludes all listed values but returns no rows if the list itself contains a NULL.

**AND / OR precedence**
- AND is evaluated before OR unless parentheses are used. Always use parentheses to make intent explicit in mixed conditions.

**LIKE, % vs _**
- `%` = zero or more characters. `_` = exactly one character. Confusing the two is one of the most common exam traps (e.g., `'H_'` only matches 2-character names starting with H, not all H-names).

**TOP / TOP PERCENT**
- `TOP n` returns a fixed row count; `TOP n PERCENT` returns a row count calculated as a percentage of the total matching rows.

**DISTINCT**
- Removes duplicate rows from the *entire selected row*, not per-column.

**UPDATE / DELETE without WHERE**
- Both apply to *every row* in the table if WHERE is omitted — always double-check before executing.

**DELETE vs TRUNCATE vs DROP**
- DELETE: removes rows (optionally filtered by WHERE), keeps structure, can fire triggers, is fully logged.
- TRUNCATE: removes *all* rows, keeps structure, cannot use WHERE, minimally logged, faster.
- DROP: removes the entire table object (structure + data) permanently.

**ALTER TABLE / sp_rename**
- SQL Server uses `ALTER TABLE ... ALTER COLUMN ...` (not MODIFY or CHANGE, which are MySQL).
- `sp_rename` argument order: old_name (table.column for columns), new_name, object_type ('COLUMN' for columns, omitted for tables).

**SELECT INTO**
- Creates a *new* table automatically and copies matching rows; the source table is untouched.
- Column aliases used in the SELECT list become actual column names in the new table.
- `WHERE 1=0` is a common trick to copy only structure, no data.

**COUNT(*) vs COUNT(column)**
- COUNT(*) counts all rows, including NULLs. COUNT(column) counts only non-NULL values in that column. COUNT(DISTINCT column) counts unique non-NULL values.

**SUM / AVG / MIN / MAX**
- All ignore NULLs when computing their result; a column of all NULLs returns NULL for SUM/AVG/MIN/MAX, not zero.

**GROUP BY**
- Any non-aggregated column in SELECT must appear in GROUP BY, or the query errors out in SQL Server.

**HAVING vs WHERE**
- WHERE filters individual rows *before* grouping and cannot contain aggregate functions.
- HAVING filters *groups* after aggregation and is the only place aggregate conditions (like `SUM(SALARY) > 20000`) can be used.

**ORDER BY, ASC/DESC**
- Default sort order is ASC if not specified. ORDER BY can reference column aliases or aggregate expressions directly.

**Clause execution order (logical processing order)**
```
FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY
```
This differs from the order clauses are *written* in a query, which is:
```
SELECT → FROM → WHERE → GROUP BY → HAVING → ORDER BY
```
