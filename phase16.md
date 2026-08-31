Haan bhai, samajh gaya 😄. Ab Phase 16–22 ko unnecessarily 7 alag long lectures nahi kheechna hai.

Ab hum Phase 16 → 22 ek hi compact block me karenge. Har topic ka core concept + syntax + 1–2 examples + important interview point bas. Jahan practical zaroori hoga, wahan short practical bhi.

🚀 SQL — PHASE 16 → 22
Advanced SQL — Compact Complete Revision
🔵 PHASE 16 — VIEWS

View = saved SQL query jo table ki tarah behave karti hai.

CREATE VIEW high_salary AS
SELECT employee_name, salary
FROM employees
WHERE salary > 40000;

Use:

SELECT * FROM high_salary;

Delete:

DROP VIEW high_salary;
Yaad rakho:
View usually actual data ka separate copy nahi hoti.
Complex query ko reusable banane ke liye useful.
Security ke liye bhi useful ho sakti hai.
🔵 PHASE 17 — CTE

CTE = Common Table Expression

Complex query ko temporary named result dene ke liye.

WITH high_salary AS (
    SELECT *
    FROM employees
    WHERE salary > 40000
)
SELECT *
FROM high_salary;

Multiple CTE:

WITH cte1 AS (...),
     cte2 AS (...)
SELECT ...
Recursive CTE

Hierarchical data jaise:

CEO
 ↓
Manager
 ↓
Employee

ke liye useful.

View vs CTE
VIEW → database me saved
CTE  → query execution ke time temporary
🔵 PHASE 18 — WINDOW FUNCTIONS 🔥

Ye bahut important hai.

Window function rows ko collapse nahi karta, unlike GROUP BY.

ROW_NUMBER()
SELECT
    employee_name,
    salary,
    ROW_NUMBER() OVER(ORDER BY salary DESC) AS rn
FROM employees;
RANK()
RANK() OVER(ORDER BY salary DESC)

Same salary → same rank, next rank skip.

DENSE_RANK()

Same salary → same rank, rank skip nahi hota.

Salary    RANK    DENSE_RANK
50000      1          1
50000      1          1
40000      3          2
PARTITION BY

Department-wise ranking:

SELECT
    employee_name,
    department,
    salary,
    RANK() OVER(
        PARTITION BY department
        ORDER BY salary DESC
    ) AS rank_no
FROM employees;
LAG() / LEAD()

Previous/next row ka value:

LAG(salary) OVER(ORDER BY employee_id)
LEAD(salary) OVER(ORDER BY employee_id)
Running Total
SUM(amount) OVER(
    ORDER BY sale_id
)
🔥 GROUP BY vs Window
GROUP BY
→ rows collapse

WINDOW FUNCTION
→ rows remain
→ extra calculated column milta hai
🔵 PHASE 19 — TRANSACTIONS

Transaction = database operations ka logical unit.

START TRANSACTION;

UPDATE accounts
SET balance = balance - 1000
WHERE id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE id = 2;

COMMIT;

Problem ho:

ROLLBACK;
SAVEPOINT
SAVEPOINT s1;

ROLLBACK TO s1;
ACID 🔥
A → Atomicity
C → Consistency
I → Isolation
D → Durability

Interview me ACID definitely important.

🔵 PHASE 20 — INDEXING

Index database ko data faster search karne me help karta hai.

CREATE INDEX idx_employee_name
ON employees(employee_name);

Delete:

DROP INDEX idx_employee_name ON employees;

Composite index:

CREATE INDEX idx_dept_salary
ON employees(department, salary);
Advantage
SELECT/search faster
Disadvantage
Extra storage
INSERT/UPDATE/DELETE can become more expensive
Important:

Har column par index banana good practice nahi hai.

🔵 PHASE 21 — NORMALIZATION

Goal:

Duplicate/redundant data ko reduce karna aur data consistency improve karna.

1NF
Atomic values
Repeating groups nahi.
2NF
1NF +
Partial dependency remove.
3NF
2NF +
Transitive dependency remove.
BCNF

3NF se stricter form.

Example

Bad:

student	course1	course2
Rahul	SQL	Java

Better:

student	course
Rahul	SQL
Rahul	Java
Anomalies
Insertion anomaly
Update anomaly
Deletion anomaly
🔵 PHASE 22 — SQL PERFORMANCE & OPTIMIZATION

Query slow hai → optimization.

EXPLAIN
EXPLAIN
SELECT *
FROM employees
WHERE salary > 50000;

Ye query execution plan ke baare me information deta hai.

Important optimization points
1. Proper indexes
2. SELECT * avoid when unnecessary
3. WHERE filtering
4. JOIN conditions correct rakho
5. Large unnecessary data avoid karo
6. Subqueries ko carefully use karo
7. EXPLAIN se query plan check karo
🧠 PHASE 16–22 — ONE-SHOT REVISION
PHASE 16 → VIEWS
Saved reusable query

PHASE 17 → CTE
Temporary named query result

PHASE 18 → WINDOW FUNCTIONS
ROW_NUMBER
RANK
DENSE_RANK
LAG
LEAD
PARTITION BY
Running Total

PHASE 19 → TRANSACTIONS
COMMIT
ROLLBACK
SAVEPOINT
ACID

PHASE 20 → INDEXING
CREATE INDEX
Composite Index
Performance

PHASE 21 → NORMALIZATION
1NF
2NF
3NF
BCNF
Anomalies

PHASE 22 → OPTIMIZATION
EXPLAIN
Indexes
Query optimization
📈 SQL STATUS

Phase 1 → 15: ✅ Complete
Phase 16 → 22: ✅ Compactly covered
Phase 23: 🔥 Advanced SQL + Interview Preparation — Baki

Overall: ~95% SQL Complete 🚀

Ab Phase 23 ko final phase rakhenge—usme unnecessarily theory nahi kheechunga; important tricky queries + interview patterns + real-world problems + final revision karenge.