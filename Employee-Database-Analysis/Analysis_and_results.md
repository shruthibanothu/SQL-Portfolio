# SQL Case Study 2 — Analysis & Results

## 1. Project Overview

This document presents selected SQL queries and their results from the Employee Database Analysis project. The analysis uses Microsoft SQL Server to explore employee information, department structures, job details, and salary patterns.

The objective is to demonstrate practical SQL skills through business-oriented questions, query execution, and interpretation of results.

**Tools:** Microsoft SQL Server and SQL Server Management Studio (SSMS)

**Database tables:** `EMPLOYEE`, `DEPARTMENT`, `JOB`, `LOCATION`

---

## 2. Question 1 — Employee Details by Department and City

### Business Question

How can employee information be combined with department names and city details to create a consolidated employee report?

### SQL Concepts

- INNER JOIN
- Table aliases
- Multi-table relationships
- Column aliases

### SQL Query

```sql
SELECT
    E.Employee_Id,
    E.First_Name,
    E.Last_Name,
    D.Name AS Department_Name,
    L.City,
    E.Salary
FROM EMPLOYEE E
INNER JOIN DEPARTMENT D
    ON E.Department_Id = D.Department_Id
INNER JOIN LOCATION L
    ON D.Location_Id = L.Location_ID;
```

### Result
Employee_Id	First_Name	Last_Name	Department_Name	City	Salary
7369	       John	      Smith	    Sales	          Chicago	800
7499	       Kevin	    Allen	    Research	      Dallas	1600
755	         Jean	      Doyle	    Research	      Dallas	2850
756	         Lynn	      Dennis	  Research	      Dallas	2750
757	         Leslie	    Baker	    Operations	    Boston	2200
7521	       Cynthia	  Wark	    Research	      Dallas	1250

### Insight

The query combines information from three related tables into one report. In this sample dataset, four employees belong to Research, while Sales and Operations each have one employee.

---

## 3. Question 2 — Departments with at Least Three Employees

### Business Question

Which departments have three or more employees?

### SQL Concepts

- INNER JOIN
- GROUP BY
- COUNT()
- HAVING
- ORDER BY

### SQL Query

```sql
SELECT
    D.Name AS Department_Name,
    COUNT(*) AS Total_Employees
FROM EMPLOYEE E
INNER JOIN DEPARTMENT D
    ON E.Department_Id = D.Department_Id
GROUP BY D.Name
HAVING COUNT(*) >= 3
ORDER BY Total_Employees DESC;
```

### Result

Department_Name|	Total_Employees
Research	     | 4

### Insight

Research is the only department meeting the minimum headcount requirement in this sample. The `HAVING` clause filters grouped results, whereas `WHERE` filters individual records before grouping.

---

## 4. Question 3 — Employee Salary Grade Classification

### Business Question

How can employees be classified into salary grades, and how many employees fall into each grade?

### Salary Grade Rules

| Salary Range | Grade |
|---|---|
| 2500 and above | A |
| 2000–2499 | B |
| 1000–1999 | C |
| Below 1000 | D |

### SQL Concepts

- CASE expression
- Derived table
- COUNT()
- GROUP BY

### SQL Query

```sql
SELECT
    Salary_Grade,
    COUNT(*) AS Number_of_Employees
FROM (
    SELECT
        CASE
            WHEN Salary >= 2500 THEN 'A'
            WHEN Salary BETWEEN 2000 AND 2499 THEN 'B'
            WHEN Salary BETWEEN 1000 AND 1999 THEN 'C'
            ELSE 'D'
        END AS Salary_Grade
    FROM EMPLOYEE
) AS GradedEmployees
GROUP BY Salary_Grade
ORDER BY Salary_Grade;
```

### Result

Salary_Grade	Number_of_Employees
A	            2
B	            1
C	            2
D	            1

### Insight

Two employees fall into Grade A, two into Grade C, and one each into Grades B and D. The `CASE` expression creates a category for each employee, and the outer query summarizes the categories.

---

## 5. Question 4 — Find the Second-Highest Salary

### Business Question

Which employee earns the second-highest distinct salary in the organization?

### SQL Concepts

- Nested subqueries
- MAX()
- Comparison operators

### SQL Query

```sql
SELECT
    Employee_Id,
    First_Name,
    Last_Name,
    Salary
FROM EMPLOYEE
WHERE Salary = (
    SELECT MAX(Salary)
    FROM EMPLOYEE
    WHERE Salary < (
        SELECT MAX(Salary)
        FROM EMPLOYEE
    )
);
```

### Result
Employee_Id	First_Name	Last_Name	Salary
756	        Lynn       Dennis	    2750

### Insight

The innermost query finds the highest salary. The next query finds the maximum salary below that value, and the outer query returns the employee earning it. This approach identifies the second-highest distinct salary.

---

## 6. Question 5 — Employees Earning Above Their Department Average

### Business Question

Which employees earn more than the average salary of their own department?

### SQL Concepts

- Correlated subquery
- AVG()
- Table aliases
- Department-level comparison

### SQL Query

```sql
SELECT
    E.Employee_Id,
    E.First_Name,
    E.Last_Name,
    E.Department_Id,
    E.Salary
FROM EMPLOYEE E
WHERE E.Salary > (
    SELECT AVG(E2.Salary)
    FROM EMPLOYEE E2
    WHERE E2.Department_Id = E.Department_Id
);
```

### Result

Employee_Id	First_Name	Last_Name	Department_Id	Salary
755	         Jean       Doyle	     30	          2850
756	         Lynn	      Dennis	   30	          2750

### Insight

Jean Doyle and Lynn Dennis earn more than the average salary within Department 30. The subquery references the outer employee's department, making this a correlated subquery rather than a comparison against one overall company average.

---

## 7. Key Findings

- The sample contains six employee records

