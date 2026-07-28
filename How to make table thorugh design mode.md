# 📘 Creating a Table Using Design Mode (SQL Server Management Studio - SSMS)

## 📖 Introduction

**Design Mode** in SQL Server Management Studio (SSMS) allows users to create database tables using a graphical interface instead of writing SQL commands.

It is beginner-friendly and commonly used in DBMS practical labs.

---

# Step 1: Open SQL Server Management Studio (SSMS)

1. Open **SQL Server Management Studio (SSMS)**.
2. Connect to your SQL Server instance.
3. Expand **Databases**.
4. Select or create the database in which you want to create the table.

Example:

```
Databases
    └── CollegeDB
```

---

# Step 2: Create a New Table

1. Expand your database.
2. Right-click **Tables**.
3. Select **New → Table**.

A **Table Designer** window will open.

---

# Step 3: Enter Column Details

Fill in the columns one by one.

|Column Name|Data Type|Allow Nulls|
|------------|---------|-----------|
|StudentID|int|❌|
|Name|varchar(50)|❌|
|Age|int|✅|
|City|varchar(50)|✅|

---

# Step 4: Set Primary Key

1. Select the **StudentID** row.
2. Right-click it.
3. Click **Set Primary Key**.

A key icon (🔑) appears beside the column.

---

# Step 5: Save the Table

1. Press **Ctrl + S** or click **Save**.
2. Enter the table name.

Example

```
Student
```

Click **OK**.

Your table is now created.

---

# Step 6: Verify the Table

Expand

```
Database
   └── Tables
```

You should see

```
Student
```

---

# Step 7: Insert Data

### Method 1 (GUI)

1. Expand **Tables**.
2. Right-click **Student**.
3. Select

```
Edit Top 200 Rows
```

A grid will appear.

Enter the values.

|StudentID|Name|Age|City|
|----------|----|---|----|
|101|Rahul|20|Ahmedabad|
|102|Priya|19|Rajkot|
|103|Amit|21|Surat|

The data is automatically saved when you move to another row.

---

### Method 2 (SQL Query)

Right-click the database.

Choose

```
New Query
```

Write

```sql
INSERT INTO Student(StudentID, Name, Age, City)
VALUES
(101,'Rahul',20,'Ahmedabad'),
(102,'Priya',19,'Rajkot'),
(103,'Amit',21,'Surat');
```

Execute using

```
F5
```

or click **Execute**.

---

# Step 8: View Data

Method 1

Right-click the table

```
Select Top 1000 Rows
```

or

Method 2

```sql
SELECT * FROM Student;
```

Output

|StudentID|Name|Age|City|
|----------|----|---|----|
|101|Rahul|20|Ahmedabad|
|102|Priya|19|Rajkot|
|103|Amit|21|Surat|

---

# Summary of Steps

|Step|Action|
|----|------|
|1|Open SSMS|
|2|Connect to SQL Server|
|3|Select Database|
|4|Right-click Tables → New → Table|
|5|Enter Columns|
|6|Set Primary Key|
|7|Save Table|
|8|Insert Data (Edit Top 200 Rows or INSERT Query)|
|9|View Data using SELECT or Select Top 1000 Rows|

---

# Important Notes

- Design Mode is useful for beginners.
- Always define a **Primary Key** whenever possible.
- Choose appropriate data types (e.g., `INT`, `VARCHAR`, `DATE`).
- Save the table after designing it.
- Use **Edit Top 200 Rows** for manual data entry.
- Use **SELECT** to verify the inserted records.

---

# Practice Exercise

Create a table named **Employee** with the following fields:

|Column Name|Data Type|
|------------|---------|
|EmpID|INT|
|EmpName|VARCHAR(50)|
|Department|VARCHAR(30)|
|Salary|DECIMAL(10,2)|

Tasks:
1. Create the table using **Design Mode**.
2. Set **EmpID** as the Primary Key.
3. Save the table.
4. Insert at least **5 records**.
5. Display all records using:

```sql
SELECT * FROM Employee;
```
