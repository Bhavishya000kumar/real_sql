🚀 SQL — PHASE 10
Chapter: Subqueries — Continued
Lecture 33: Correlated Subquery — Deep Dive
📊 SQL Progress

Overall: ~60% Complete 🟢

Phase 10 — Subqueries
Topic	Status
Subquery Basics	✅
Single-value Subquery	✅
Multiple-row Subquery	✅
IN / NOT IN	✅
EXISTS / NOT EXISTS	✅
ANY / ALL	✅
Correlated Subquery	🔥 Aaj
Nested Subquery	⏳
Subquery in SELECT	⏳
Subquery in FROM	⏳
Subquery vs JOIN	⏳
1. Correlated Subquery kya hoti hai?

Pehle normal subquery:

SELECT student_name
FROM students
WHERE age > (
    SELECT AVG(age)
    FROM students
);

Inner query:

SELECT AVG(age)
FROM students;

Ye independently chal sakti hai.

Lekin correlated subquery me inner query outer query ki kisi value par depend karti hai.

Simple definition:

A correlated subquery is a subquery that depends on a value from the outer query.

Ye interview me directly poocha ja sakta hai.

2. Ekdum simple example

Maan lo:

employees
id	name	salary	department_id
1	Rahul	30000	1
2	Aman	50000	1
3	Rohit	40000	2
4	Priya	60000	2

Question:

Har department me jo employee apne department ki average salary se zyada kama raha hai, usko find karo.

Dhyan do:

Hume overall average salary nahi chahiye.

Hume:

CSE ki average salary
ECE ki average salary

alag-alag chahiye.

3. Pehle manually samjho
Department 1

Salaries:

30000
50000

Average:

40000

So:

Rahul   30000 > 40000 ❌
Aman    50000 > 40000 ✅
Department 2

Salaries:

40000
60000

Average:

50000

So:

Rohit   40000 > 50000 ❌
Priya   60000 > 50000 ✅

Final:

Aman
Priya
4. Ab SQL likhte hain 🔥
SELECT e.employee_name, e.salary, e.department_id
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);

Ab isko bahut dhyan se samjho.

5. Outer Query
SELECT e.employee_name, e.salary, e.department_id
FROM employees e

Hum employees ko e alias de rahe hain.

employees → e

Outer query employees ko ek-ek karke consider karegi.

6. Inner Query
SELECT AVG(e2.salary)
FROM employees e2
WHERE e2.department_id = e.department_id

Yahan:

employees → e2

Aur sabse important line:

WHERE e2.department_id = e.department_id

e2.department_id inner query se hai.

Lekin:

e.department_id

outer query se aa raha hai.

🔥 Yahi correlation hai.

7. Dry Run — Rahul

Outer query Rahul ko leti hai:

Rahul
salary = 30000
department_id = 1

Ab inner query ko pata chala:

e.department_id = 1

So inner query effectively:

SELECT AVG(e2.salary)
FROM employees e2
WHERE e2.department_id = 1;

Result:

40000

Outer query:

30000 > 40000

❌ Rahul reject.

8. Next — Aman

Outer:

Aman
salary = 50000
department_id = 1

Inner:

SELECT AVG(e2.salary)
FROM employees e2
WHERE e2.department_id = 1;

Result:

40000

Then:

50000 > 40000

✅ Aman selected.

9. Next — Rohit

Outer:

Rohit
salary = 40000
department_id = 2

Inner query automatically department 2 ke liye chalegi:

SELECT AVG(e2.salary)
FROM employees e2
WHERE e2.department_id = 2;

Result:

50000

Then:

40000 > 50000

❌

10. Next — Priya
Priya
salary = 60000
department_id = 2

Inner:

average = 50000

Comparison:

60000 > 50000

✅

🔥 Final Result
Aman
Priya
11. Ab actual difference dekho
Normal Subquery
SELECT AVG(salary)
FROM employees;

Result:

45000

Ye poori table ka average hai.

