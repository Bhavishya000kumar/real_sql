🚀 SQL — PHASE 14
Chapter: SQL Functions
Complete Phase — All Functions in One Go 🔥

Haan bhai, Phase 14 start.
Aur jaise fix kiya hai, Functions ke saare important topics isi ek Phase 14 me complete karenge — beech me Phase 14.1/14.2 nahi.

📊 SQL ROADMAP
Overall SQL Progress: ~78% 🟢
Phase 14 — SQL Functions
1. Functions kya hoti hain
2. Aggregate Functions
   ├── COUNT()
   ├── SUM()
   ├── AVG()
   ├── MIN()
   └── MAX()

3. String Functions
   ├── CONCAT()
   ├── LENGTH()
   ├── LOWER()
   ├── UPPER()
   ├── SUBSTRING()
   ├── TRIM()
   └── REPLACE()

4. Numeric Functions
   ├── ROUND()
   ├── CEIL()
   ├── FLOOR()
   └── ABS()

5. Date & Time Functions
   ├── NOW()
   ├── CURDATE()
   ├── CURTIME()
   ├── DATE()
   ├── YEAR()
   ├── MONTH()
   ├── DAY()
   └── DATEDIFF()

6. NULL Functions
   ├── IFNULL()
   ├── COALESCE()
   └── NULLIF()

7. CASE Expression

8. Functions with
   ├── WHERE
   ├── GROUP BY
   ├── HAVING
   ├── ORDER BY
   └── JOIN

9. Complete Practical
10. Practice Questions + Solutions
11. Interview Questions
1. SQL Function kya hoti hai?

Simple language:

Function ek built-in operation hoti hai jo input leti hai aur koi result return karti hai.

Example:

SELECT UPPER('rahul');

Result:

RAHUL

Yahan:

UPPER()
  ↓
Input: rahul
  ↓
Output: RAHUL
2. Functions ke major types

Hum broadly inko samjhenge:

SQL FUNCTIONS
│
├── Aggregate
│   └── Multiple rows → One result
│
├── String
│   └── Text ke saath kaam
│
├── Numeric
│   └── Numbers ke saath kaam
│
├── Date/Time
│   └── Dates & time
│
└── NULL functions
    └── NULL handle karna
🔥 PART 1 — AGGREGATE FUNCTIONS

Aggregate function ka simple meaning:

Multiple rows ke data ko process karke generally ek result return karna.

Example:

Marks:
80
90
70

AVG():

80 + 90 + 70
─────────────
      3

= 80
3. COUNT()

COUNT() rows/counting ke liye use hota hai.

Suppose:

employees

id
1
2
3
4
5

Query:

SELECT COUNT(*)
FROM employees;

Result:

5
COUNT(*)

Table/result me rows count karta hai.

4. COUNT(column)
SELECT COUNT(email)
FROM employees;

Important:

COUNT(column) NULL values ko count nahi karta.

Example:

id	email
1	a@gmail.com
2	NULL
3	b@gmail.com
SELECT COUNT(email)
FROM employees;

Result:

2

But:

SELECT COUNT(*)
FROM employees;

Result:

3

🔥 Ye interview me bahut important hai.

5. COUNT(DISTINCT column)

Unique values count karni ho:

SELECT COUNT(DISTINCT department_id)
FROM employees;

Example:

department_id

1
1
2
2
3

Result:

3
6. SUM()

Numbers ka total:

SELECT SUM(salary)
FROM employees;

Example:

20000
30000
40000

Result:

90000
7. AVG()

Average:

SELECT AVG(salary)
FROM employees;

Example:

20000
30000
40000

Result:

30000
8. MIN()

Smallest value:

SELECT MIN(salary)
FROM employees;
9. MAX()

Largest value:

SELECT MAX(salary)
FROM employees;
🧠 Aggregate Functions Shortcut
COUNT → Kitne?
SUM   → Total kitna?
AVG   → Average?
MIN   → Sabse chhota?
MAX   → Sabse bada?
🔥 Practical Setup

