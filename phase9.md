🚀 SQL — Lecture 31
EXISTS & NOT EXISTS

Pichhle lecture me humne seekha tha:

IN (subquery)

ka use tab hota hai jab hume subquery se aane wali values ke basis par rows filter karni hoti hain.

Aaj ka concept thoda different hai.

EXISTS ka simple meaning hai:

"Kya aisa koi matching record exist karta hai?"

Aur NOT EXISTS:

"Kya aisa koi matching record exist nahi karta?"

1. Sabse pehle EXISTS ko simple language me samjho

Maan lo hamare paas:

students
student_id	student_name	department_id
101	Rahul	1
102	Aman	2
103	Rohit	1
104	Priya	3
105	Neha	2
106	Karan	1
departments
department_id	department_name
1	CSE
2	ECE
3	Mechanical

Ab question:

Aise departments find karo jisme kam se kam ek student hai.

Hume student ka naam nahi chahiye.

Hume student ki ID bhi nahi chahiye.

Hume bas check karna hai:

Kya is department ka koi student exist karta hai?

Yahi kaam EXISTS karta hai.

2. Basic syntax
SELECT ...
FROM table1
WHERE EXISTS (
    SELECT ...
    FROM table2
    WHERE condition
);

Dhyan do:

EXISTS ke andar wali query ka actual data/value important nahi hota.

Important hai:

Kuch matching record mila? 
        ↓
       YES → TRUE
       NO  → FALSE
3. Pehla practical example

Question:

Un departments ko find karo jisme students exist karte hain.

SELECT d.department_id, d.department_name
FROM departments d
WHERE EXISTS (
    SELECT 1
    FROM students s
    WHERE s.department_id = d.department_id
);

Ab isko ekdum line-by-line samjho.

Outer query
SELECT d.department_id, d.department_name
FROM departments d

Hum departments table se departments nikal rahe hain.

d ek alias hai.

Matlab:

departments → d
Ab EXISTS
WHERE EXISTS (

Matlab:

Har department ke liye check karo ki andar wali query koi matching student find kar pa rahi hai ya nahi.

Inner query
SELECT 1
FROM students s
WHERE s.department_id = d.department_id

Yahan:

students → s
departments → d

Aur condition:

s.department_id = d.department_id

Matlab:

Student ka department_id aur current department ka department_id same hai kya?

4. Dry Run 🔥

Ab departments ko ek-ek karke check karte hain.

Department 1 — CSE
CSE ka id = 1

Students me check:

Rahul → department_id = 1 ✅
Rohit → department_id = 1 ✅
Karan → department_id = 1 ✅

Student mil gaya.

So:

EXISTS = TRUE

CSE output me aayega.

Department 2 — ECE

Students me:

Aman → 2 ✅
Neha → 2 ✅

Match mil gaya.

EXISTS = TRUE

ECE output me aayega.

Department 3 — Mechanical

Students me:

Priya → 3 ✅

Match mil gaya.

EXISTS = TRUE

Mechanical bhi output me aayega.

5. SELECT 1 kyun likha?

Ye bahut common question hai.

Humne likha:

SELECT 1

EXISTS ko actual value se matlab nahi hai.

Usko bas ye pata karna hai:

record mila? YES / NO

Isliye ye bhi technically kaam kar sakta hai:

SELECT *

ya:

SELECT s.student_id

Lekin conventionally:

SELECT 1

likha jata hai because hume actual column/value chahiye hi nahi.

Yaad rakho:
EXISTS → existence check
6. IN vs EXISTS

Ye bahut important difference hai.

IN

Pehle subquery values return karti hai:

SELECT department_id
FROM students;

Suppose:

1
2
1
3
2
1

Outer query un values ke basis par comparison karti hai.

EXISTS

EXISTS ko values ki list nahi chahiye.

Wo bas poochta hai:

"Kya matching row hai?"
Simple difference:
IN
↓
Values ke saath comparison

EXISTS
↓
Matching row exist karti hai ya nahi
7. NOT EXISTS

Ab iska opposite.

NOT EXISTS ka meaning:

Matching record exist nahi karta.

Example:

Aise departments find karo jisme koi student nahi hai.

SELECT d.department_id, d.department_name
FROM departments d
WHERE NOT EXISTS (
    SELECT 1
    FROM students s
    WHERE s.department_id = d.department_id
);

Logic:

Department
     ↓
Student matching hai?
     ↓
YES → NOT EXISTS = FALSE ❌
NO  → NOT EXISTS = TRUE ✅
8. Real-life example

Socho:

Departments = classrooms
Students = students sitting in classroom

Question:

Kaunse classrooms me koi student hai?

EXISTS

Question:

Kaunse classrooms completely empty hain?

NOT EXISTS

Bas itna simple hai.

9. Practical MySQL Workbench

Ab actual query run karte hain.

Step 1

MySQL Workbench open karo.

Step 2

Wahi existing connection open karo.

Step 3

Ye query run karo:

SELECT d.department_id, d.department_name
FROM departments d
WHERE EXISTS (
    SELECT 1
    FROM students s
    WHERE s.department_id = d.department_id
);

Expected result me wahi departments aayenge jinke students hain.

10. NOT EXISTS practical

Ab run karo:

SELECT d.department_id, d.department_name
FROM departments d
WHERE NOT EXISTS (
    SELECT 1
    FROM students s
    WHERE s.department_id = d.department_id
);

Agar kisi department ka koi student nahi hai, wo output me aayega.

11. Ek aur important example

Question:

Un students ko find karo jinke department ka record departments table me exist karta hai.

SELECT s.student_name
FROM students s
WHERE EXISTS (
    SELECT 1
    FROM departments d
    WHERE d.department_id = s.department_id
);

Logic:

Rahul ka department_id = 1
             ↓
departments me 1 exist?
             ↓
YES
             ↓
Rahul output

Aman:

2
↓
2 exist?
↓
YES
↓
Aman output
12. EXISTS correlated kyun hai?

Ab ek important term:

Correlated Subquery

Pichhle examples me inner query outer query ki value use kar rahi hai.

Example:

WHERE s.department_id = d.department_id

Yahan d.department_id outer query se aa raha hai.

Isliye inner query outer query par depend kar rahi hai.

Isko:

Correlated Subquery

kehte hain.

Conceptually:

Outer row
   ↓
Inner query
   ↓
Check
   ↓
Next outer row
   ↓
Inner query again

Isliye EXISTS ke saath correlated subqueries bahut commonly milti hain.

13. EXISTS ka sabse important point

EXISTS ko ye matter nahi karta ki inner query:

1

return kare,

ya:

100

return kare,

ya:

Rahul

return kare.

Usko bas ye matter karta hai:

At least one row exists?
YES
TRUE
NO
FALSE
14. Common mistake ❌

Beginners kabhi-kabhi aisa sochte hain:

WHERE EXISTS (
    SELECT department_id
    FROM departments
);

Matlab saare departments exist hain, isliye ye condition generally har outer row ke liye true ho sakti hai.

EXISTS me correlation condition bahut important hoti hai jab hume matching records check karne hain.

Correct pattern:

WHERE EXISTS (
    SELECT 1
    FROM departments d
    WHERE d.department_id = s.department_id
);
🧠 Quick Revision
EXISTS

Matching record exists karta hai ya nahi?

WHERE EXISTS (
    SELECT 1
    FROM ...
    WHERE ...
);
NOT EXISTS

Matching record exist nahi karta?

WHERE NOT EXISTS (
    SELECT 1
    FROM ...
    WHERE ...
);
Most important idea:
EXISTS
↓
At least ONE matching row?
↓
YES → TRUE
NO  → FALSE
📝 Practice
Q1

departments table se un departments ko find karo jinke andar at least one student hai using EXISTS.

Q2

departments table se un departments ko find karo jinke andar koi student nahi hai using NOT EXISTS.

Q3

Un students ko find karo jinka department_id departments table me exist karta hai.

Q4

Un students ko find karo jinka department record departments table me exist nahi karta.

✅ Solutions
Q1
SELECT d.department_id, d.department_name
FROM departments d
WHERE EXISTS (
    SELECT 1
    FROM students s
    WHERE s.department_id = d.department_id
);
Q2
SELECT d.department_id, d.department_name
FROM departments d
WHERE NOT EXISTS (
    SELECT 1
    FROM students s
    WHERE s.department_id = d.department_id
);
Q3
SELECT s.student_id, s.student_name
FROM students s
WHERE EXISTS (
    SELECT 1
    FROM departments d
    WHERE d.department_id = s.department_id
);
Q4
SELECT s.student_id, s.student_name
FROM students s
WHERE NOT EXISTS (
    SELECT 1
    FROM departments d
    WHERE d.department_id = s.department_id
);
🎯 Interview Questions
Q1. What is EXISTS?

EXISTS checks whether the subquery returns at least one row.

Q2. What is NOT EXISTS?

NOT EXISTS checks whether the subquery returns no rows.

Q3. Does EXISTS care about the actual value returned?

No. It mainly checks whether at least one row exists.

Q4. What is a correlated subquery?

A subquery that references a column/value from the outer query.

🔥 Aaj ka concept ek line me
IN       → "Kya ye value is list me hai?"

EXISTS   → "Kya matching row exist karti hai?"

NOT EXISTS → "Kya matching row exist nahi karti?"

Next Lecture: ANY, ALL + IN vs EXISTS ko properly compare karenge, phir correlated subquery ko aur deeply practice karenge.

🚀 SQL — Lecture 32
ANY / ALL + IN vs EXISTS

Pichhle 2 lectures me humne ye samjha:

Single-value subquery
Multiple-row subquery
IN
NOT IN
EXISTS
NOT EXISTS
Correlated subquery ka basic idea

Aaj hum ANY aur ALL samjhenge. Ye initially thoda confusing lagta hai, isliye ekdum basic se karenge.

1. Sabse pehle ANY kya hai?

ANY ka simple meaning:

"Kya condition kam se kam ek value ke saath TRUE hai?"

Yaad rakhne ka shortcut:

ANY = At least ONE

Matlab agar subquery se multiple values aayi:

10
20
30

aur hum likhte hain:

salary > ANY (...)

to SQL check karega:

Kya salary 10 se greater hai?
Ya 20 se greater hai?
Ya 30 se greater hai?

Agar ek bhi comparison TRUE ho gaya → condition TRUE.

2. Ekdum simple example

Suppose subquery result:

10
20
30

Aur:

50 > ANY (10, 20, 30)

Check:

50 > 10  ✅
50 > 20  ✅
50 > 30  ✅

At least one TRUE hai.

Therefore:

ANY = TRUE
Ab doosra:
15 > ANY (10, 20, 30)

Check:

15 > 10  ✅
15 > 20  ❌
15 > 30  ❌

Ek TRUE mil gaya.

Therefore:

ANY = TRUE

🔥 ANY ko sab conditions TRUE nahi chahiye. Bas ek TRUE chahiye.

3. ALL kya hai?

ALL ka meaning:

"Kya condition subquery ki ALL values ke saath TRUE hai?"

Shortcut:

ALL = Every single one

Suppose:

10
20
30
Example:
50 > ALL (10,20,30)

Check:

50 > 10  ✅
50 > 20  ✅
50 > 30  ✅

Sab TRUE.

Therefore:

ALL = TRUE
But:
25 > ALL (10,20,30)

Check:

25 > 10  ✅
25 > 20  ✅
25 > 30  ❌

Ek FALSE aa gaya.

Therefore:

ALL = FALSE
4. ANY vs ALL — sabse important

Ye table yaad rakhna:

Keyword	Meaning
ANY	At least ONE condition true
ALL	EVERY condition true

Shortcut:

ANY → ek bhi chalega ✅

ALL → sab hona chahiye ✅
5. Ab SQL me actual example

Maan lo employees:

employee	salary
Rahul	30000
Aman	40000
Rohit	50000
Priya	60000

Question:

Aise employees find karo jinki salary kisi bhi employee ki salary se zyada hai.

Query:

SELECT employee_name, salary
FROM employees
WHERE salary > ANY (
    SELECT salary
    FROM employees
);

Inner query:

SELECT salary
FROM employees;

Result:

30000
40000
50000
60000

Ab suppose Rahul:

30000 > ANY (30000,40000,50000,60000)

Check:

30000 > 30000 ❌
30000 > 40000 ❌
30000 > 50000 ❌
30000 > 60000 ❌

No TRUE.

Rahul ❌

Aman:

40000 > 30000 ✅

Bas ek TRUE mil gaya.

Aman ✅

Rohit:

50000 > 30000 ✅

Rohit ✅

Priya:

60000 > 30000 ✅

Priya ✅

So output:

Aman
Rohit
Priya
6. ALL example

Question:

Aise employees find karo jinki salary sab employees ki salary se zyada hai.

SELECT employee_name, salary
FROM employees
WHERE salary > ALL (
    SELECT salary
    FROM employees
);

Ab:

Rahul
30000 > ALL (30000,40000,50000,60000)

❌

Aman
40000 > 30000 ✅
40000 > 40000 ❌

So ❌

Rohit
50000 > 60000 ❌

So ❌

Priya
60000 > 30000 ✅
60000 > 40000 ✅
60000 > 50000 ✅
60000 > 60000 ❌

So ❌

Koi result nahi aayega, kyunki koi salary apni khud ki salary se greater nahi ho sakti.

Ye example hume ek important point dikhata hai:

Comparison carefully samajhna zaroori hai.

7. Better ALL example

Suppose hum question change karte hain:

Aise employees find karo jinki salary baaki given salaries se greater hai.

Agar subquery me:

30000
40000
50000

hai, then:

SELECT employee_name, salary
FROM employees
WHERE salary > ALL (
    SELECT salary
    FROM employees
    WHERE salary < 60000
);

Inner result:

30000
40000
50000

Ab:

60000 > 30000 ✅
60000 > 40000 ✅
60000 > 50000 ✅

So Priya qualify karegi.

8. ANY ko MIN() se relate karo

Ye interview trick hai. 👀

Suppose:

10
20
30

Condition:

X > ANY (10,20,30)

Actually logically iska relation minimum se hai.

Minimum:

10

Agar:

X > 10

true hai, to X > ANY(...) true ho sakta hai.

So:

X > ANY(values)
≈
X > MIN(values)
9. ALL ko MAX() se relate karo

Similarly:

X > ALL (10,20,30)

ka relation maximum se hai.

Maximum:

30

Agar:

X > 30

true hai, to X sab values se greater hoga.

So:

X > ALL(values)
≈
X > MAX(values)

⚠️ Ye conceptual understanding hai. Interview me exact query ko blindly replace mat karna; NULLs aur operators ki wajah se behavior details matter kar sakti hain.

10. Different operators ke saath ANY

ANY sirf > ke saath nahi hota.

Examples:

salary > ANY (...)
salary < ANY (...)
salary >= ANY (...)
salary <= ANY (...)
salary = ANY (...)
11. = ANY ko dhyan se dekho

= ANY practically IN jaisa behave karta hai.

Example:

WHERE department_id = ANY (
    SELECT department_id
    FROM departments
    WHERE department_name IN ('CSE','ECE')
);

Inner result:

1
2

So:

department_id = ANY (1,2)

means:

department_id = 1
OR
department_id = 2

Which is essentially:

WHERE department_id IN (1,2)
Interview point:
= ANY
≈
IN
12. IN vs ANY
IN
WHERE department_id IN (
    SELECT department_id
    FROM departments
);

Mainly membership check:

"Kya value in returned values me hai?"

ANY
WHERE salary > ANY (
    SELECT salary
    FROM employees
);

Comparison:

"Kya comparison at least ek returned value ke against TRUE hai?"

13. ANY vs EXISTS

Ye bhi important.

EXISTS
Matching row exist karti hai?
ANY
Comparison at least ek returned value ke saath TRUE hai?

Example:

EXISTS → "Koi student hai?"

ANY → "Kya salary kisi ek salary se greater hai?"
14. Practical — MySQL Workbench

Ab actual practice karte hain.

Step 1

MySQL Workbench open karo.

Step 2

Wahi connection open karo.

Step 3

Agar employees table abhi nahi bana hai, to practice ke liye ye run karo:

CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(50),
    salary INT
);
Step 4

