# Lab 18 – Perform SQL Queries Using Subqueries

## Part – A

### From the table STUDENT

### 1. Display the details of students whose SPI is greater than the average SPI.

```sql
SELECT *
FROM STUDENT
WHERE SPI > (SELECT AVG(SPI) FROM STUDENT);
```

### 2. Display the names of students whose SPI is less than the average SPI.

```sql
SELECT NAME
FROM STUDENT
WHERE SPI < (SELECT AVG(SPI) FROM STUDENT);
```

### 3. Display the student details who has the highest SPI.

```sql
SELECT *
FROM STUDENT
WHERE SPI >= ALL (SELECT SPI FROM STUDENT);
```

### 4. Display the student details who has the lowest SPI.

```sql
SELECT *
FROM STUDENT
WHERE SPI <= ALL (SELECT SPI FROM STUDENT);
```

### 5. Display the students whose SPI is greater than SPI of student DHARMIK.

```sql
SELECT *
FROM STUDENT
WHERE SPI > ALL
(
    SELECT SPI
    FROM STUDENT
    WHERE NAME = 'DHARMIK'
);
```

### 6. Display the students whose SPI is less than SPI of student RIYA.

```sql
SELECT *
FROM STUDENT
WHERE SPI < ALL
(
    SELECT SPI
    FROM STUDENT
    WHERE NAME = 'RIYA'
);
```

### 7. Display the students who belong to the same branch as KRUNAL.

```sql
SELECT *
FROM STUDENT
WHERE BRANCH = ANY
(
    SELECT BRANCH
    FROM STUDENT
    WHERE NAME = 'KRUNAL'
);
```

### 8. Display the students whose branch is different from HETVI.

```sql
SELECT *
FROM STUDENT
WHERE BRANCH <> ALL
(
    SELECT BRANCH
    FROM STUDENT
    WHERE NAME = 'HETVI'
);
```

### 9. Display the highest SPI from RESULT table.

```sql
SELECT SPI
FROM RESULT
WHERE SPI >= ALL
(
    SELECT SPI
    FROM RESULT
);
```

### 10. Display the second lowest SPI from RESULT table.

```sql
SELECT MIN(SPI) AS Second_Lowest_SPI
FROM RESULT
WHERE SPI > ANY
(
    SELECT MIN(SPI)
    FROM RESULT
);
```

### 11. Display the names of students whose SPI is above branch-wise average SPI.

```sql
SELECT NAME
FROM STUDENT S
WHERE SPI >
(
    SELECT AVG(SPI)
    FROM STUDENT S2
    WHERE S2.BRANCH = S.BRANCH
);
```

### 12. Display the branch having maximum average SPI.

```sql
SELECT BRANCH
FROM STUDENT
GROUP BY BRANCH
HAVING AVG(SPI) >= ALL
(
    SELECT AVG(SPI)
    FROM STUDENT
    GROUP BY BRANCH
);
```

### 13. Display the branch having minimum average SPI.

```sql
SELECT BRANCH
FROM STUDENT
GROUP BY BRANCH
HAVING AVG(SPI) <= ALL
(
    SELECT AVG(SPI)
    FROM STUDENT
    GROUP BY BRANCH
);
```

---

# Part – B

### From the tables STUDENT_INFO and RESULT

### 14. Display the students whose SPI is greater than all students of ME branch.

```sql
SELECT SI.NAME, SI.BRANCH, R.SPI
FROM STUDENT_INFO SI
JOIN RESULT R ON SI.RNO = R.RNO
WHERE R.SPI > ALL
(
    SELECT R2.SPI
    FROM STUDENT_INFO SI2
    JOIN RESULT R2 ON SI2.RNO = R2.RNO
    WHERE SI2.BRANCH = 'ME'
);
```

### 15. Display the students whose SPI is less than any student of ME branch.

```sql
SELECT SI.NAME, SI.BRANCH, R.SPI
FROM STUDENT_INFO SI
JOIN RESULT R ON SI.RNO = R.RNO
WHERE R.SPI < ANY
(
    SELECT R2.SPI
    FROM STUDENT_INFO SI2
    JOIN RESULT R2 ON SI2.RNO = R2.RNO
    WHERE SI2.BRANCH = 'ME'
);
```

### 16. Display the student details whose SPI is not equal to any SPI of EC branch students.

```sql
SELECT SI.NAME, SI.BRANCH, R.SPI
FROM STUDENT_INFO SI
JOIN RESULT R ON SI.RNO = R.RNO
WHERE R.SPI <> ALL
(
    SELECT R2.SPI
    FROM STUDENT_INFO SI2
    JOIN RESULT R2 ON SI2.RNO = R2.RNO
    WHERE SI2.BRANCH = 'EC'
);
```

### 17. Display the names of students who scored higher SPI than student of RNO 103.

```sql
SELECT SI.NAME
FROM STUDENT_INFO SI
JOIN RESULT R ON SI.RNO = R.RNO
WHERE R.SPI >
(
    SELECT SPI
    FROM RESULT
    WHERE RNO = 103
);
```