Correlated Subquery
SELECT AVG(e2.salary)
FROM employees e2
WHERE e2.department_id = e.department_id;

Ye:

Current employee ke department ka average

nikalti hai.

That's why correlated subquery powerful hai.

12. Most Important Diagram
             OUTER QUERY
                 ↓
        Employee Rahul
        department = 1
                 ↓
          INNER QUERY
                 ↓
       department = 1
                 ↓
         AVG salary = 40000
                 ↓
      Rahul salary > 40000?
                 ↓
                 ❌
                 
                 ↓
        Next employee
                 ↓
             Aman
        department = 1
                 ↓
          INNER QUERY
                 ↓
         AVG = 40000
                 ↓
       50000 > 40000?
                 ↓
                 ✅

Matlab inner query outer row ke according change ho rahi hai.

13. Isliye naam "Correlated"

Normal subquery:

Outer Query ← Inner Query

Inner query independently execute ho sakti hai.

Correlated:

Outer Query
     ↓
Inner Query
     ↑
Outer Query ki value

Dono queries connected hain.

14. Practical Practice

Ab MySQL Workbench me ye query run karo:

SELECT e.employee_name, e.salary, e.department_id
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);

Expected:

Aman
Priya
15. Ek aur important example

Question:

Har department ka highest paid employee find karo.

Correlated subquery:

SELECT e.employee_name, e.salary, e.department_id
FROM employees e
WHERE e.salary = (
    SELECT MAX(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
Department 1
30000
50000

MAX:

50000

Aman ✅

Department 2
40000
60000

MAX:

60000

Priya ✅

Output:

Aman
Priya

🔥 Ye interview-level pattern hai.

16. Correlated Subquery ko identify kaise karoge?

Question dekhte hi check karo:

Kya inner query outer query ki koi column use kar rahi hai?

Example:

WHERE e2.department_id = e.department_id

Yahan:

e2 → inner
e  → outer

So:

Correlated Subquery ✅
17. Interview Definition 📌
What is a correlated subquery?

A correlated subquery is a subquery that references a column from the outer query and therefore depends on the outer query for its execution.

Simple language:

Inner query outer query ki value par dependent hoti hai.

18. Correlated vs Normal Subquery
Normal Subquery	Correlated Subquery
Outer query se independent ho sakti hai	Outer query par dependent
Usually independently execute hoti hai	Outer row ke context me evaluate hoti hai
Outer column reference zaroori nahi	Outer column reference hota hai
Often simpler	Often more complex
⚠️ Performance Point

Correlated subquery ko samajhne ka conceptual model ye hai ki inner query outer rows ke context me repeatedly evaluate ho sakti hai.

Isliye large datasets par ye kabhi-kabhi expensive ho sakti hai.

Isi reason se interviews me frequently poocha jata hai:

Can you replace a correlated subquery with a JOIN or window function?

Ye hum Subquery vs JOIN wale lecture me properly karenge.

Abhi performance optimization ki tension nahi. Pehle concept solid karo.

📝 Practice

Pehle khud try karna, phir neeche answer se match karna.

Q1

Har department ka minimum salary find karne wale employees nikalo.

Q2

Har department ki average salary se kam salary wale employees nikalo.

Q3

Har department ka highest salary wala employee nikalo.

✅ Solutions
Q1
SELECT e.employee_name, e.salary, e.department_id
FROM employees e
WHERE e.salary = (
    SELECT MIN(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
Q2
SELECT e.employee_name, e.salary, e.department_id
FROM employees e
WHERE e.salary < (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
Q3
SELECT e.employee_name, e.salary, e.department_id
FROM employees e
WHERE e.salary = (
    SELECT MAX(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
🧠 Aaj ke Notes
CORRELATED SUBQUERY

Inner query outer query ki value/reference use karti hai.

Example:

WHERE e2.department_id = e.department_id

e2 → inner query
e  → outer query

Therefore → Correlated Subquery
Golden Rule ⭐
Normal Subquery:
Inner → independent

Correlated Subquery:
Inner → depends on Outer
📊 Phase 10 Progress
Subquery Basics          ✅
Single-value             ✅
Multiple-row             ✅
IN / NOT IN              ✅
EXISTS / NOT EXISTS      ✅
ANY / ALL                ✅
Correlated Subquery      ✅  ← TODAY
Phase 10 me ab baki:
⏳ Nested Subquery
⏳ Subquery in SELECT
⏳ Subquery in FROM
⏳ Subquery vs JOIN
⏳ Subquery complete practice

Uske baad Phase 10 ka next chapter → Set Operations (UNION, UNION ALL, etc.) start hoga.

🚀 SQL — PHASE 10
Chapter: Subqueries — Continued
Lecture 34: Nested Subquery + Subquery in SELECT & FROM

Haan, chalo next. Aaj Subquery chapter ke remaining 3 important forms karte hain, taaki ye section almost complete ho jaye.

📊 SQL ROADMAP
Overall SQL Progress: ~62–63% 🟢
Phase 10 — Subqueries
Topic	Status
Subquery Basics	✅
Single-value Subquery	✅
Multiple-row Subquery	✅
IN / NOT IN	✅
EXISTS / NOT EXISTS	✅
ANY / ALL	✅
Correlated Subquery	✅
Nested Subquery	🔥 TODAY
Subquery in SELECT	🔥 TODAY
Subquery in FROM	🔥 TODAY
Subquery vs JOIN	⏳
Final Subquery Practice	⏳
PART 1 — Nested Subquery
1. Nested Subquery kya hoti hai?

Simple language:

Jab ek subquery ke andar bhi ek aur subquery ho, use Nested Subquery kehte hain.

Matlab:

Outer Query
    ↓
  Subquery
    ↓
Nested Subquery

Ya:

Query
 └── Query
      └── Query
2. Simple example

Question:

Company ke highest-paid employee ka naam find karo.

Normal subquery se:

SELECT employee_name
FROM employees
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
);

Yahan sirf ek subquery hai.

Ab nested example banate hain.

Suppose:

Un employees ko find karo jo Delhi location wale department me kaam karte hain aur unki salary overall average salary se zyada hai.

Hume 2 cheezein find karni hain:

Delhi wale departments
Overall average salary

Query:

SELECT employee_name, salary
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE location = 'Delhi'
)
AND salary > (
    SELECT AVG(salary)
    FROM employees
);

Technically yahan multiple subqueries hain.

Lekin proper nested structure samajhne ke liye ek aur example dekho.

3. Proper Nested Subquery Example

Suppose tables:

employees
employee_name | salary | department_id
departments
department_id | department_name | location

Question:

Delhi me located departments ke employees me se highest salary wale employee ko find karo.

Pehle Delhi departments:

SELECT department_id
FROM departments
WHERE location = 'Delhi';

Suppose result:

1
3

Ab in departments ke employees:

SELECT MAX(salary)
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE location = 'Delhi'
);

Inner query:

SELECT department_id
FROM departments
WHERE location = 'Delhi'

Result:

1
3

Us result ko outer subquery use kar rahi hai:

SELECT MAX(salary)
FROM employees
WHERE department_id IN (1,3);

Suppose result:

70000

Ab final employee:

SELECT employee_name, salary
FROM employees
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
    WHERE department_id IN (
        SELECT department_id
        FROM departments
        WHERE location = 'Delhi'
    )
);

🔥 Ab dekho actual nesting:

Main Query
    ↓
MAX salary wali Subquery
    ↓
Delhi departments wali Subquery

Ye Nested Subquery ka basic pattern hai.

4. Isko step-by-step visualize karo
                    MAIN QUERY
                        ↓
             salary = [something]
                        ↓
              MAX(salary) QUERY
                        ↓
       department_id IN [something]
                        ↓
             Delhi departments
                        ↓
                  1, 3

Phir:

1,3
 ↓
Delhi departments ke employees
 ↓
MAX salary
 ↓
70000
 ↓
Main query
 ↓
Employee with salary 70000
PART 2 — Subquery inside SELECT

Ab ek bahut useful form.

Usually hum likhte hain:

SELECT employee_name, salary
FROM employees;

Lekin SELECT ke andar bhi subquery aa sakti hai.

5. Example

Question:

Har employee ke saath company ki average salary bhi dikhao.

SELECT
    employee_name,
    salary,
    (SELECT AVG(salary) FROM employees) AS average_salary
FROM employees;

Suppose average:

45000

Output:

employee_name	salary	average_salary
Rahul	30000	45000
Aman	50000	45000
Rohit	40000	45000
Priya	60000	45000

Notice karo:

AVG(salary) ek hi value return kar raha hai:

45000

Aur wo har row ke saath display ho rahi hai.

6. Ye kaise kaam kar raha hai?

Query:

SELECT
    employee_name,
    salary,
    (SELECT AVG(salary) FROM employees) AS average_salary
FROM employees;

Outer query:

FROM employees

employees ki rows la rahi hai.

Subquery:

SELECT AVG(salary)
FROM employees

company average nikal rahi hai.

Phir:

Rahul → 30000 → 45000
Aman  → 50000 → 45000
Rohit → 40000 → 45000
Priya → 60000 → 45000
7. Practical

Workbench me run karo:

SELECT
    employee_name,
    salary,
    (SELECT AVG(salary) FROM employees) AS average_salary
FROM employees;

Output me har employee ke saath same average salary aani chahiye.

8. Ek aur useful example

Question:

Har employee ke saath maximum salary bhi dikhao.

SELECT
    employee_name,
    salary,
    (SELECT MAX(salary) FROM employees) AS maximum_salary
FROM employees;

Output:

Rahul   30000   60000
Aman    50000   60000
Rohit   40000   60000
Priya   60000   60000
PART 3 — Subquery inside FROM

Ab thoda advanced.

Subquery ko hum FROM ke andar bhi use kar sakte hain.

Isko generally derived table kaha jata hai.

9. Derived Table kya hota hai?

Example:

SELECT *
FROM (
    SELECT employee_name, salary
    FROM employees
    WHERE salary > 40000
) AS high_salary;

Yahan:

(
    SELECT employee_name, salary
    FROM employees
    WHERE salary > 40000
)

ek temporary result/table jaisa behave kar raha hai.

Isliye usko alias dena padta hai:

AS high_salary
10. Step-by-step

Inner query:

SELECT employee_name, salary
FROM employees
WHERE salary > 40000;

Suppose result:

employee_name	salary
Aman	50000
Priya	60000

Ab SQL ise temporarily table maan sakta hai:

high_salary
-----------------
employee_name
salary

Outer query:

SELECT *
FROM high_salary;

So complete:

SELECT *
FROM (
    SELECT employee_name, salary
    FROM employees
    WHERE salary > 40000
) AS high_salary;
11. Derived table ka useful example

Question:

Salary > 40000 wale employees me se highest salary find karo.

Pehle filtered employees:

SELECT employee_name, salary
FROM employees
WHERE salary > 40000;

Ab us result par MAX() lagana hai:

SELECT MAX(salary)
FROM (
    SELECT salary
    FROM employees
    WHERE salary > 40000
) AS high_salary;

Inner:

50000
60000

Outer:

MAX = 60000
12. FROM wali subquery ka naam

Interview me agar poocha:

What is a subquery in the FROM clause called?

Answer:

Derived Table

Example:

FROM (
    SELECT ...
) AS result
13. Ek important rule ⚠️

FROM ke andar subquery ko generally alias dena zaroori hota hai.

❌ Avoid:

SELECT *
FROM (
    SELECT salary
    FROM employees
);

✅ Correct:

SELECT *
FROM (
    SELECT salary
    FROM employees
) AS result;
🧠 Ab 3 forms ko compare karo
1️⃣ Subquery in WHERE
SELECT employee_name
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);

Use: Filtering.

2️⃣ Subquery in SELECT
SELECT
    employee_name,
    salary,
    (SELECT AVG(salary) FROM employees) AS avg_salary
FROM employees;

Use: Additional calculated information display karna.

3️⃣ Subquery in FROM
SELECT *
FROM (
    SELECT employee_name, salary
    FROM employees
    WHERE salary > 40000
) AS result;

Use: Subquery ke result ko temporary table/derived table ki tarah use karna.

📌 Super Important Diagram
SUBQUERY

        WHERE
          ↓
     Filtering

        SELECT
          ↓
 Additional information

        FROM
          ↓
 Derived Table
📝 Practice

Pehle khud try karo 👇

Q1

Har employee ke saath minimum salary bhi display karo.

Q2

Har employee ke saath average salary aur employee ki salary display karo.

Q3

employees me se salary 40000 se greater employees ko ek derived table banao aur us derived table se maximum salary find karo.

Q4

Delhi departments me kaam karne wale employees me se highest salary wale employee ko nested subquery se find karo.

✅ Solutions
Q1
SELECT
    employee_name,
    salary,
    (SELECT MIN(salary) FROM employees) AS minimum_salary
FROM employees;
Q2
SELECT
    employee_name,
    salary,
    (SELECT AVG(salary) FROM employees) AS average_salary
FROM employees;
Q3
SELECT MAX(salary)
FROM (
    SELECT salary
    FROM employees
    WHERE salary > 40000
) AS high_salary;
Q4
SELECT employee_name, salary
FROM employees
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
    WHERE department_id IN (
        SELECT department_id
        FROM departments
        WHERE location = 'Delhi'
    )
);
🎯 Interview Questions
Q1. What is a nested subquery?

A subquery containing another subquery inside it.

Q2. What is a derived table?

A subquery used in the FROM clause whose result behaves like a temporary table for the outer query.

Q3. Can a subquery be used in the SELECT clause?

Yes.

Example:

SELECT
    employee_name,
    (SELECT AVG(salary) FROM employees) AS avg_salary
FROM employees;
Q4. Why is an alias used for a derived table?

Because the derived table needs a name that the outer query can reference.

📊 PHASE 10 — Updated Progress
Subquery Section
Subquery Basics              ✅
Single-value Subquery        ✅
Multiple-row Subquery        ✅
IN / NOT IN                  ✅
EXISTS / NOT EXISTS          ✅
ANY / ALL                    ✅
Correlated Subquery          ✅
Nested Subquery              ✅
Subquery in SELECT           ✅
Subquery in FROM             ✅
Baki:
⏳ Subquery vs JOIN
⏳ Complete Subquery Practice

Uske baad Phase 10 ka next major section: UNION, UNION ALL, INTERSECT, EXCEPT.

Overall SQL ≈ 65% complete 🟢.


🚀 SQL — PHASE 10
Chapter: Subqueries — Final Part
Lecture 35: Subquery vs JOIN + Final Subquery Revision

Aaj Subquery section ka last important part karte hain. Iske baad Subqueries ko close karke next topic Set Operations start karenge.

📊 SQL ROADMAP
Overall SQL Progress: ~66% 🟢
Phase 10 — Subqueries
Topic	Status
Subquery Basics	✅
Single-value Subquery	✅
Multiple-row Subquery	✅
IN / NOT IN	✅
EXISTS / NOT EXISTS	✅
ANY / ALL	✅
Correlated Subquery	✅
Nested Subquery	✅
Subquery in SELECT	✅
Subquery in FROM	✅
Subquery vs JOIN	🔥 TODAY
Final Subquery Practice	🔥 TODAY
1. Sabse pehle — Subquery vs JOIN

Dono ka use kabhi-kabhi same problem solve karne ke liye ho sakta hai.

Example:

Hume employee ka naam aur uske department ka naam chahiye.

Tables:

employees
employee_id	employee_name	department_id
1	Rahul	1
2	Aman	2
3	Rohit	1
departments
department_id	department_name
1	CSE
2	ECE
2. JOIN se
SELECT
    e.employee_name,
    d.department_name
FROM employees e
JOIN departments d
ON e.department_id = d.department_id;

Output:

employee_name	department_name
Rahul	CSE
Aman	ECE
Rohit	CSE
3. Subquery se bhi kuch situations me kar sakte ho
SELECT
    employee_name,
    (
        SELECT department_name
        FROM departments d
        WHERE d.department_id = e.department_id
    ) AS department_name
FROM employees e;

Yahan inner query outer employee ki department_id use kar rahi hai.

So ye correlated subquery hai.

4. Dono me difference kya hai?
JOIN
employees
    ↓
JOIN
    ↓
departments

Dono tables ko combine karta hai.

Subquery
Outer Query
     ↓
Inner Query
     ↓
Result

Ek query ke result ko doosri query me use karta hai.

5. Kab JOIN prefer karna hai?

Agar question simply bol raha hai:

"Employees ke saath department information dikhao."

To generally:

JOIN

zyada natural hai.

Example:

SELECT e.employee_name, d.department_name
FROM employees e
JOIN departments d
ON e.department_id = d.department_id;
6. Kab Subquery useful hai?

Jab question me comparison/filtering type ka logic ho:

Average salary se zyada salary wale employees.

SELECT employee_name, salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);

