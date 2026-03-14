# EliteTech-SQL-internship-task
  
---

# SQL Database Internship Tasks

This repository contains the implementation of four database tasks performed using **MySQL Workbench** and **Microsoft SQL Server**. The tasks demonstrate practical knowledge of SQL including joins, advanced data analysis, database migration, and backup & recovery.

---

# Database Used

**Database Name:** `company_db`

Tables created:

* **Employees**
* **Departments**
* **Salaries**

These tables were used across all tasks to demonstrate different SQL concepts.

---

# Task 1 – SQL Joins

## Objective

To combine data from multiple tables using different types of SQL joins.

## Steps Performed

* Created tables **Employees** and **Departments** in the `company_db` database.
* Inserted sample data into both tables.
* Executed different types of joins to retrieve meaningful combined data.

## Joins Implemented

**1. INNER JOIN**

* Retrieves only matching records from both tables.

```sql
SELECT e.emp_name, d.dept_name
FROM Employees e
INNER JOIN Departments d
ON e.dept_id = d.dept_id;
```

**2. LEFT JOIN**

* Retrieves all records from the left table (Employees) and matching records from Departments.

```sql
SELECT e.emp_name, d.dept_name
FROM Employees e
LEFT JOIN Departments d
ON e.dept_id = d.dept_id;
```

**3. RIGHT JOIN**

* Retrieves all records from the right table (Departments) and matching records from Employees.

```sql
SELECT e.emp_name, d.dept_name
FROM Employees e
RIGHT JOIN Departments d
ON e.dept_id = d.dept_id;
```

**4. FULL JOIN (Simulated in MySQL)**

Since MySQL does not directly support FULL JOIN, it was simulated using `UNION`.

```sql
SELECT e.emp_name, d.dept_name
FROM Employees e
LEFT JOIN Departments d ON e.dept_id = d.dept_id

UNION

SELECT e.emp_name, d.dept_name
FROM Employees e
RIGHT JOIN Departments d ON e.dept_id = d.dept_id;
```

## Outcome

Successfully combined data from multiple tables and understood how different joins return different result sets.

---

# Task 2 – Data Analysis with Complex Queries

## Objective

To perform advanced data analysis using SQL features such as:

* Window Functions
* Subqueries
* Common Table Expressions (CTEs)

## Steps Performed

* Created a **Salaries** table.
* Inserted salary data for employees.
* Performed analytical queries to identify trends and patterns in the dataset.

---

## Subquery Example

Finding employees whose salary is higher than the average salary.

```sql
SELECT emp_id, salary
FROM Salaries
WHERE salary > (
    SELECT AVG(salary) FROM Salaries
);
```

---

## Window Function Example

Ranking employees based on salary.

```sql
SELECT emp_id, salary,
RANK() OVER (ORDER BY salary DESC) AS salary_rank
FROM Salaries;
```

---

## CTE Example

Calculating the average salary per department.

```sql
WITH DeptSalary AS (
    SELECT d.dept_name, AVG(s.salary) AS avg_salary
    FROM Employees e
    JOIN Departments d ON e.dept_id = d.dept_id
    JOIN Salaries s ON e.emp_id = s.emp_id
    GROUP BY d.dept_name
)

SELECT * FROM DeptSalary;
```

## Outcome

Used advanced SQL features to analyze data and generate insights from relational datasets.

---

# Task 3 – Database Migration

## Objective

To migrate data from **MySQL** to **Microsoft SQL Server** while maintaining data integrity.

## Steps Performed

1. Created the `company_db` schema in **SQL Server**.
2. Recreated tables:

   * Employees
   * Departments
   * Salaries
3. Migrated the data from MySQL to SQL Server using SQL insert scripts.
4. Verified that data was transferred correctly.

---

## Data Integrity Verification

Row counts were compared between both databases.

```sql
SELECT COUNT(*) FROM Employees;
SELECT COUNT(*) FROM Departments;
SELECT COUNT(*) FROM Salaries;
```

If the row counts matched in both databases, the migration was considered successful.

## Outcome

The migration process successfully transferred data from MySQL to SQL Server without data loss.

---

# Task 4 – Database Backup and Recovery

## Objective

To demonstrate how to back up a database and restore it in case of failure.

## Backup Process

1. Opened **MySQL Workbench**.

2. Navigated to:

   ```
   Server → Data Export
   ```

3. Selected the `company_db` database.

4. Chose **Export to Self-Contained File**.

5. Generated a backup file:

```
company_db_backup.sql
```

---

## Recovery Process

1. Simulated a database failure by dropping the database.

```sql
DROP DATABASE company_db;
```

2. Restored the database using:

```
Server → Data Import
```

3. Selected the previously created backup file.

4. Imported the database to recreate tables and data.

---

## Recovery Verification

```sql
USE company_db;

SELECT COUNT(*) FROM Employees;
SELECT COUNT(*) FROM Departments;
SELECT COUNT(*) FROM Salaries;
```

Matching record counts confirmed that the database was successfully restored.

---

# Conclusion

This project demonstrated key database management concepts including:

* SQL joins and relational data retrieval
* Advanced analytical queries using window functions and CTEs
* Cross-platform database migration
* Database backup and recovery procedures

These tasks provided practical experience with real-world database operations using **MySQL Workbench** and **Microsoft SQL Server**.

---

