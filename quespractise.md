🏆 SQL — FINAL 100 PRACTICE QUESTIONS
🟢 PART 1 — BASIC SQL (1–20)

Assume:

employees(
    employee_id,
    employee_name,
    department,
    salary,
    city,
    email
)
Q1. Saare employees display karo.
SELECT * FROM employees;
Q2. Sirf employee name aur salary display karo.
SELECT employee_name, salary
FROM employees;
Q3. Unique departments nikalo.
SELECT DISTINCT department
FROM employees;
Q4. Salary > 50000 wale employees.
SELECT *
FROM employees
WHERE salary > 50000;
Q5. Salary >= 50000 wale employees.
SELECT *
FROM employees
WHERE salary >= 50000;
Q6. Salary 30000–60000 ke beech.
SELECT *
FROM employees
WHERE salary BETWEEN 30000 AND 60000;
Q7. CSE department ke employees.
SELECT *
FROM employees
WHERE department = 'CSE';
Q8. Delhi ya Mumbai ke employees.
SELECT *
FROM employees
WHERE city IN ('Delhi', 'Mumbai');
Q9. Delhi ke alawa employees.
SELECT *
FROM employees
WHERE city <> 'Delhi';
Q10. Name 'A' se start hota ho.
SELECT *
FROM employees
WHERE employee_name LIKE 'A%';
Q11. Name 'a' par end hota ho.
SELECT *
FROM employees
WHERE employee_name LIKE '%a';
Q12. Name me 'rah' present ho.
SELECT *
FROM employees
WHERE employee_name LIKE '%rah%';
Q13. Salary descending order me.
SELECT *
FROM employees
ORDER BY salary DESC;
Q14. Salary ascending order me.
SELECT *
FROM employees
ORDER BY salary ASC;
Q15. Top 5 highest salaries.
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 5;
Q16. Lowest salary wala employee.
SELECT *
FROM employees
ORDER BY salary ASC
LIMIT 1;
Q17. Total employees count.
SELECT COUNT(*)
FROM employees;
Q18. Total salary.
SELECT SUM(salary)
FROM employees;
Q19. Average salary.
SELECT AVG(salary)
FROM employees;
Q20. Highest aur lowest salary ek saath.
SELECT
    MAX(salary) AS highest_salary,
    MIN(salary) AS lowest_salary
FROM employees;
🟢 PART 2 — AGGREGATE + GROUP BY (21–35)
Q21. Department-wise employee count.
SELECT department, COUNT(*) AS total
FROM employees
GROUP BY department;
Q22. Department-wise total salary.
SELECT department, SUM(salary) AS total_salary
FROM employees
GROUP BY department;
Q23. Department-wise average salary.
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
Q24. Department-wise maximum salary.
SELECT department, MAX(salary)
FROM employees
GROUP BY department;
Q25. Department-wise minimum salary.
SELECT department, MIN(salary)
FROM employees
GROUP BY department;
Q26. Sirf departments jahan 5 se zyada employees hain.
SELECT department, COUNT(*) AS total
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
Q27. Average salary > 50000 wale departments.
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
Q28. Total salary > 2 lakh wale departments.
SELECT department, SUM(salary) AS total_salary
FROM employees
GROUP BY department
HAVING SUM(salary) > 200000;
Q29. City-wise employee count.
SELECT city, COUNT(*) AS total
FROM employees
GROUP BY city;
Q30. City-wise average salary.
SELECT city, AVG(salary) AS avg_salary
FROM employees
GROUP BY city;
Q31. Department + city wise employee count.
SELECT department, city, COUNT(*) AS total
FROM employees
GROUP BY department, city;
Q32. Highest average salary wala department.
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
ORDER BY avg_salary DESC
LIMIT 1;
Q33. Highest total salary wala department.
SELECT department, SUM(salary) AS total_salary
FROM employees
GROUP BY department
ORDER BY total_salary DESC
LIMIT 1;
Q34. Sirf departments jahan minimum salary > 30000.
SELECT department, MIN(salary) AS min_salary
FROM employees
GROUP BY department
HAVING MIN(salary) > 30000;
Q35. Departments ko employee count ke descending order me.
SELECT department, COUNT(*) AS total
FROM employees
GROUP BY department
ORDER BY total DESC;
🟡 PART 3 — STRING / NULL / CASE FUNCTIONS (36–50)
Q36. Employee names uppercase.
SELECT UPPER(employee_name)
FROM employees;
Q37. Employee names lowercase.
SELECT LOWER(employee_name)
FROM employees;
Q38. Name ki length.
SELECT employee_name, LENGTH(employee_name)
FROM employees;
Q39. Name + city combine karo.
SELECT CONCAT(employee_name, ' - ', city)
FROM employees;
Q40. Name ka first 3 characters.
SELECT SUBSTRING(employee_name, 1, 3)
FROM employees;
Q41. Name ke beginning/end spaces remove.
SELECT TRIM(employee_name)
FROM employees;
Q42. Email me gmail.com ko company.com se replace karo.
SELECT REPLACE(email, 'gmail.com', 'company.com')
FROM employees;
Q43. NULL email ko 'Not Provided' dikhao.
SELECT
    employee_name,
    IFNULL(email, 'Not Provided') AS email
