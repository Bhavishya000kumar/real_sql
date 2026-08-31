Haan, bilkul. Yahin se continue karte hain. 🔥
JOIN chapter complete ho gaya tha, to ab next major chapter:

🚀 SQL — Phase 8
Lecture 29: SUBQUERY — Part 1

Aaj sirf Subquery ka basic concept + simple single-row subquery properly samjhenge. Ek saath bahut kuch nahi bharunga.

1. Sabse pehle: Subquery hota kya hai?

Naam ko todho:

Sub + Query

Matlab:

Ek SQL query ke andar doosri SQL query.

Example:

SELECT student_name
FROM students
WHERE age > (
    SELECT AVG(age)
    FROM students
);

Yahan outer query hai:

SELECT student_name
FROM students
WHERE age > (...)

Aur brackets ke andar:

SELECT AVG(age)
FROM students

ye inner query / subquery hai.

Simple structure:
Outer Query
     ↓
   WHERE
     ↓
  Subquery
     ↓
  Result
     ↓
Outer Query uses that result
2. Subquery ki zarurat kyun padti hai?

Ek simple question lete hain:

Average age se zyada age wale students dikhao.

Pehle hume average age nikalni padegi.

SELECT AVG(age)
FROM students;

Maan lo result aaya:

21.1

Ab hume chahiye:

age > 21.1

Normally hume do queries chalani padti:

Query 1
SELECT AVG(age)
FROM students;
Query 2
SELECT student_name
FROM students
WHERE age > 21.1;

Lekin SQL me hum dono ka kaam ek hi query me kar sakte hain.

SELECT student_name
FROM students
WHERE age > (
    SELECT AVG(age)
    FROM students
);

🔥 Yehi subquery ka basic use hai.

3. Computer internally kya karega?

Ye part bahut important hai.

Query:

SELECT student_name
FROM students
WHERE age > (
    SELECT AVG(age)
    FROM students
);

Conceptually pehle andar wali query ka result niklega:

SELECT AVG(age)
FROM students;

Suppose result:

21.1

Ab SQL conceptually outer query ko aise treat karega:

SELECT student_name
FROM students
WHERE age > 21.1;

Phir students ko check karega:

Rahul   age 20  → 20 > 21.1 ❌

Aman    age 21  → 21 > 21.1 ❌

Rohit   age 22  → 22 > 21.1 ✅

Priya   age 19  → 19 > 21.1 ❌

...

Aur jo condition satisfy karega, wahi output me aayega.

4. Subquery ko pehchanoge kaise?

Usually subquery:

(
    SELECT ...
)

parentheses () ke andar hoti hai.

Example:

WHERE age > (
    SELECT AVG(age)
    FROM students
)

Bracket ke andar wali SELECT query = Subquery

5. Ek aur simple example

Question:

Sabse zyada age wale student ka naam find karo.

Pehle maximum age:

SELECT MAX(age)
FROM students;

Suppose:

23

Ab:

SELECT student_name
FROM students
WHERE age = 23;

Subquery se:

SELECT student_name
FROM students
WHERE age = (
    SELECT MAX(age)
    FROM students
);
6. Is query ko line-by-line samjho
SELECT student_name

Student ka naam chahiye.

FROM students

Data students table se chahiye.

WHERE age =

Aise students chahiye jinki age kisi particular value ke equal hai.

Aur wo value?

(
    SELECT MAX(age)
    FROM students
)

Matlab:

Students table ki maximum age nikalo.

Phir:

age = maximum age
7. Practical — MySQL Workbench

Ab actual practice karte hain.

Step 1

MySQL Workbench open karo.

Step 2

Apna wahi existing connection open karo jisme hum students aur departments tables use kar rahe hain.

Step 3

SQL Editor me ye query likho:

SELECT student_name
FROM students
WHERE age = (
    SELECT MAX(age)
    FROM students
);
Step 4

⚡ Execute karo.

Expected result

Hamare current data ke according maximum age:

23

Isliye:

Ankit

aayega.

8. Ek important baat

Subquery ka result outer query ke liye input ban raha hai.