Data insert karo:

INSERT INTO employees
(employee_id, employee_name, salary)
VALUES
(1, 'Rahul', 30000),
(2, 'Aman', 40000),
(3, 'Rohit', 50000),
(4, 'Priya', 60000);
Step 5

Check:

SELECT * FROM employees;
15. ANY practice query

Run:

SELECT employee_name, salary
FROM employees
WHERE salary > ANY (
    SELECT salary
    FROM employees
);

Think karo:

Kaunsi salaries at least ek salary se greater hain?

16. ALL practice

Ab:

SELECT employee_name, salary
FROM employees
WHERE salary >= ALL (
    SELECT salary
    FROM employees
);

Ab >= use kiya hai.

So highest salary kya hogi?

60000

Priya qualify karegi.

🔥 Ye example bahut important hai:

salary >= ALL(salaries)

essentially highest salary identify karne ka ek tareeka ho sakta hai.

17. ANY ka ek aur example

Question:

Employees find karo jinki salary 40000 ya kisi returned salary se greater hai.

Simple practice ke liye:

SELECT employee_name, salary
FROM employees
WHERE salary > ANY (
    SELECT salary
    FROM employees
    WHERE salary >= 40000
);

Inner query:

40000
50000
60000

Now:

salary > ANY(40000,50000,60000)

