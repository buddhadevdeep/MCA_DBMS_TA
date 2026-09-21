# Lab 20 – Implement Window Functions for Advanced Data Analysis

## Part – A

### From the table STUDENT

### 1. Display rank of students based on SPI.

```sql
SELECT SNAME, SPI,
       RANK() OVER (ORDER BY SPI DESC) AS RANK
FROM STUDENT;
```

### 2. Display dense rank of students based on SPI.

```sql
SELECT SNAME, SPI,
       DENSE_RANK() OVER (ORDER BY SPI DESC) AS DENSE_RANK
FROM STUDENT;
```

### 3. Display sequential number for each student record.

```sql
SELECT SNAME, SPI,
       ROW_NUMBER() OVER (ORDER BY SID) AS SEQ_NO
FROM STUDENT;
```

### 4. Display branch-wise rank of students.

```sql
SELECT SNAME, BRANCH, SPI,
       RANK() OVER
       (PARTITION BY BRANCH ORDER BY SPI DESC) AS BRANCH_RANK
FROM STUDENT;
```

### 5. Display branch-wise dense ranking of students.

```sql
SELECT SNAME, BRANCH, SPI,
       DENSE_RANK() OVER
       (PARTITION BY BRANCH ORDER BY SPI DESC) AS BRANCH_DENSE_RANK
FROM STUDENT;
```

### 6. Display branch-wise sequential numbering of students.

```sql
SELECT SNAME, BRANCH, SPI,
       ROW_NUMBER() OVER
       (PARTITION BY BRANCH ORDER BY SPI DESC) AS BRANCH_SEQ_NO
FROM STUDENT;
```

### 7. Display SNAME, Current SPI, Previous SPI and SPI Difference with previous student in ascending order of SPI.

```sql
SELECT SNAME,
       SPI AS CURRENT_SPI,
       LAG(SPI) OVER (ORDER BY SPI) AS PREVIOUS_SPI,
       SPI - LAG(SPI) OVER (ORDER BY SPI) AS SPI_DIFFERENCE
FROM STUDENT
ORDER BY SPI;
```

### 8. Display SNAME, Current SPI, Next SPI and SPI Difference with next student in descending order of SPI.

```sql
SELECT SNAME,
       SPI AS CURRENT_SPI,
       LEAD(SPI) OVER (ORDER BY SPI DESC) AS NEXT_SPI,
       SPI - LEAD(SPI) OVER (ORDER BY SPI DESC) AS SPI_DIFFERENCE
FROM STUDENT
ORDER BY SPI DESC;
```

### 9. Display top 3 students based on SPI.

```sql
SELECT SNAME, BRANCH, SPI
FROM
(
    SELECT SNAME, BRANCH, SPI,
           ROW_NUMBER() OVER (ORDER BY SPI DESC) AS RN
    FROM STUDENT
) S
WHERE RN <= 3;
```

### 10. Display top 2 students from each branch.

```sql
SELECT SNAME, BRANCH, SPI
FROM
(
    SELECT SNAME, BRANCH, SPI,
           ROW_NUMBER() OVER
           (PARTITION BY BRANCH ORDER BY SPI DESC) AS RN
    FROM STUDENT
) S
WHERE RN <= 2;
```

---

# Part – B

### 11. Display 5th highest SPI.

```sql
SELECT SPI
FROM
(
    SELECT SPI,
           DENSE_RANK() OVER (ORDER BY SPI DESC) AS DR
    FROM STUDENT
) S
WHERE DR = 5;
```

### 12. Display 6th highest SPI.

```sql
SELECT SPI
FROM
(
    SELECT SPI,
           DENSE_RANK() OVER (ORDER BY SPI DESC) AS DR
    FROM STUDENT
) S
WHERE DR = 6;
```

### 13. Display students having same ranking.

```sql
SELECT SNAME, SPI,
       RANK() OVER (ORDER BY SPI DESC) AS RANK
FROM STUDENT
WHERE SPI IN
(
    SELECT SPI
    FROM STUDENT
    GROUP BY SPI
    HAVING COUNT(*) > 1
);
```

### 14. Display SNAME, Previous SPI, Current SPI and Next SPI based on ascending order of SPI.

```sql
SELECT SNAME,
       LAG(SPI) OVER (ORDER BY SPI) AS PREVIOUS_SPI,
       SPI AS CURRENT_SPI,
       LEAD(SPI) OVER (ORDER BY SPI) AS NEXT_SPI
FROM STUDENT
ORDER BY SPI;
```

### 15. Display topper of each branch.

```sql
SELECT SNAME, BRANCH, SPI
FROM
(
    SELECT SNAME, BRANCH, SPI,
           RANK() OVER
           (PARTITION BY BRANCH ORDER BY SPI DESC) AS RANK
    FROM STUDENT
) S
WHERE RANK = 1;
```

---

# Part – C

### 16. Display students whose SPI is greater than the previous student and less than the next student.

```sql
SELECT SNAME, SPI
FROM
(
    SELECT SNAME, SPI,
           LAG(SPI) OVER (ORDER BY SID) AS PREVIOUS_SPI,
           LEAD(SPI) OVER (ORDER BY SID) AS NEXT_SPI
    FROM STUDENT
) S
WHERE SPI > PREVIOUS_SPI
  AND SPI < NEXT_SPI;
```

### 17. Display branch-wise second topper students.

```sql
SELECT SNAME, BRANCH, SPI
FROM
(
    SELECT SNAME, BRANCH, SPI,
           DENSE_RANK() OVER
           (PARTITION BY BRANCH ORDER BY SPI DESC) AS DR
    FROM STUDENT
) S
WHERE DR = 2;
```

### 18. Display students whose rank and dense rank are different.

```sql
SELECT SNAME, SPI, RANK, DENSE_RANK
FROM
(
    SELECT SNAME, SPI,
           RANK() OVER (ORDER BY SPI DESC) AS RANK,
           DENSE_RANK() OVER (ORDER BY SPI DESC) AS DENSE_RANK
    FROM STUDENT
) S
WHERE RANK <> DENSE_RANK;
```

### 19. Display consecutive students having same branch ordered by SPI.

```sql
SELECT SNAME, BRANCH, SPI
FROM
(
    SELECT SNAME, BRANCH, SPI,
           LAG(BRANCH) OVER (ORDER BY SPI) AS PREVIOUS_BRANCH,
           LEAD(BRANCH) OVER (ORDER BY SPI) AS NEXT_BRANCH
    FROM STUDENT
) S
WHERE BRANCH = PREVIOUS_BRANCH
   OR BRANCH = NEXT_BRANCH
ORDER BY SPI;
```

### 20. Display students whose SPI difference with previous student is maximum.

```sql
SELECT SNAME, SPI, SPI_DIFFERENCE
FROM
(
    SELECT SNAME, SPI,
           SPI - LAG(SPI) OVER (ORDER BY SPI) AS SPI_DIFFERENCE
    FROM STUDENT
) S
WHERE SPI_DIFFERENCE =
(
    SELECT MAX(SPI_DIFFERENCE)
    FROM
    (
        SELECT SPI - LAG(SPI) OVER (ORDER BY SPI) AS SPI_DIFFERENCE
        FROM STUDENT
    ) T
);
```