Yahan subquery bahut natural hai.

7. Same problem — JOIN vs Subquery

Question:

Department average salary se zyada earn karne wale employees find karo.

Correlated Subquery:
SELECT e.employee_name, e.salary
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
JOIN approach

Pehle department-wise average:

SELECT department_id, AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id;

Ab JOIN:

SELECT
    e.employee_name,
    e.salary
FROM employees e
JOIN (
    SELECT department_id, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
) a
ON e.department_id = a.department_id
WHERE e.salary > a.avg_salary;

Dono ka logic same hai.

8. Interview me kya bolna hai?

Agar interviewer pooche:

Subquery or JOIN — which is better?

❌ Ye mat bolna:

JOIN is always better.

Ya:

Subquery is always better.

Correct understanding:

It depends on the problem, query structure, readability and execution plan.

Kuch cases me JOIN clearer/efficient ho sakta hai, kuch cases me subquery simpler hoti hai.

9. EXISTS vs JOIN

Ye bhi important interview comparison hai.

Suppose:

Aise departments find karo jisme at least ek employee exist karta hai.

EXISTS
SELECT d.department_name
FROM departments d
WHERE EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.department_id = d.department_id
);

Meaning:

"Kya is department ka koi employee exist karta hai?"
JOIN
SELECT DISTINCT d.department_name
FROM departments d
JOIN employees e
ON d.department_id = e.department_id;

