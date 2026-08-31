🚀 SQL — PHASE 15
Advanced GROUP BY & SQL Analysis 🔥

Bilkul bhai ❤️ Phase 15 start karte hain.
Aur fixed rule ke according Phase 15 ke saare related concepts isi ek phase me complete karenge.

📊 SQL ROADMAP — CURRENT STATUS
Phase 1–13  → ✅ Complete
Phase 14    → ✅ SQL Functions
Phase 15    → 🚀 STARTING
Overall SQL Progress: ~82% 🟢
📚 PHASE 15 — COMPLETE SYLLABUS

Is phase me:

1. GROUP BY — Advanced Revision
2. Multiple-column GROUP BY
3. GROUP BY + Aggregate Functions
4. WHERE + GROUP BY
5. GROUP BY + HAVING
6. WHERE vs HAVING
7. HAVING with multiple conditions
8. GROUP BY + CASE
9. GROUP BY + JOIN
10. GROUP BY + JOIN + HAVING
11. DISTINCT vs GROUP BY
12. Aggregate Functions without GROUP BY
13. GROUP BY with expressions/functions
14. Finding duplicates
15. Removing duplicates conceptually
16. Department-wise / category-wise analysis
17. Top groups
18. Aggregate + Subquery
19. Nested aggregation
20. Real-world analytical queries
21. Complete Practical
22. Practice Questions + Solutions
23. Interview Questions

Ab ek-ek concept basic → advanced karte hain.

1️⃣ GROUP BY — Basic Revision

GROUP BY ka simple meaning:

Same value wali rows ko groups me divide karna.

Example:

employee	department	salary
Rahul	CSE	30000
Aman	CSE	40000
Rohit	ECE	25000
Priya	ECE	50000
Neha	ME	35000

Agar hum:

SELECT department
FROM function_practice
GROUP BY department;

likhenge:

department
CSE
ECE
ME

Matlab:

CSE
 ├── Rahul
 └── Aman

ECE
 ├── Rohit
 └── Priya

ME
 └── Neha
2️⃣ GROUP BY + COUNT()

Sabse common use.

SELECT department, COUNT(*) AS total_employees
FROM function_practice
GROUP BY department;

Output:

department	total_employees
CSE	2
ECE	2
ME	1
Logic:
GROUP BY department
        ↓
CSE group
ECE group
ME group
        ↓
COUNT each group
3️⃣ GROUP BY + SUM()

Department-wise total salary:

SELECT
    department,
    SUM(salary) AS total_salary
FROM function_practice
GROUP BY department;

Output:

department	total_salary
CSE	70000
ECE	75000
ME	35000
4️⃣ GROUP BY + AVG()
SELECT
    department,
    AVG(salary) AS average_salary
FROM function_practice
GROUP BY department;

Result:

department	average_salary
CSE	35000
ECE	37500
ME	35000
5️⃣ Multiple-column GROUP BY 🔥

Ye important hai.

Suppose:

department	gender	salary
CSE	M	30000
CSE	M	40000
CSE	F	50000
ECE	M	25000

Agar:

SELECT department, gender, COUNT(*)
FROM employees
GROUP BY department, gender;

To grouping department + gender ke combination par hogi.

Concept:

CSE + M
CSE + F
ECE + M
🧠 Important Rule
GROUP BY department, gender

ka matlab:

Pehle sirf department ke groups nahi, department + gender ka unique combination group hoga.

6️⃣ WHERE + GROUP BY

WHERE pehle rows filter karta hai.

Example:

SELECT department, AVG(salary)
FROM function_practice
WHERE salary >= 30000
GROUP BY department;

Logic:

Table
 ↓
WHERE salary >= 30000
 ↓
Filtered rows
 ↓
GROUP BY department
 ↓
AVG()
7️⃣ WHERE vs HAVING 🔥🔥

Ye bahut important interview question hai.

WHERE

Individual rows filter karta hai.

SELECT *
FROM function_practice
WHERE salary > 30000;
HAVING

Groups ko filter karta hai.

SELECT department, AVG(salary)
FROM function_practice
GROUP BY department
HAVING AVG(salary) > 35000;
🧠 Simple Trick
WHERE
→ Row ko dekho

HAVING
→ Group ko dekho

Example:

salary > 30000

→ WHERE

AVG(salary) > 35000

→ HAVING

8️⃣ SQL Logical Order 🔥

Query:

SELECT department, AVG(salary)
FROM function_practice
WHERE salary > 25000
GROUP BY department
HAVING AVG(salary) > 30000
ORDER BY AVG(salary) DESC;