Ab actual practice karte hain.

MySQL Workbench me New SQL Tab kholo.

Apna database select karo:

USE sql_practice;

Phir:

CREATE TABLE function_practice (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(50),
    department VARCHAR(50),
    salary DECIMAL(10,2)
);

Run karo.

Data:

INSERT INTO function_practice
VALUES
(1, 'Rahul', 'CSE', 30000),
(2, 'Aman', 'CSE', 40000),
(3, 'Rohit', 'ECE', 25000),
(4, 'Priya', 'ECE', 50000),
(5, 'Neha', 'ME', 35000);

Check:

SELECT *
FROM function_practice;
10. COUNT Practice
SELECT COUNT(*)
FROM function_practice;

Result:

5
11. SUM
SELECT SUM(salary)
FROM function_practice;

Total:

185000
12. AVG
SELECT AVG(salary)
FROM function_practice;

Result:

37000
13. MIN
SELECT MIN(salary)
FROM function_practice;

Result:

25000
14. MAX
SELECT MAX(salary)
FROM function_practice;

Result:

50000
🔥 PART 2 — STRING FUNCTIONS

String = text.

Example:

'Rahul'
'Delhi'
'Python'
15. UPPER()

Text ko uppercase:

SELECT UPPER('rahul');

Output:

RAHUL

Table:

SELECT UPPER(employee_name)
FROM function_practice;
16. LOWER()

Lowercase:

SELECT LOWER('RAHUL');

Output:

rahul
17. CONCAT()

Multiple strings join karna.

SELECT CONCAT('Hello ', 'Rahul');

Output:

Hello Rahul

Table example:

SELECT CONCAT(employee_name, ' - ', department)
FROM function_practice;

Output:

Rahul - CSE
Aman - CSE
...
18. LENGTH()

String ki length:

SELECT LENGTH('Rahul');

Result:

5

Table:

SELECT employee_name, LENGTH(employee_name)
FROM function_practice;
19. TRIM()

Beginning aur ending ke extra spaces remove karta hai.

SELECT TRIM('   Rahul   ');

Output:

Rahul
20. SUBSTRING()

String ka ek portion nikalna.

SELECT SUBSTRING('Rahul', 1, 3);

Result:

Rah

MySQL me indexing yahan 1 se start hoti hai.

Format:

SUBSTRING(string, start, length)
21. REPLACE()

Ek text ko dusre text se replace karna.

SELECT REPLACE('I love Java', 'Java', 'SQL');

Output:

I love SQL
🧠 String Shortcut
UPPER     → CAPITAL
LOWER     → small
CONCAT    → join
LENGTH    → length
TRIM      → extra spaces remove
SUBSTRING → part of text
REPLACE   → text replace
🔥 PART 3 — NUMERIC FUNCTIONS
22. ROUND()

Decimal round karna:

SELECT ROUND(45.6789);

Result:

46

Specific decimal places:

SELECT ROUND(45.6789, 2);

Result:

45.68
23. CEIL()

Number ko next/up integer ki taraf le jata hai.

SELECT CEIL(4.2);

Result:

5
24. FLOOR()

Down integer:

SELECT FLOOR(4.9);

Result:

4
25. ABS()

Absolute value:

SELECT ABS(-50);

Result:

50
🧠 Numeric Shortcut
ROUND → Round
CEIL  → Upar
FLOOR → Neeche
ABS   → Positive magnitude
🔥 PART 4 — DATE & TIME FUNCTIONS
26. NOW()

Current date + time:

SELECT NOW();

Example:

2026-08-31 21:30:00

Exact value tumhare execution time par depend karegi.

27. CURDATE()

Current date:

SELECT CURDATE();

Example:

2026-08-31
28. CURTIME()

Current time:

SELECT CURTIME();
29. DATE()

Datetime se sirf date:

SELECT DATE('2026-08-31 15:30:20');

Result:

2026-08-31
30. YEAR()
SELECT YEAR('2026-08-31');

Result:

2026
31. MONTH()
SELECT MONTH('2026-08-31');

Result:

8
32. DAY()
SELECT DAY('2026-08-31');

Result:

31
33. DATEDIFF()

Do dates ke beech days ka difference:

SELECT DATEDIFF('2026-08-31', '2026-08-01');

Result:

30

Format:

DATEDIFF(later_date, earlier_date)

Important:

DATEDIFF() primarily days ka difference return karta hai.

🔥 PART 5 — NULL FUNCTIONS

NULL SQL ka very important concept hai.

34. IFNULL()

Agar value NULL hai, alternative value use karo.

SELECT IFNULL(NULL, 0);

Result:

0

Example:

SELECT employee_name, IFNULL(salary, 0)
FROM function_practice;

Agar salary NULL hui:

NULL → 0
35. COALESCE()

COALESCE() multiple values me se first non-NULL value return karta hai.

SELECT COALESCE(NULL, NULL, 'Rahul', 'Aman');

Result:

Rahul

Because Rahul first non-NULL value hai.

36. IFNULL vs COALESCE
IFNULL
→ generally 2 arguments
→ first NULL ho to second

COALESCE
→ multiple arguments
→ first non-NULL

Example:

SELECT IFNULL(NULL, 'A');
SELECT COALESCE(NULL, NULL, 'A', 'B');

Both return:

A
37. NULLIF()

Do values compare karta hai.

SELECT NULLIF(10, 10);

Result:

NULL

Because values equal hain.

Agar:

SELECT NULLIF(10, 20);

Result:

10

Shortcut:

NULLIF(a,b)
→ a = b → NULL
→ a ≠ b → a
🔥 PART 6 — CASE

CASE SQL me if-else jaisa kaam karta hai.

Example:

Salary ke basis par category:

SELECT
    employee_name,
    salary,
    CASE
        WHEN salary >= 40000 THEN 'High'
        WHEN salary >= 30000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category
FROM function_practice;

Output:

employee_name	salary	salary_category
Rahul	30000	Medium
Aman	40000	High
Rohit	25000	Low
Priya	50000	High
Neha	35000	Medium
38. CASE ko programming se compare karo

C++/Java me:

if salary >= 40000
    High
else if salary >= 30000
    Medium
else
    Low

SQL:

CASE
    WHEN salary >= 40000 THEN 'High'
    WHEN salary >= 30000 THEN 'Medium'
    ELSE 'Low'
END

🔥 Same logic.

39. CASE + GROUP BY

Example:

SELECT
    department,
    CASE
        WHEN salary >= 40000 THEN 'High'
        ELSE 'Low'
    END AS category,
    COUNT(*) AS total
FROM function_practice
GROUP BY department, category;

Yahan CASE ka result bhi grouping me use ho raha hai.

40. Functions + WHERE

Example:

SELECT *
FROM function_practice
WHERE UPPER(employee_name) = 'RAHUL';
41. Functions + ORDER BY

Highest salary:

SELECT employee_name, ROUND(salary, 0) AS rounded_salary
FROM function_practice
ORDER BY rounded_salary DESC;
42. Aggregate + GROUP BY 🔥

Ab functions ka actual power:

SELECT
    department,
    COUNT(*) AS employee_count,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary,
    MIN(salary) AS minimum_salary,
    MAX(salary) AS maximum_salary
FROM function_practice
GROUP BY department;

Result conceptually:

department	employee_count	total_salary	average_salary	minimum	maximum
CSE	2	70000	35000	30000	40000
ECE	2	75000	37500	25000	50000
ME	1	35000	35000	35000	35000

🔥 Ye interview-level basic analytical SQL hai.