Isko yaad rakhne ka easiest way:

Inner Query
    ↓
Result
    ↓
Outer Query
    ↓
Final Result
9. Example — Average Salary

Ab students ki jagah employees imagine karo.

Question:

Average salary se zyada salary wale employees find karo.

SELECT employee_name, salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);

Inner query:

SELECT AVG(salary)
FROM employees;

Average salary nikalegi.

Outer query:

salary > average_salary

wale employees nikalegi.

10. Example — Minimum Age

Question:

Sabse kam age wale students find karo.

SELECT student_name, age
FROM students
WHERE age = (
    SELECT MIN(age)
    FROM students
);

Inner query:

SELECT MIN(age)
FROM students;

minimum age nikalegi.

Outer query us age wale students ko find karegi.

11. Example — Maximum Age se kam age

Question:

Un students ko find karo jinki age maximum age se kam hai.

SELECT student_name, age
FROM students
WHERE age < (
    SELECT MAX(age)
    FROM students
);
⭐ Ab ek important concept

Aaj jo humne examples dekhe unme subquery ek single value return kar rahi hai.

For example:

SELECT MAX(age)
FROM students;

Result:

23

Ek value.

Ya:

SELECT AVG(age)
FROM students;

Result:

21.1

Ek value.

Isliye hum operators use kar sakte hain:

=
>
<
>=
<=
<>
📌 Isko kya bolte hain?

Is type ko generally single-row / scalar subquery context me samjha jata hai, jab subquery ek single value return karti hai.

Example:

WHERE age = (
    SELECT MAX(age)
    FROM students
)
⚠️ Common Mistake

Ye query:

SELECT student_name
FROM students
WHERE age = (
    SELECT age
    FROM students
);

Problem kar sakti hai.

Kyun?

Andar wali query:

SELECT age
FROM students;

multiple rows return karegi.

Example:

20
21
22
19
20
21
23
20
22

Lekin = ko yahan ek single value chahiye.

Isliye aage hum seekhenge ki jab subquery multiple values return kare to kya karna hai.

Uske liye IN etc. aayega.

🧠 Aaj ka Golden Concept

Subquery ko ratna nahi hai.

Bas ye picture dimaag me rakho:

        SUBQUERY
           ↓
   koi result/value
           ↓
      OUTER QUERY
           ↓
      FINAL RESULT
📒 Quick Notes
Subquery

A query written inside another SQL query.

Basic structure:

SELECT ...
FROM ...
WHERE column operator (
    SELECT ...
    FROM ...
);
Inner Query

Bracket ke andar wali query.

Outer Query

Main/bahar wali query.

Scalar/Single-value Subquery

Jo ek single value return kare.

Example:

SELECT MAX(age)
FROM students;
🧑‍💻 Practice — Pehle Khud Try Karna
Q1

Students table se minimum age wale student ka naam find karo.

Q2

Students table se un students ko find karo jinki age average age se zyada hai.

Q3

Students table se un students ka naam aur age find karo jinki age maximum age ke equal hai.

✅ Solutions
Q1
SELECT student_name
FROM students
WHERE age = (
    SELECT MIN(age)
    FROM students
);
Q2
SELECT student_name, age
FROM students
WHERE age > (
    SELECT AVG(age)
    FROM students
);
Q3
SELECT student_name, age
FROM students
WHERE age = (
    SELECT MAX(age)
    FROM students
);
🎯 Interview Question
Q: What is a subquery?

Answer:

A subquery is a query written inside another SQL query. The result of the inner query is used by the outer query.

Simple way:

Inner Query → Result → Outer Query
🔥 Aaj ka lecture yahin complete

Aaj tumhe bas ye solidly aana chahiye:

Subquery kya hai?
        ↓
Inner query
        ↓
Outer query
        ↓
Single value kaise return hoti hai
        ↓
Outer query us value ko kaise use karti hai

Next Lecture: Subquery Part-2 — Multiple-row Subquery + IN

Wahan hum dekhenge ki agar andar wali query ek nahi, bahut saari values return kare to SQL me usko kaise handle karte hain.