Conceptual processing order:

FROM
 ↓
WHERE
 ↓
GROUP BY
 ↓
HAVING
 ↓
SELECT
 ↓
ORDER BY

Ye order interviews me bahut poocha jata hai.

9️⃣ HAVING with Multiple Conditions

Example:

SELECT
    department,
    COUNT(*) AS total,
    AVG(salary) AS avg_salary
FROM function_practice
GROUP BY department
HAVING COUNT(*) >= 2
   AND AVG(salary) > 30000;

Matlab:

Department me >= 2 employees
AND
Average salary > 30000

dono conditions true honi chahiye.

🔟 GROUP BY + CASE 🔥

Salary categories:

SELECT
    CASE
        WHEN salary >= 40000 THEN 'High'
        WHEN salary >= 30000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category,
    COUNT(*) AS total
FROM function_practice
GROUP BY
    CASE
        WHEN salary >= 40000 THEN 'High'
        WHEN salary >= 30000 THEN 'Medium'
        ELSE 'Low'
    END;

Concept:

30000 → Medium
40000 → High
25000 → Low
50000 → High
35000 → Medium

Result:

salary_category	total
High	2
Medium	2
Low	1
1️⃣1️⃣ GROUP BY + JOIN 🔥🔥

Ye real-world SQL me bahut important hai.

Suppose:

departments
department_id	department_name
1	CSE
2	ECE
3	ME
employees
employee_id	name	department_id	salary
101	Rahul	1	30000
102	Aman	1	40000
103	Rohit	2	25000

Query:

SELECT
    d.department_name,
    COUNT(e.employee_id) AS total_employees
FROM departments d
JOIN employees e
ON d.department_id = e.department_id
GROUP BY d.department_name;

Logic:

JOIN
 ↓
Department + Employee data
 ↓
GROUP BY department
 ↓
COUNT employees
1️⃣2️⃣ GROUP BY + JOIN + HAVING

Example:

SELECT
    d.department_name,
    AVG(e.salary) AS avg_salary
FROM departments d
JOIN employees e
ON d.department_id = e.department_id
GROUP BY d.department_name
HAVING AVG(e.salary) > 30000;

Meaning:

Sirf woh departments dikhao jinki average salary 30,000 se zyada hai.

1️⃣3️⃣ DISTINCT vs GROUP BY
DISTINCT

Duplicate values remove:

SELECT DISTINCT department
FROM employees;
GROUP BY

Groups create:

SELECT department
FROM employees
GROUP BY department;

Agar sirf unique department names chahiye:

DISTINCT → simpler

Agar calculation karni hai:

GROUP BY → useful

Example:

SELECT department, COUNT(*)
FROM employees
GROUP BY department;
1️⃣4️⃣ Aggregate without GROUP BY

Important:

SELECT AVG(salary)
FROM employees;

Valid hai.

Yahan entire table ko one group ki tarah treat kiya ja sakta hai.

Result:

Average salary of all employees
1️⃣5️⃣ GROUP BY with Functions

Phase 14 ke functions yahan kaam aayenge.

Example:

SELECT
    UPPER(department) AS dept,
    COUNT(*)
FROM function_practice
GROUP BY UPPER(department);

Ya:

SELECT
    YEAR(hire_date),
    COUNT(*)
FROM employees
GROUP BY YEAR(hire_date);

Matlab function ka result grouping ke liye use kar sakte hain.

🔥 1️⃣6️⃣ Finding Duplicates

Very common interview problem.

Suppose emails:

a@gmail.com
b@gmail.com
a@gmail.com
c@gmail.com
b@gmail.com

Duplicates find:

SELECT
    email,
    COUNT(*) AS total
FROM employees
GROUP BY email
HAVING COUNT(*) > 1;

Output:

a@gmail.com → 2
b@gmail.com → 2

🔥 Is pattern ko yaad kar lo:

GROUP BY column
HAVING COUNT(*) > 1

= Find duplicates

1️⃣7️⃣ GROUP BY + ORDER BY

Department-wise salary total ko highest se lowest:

SELECT
    department,
    SUM(salary) AS total_salary
FROM function_practice
GROUP BY department
ORDER BY total_salary DESC;
1️⃣8️⃣ Top Group

Highest total salary wala department:

SELECT
    department,
    SUM(salary) AS total_salary
FROM function_practice
GROUP BY department
ORDER BY total_salary DESC
LIMIT 1;
1️⃣9️⃣ Aggregate + Subquery 🔥