43. Aggregate + HAVING

Suppose departments jinki average salary 35000 se zyada hai:

SELECT
    department,
    AVG(salary) AS avg_salary
FROM function_practice
GROUP BY department
HAVING AVG(salary) > 35000;

Notice:

WHERE
→ individual rows

HAVING
→ groups / aggregate results
44. Function + JOIN

Suppose department table:

departments
department_id
department_name

Employees:

employee_id
employee_name
department_id
salary

Query:

SELECT
    d.department_name,
    COUNT(e.employee_id) AS total_employees,
    AVG(e.salary) AS avg_salary
FROM departments d
JOIN employees e
ON d.department_id = e.department_id
GROUP BY d.department_name;

Yahan:

JOIN
+
COUNT
+
AVG
+
GROUP BY

sab ek saath use ho rahe hain.

🧠 Functions ka Master Map
AGGREGATE
COUNT
SUM
AVG
MIN
MAX

STRING
CONCAT
LENGTH
LOWER
UPPER
SUBSTRING
TRIM
REPLACE

NUMERIC
ROUND
CEIL
FLOOR
ABS

DATE/TIME
NOW
CURDATE
CURTIME
DATE
YEAR
MONTH
DAY
DATEDIFF

NULL
IFNULL
COALESCE
NULLIF

CONDITIONAL
CASE
🧪 COMPLETE PRACTICE

Ab bina answer dekhe try karo.

Q1

Total employees count karo.

Q2

Total salary nikalo.

Q3

Highest salary nikalo.

Q4

Lowest salary nikalo.

Q5

Average salary nikalo.

Q6

Employee names uppercase me show karo.

Q7

Employee name aur department ko ek string me combine karo.

Example:

Rahul - CSE
Q8

Employee names ki length nikalo.

Q9

Salary ko nearest thousand tak round karo.

Q10

Department-wise employee count nikalo.

Q11

Department-wise average salary nikalo.

Q12

Sirf woh departments dikhao jinki average salary 35000 se greater hai.

Q13

Salary ke basis par:

>= 40000 → High
>= 30000 → Medium
else → Low
Q14

Current date nikalo.

Q15

Current date se 2026-01-01 tak days difference nikalo.

✅ SOLUTIONS
Q1
SELECT COUNT(*)
FROM function_practice;
Q2
SELECT SUM(salary)
FROM function_practice;
Q3
SELECT MAX(salary)
FROM function_practice;
Q4
SELECT MIN(salary)
FROM function_practice;
Q5
SELECT AVG(salary)
FROM function_practice;
Q6
SELECT UPPER(employee_name)
FROM function_practice;
Q7
SELECT CONCAT(employee_name, ' - ', department)
FROM function_practice;
Q8
SELECT employee_name, LENGTH(employee_name)
FROM function_practice;
Q9
SELECT employee_name, ROUND(salary, -3)
FROM function_practice;
Q10
SELECT department, COUNT(*)
FROM function_practice
GROUP BY department;
Q11
SELECT department, AVG(salary)
FROM function_practice
GROUP BY department;
Q12
SELECT department, AVG(salary) AS avg_salary
FROM function_practice
GROUP BY department
HAVING AVG(salary) > 35000;
Q13
SELECT
    employee_name,
    salary,
    CASE
        WHEN salary >= 40000 THEN 'High'
        WHEN salary >= 30000 THEN 'Medium'
        ELSE 'Low'
    END AS category
FROM function_practice;
Q14
SELECT CURDATE();
Q15
SELECT DATEDIFF(CURDATE(), '2026-01-01');
🎯 INTERVIEW QUESTIONS
1. SQL Function kya hai?

A predefined operation that takes input and returns a result.

2. Aggregate Function kya hai?

Multiple rows ko process karke generally summarized result provide karti hai.