### 18. Display the students whose SPI is greater than average SPI of their own branch.

```sql
SELECT SI.NAME, SI.BRANCH, R.SPI
FROM STUDENT_INFO SI
JOIN RESULT R ON SI.RNO = R.RNO
WHERE R.SPI >
(
    SELECT AVG(R2.SPI)
    FROM STUDENT_INFO SI2
    JOIN RESULT R2 ON SI2.RNO = R2.RNO
    WHERE SI2.BRANCH = SI.BRANCH
);
```

### 19. Display the students whose SPI is greater than the average SPI of CE branch but greater than the maximum SPI of ME branch.

```sql
SELECT SI.NAME, SI.BRANCH, R.SPI
FROM STUDENT_INFO SI
JOIN RESULT R ON SI.RNO = R.RNO
WHERE R.SPI >
(
    SELECT AVG(R2.SPI)
    FROM STUDENT_INFO SI2
    JOIN RESULT R2 ON SI2.RNO = R2.RNO
    WHERE SI2.BRANCH = 'CE'
)
AND R.SPI > ALL
(
    SELECT R3.SPI
    FROM STUDENT_INFO SI3
    JOIN RESULT R3 ON SI3.RNO = R3.RNO
    WHERE SI3.BRANCH = 'ME'
);
```

### 20. Display the branch names whose average SPI is greater than the overall average SPI.

```sql
SELECT BRANCH
FROM STUDENT_INFO SI
JOIN RESULT R ON SI.RNO = R.RNO
GROUP BY BRANCH
HAVING AVG(R.SPI) >
(
    SELECT AVG(SPI)
    FROM RESULT
);
```

### 21. Display the students who have maximum SPI in their respective branch.

```sql
SELECT SI.NAME, SI.BRANCH, R.SPI
FROM STUDENT_INFO SI
JOIN RESULT R ON SI.RNO = R.RNO
WHERE R.SPI >= ALL
(
    SELECT R2.SPI
    FROM STUDENT_INFO SI2
    JOIN RESULT R2 ON SI2.RNO = R2.RNO
    WHERE SI2.BRANCH = SI.BRANCH
);
```

### 22. Display the students whose SPI is greater than their average SPI of their branch and greater than overall average SPI.

```sql
SELECT SI.NAME, SI.BRANCH, R.SPI
FROM STUDENT_INFO SI
JOIN RESULT R ON SI.RNO = R.RNO
WHERE R.SPI >
(
    SELECT AVG(R2.SPI)
    FROM STUDENT_INFO SI2
    JOIN RESULT R2 ON SI2.RNO = R2.RNO
    WHERE SI2.BRANCH = SI.BRANCH
)
AND R.SPI >
(
    SELECT AVG(SPI)
    FROM RESULT
);
```

---

# Part – C

### 23. Display the students whose SPI is greater than at least one student of every branch.

```sql
SELECT SI.NAME, SI.BRANCH, R.SPI
FROM STUDENT_INFO SI
JOIN RESULT R ON SI.RNO = R.RNO
WHERE R.SPI > ALL
(
    SELECT MIN(R2.SPI)
    FROM STUDENT_INFO SI2
    JOIN RESULT R2 ON SI2.RNO = R2.RNO
    GROUP BY SI2.BRANCH
);
```

### 24. Display the students whose SPI is less than all students of CE branch.

```sql
SELECT SI.NAME, SI.BRANCH, R.SPI
FROM STUDENT_INFO SI
JOIN RESULT R ON SI.RNO = R.RNO
WHERE R.SPI < ALL
(
    SELECT R2.SPI
    FROM STUDENT_INFO SI2
    JOIN RESULT R2 ON SI2.RNO = R2.RNO
    WHERE SI2.BRANCH = 'CE'
);
```

### 25. Display the branch that contains the student with highest SPI.

```sql
SELECT DISTINCT SI.BRANCH
FROM STUDENT_INFO SI
JOIN RESULT R ON SI.RNO = R.RNO
WHERE R.SPI >= ALL
(
    SELECT SPI
    FROM RESULT
);
```

### 26. Display the students whose SPI is less than the SPI of every student in CE branch and greater than every student in ME branch.

```sql
SELECT SI.NAME, SI.BRANCH, R.SPI
FROM STUDENT_INFO SI
JOIN RESULT R ON SI.RNO = R.RNO
WHERE R.SPI < ALL
(
    SELECT R2.SPI
    FROM STUDENT_INFO SI2
    JOIN RESULT R2 ON SI2.RNO = R2.RNO
    WHERE SI2.BRANCH = 'CE'
)
AND R.SPI > ALL
(
    SELECT R3.SPI
    FROM STUDENT_INFO SI3
    JOIN RESULT R3 ON SI3.RNO = R3.RNO
    WHERE SI3.BRANCH = 'ME'
);
```
