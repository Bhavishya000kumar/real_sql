Bilkul 👍 Set Operations ko ek hi Phase 11 me complete karenge. Iske andar jitne important concepts/interview points hain, sab ek saath cover karenge—alag-alag phase nahi banayenge.

🚀 SQL — PHASE 11
Chapter: Set Operations
Complete Set Operations — One Phase
📊 SQL ROADMAP
Overall SQL Progress: ~68% 🟢
Phase 10 — Subqueries

100% COMPLETE ✅

Phase 11 — Set Operations

0% → TODAY COMPLETE karenge 🔥

Is Phase 11 me:

UNION
UNION ALL
INTERSECT
EXCEPT
Rules of Set Operations
Column matching
Data-type compatibility
ORDER BY with Set Operations
Duplicates
NULL handling
Set Operations vs JOIN
Interview questions
Practical questions
1. Sabse pehle — Set Operations kya hain?

Simple language:

Set Operations ka use do ya do se zyada SELECT queries ke results ko combine/compare karne ke liye hota hai.

Example:

Query 1
   ↓
Result 1

Query 2
   ↓
Result 2

       ↓
 SET OPERATION
       ↓
Combined Result

Important:

Set Operations tables ko directly JOIN nahi karti.

Ye SELECT ke results par kaam karti hain.

2. SQL me main Set Operations
SET OPERATIONS
│
├── UNION
├── UNION ALL
├── INTERSECT
└── EXCEPT

In 4 ko properly samajh lo, Set Operations ka major part clear.

3. UNION

UNION ka meaning:

Do queries ke results ko combine karo aur duplicate rows hata do.

Example:

Table 1:

students_2025
name
Rahul
Aman
Rohit

Table 2:

students_2026
name
Aman
Priya
Rohit

Query:

SELECT name
FROM students_2025

UNION

SELECT name
FROM students_2026;

Result:

name
Rahul
Aman
Rohit
Priya

Notice:

Aman → duplicate tha → ek baar
Rohit → duplicate tha → ek baar
Shortcut:
UNION = Combine + Remove duplicates
4. UNION ALL

Ab:

SELECT name
FROM students_2025

UNION ALL

SELECT name
FROM students_2026;

Result:

name
Rahul
Aman
Rohit
Aman
Priya
Rohit

Duplicate remove nahi hue.

Shortcut:
UNION ALL = Combine + Keep duplicates
5. UNION vs UNION ALL 🔥
UNION	UNION ALL
Duplicates remove karta hai	Duplicates rakhta hai
Distinct result	All rows
Duplicate elimination ke liye processing lagti hai	Generally simpler/faster
Use when duplicates unwanted	Use when duplicates meaningful

Interview:

Why is UNION ALL generally faster than UNION?

Because UNION ko duplicate elimination karni padti hai, while UNION ALL simply results combine karta hai.

6. Sabse important rule — Number of columns

UNION me dono queries me same number of columns hone chahiye.

✅ Correct:

SELECT name, age
FROM students_2025

UNION

SELECT name, age
FROM students_2026;

Dono me:

2 columns

❌ Wrong:

SELECT name, age
FROM students_2025

UNION

SELECT name
FROM students_2026;

Pehli query:

2 columns

Second:

1 column

Error aayega.

7. Column names same hona zaroori hai?

Nahi.

Example:

SELECT name, age
FROM students

UNION

SELECT employee_name, experience
FROM employees;

Column names different hain, phir bhi technically UNION possible hai, provided column count and compatible types satisfy requirements.

Result ke column names generally first SELECT se aate hain.

8. Data types compatible hone chahiye

Example:

SELECT employee_id
FROM employees

UNION

SELECT department_id
FROM departments;

Agar dono compatible numeric types hain → okay.

Lekin completely incompatible types avoid karo.

Simple rule:

Same number of columns + corresponding columns compatible data types.

9. Column order matters ⚠️

Suppose:

SELECT name, age
FROM students

UNION

SELECT age, name
FROM students2;

Number same hai:

2 + 2

Lekin positions matter karti hain:

Column 1 ↔ Column 1
Column 2 ↔ Column 2

So:

name ↔ age
age ↔ name

Ye logically wrong result de sakta hai.

10. INTERSECT

Ab interesting operation.

INTERSECT ka meaning:

Dono queries me jo rows common hain, sirf wahi return karo.

Example:

Query 1:

Rahul
Aman
Rohit

Query 2:

Aman
Priya
Rohit

INTERSECT:

Aman
Rohit