Haan, bilkul. Pehle current progress clear kar dete hain, phir next lecture start karte hain. 👇

📊 SQL Progress

Abhi tak roughly 55–60% SQL course complete hai.

✅ Jo ho chuka hai
SQL Basics
Database / Table / Row / Column
CREATE DATABASE
CREATE TABLE
Data types
INSERT
SELECT
DISTINCT
WHERE
Comparison operators
AND / OR / NOT
BETWEEN
IN / NOT IN
LIKE
Wildcards % / _
IS NULL / IS NOT NULL
ORDER BY
LIMIT
UPDATE
DELETE
Aggregate functions — COUNT, SUM, AVG, MIN, MAX
Basic SQL functions
GROUP BY
HAVING
WHERE vs HAVING
INNER JOIN
LEFT JOIN
RIGHT JOIN
FULL OUTER JOIN concept + MySQL UNION approach
SELF JOIN
CROSS JOIN
JOIN aliases / multiple-table JOIN basics
Subquery basics
Single-value/scalar subquery
⏳ Abhi jo important topics baki hain
Multiple-row subquery
IN with subquery
EXISTS / NOT EXISTS
ANY / ALL
Correlated subquery
Subquery vs JOIN
UNION / UNION ALL properly
Constraints
ALTER TABLE
Database relationships
Normalization
Views
Indexes
Transactions + ACID
CTE
Window Functions
Advanced SQL
Interview SQL problems
Final SQL problem solving

Toh abhi ka next major section = Subqueries.

🚀 SQL — Lecture 30
Subquery Part 2 — Multiple-Row Subquery + IN

Pichhle lecture me humne dekha tha:

SELECT student_name
FROM students
WHERE age = (
    SELECT MAX(age)
    FROM students
);

Yahan inner query ne sirf ek value di:

23

Isliye humne = use kiya.

Aaj problem ulta hai.

1. Multiple-row subquery kya hota hai?

Suppose hum ye query chalate hain:

SELECT age
FROM students;

Output kuch aisa hoga:

20
21
22
19
20
21
23
20
22

Ab dekho:

Inner query ne ek value nahi, multiple values return ki hain.

Isko hum multiple-row subquery bolte hain.

2. Problem kya hogi?

Maan lo question hai:

CSE ya ECE department ke students find karo.

Departments table:

id    department
1     CSE
2     ECE
3     Mechanical
4     Civil
5     Electrical

Students me:

student_id   name     department_id
101          Rahul       1
102          Aman        2
103          Rohit       1
104          Priya       3
105          Neha        2
106          Karan       1
...

Ab hum pehle departments ki IDs nikal sakte hain:

SELECT department_id
FROM departments
WHERE department_name IN ('CSE', 'ECE');

Result:

1
2

Ab hume students me department_id 1 ya 2 wale chahiye.

Yahan ek saath multiple values hain.

3. Yahin IN kaam aata hai

Query:

SELECT student_name, department_id
FROM students
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE department_name IN ('CSE', 'ECE')
);

Isko slowly samjho.

Inner query:
SELECT department_id
FROM departments
WHERE department_name IN ('CSE', 'ECE');

Result:

1
2

Ab outer query conceptually ban gayi:

SELECT student_name, department_id
FROM students
WHERE department_id IN (1, 2);

Ab SQL check karega:

Rahul   1 → IN (1,2) ✅
Aman    2 → IN (1,2) ✅
Rohit   1 → IN (1,2) ✅
Priya   3 → IN (1,2) ❌
Neha    2 → IN (1,2) ✅
Karan   1 → IN (1,2) ✅

🔥 Bas yahi multiple-row subquery ka core idea hai.

4. = vs IN

Ye bahut important hai.

=

Ek value ke liye:

WHERE age = (
    SELECT MAX(age)
    FROM students
);

Inner query:

23

Single value.

IN

Multiple values ke liye:

WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE department_name IN ('CSE', 'ECE')
);

Inner query:

1
2

Multiple values.

Yaad rakho:
Single value
     ↓
     =