FROM employees;
Q44. First non-NULL value nikalo.
SELECT COALESCE(NULL, NULL, 'SQL', 'Java');
Q45. Salary category banao.
SELECT
    employee_name,
    salary,
    CASE
        WHEN salary >= 70000 THEN 'High'
        WHEN salary >= 40000 THEN 'Medium'
        ELSE 'Low'
    END AS category
FROM employees;
Q46. Salary ko nearest 1000 round karo.
SELECT employee_name, ROUND(salary, -3)
FROM employees;
Q47. Salary ka absolute value.
SELECT ABS(salary)
FROM employees;
Q48. Salary ko ceil karo.
SELECT CEIL(salary)
FROM employees;
Q49. Salary ko floor karo.
SELECT FLOOR(salary)
FROM employees;
Q50. Salary categories ka count.
SELECT
    CASE
        WHEN salary >= 70000 THEN 'High'
        WHEN salary >= 40000 THEN 'Medium'
        ELSE 'Low'
    END AS category,
    COUNT(*) AS total
FROM employees
GROUP BY
    CASE
        WHEN salary >= 70000 THEN 'High'
        WHEN salary >= 40000 THEN 'Medium'
        ELSE 'Low'
    END;
🟡 PART 4 — SUBQUERIES (51–65)
Q51. Average salary se zyada salary wale employees.
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
Q52. Average salary se kam salary wale employees.
SELECT *
FROM employees
WHERE salary < (
    SELECT AVG(salary)
    FROM employees
);
Q53. Highest salary wala employee.
SELECT *
FROM employees
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
);
Q54. Lowest salary wala employee.
SELECT *
FROM employees
WHERE salary = (
    SELECT MIN(salary)
    FROM employees
);
Q55. Second highest salary.
SELECT MAX(salary)
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
Q56. Third highest salary.
SELECT DISTINCT salary
FROM employees
ORDER BY salary DESC
LIMIT 1 OFFSET 2;
Q57. Average salary se zyada employees ka count.
SELECT COUNT(*)
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
Q58. Highest salary wale department ke employees.
SELECT *
FROM employees
WHERE department = (
    SELECT department
    FROM employees
    ORDER BY salary DESC
    LIMIT 1
);
Q59. CSE ke average salary se zyada salary wale employees.
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
    WHERE department = 'CSE'
);
Q60. CSE department ki maximum salary.
SELECT MAX(salary)
FROM employees
WHERE department = 'CSE';
Q61. CSE ke maximum salary ke equal employees.
SELECT *
FROM employees
WHERE department = 'CSE'
AND salary = (
    SELECT MAX(salary)
    FROM employees
    WHERE department = 'CSE'
);
Q62. Overall average se zyada average salary wale departments.
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > (
    SELECT AVG(salary)
    FROM employees
);
Q63. Employees belonging to departments having >5 employees.
SELECT *
FROM employees
WHERE department IN (
    SELECT department
    FROM employees
    GROUP BY department
    HAVING COUNT(*) > 5
);
Q64. Highest average salary department.
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
ORDER BY avg_salary DESC
LIMIT 1;
Q65. Department-wise average salary me overall highest average.
SELECT MAX(avg_salary)
FROM (
    SELECT department, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
) AS x;
🔴 PART 5 — JOINS (66–80)

Assume:

employees
employee_id
employee_name
department_id
salary

departments
department_id
department_name
Q66. Employee + department name.
SELECT
    e.employee_name,
    d.department_name