Because ye dono me present hain.

11. SQL Example
SELECT name
FROM students_2025

INTERSECT

SELECT name
FROM students_2026;

Result:

name
Aman
Rohit
Shortcut:
INTERSECT = Common rows
⚠️ MySQL Important

Tum MySQL Workbench use kar rahe ho, isliye ye important hai:

MySQL 8.4 documentation ke according INTERSECT supported hai, aur current MySQL versions me set-operator syntax available hai.

Lekin agar kisi older MySQL setup me syntax support na mile, to same logic ko INNER JOIN/EXISTS se reproduce kiya ja sakta hai.

Interview me DBMS/version ka context dekhna.

12. EXCEPT

EXCEPT ka meaning:

First query me jo rows hain, lekin second query me nahi hain.

Example:

Query 1:

Rahul
Aman
Rohit

Query 2:

Aman
Priya
Rohit

EXCEPT:

Rahul

Because Rahul first me hai, second me nahi.

13. Example
SELECT name
FROM students_2025

EXCEPT

SELECT name
FROM students_2026;

Result:

Rahul
Shortcut:
EXCEPT = First − Second
14. INTERSECT vs EXCEPT

Suppose:

A = {1,2,3}
B = {2,3,4}
INTERSECT
A ∩ B

Result:

{2,3}
EXCEPT
A − B

Result:

{1}
15. Sabko ek saath visualize karo 🔥

Suppose:

A = {1,2,3}
B = {2,3,4}
UNION
A ∪ B
=
{1,2,3,4}
UNION ALL
{1,2,3,2,3,4}
INTERSECT
A ∩ B
=
{2,3}
EXCEPT
A − B
=
{1}
🧠 Golden Memory Trick
UNION
↓
Sabko mila do

UNION ALL
↓
Sabko mila do + duplicate bhi rakho

INTERSECT
↓
Common nikalo

EXCEPT
↓
Pehle wale me se second wale ko hatao
16. Real-life Example

Imagine:

employees_2025

2025 me kaam karne wale employees.

employees_2026

2026 me kaam karne wale employees.

Dono years me kaam karne wale:
SELECT employee_id
FROM employees_2025

INTERSECT

SELECT employee_id
FROM employees_2026;

Meaning:

Employees who appear in both years.

Sirf 2025 wale:
SELECT employee_id
FROM employees_2025

EXCEPT

SELECT employee_id
FROM employees_2026;

Meaning:

2025 me the but 2026 me nahi.

Kisi bhi year me kaam karne wale:
SELECT employee_id
FROM employees_2025

UNION

SELECT employee_id
FROM employees_2026;

Meaning:

At least one of the two years.

17. ORDER BY ke saath Set Operations

Important rule:

Usually overall combined result ko sort karna ho to ORDER BY end me lagate hain.

SELECT name
FROM students_2025

UNION

SELECT name
FROM students_2026

ORDER BY name;

Not:

SELECT name
FROM students_2025
ORDER BY name

UNION

SELECT name
FROM students_2026;

Basic set-operation query me final ordering ke liye final ORDER BY use karo.

18. LIMIT bhi generally final result par

Example:

SELECT name
FROM students_2025

UNION

SELECT name
FROM students_2026

ORDER BY name
LIMIT 5;

Meaning:

Results combine
Duplicates remove
Sort
Top 5
19. Set Operations vs JOIN 🔥

Ye interview me important hai.

JOIN

Do tables ke columns ko side-by-side combine karta hai.

Employee        Department
   ↓                ↓
       JOIN
        ↓
Employee + Department columns

Example:

SELECT e.employee_name, d.department_name
FROM employees e
JOIN departments d
ON e.department_id = d.department_id;
UNION

Queries ke rows ko vertically combine karta hai.

Query 1
------
A
B
C

Query 2
------
D
E
F

UNION

------
A
B
C
D
E
F
Shortcut:
JOIN  → columns side-by-side
UNION → rows one below another

🔥 Ye line yaad rakho.

20. Set Operations ka basic structure
SELECT column1, column2
FROM table1

UNION

SELECT column1, column2
FROM table2;

Similarly:

SELECT column1
FROM table1

INTERSECT

SELECT column1
FROM table2;
SELECT column1
FROM table1

EXCEPT

SELECT column1
FROM table2;
21. Practical Practice

Ab Workbench me actual practice karte hain.

Agar tumhare paas already suitable tables hain, unhe use kar sakte ho. Nahi hain to ek simple practice setup bana lo.