3. Five common aggregate functions?
COUNT
SUM
AVG
MIN
MAX
4. COUNT(*) vs COUNT(column)?
COUNT(*)       → rows count
COUNT(column)  → non-NULL values count
5. UNION aur COUNT ka relation?

Direct relation nahi; COUNT aggregate function hai, UNION set operation hai.

6. WHERE aur HAVING?
WHERE
→ rows filter

HAVING
→ groups/aggregate results filter
7. IFNULL()?

NULL ko specified replacement value se replace kar sakta hai.

8. COALESCE()?

Multiple expressions me se first non-NULL value return karta hai.

9. NULLIF()?

Equal values par NULL, otherwise first expression return karta hai.

10. CASE kya hai?

SQL ka conditional expression, similar to if/else logic.

11. NOW() vs CURDATE()?
NOW()      → date + time
CURDATE()  → date only
12. CEIL() vs FLOOR()?
CEIL  → upward integer
FLOOR → downward integer
13. ROUND(45.678,2)?
45.68
14. DATEDIFF() kya return karta hai?

Do dates ke beech number of days.

15. UPPER()?

Text ko uppercase me convert karta hai.

16. SUBSTRING()?

String ka specified portion return karta hai.

17. TRIM()?

Leading/trailing spaces remove karta hai.

18. REPLACE()?

String ke matching portion ko replace karta hai.

19. MIN() aur MAX() kis type ke data par useful hain?

Numbers, dates, aur comparable values par.

20. Kya aggregate function ko GROUP BY ke saath use kar sakte hain?

Yes. Ye SQL analytics ka very common pattern hai.

🔥 5 SUPER-IMPORTANT INTERVIEW TRAPS
Trap 1
COUNT(*)

NULL rows ko bhi row ke roop me count karega.

Trap 2
COUNT(email)

NULL emails count nahi karega.

Trap 3
AVG(salary)

Normally NULL salary values average calculation me ignore hoti hain.

Trap 4
WHERE AVG(salary) > 30000

❌ Aggregate filtering ke liye normally HAVING use karoge.

HAVING AVG(salary) > 30000

✅

Trap 5
COALESCE(NULL, NULL, 10, 20)

Result:

10

Because first non-NULL.

🏆 PHASE 14 FINAL REVISION
                 SQL FUNCTIONS
                       │
       ┌───────────────┼────────────────┐
       ↓               ↓                ↓
  AGGREGATE         STRING           NUMERIC
       │               │                │
 COUNT              CONCAT            ROUND
 SUM                LENGTH            CEIL
 AVG                LOWER             FLOOR
 MIN                UPPER             ABS
 MAX                SUBSTRING
                    TRIM
                    REPLACE
       │
       ├──────────── DATE/TIME
       │              │
       │             NOW
       │             CURDATE
       │             CURTIME
       │             DATE
       │             YEAR
       │             MONTH
       │             DAY
       │             DATEDIFF
       │
       ├──────────── NULL
       │              │
       │             IFNULL
       │             COALESCE
       │             NULLIF
       │
       └──────────── CONDITIONAL
                      │
                     CASE
📊 PHASE 14 STATUS
Functions Basics       ✅
Aggregate Functions    ✅
COUNT                  ✅
SUM                    ✅
AVG                    ✅
MIN                    ✅
MAX                    ✅

String Functions       ✅
Numeric Functions      ✅
Date/Time Functions    ✅
NULL Functions         ✅
CASE                   ✅

Functions + WHERE      ✅
Functions + GROUP BY   ✅
Functions + HAVING     ✅
Functions + JOIN       ✅

Practical              ✅
Questions + Solutions  ✅
Interview Questions    ✅
🟢 PHASE 14 = 100% COMPLETE
Overall SQL Progress: ~82% COMPLETE

Ab next roadmap ke according Phase 15 — Advanced GROUP BY & SQL Analysis hoga.
Aur usme bhi jo kuch related hai, sab ek hi Phase 15 me ek go me complete karenge.