FROM employees e
JOIN departments d
ON e.department_id = d.department_id;
Q67. Employee name + salary + department.
SELECT
    e.employee_name,
    e.salary,
    d.department_name
FROM employees e
JOIN departments d
ON e.department_id = d.department_id;
Q68. CSE department employees.
SELECT e.*
FROM employees e
JOIN departments d
ON e.department_id = d.department_id
WHERE d.department_name = 'CSE';
Q69. Department-wise employee count using JOIN.
SELECT
    d.department_name,
    COUNT(e.employee_id) AS total
FROM departments d
JOIN employees e
ON d.department_id = e.department_id
GROUP BY d.department_name;
Q70. Department-wise average salary.
SELECT
    d.department_name,
    AVG(e.salary) AS avg_salary
FROM departments d
JOIN employees e
ON d.department_id = e.department_id
GROUP BY d.department_name;
Q71. Departments having average salary >50000.
SELECT
    d.department_name,
    AVG(e.salary) AS avg_salary
FROM departments d
JOIN employees e
ON d.department_id = e.department_id
GROUP BY d.department_name
HAVING AVG(e.salary) > 50000;
Q72. Highest paid employee with department name.
SELECT
    e.employee_name,
    e.salary,
    d.department_name
FROM employees e
JOIN departments d
ON e.department_id = d.department_id
ORDER BY e.salary DESC
LIMIT 1;
Q73. LEFT JOIN — all departments including empty ones.
SELECT
    d.department_name,
    COUNT(e.employee_id) AS total
FROM departments d
LEFT JOIN employees e
ON d.department_id = e.department_id
GROUP BY d.department_name;
Q74. Departments having no employees.
SELECT d.department_name
FROM departments d
LEFT JOIN employees e
ON d.department_id = e.department_id
WHERE e.employee_id IS NULL;
Q75. Employees without matching department.
SELECT e.*
FROM employees e
LEFT JOIN departments d
ON e.department_id = d.department_id
WHERE d.department_id IS NULL;
Q76. Department-wise total salary.
SELECT
    d.department_name,
    SUM(e.salary) AS total_salary
FROM departments d
JOIN employees e
ON d.department_id = e.department_id
GROUP BY d.department_name;
Q77. Department with highest total salary.
SELECT
    d.department_name,
    SUM(e.salary) AS total_salary
FROM departments d
JOIN employees e
ON d.department_id = e.department_id
GROUP BY d.department_name
ORDER BY total_salary DESC
LIMIT 1;
Q78. Employees earning more than their department average.
SELECT e.*
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);

🔥 Important correlated subquery.