Step 1 — Table 1
CREATE TABLE students_2025 (
    student_id INT,
    student_name VARCHAR(50)
);
Step 2 — Data
INSERT INTO students_2025 VALUES
(1, 'Rahul'),
(2, 'Aman'),
(3, 'Rohit');
Step 3 — Table 2
CREATE TABLE students_2026 (
    student_id INT,
    student_name VARCHAR(50)
);
Step 4 — Data
INSERT INTO students_2026 VALUES
(2, 'Aman'),
(3, 'Rohit'),
(4, 'Priya');
22. UNION Practice
SELECT student_name
FROM students_2025

UNION

SELECT student_name
FROM students_2026;

Expected:

Rahul
Aman
Rohit
Priya
23. UNION ALL Practice
SELECT student_name
FROM students_2025

UNION ALL

SELECT student_name
FROM students_2026;

Expected:

Rahul
Aman
Rohit
Aman
Rohit
Priya
24. INTERSECT Practice
SELECT student_name
FROM students_2025

INTERSECT

SELECT student_name
FROM students_2026;

Expected:

Aman
Rohit
25. EXCEPT Practice
SELECT student_name
FROM students_2025

EXCEPT

SELECT student_name
FROM students_2026;

Expected:

Rahul
📝 Ab Khud Se Questions

Pehle khud solve karna, answers neeche hain.

Q1

2025 aur 2026 dono years me present students find karo.

Q2

Dono years ke saare unique students find karo.

Q3

2025 me hain but 2026 me nahi hain, unhe find karo.

Q4

Dono years ke students ko duplicates ke saath combine karo.

Q5

Combined unique students ko alphabetical order me display karo.

✅ Solutions
Q1 — Common
SELECT student_name
FROM students_2025

INTERSECT

SELECT student_name
FROM students_2026;
Q2 — Unique combined
SELECT student_name
FROM students_2025

UNION

SELECT student_name
FROM students_2026;
Q3 — 2025 only
SELECT student_name
FROM students_2025

EXCEPT

SELECT student_name
FROM students_2026;
Q4 — Duplicates ke saath
SELECT student_name
FROM students_2025

UNION ALL

SELECT student_name
FROM students_2026;
Q5 — Alphabetical
SELECT student_name
FROM students_2025

UNION

SELECT student_name
FROM students_2026

ORDER BY student_name;
🎯 Interview Questions
Q1. What is a Set Operation?

Do ya zyada SELECT query results ko combine ya compare karne ke liye used operator.

Q2. UNION vs UNION ALL?
UNION     → duplicates remove
UNION ALL → duplicates retain
Q3. Which is generally faster?
UNION ALL

because it doesn't need duplicate elimination.

Q4. INTERSECT kya karta hai?

Dono result sets ki common rows return karta hai.

Q5. EXCEPT kya karta hai?

First result set me present but second result set me absent rows return karta hai.

Q6. UNION ke liye kya conditions hain?

Mainly:

Same number of columns
Corresponding columns compatible data types
Column positions matter
Q7. Kya column names same hone chahiye?

No.

Q8. UNION aur JOIN me difference?
UNION → rows vertically combine
JOIN  → columns horizontally combine
Q9. UNION ka result ka column name kahan se aata hai?

Normally first SELECT ke column names/aliases determine the output column names.

Q10. ORDER BY kahan lagana chahiye?

Combined result ko sort karna ho to generally final set operation ke baad.

🧠 PHASE 11 — One-Page Notes
SET OPERATIONS
│
├── UNION
│   └── Combine + Remove duplicates
│
├── UNION ALL
│   └── Combine + Keep duplicates
│
├── INTERSECT
│   └── Common rows
│
└── EXCEPT
    └── First - Second
Rules:
Same number of columns
        +
Compatible data types
        +
Same column positions
JOIN vs SET:
JOIN
→ columns combine

SET OPERATION
→ rows/results combine
📊 PHASE 11 STATUS

Set Operations → COMPLETE ✅

UNION          ✅
UNION ALL      ✅
INTERSECT      ✅
EXCEPT         ✅
Rules          ✅
Duplicates     ✅
ORDER BY       ✅
JOIN vs SET    ✅
Practical      ✅
Interview      ✅
🎉 Phase 11 Complete — 100%
Overall SQL:

~72% Complete 🟢

Next roadmap me Phase 12 — Constraints & Keys aayega:

PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
DEFAULT
CHECK
Referential Integrity
ON DELETE
ON UPDATE

Aur isme hum actual tables bana ke constraints practice karenge, sirf theory nahi.