Yahan duplicates aa sakte hain agar ek department me multiple employees hain, isliye DISTINCT ki zarurat pad sakti hai.

⭐ Important Point

EXISTS ka main purpose:

Existence check

JOIN ka main purpose:

Tables ko combine karna
10. IN vs EXISTS

Example:

SELECT employee_name
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE location = 'Delhi'
);

vs:

SELECT e.employee_name
FROM employees e
WHERE EXISTS (
    SELECT 1
    FROM departments d
    WHERE d.department_id = e.department_id
      AND d.location = 'Delhi'
);

Dono se same type ka result mil sakta hai.

Simple difference:

IN
↓
Returned values ke andar membership check

EXISTS
↓
Matching row exist karti hai ya nahi
11. NOT IN vs NOT EXISTS ⚠️

Ye interview me bahut important hai.

NOT IN ke saath NULL problematic ho sakta hai.

Example:

WHERE department_id NOT IN (
    SELECT department_id
    FROM departments
);

Agar subquery result me NULL aa gaya, to SQL's three-valued logic ki wajah se unexpected/no rows mil sakte hain.

NOT EXISTS often safer pattern hota hai:

WHERE NOT EXISTS (
    SELECT 1
    FROM departments d
    WHERE d.department_id = e.department_id
);
Interview takeaway:

Be careful with NOT IN when the subquery can return NULL.

🧠 Ab poora Subquery chapter revise karo
12. Single-value

Subquery:

SELECT AVG(salary)
FROM employees;

Ek value:

45000

Use:

WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
13. Multiple-value
WHERE department_id IN (
    SELECT department_id
    FROM departments
);

Subquery multiple values return kar sakti hai.

14. EXISTS
WHERE EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.department_id = d.department_id
);

Meaning:

Matching row exists?
15. ANY
WHERE salary > ANY (
    SELECT salary
    FROM employees
);

Meaning:

At least ONE comparison TRUE
16. ALL
WHERE salary > ALL (
    SELECT salary
    FROM employees
);

Meaning:

EVERY comparison TRUE
17. Correlated
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);

Important:

e2 → inner
e  → outer

Inner query outer query ki value use kar rahi hai.

18. Nested
SELECT employee_name
FROM employees
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
    WHERE department_id IN (
        SELECT department_id
        FROM departments
        WHERE location = 'Delhi'
    )
);

Structure:

Main Query
   ↓
Subquery
   ↓
Nested Subquery
19. Subquery in SELECT
SELECT
    employee_name,
    salary,
    (SELECT AVG(salary) FROM employees) AS avg_salary
FROM employees;

Use:

Additional information display karna
20. Subquery in FROM
SELECT *
FROM (
    SELECT employee_name, salary
    FROM employees
    WHERE salary > 40000
) AS high_salary;

Isko:

Derived Table

kehte hain.

🔥 FINAL SUBQUERY PRACTICE

Ab 5 questions. Pehle khud solve karna, uske baad answer dekhna.

Q1

Company ki average salary se zyada salary wale employees find karo.

Q2

Har department ki average salary se zyada salary wale employees find karo.

Q3

Har department ka highest-paid employee find karo.

Q4

Delhi location ke departments me kaam karne wale employees find karo.

Q5

Aise departments find karo jisme koi employee exist karta hai.

✅ Answers
Q1
SELECT employee_name, salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
Q2
SELECT e.employee_name, e.salary
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
Q3
SELECT e.employee_name, e.salary
FROM employees e
WHERE e.salary = (
    SELECT MAX(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
Q4
SELECT employee_name
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE location = 'Delhi'
);
Q5
SELECT d.department_name
FROM departments d
WHERE EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.department_id = d.department_id
);
🎯 Interview Quick Fire

1. What is a subquery?

Query ke andar ek query.

2. What is a correlated subquery?

Inner query outer query ki value/reference par depend karti hai.

3. What is EXISTS used for?

Matching row ke existence ko check karne ke liye.

4. ANY ka meaning?

At least one comparison TRUE.

5. ALL ka meaning?

Every comparison TRUE.

6. = ANY kis ke similar hai?

IN

7. FROM me subquery ko kya bolte hain?

Derived table.

8. Kya subquery SELECT me aa sakti hai?

Yes.

9. NOT IN ke saath kya important issue hai?

Subquery result me NULL hone par unexpected behavior ho sakta hai.

10. JOIN vs Subquery?

Koi universally "better" nahi; problem, readability aur execution plan par depend karta hai.

✅ PHASE 10 — SUBQUERY COMPLETE 🎉
Subquery Basics              ✅
Single-value                 ✅
Multiple-row                 ✅
IN / NOT IN                  ✅
EXISTS / NOT EXISTS          ✅
ANY / ALL                    ✅
Correlated Subquery          ✅
Nested Subquery              ✅
Subquery in SELECT           ✅
Subquery in FROM             ✅
Subquery vs JOIN             ✅
Final Practice               ✅
📈 Current Progress

Phase 10 Subqueries → 100% COMPLETE ✅

Overall SQL → ~68% COMPLETE 🟢

Next:
🔥 Phase 10 — Set Operations
UNION
UNION ALL
INTERSECT
EXCEPT

Phir inke differences + examples + practical + interview questions karenge, same format me.