Multiple values
     ↓
     IN
5. Practical — MySQL Workbench

Ab actual me run karo.

Step 1

MySQL Workbench open karo.

Step 2

Wahi connection open karo jisme students aur departments tables hain.

Step 3

Pehle sirf inner query run karo:

SELECT department_id
FROM departments
WHERE department_name IN ('CSE', 'ECE');
Expected output:
1
2

Agar ye sahi aa gaya, tab next query run karo:

SELECT student_name, department_id
FROM students
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE department_name IN ('CSE', 'ECE')
);
6. NOT IN bhi same logic

Agar question ho:

CSE aur ECE ko chhodkar baaki students dikhao.

SELECT student_name, department_id
FROM students
WHERE department_id NOT IN (
    SELECT department_id
    FROM departments
    WHERE department_name IN ('CSE', 'ECE')
);

Inner query:

1
2

Outer condition:

department_id NOT IN (1,2)

So:

3
4
5

wale departments ke students milenge.

7. Ek aur example

Question:

Un employees ko find karo jo un departments me hain jinka location Delhi hai.

Suppose departments:

id   department   location
1    CSE          Delhi
2    ECE          Mumbai
3    HR           Delhi
4    Sales        Pune

Inner query:

SELECT id
FROM departments
WHERE location = 'Delhi';

Result:

1
3

Outer:

SELECT employee_name
FROM employees
WHERE department_id IN (
    SELECT id
    FROM departments
    WHERE location = 'Delhi'
);

Conceptually:

WHERE department_id IN (1,3)
8. Multiple-row ka matlab hamesha multiple columns nahi hota

Important distinction:

Multiple rows
1
2
3
4

Ye multiple rows hain, but one column.

Multiple columns
1 CSE
2 ECE
3 HR

Ye multiple columns hain.

Aaj hum mainly multiple rows + one column wali subquery samajh rahe hain.

9. Common mistake ❌

Aisi query:

SELECT student_name
FROM students
WHERE department_id = (
    SELECT department_id
    FROM departments
);

Problem:

Inner query multiple rows return karegi:

1
2
3
4
5

Lekin = ko single value chahiye.

Is situation me:

IN

use karna appropriate hai:

SELECT student_name
FROM students
WHERE department_id IN (
    SELECT department_id
    FROM departments
);
🧠 Quick Revision
Scalar / single-value subquery
WHERE age = (
    SELECT MAX(age)
    FROM students
);

Result:

23
Multiple-row subquery
WHERE department_id IN (
    SELECT department_id
    FROM departments
);

Result:

1
2
3
4
5
Golden Rule
Subquery → 1 value
       ↓
       =

Subquery → multiple values
       ↓
       IN
📝 Practice
Q1

students table se un students ka naam nikalo jo CSE ya ECE department me hain, using a subquery.

Q2

departments table se department_id nikalo jinke department ka naam Mechanical ya Civil hai. Phir subquery use karke un departments ke students nikalo.

Q3

Un students ko find karo jo CSE department me nahi hain, using a subquery.

✅ Solutions
Q1
SELECT student_name
FROM students
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE department_name IN ('CSE', 'ECE')
);
Q2
SELECT student_name
FROM students
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE department_name IN ('Mechanical', 'Civil')
);
Q3
SELECT student_name
FROM students
WHERE department_id NOT IN (
    SELECT department_id
    FROM departments
    WHERE department_name = 'CSE'
);
🎯 Interview Point

Q: = aur IN subquery me kab use karte hain?

Answer:

= generally tab use karte hain jab subquery single value return kare.

IN tab use karte hain jab subquery multiple values return kar sakti hai.

Example:

-- Single value
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
);
-- Multiple values
WHERE department_id IN (
    SELECT id
    FROM departments
    WHERE location = 'Delhi'
);
🔜 Next

Lecture 31 — EXISTS & NOT EXISTS

Isme ek naya logic aayega:

"Mujhe actual value nahi chahiye, mujhe bas ye check karna hai ki matching record EXISTS karta hai ya nahi."

Ye interviews me kaafi important hai.  