At least one comparison TRUE hona chahiye.

⚠️ Common confusion

Ye mat sochna:

ANY = sab

❌ Wrong.

ANY = at least one
ALL = every one

Ye distinction bahut important hai.

🧠 Super Quick Revision
ANY
↓
At least ONE comparison TRUE
ALL
↓
EVERY comparison TRUE
Example:

Values:

10, 20, 30
50 > ANY(10,20,30)

✅ TRUE

because 50 > 10.

But:

50 > ALL(10,20,30)

✅ TRUE

because 50 is greater than all.

Now:

25 > ANY(10,20,30)

✅ TRUE

because 25 > 10.

But:

25 > ALL(10,20,30)

❌ FALSE

because 25 > 30 is false.

📝 Practice — Pehle Khud Solve Karna
Q1

employees table se un employees ko find karo jinki salary at least one employee ki salary se greater hai using ANY.

Q2

Un employees ko find karo jinki salary sab employees ki salary se greater ya equal hai using ALL.

Q3

students table se un students ko find karo jinka department_id returned department IDs me se kisi ek ke equal hai using ANY.

Q4

IN aur = ANY ka difference/example likho.

✅ Solutions
Q1
SELECT employee_name, salary
FROM employees
WHERE salary > ANY (
    SELECT salary
    FROM employees
);
Q2
SELECT employee_name, salary
FROM employees
WHERE salary >= ALL (
    SELECT salary
    FROM employees
);
Q3
SELECT student_name, department_id
FROM students
WHERE department_id = ANY (
    SELECT department_id
    FROM departments
);
Q4

IN:

WHERE department_id IN (
    SELECT department_id
    FROM departments
);

Equivalent idea:

WHERE department_id = ANY (
    SELECT department_id
    FROM departments
);
🎯 Interview Questions
Q1. What does ANY mean?

ANY means the comparison must be true for at least one value returned by the subquery.

Q2. What does ALL mean?

ALL means the comparison must be true for every value returned by the subquery.

Q3. = ANY is similar to what?
= ANY
≈
IN
Q4. > ALL conceptually relates to which aggregate?
> ALL(values)
≈
> MAX(values)
Q5. > ANY conceptually relates to which aggregate?
> ANY(values)
≈
> MIN(values)
🔥 Aaj ka final picture

Ab tak Subqueries me:

SUBQUERY
│
├── Single-value
│      └── =, >, < ...
│
├── Multiple-row
│      └── IN / NOT IN
│
├── EXISTS
│
├── NOT EXISTS
│
├── ANY
│
└── ALL

Aur next hum Correlated Subquery ko properly deep-dive karenge — kyunki ab tak humne uska naam aur basic idea dekha hai, lekin actual execution ko outer row → inner query → result ke through properly practice karna baki ha