Q79. Each department ka highest-paid employee.
SELECT e.*
FROM employees e
WHERE e.salary = (
    SELECT MAX(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
Q80. Department-wise employee count + average salary.
SELECT
    d.department_name,
    COUNT(e.employee_id) AS total_employees,
    AVG(e.salary) AS avg_salary
FROM departments d
LEFT JOIN employees e
ON d.department_id = e.department_id
GROUP BY d.department_name;
🔴 PART 6 — WINDOW FUNCTIONS (81–90)
Q81. Salary ranking.
SELECT
    employee_name,
    salary,
    RANK() OVER(ORDER BY salary DESC) AS salary_rank
FROM employees;
Q82. Row number by salary.
SELECT
    employee_name,
    salary,
    ROW_NUMBER() OVER(ORDER BY salary DESC) AS rn
FROM employees;
Q83. Dense rank.
SELECT
    employee_name,
    salary,
    DENSE_RANK() OVER(ORDER BY salary DESC) AS salary_rank
FROM employees;
Q84. Department-wise ranking.
SELECT
    employee_name,
    department,
    salary,
    RANK() OVER(
        PARTITION BY department
        ORDER BY salary DESC
    ) AS dept_rank
FROM employees;
Q85. Previous employee salary.
SELECT
    employee_name,
    salary,
    LAG(salary) OVER(
        ORDER BY employee_id
    ) AS previous_salary
FROM employees;
Q86. Next employee salary.
SELECT
    employee_name,
    salary,
    LEAD(salary) OVER(
        ORDER BY employee_id
    ) AS next_salary
FROM employees;
Q87. Running salary total.
SELECT
    employee_name,
    salary,
    SUM(salary) OVER(
        ORDER BY employee_id
    ) AS running_total
FROM employees;
Q88. Department-wise running salary.
SELECT
    employee_name,
    department,
    salary,
    SUM(salary) OVER(
        PARTITION BY department
        ORDER BY employee_id
    ) AS running_total
FROM employees;
Q89. Top 2 employees from every department.
SELECT *
FROM (
    SELECT
        employee_name,
        department,
        salary,
        ROW_NUMBER() OVER(
            PARTITION BY department
            ORDER BY salary DESC
        ) AS rn
    FROM employees
) x
WHERE rn <= 2;
Q90. Second highest salary in every department.
SELECT *
FROM (
    SELECT
        employee_name,
        department,
        salary,
        DENSE_RANK() OVER(
            PARTITION BY department
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) x
WHERE rnk = 2;
🔴 PART 7 — INTERVIEW / ADVANCED (91–100)
Q91. Duplicate emails find karo.
SELECT email, COUNT(*) AS total
FROM employees
GROUP BY email
HAVING COUNT(*) > 1;
Q92. Duplicate employee names.
SELECT employee_name, COUNT(*) AS total
FROM employees
GROUP BY employee_name
HAVING COUNT(*) > 1;
Q93. Employees whose salary is greater than all CSE employees.
SELECT *
FROM employees
WHERE salary > ALL (
    SELECT salary
    FROM employees
    WHERE department = 'CSE'
);
Q94. Employees whose salary matches any CSE salary.
SELECT *
FROM employees
WHERE salary IN (
    SELECT salary
    FROM employees
    WHERE department = 'CSE'
);
Q95. Employees earning more than their department average.
SELECT e.*
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department = e.department
);
Q96. Department having the highest average salary.
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
ORDER BY avg_salary DESC
LIMIT 1;
Q97. Third highest distinct salary.
SELECT DISTINCT salary
FROM employees
ORDER BY salary DESC
LIMIT 1 OFFSET 2;
Q98. Employees having the third highest salary.
SELECT *
FROM employees
WHERE salary = (
    SELECT DISTINCT salary
    FROM employees
    ORDER BY salary DESC
    LIMIT 1 OFFSET 2
);
Q99. Find employees whose salary is higher than previous employee.
SELECT *
FROM (
    SELECT
        employee_id,
        employee_name,
        salary,
        LAG(salary) OVER(
            ORDER BY employee_id
        ) AS previous_salary
    FROM employees
) x
WHERE salary > previous_salary;
Q100. 🔥 Each department ka highest-paid employee with department name.
SELECT *
FROM (
    SELECT
        e.employee_name,
        d.department_name,
        e.salary,
        RANK() OVER(
            PARTITION BY d.department_id
            ORDER BY e.salary DESC
        ) AS rnk
    FROM employees e
    JOIN departments d
    ON e.department_id = d.department_id
) x
WHERE rnk = 1;
🧠 100 QUESTIONS ME KYA-KYA COVER HO GAYA?
SELECT / WHERE              ✅
DISTINCT                    ✅
LIKE / IN / BETWEEN         ✅
ORDER BY / LIMIT            ✅

COUNT / SUM / AVG           ✅
MIN / MAX                   ✅
GROUP BY                    ✅
HAVING                      ✅

String Functions            ✅
Numeric Functions           ✅
NULL Functions              ✅
CASE                        ✅

Subqueries                  ✅
Correlated Subqueries       ✅
JOIN                        ✅
LEFT JOIN                   ✅

Duplicate Detection         ✅
Top N                       ✅
Nth Highest Salary          ✅

ROW_NUMBER                  ✅
RANK                        ✅
DENSE_RANK                  ✅
PARTITION BY                ✅
LAG                         ✅
LEAD                        ✅
Running Total               ✅

Views                       ✅
CTE                         ✅
Transactions                ✅
Indexing                    ✅
Normalization               ✅
Optimization                ✅
🏆 SQL FINAL STATUS

Theory: ✅
Basic SQL: ✅
Intermediate: ✅
Advanced: ✅
JOINs: ✅
Subqueries: ✅
Window Functions: ✅
Interview Patterns: ✅
100 Practice Questions: ✅

🎯 Ab tumhara SQL ka main syllabus complete maan sakte ho.

Sabse important ab ye hai ki 100 questions ko khud se solve karo. Sirf solutions padhne se SQL strong nahi hota—query ko khud type karke error aayega tabhi actual command samajh me permanently baithti hai.