Question:

Average salary se zyada salary wale employees find karo.

Pehle average:

SELECT AVG(salary)
FROM function_practice;

Then:

SELECT *
FROM function_practice
WHERE salary > (
    SELECT AVG(salary)
    FROM function_practice
);

Logic:

Subquery
   ↓
Average salary
   ↓
Outer query
   ↓
salary > average
2️⃣0️⃣ Department ka Average se Compare

Question:

Kaunse departments ki average salary overall average salary se zyada hai?

SELECT
    department,
    AVG(salary) AS avg_salary
FROM function_practice
GROUP BY department
HAVING AVG(salary) > (
    SELECT AVG(salary)
    FROM function_practice
);

🔥 Ye GROUP BY + HAVING + Subquery + Aggregate ka combination hai.

2️⃣1️⃣ Nested Aggregation Concept

Question:

Departments ki average salaries me highest average salary kya hai?

Concept:

Employee salaries
      ↓
Department-wise AVG
      ↓
Highest AVG

Query:

SELECT MAX(avg_salary)
FROM (
    SELECT department, AVG(salary) AS avg_salary
    FROM function_practice
    GROUP BY department
) AS dept_avg;

Inner query:

SELECT department, AVG(salary) AS avg_salary
FROM function_practice
GROUP BY department;

Outer query:

MAX(avg_salary)

🔥 Isko aggregate result par aggregation samajho.

🧪 COMPLETE PRACTICAL — PHASE 15

Ab ek fresh table bana lo.

CREATE TABLE sales_p15 (
    sale_id INT PRIMARY KEY,
    employee_name VARCHAR(50),
    department VARCHAR(50),
    city VARCHAR(50),
    amount DECIMAL(10,2)
);

Insert:

INSERT INTO sales_p15
VALUES
(1, 'Rahul', 'CSE', 'Delhi', 50000),
(2, 'Aman', 'CSE', 'Delhi', 30000),
(3, 'Rohit', 'ECE', 'Mumbai', 40000),
(4, 'Priya', 'ECE', 'Delhi', 60000),
(5, 'Neha', 'ME', 'Mumbai', 25000),
(6, 'Karan', 'CSE', 'Mumbai', 45000),
(7, 'Pooja', 'ME', 'Delhi', 35000),
(8, 'Vikas', 'ECE', 'Mumbai', 30000);

Check:

SELECT *
FROM sales_p15;
🧪 PRACTICE 1

Department-wise total sales.

Try yourself:

Expected idea:

CSE → ?
ECE → ?
ME  → ?
Solution
SELECT
    department,
    SUM(amount) AS total_sales
FROM sales_p15
GROUP BY department;
🧪 PRACTICE 2

City-wise total sales.

Solution
SELECT
    city,
    SUM(amount) AS total_sales
FROM sales_p15
GROUP BY city;
🧪 PRACTICE 3

Department-wise average sale.

Solution
SELECT
    department,
    AVG(amount) AS avg_sale
FROM sales_p15
GROUP BY department;
🧪 PRACTICE 4

Sirf woh departments jinke total sales 100000 se greater hain.

Solution
SELECT
    department,
    SUM(amount) AS total_sales
FROM sales_p15
GROUP BY department
HAVING SUM(amount) > 100000;
🧪 PRACTICE 5

Har city me kitni sales hui?

Solution
SELECT
    city,
    COUNT(*) AS total_sales
FROM sales_p15
GROUP BY city;
🧪 PRACTICE 6

Highest-selling department find karo.

Solution
SELECT
    department,
    SUM(amount) AS total_sales
FROM sales_p15
GROUP BY department
ORDER BY total_sales DESC
LIMIT 1;
🧪 PRACTICE 7

Average sale se zyada amount wali sales.

Solution
SELECT *
FROM sales_p15
WHERE amount > (
    SELECT AVG(amount)
    FROM sales_p15
);
🧪 PRACTICE 8 🔥

Department-wise sales count nikalo, lekin sirf woh departments jahan at least 3 sales hain.

Solution
SELECT
    department,
    COUNT(*) AS total_sales
FROM sales_p15
GROUP BY department
HAVING COUNT(*) >= 3;
🧪 PRACTICE 9 🔥

City + department wise total sales.

Solution
SELECT
    city,
    department,
    SUM(amount) AS total_sales
FROM sales_p15
GROUP BY city, department;
🧪 PRACTICE 10 🔥🔥

Har department ki average sale nikalo aur sirf woh departments dikhao jinki average sale overall average sale se greater hai.

Solution
SELECT
    department,
    AVG(amount) AS avg_sale
FROM sales_p15
GROUP BY department
HAVING AVG(amount) > (
    SELECT AVG(amount)
    FROM sales_p15
);
🧠 MOST IMPORTANT PATTERNS

Inko ratna nahi, pattern samajhna hai:

Pattern 1
SELECT column, COUNT(*)
FROM table
GROUP BY column;

→ Count per group

Pattern 2
SELECT column, SUM(amount)
FROM table
GROUP BY column;

→ Total per group

Pattern 3
SELECT column, AVG(amount)
FROM table
GROUP BY column;

→ Average per group

Pattern 4
GROUP BY column
HAVING COUNT(*) > 1

→ Duplicate values

Pattern 5
GROUP BY column
HAVING SUM(amount) > X

→ Groups whose total exceeds X

Pattern 6
GROUP BY column
ORDER BY aggregate DESC
LIMIT 1

→ Highest group

Pattern 7
HAVING aggregate > (
    SELECT aggregate
    FROM table
)

→ Group aggregate compared with overall aggregate

🎯 INTERVIEW QUESTIONS
Q1. GROUP BY kya karta hai?

Same values wali rows ko groups me divide karta hai, usually aggregate calculations ke saath.

Q2. WHERE aur HAVING me difference?
WHERE  → rows filter
HAVING → groups filter
Q3. Kya HAVING ke bina GROUP BY use kar sakte hain?

Yes.

Q4. Kya GROUP BY ke bina aggregate function use kar sakte hain?

Yes.

SELECT COUNT(*)
FROM employees;
Q5. Duplicate records find kaise karenge?
SELECT column, COUNT(*)
FROM table
GROUP BY column
HAVING COUNT(*) > 1;
Q6. Multiple columns GROUP BY?
GROUP BY department, city;

Combination ke basis par groups bante hain.

Q7. DISTINCT vs GROUP BY?

DISTINCT duplicate values remove karne ke liye simple option hai; GROUP BY grouping aur aggregation ke liye commonly use hota hai.

Q8. HAVING me aggregate function use kar sakte hain?

Yes.

HAVING COUNT(*) > 5
Q9. WHERE me aggregate function directly use kar sakte hain?

Normally no.

Wrong:

WHERE AVG(salary) > 30000

Correct:

HAVING AVG(salary) > 30000
Q10. SQL ka logical processing order?
FROM
WHERE
GROUP BY
HAVING
SELECT
ORDER BY
LIMIT
Q11. Top department kaise find karenge?
GROUP BY
ORDER BY aggregate DESC
LIMIT 1
Q12. GROUP BY department, city kya karta hai?

Department + city ke combination par groups create karta hai.

🔥 PHASE 15 — FINAL REVISION
GROUP BY
   ↓
Rows → Groups
   ↓
Aggregate Functions
   ↓
COUNT / SUM / AVG / MIN / MAX
   ↓
WHERE
→ Before grouping
   ↓
HAVING
→ After grouping
   ↓
CASE
→ Conditional grouping
   ↓
JOIN
→ Multiple tables
   ↓
SUBQUERY
→ Compare with calculated result
   ↓
ORDER BY + LIMIT
→ Top groups
📊 PHASE 15 STATUS
Advanced GROUP BY             ✅
Multiple-column GROUP BY      ✅
GROUP BY + Aggregates         ✅
WHERE + GROUP BY              ✅
HAVING                        ✅
WHERE vs HAVING               ✅
Multiple HAVING conditions    ✅
GROUP BY + CASE               ✅
GROUP BY + JOIN               ✅
JOIN + HAVING                 ✅
DISTINCT vs GROUP BY          ✅
Aggregate without GROUP BY    ✅
Functions + GROUP BY          ✅
Duplicate detection           ✅
ORDER BY + GROUP BY           ✅
Top groups                    ✅
Aggregate + Subquery          ✅
Nested Aggregation            ✅
Real-world analysis           ✅
Practical                     ✅
Practice + Solutions          ✅
Interview Questions            ✅
🟢 PHASE 15 = COMPLETE
📈 Overall SQL Progress: ~86% COMPLETE
Completed:
Phase 1 → 15 ✅

Remaining:
Phase 16 → Views
Phase 17 → CTE
Phase 18 → Window Functions
Phase 19 → Transactions
Phase 20 → Indexing
Phase 21 → Normalization
Phase 22 → Performance & Optimization
Phase 23 → Advanced SQL + Interview

Phase 15 officially DONE. 🔥