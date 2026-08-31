🚀 SQL — PHASE 12
Chapter: Constraints & Keys
Lecture 36: SQL Constraints — Complete Foundation

Haan bhai 😄 Phase 12 start karte hain.
Aaj se hum Constraints & Keys start karenge. Is phase me theory ke saath actual table bana ke practice bhi karenge.

📊 SQL ROADMAP
Overall SQL Progress: ~72% 🟢
Phase 12 — Constraints & Keys

Aaj:

Constraints kya hote hain
PRIMARY KEY
NOT NULL
UNIQUE
DEFAULT
CHECK

Aage isi Phase 12 me:

FOREIGN KEY
Primary Key vs Foreign Key
Referential Integrity
ON DELETE
ON UPDATE
Multiple constraints together
Practical database design
Interview questions
Final practice
1. Constraint kya hota hai?

Sabse pehle simple language me:

Constraint ek rule hota hai jo database ke data par lagaya jata hai.

Example:

Agar hum chahte hain ki student ka student_id duplicate na ho:

student_id INT PRIMARY KEY

Database automatically ensure karega ki:

1
2
3

allowed hai.

Lekin:

1
2
2

❌ allowed nahi hoga.

2. Constraints ki zarurat kyun?

Suppose humne table banaya:

CREATE TABLE students (
    student_id INT,
    name VARCHAR(50),
    age INT
);

Ab koi bhi ye insert kar sakta hai:

INSERT INTO students VALUES
(NULL, NULL, -500);

😵 Data kharab ho gaya.

Constraints lagakar hum database ko bolte hain:

ID empty nahi hona chahiye
Name empty nahi hona chahiye
ID duplicate nahi hona chahiye
Age valid range me honi chahiye
3. Main SQL Constraints
CONSTRAINTS
│
├── PRIMARY KEY
├── FOREIGN KEY
├── NOT NULL
├── UNIQUE
├── DEFAULT
└── CHECK

In sabko properly samajhna hai.

4. PRIMARY KEY 🔥
Definition

Primary Key ek column ya columns ka combination hota hai jo table ki har row ko uniquely identify karta hai.

Example:

student_id INT PRIMARY KEY

Student ID:

1 → Rahul
2 → Aman
3 → Rohit

Har student ka ID unique hai.

5. Primary Key ke 2 main rules

Primary Key:

1. Duplicate nahi ho sakti
1
2
3

✅

But:

1
2
2

❌

2. NULL nahi ho sakti
NULL

❌

So remember:

PRIMARY KEY
=
UNIQUE + NOT NULL

Conceptually ye sabse important shortcut hai.

6. Example
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50)
);

Valid:

INSERT INTO students VALUES
(1, 'Rahul');

INSERT INTO students VALUES
(2, 'Aman');

Invalid:

INSERT INTO students VALUES
(1, 'Rohit');

❌ Because 1 already exists.

7. NULL Primary Key
INSERT INTO students VALUES
(NULL, 'Rohit');

❌ Error.

Because Primary Key cannot be NULL.

8. NOT NULL

Definition:

NOT NULL ensure karta hai ki column me NULL value store na ho.

Example:

student_name VARCHAR(50) NOT NULL

Table:

CREATE TABLE students (
    student_id INT,
    student_name VARCHAR(50) NOT NULL
);

Valid:

INSERT INTO students
VALUES (1, 'Rahul');

Invalid:

INSERT INTO students
VALUES (2, NULL);

❌

9. NOT NULL vs PRIMARY KEY

Important difference:

Primary Key
Unique
+
Not NULL
NOT NULL

Sirf:

NULL allowed nahi

Duplicate allowed ho sakte hain.

Example:

email VARCHAR(100) NOT NULL

Ye guarantee karta hai email NULL nahi hoga.

Lekin duplicate emails ko ye automatically prevent nahi karta.

10. UNIQUE

Definition:

UNIQUE constraint column ki values ko duplicate hone se rokta hai.

Example:

email VARCHAR(100) UNIQUE

Data:

rahul@gmail.com
aman@gmail.com

✅

But:

rahul@gmail.com
rahul@gmail.com

❌

11. UNIQUE vs PRIMARY KEY 🔥
PRIMARY KEY	UNIQUE
Unique values	Unique values
NULL allowed nahi	NULL handling DBMS-specific ho sakti hai; MySQL me UNIQUE column multiple NULLs allow kar sakta hai
Table me generally one primary key	Multiple UNIQUE constraints ho sakte hain
Row identification ke liye	Duplicate prevention ke liye

Example:

CREATE TABLE students (
    student_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);

Yahan:

student_id → Primary Key
email      → Unique
12. DEFAULT

Definition:

Agar INSERT ke waqt value nahi di gayi, to DEFAULT value automatically use ho sakti hai.

Example:

status VARCHAR(20) DEFAULT 'Active'

Table:

CREATE TABLE students (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50),
    status VARCHAR(20) DEFAULT 'Active'
);

Ab:

INSERT INTO students
(student_id, student_name)
VALUES
(1, 'Rahul');

Humne status nahi diya.

Database:

status = Active

automatically use karega.

13. Another DEFAULT Example
city VARCHAR(50) DEFAULT 'Delhi'

Agar city nahi di:

Delhi

automatically aa sakti hai.

14. CHECK 🔥

Definition:

CHECK constraint kisi condition ko enforce karta hai.

Example:

age INT CHECK (age >= 18)

Meaning:

Age >= 18 hona chahiye.

Valid:

18
20
25

Invalid:

17
10
-5
15. Example
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50) NOT NULL,
    age INT CHECK (age >= 18)
);

Valid:

INSERT INTO students
VALUES (1, 'Rahul', 20);

❌ Invalid:

INSERT INTO students
VALUES (2, 'Aman', 15);

Because:

15 >= 18

False.

16. Multiple CHECK conditions

Example:

age INT CHECK (age >= 18 AND age <= 60)

Meaning:

18 ≤ age ≤ 60
17. Ab sabko ek table me dekho 🔥
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    age INT CHECK (age >= 18),
    status VARCHAR(20) DEFAULT 'Active'
);

Ab database ke rules:

student_id
→ Unique + Not NULL

student_name
→ Not NULL

email
→ Duplicate nahi

age
→ 18 ya usse zyada

status
→ Agar value nahi di → Active
🧪 AB PRACTICAL KARTE HAIN

Tum MySQL Workbench use kar rahe ho, to wahi pe practice karenge.

Step 1 — New SQL Tab

MySQL Workbench open karo.

Top me:

File
Edit
View
Query
...

Uske neeche SQL + / New SQL Tab type option hota hai.

Uspe click karo.

Step 2 — Ye database select karo

Jo database tum practice ke liye use kar rahe ho usko select karo.

Agar sql_practice database hai:

USE sql_practice;

Run karo.

Step 3 — Practice table banao
CREATE TABLE student_constraints (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    age INT CHECK (age >= 18),
    status VARCHAR(20) DEFAULT 'Active'
);

Run karo.

18. Table check karo
DESC student_constraints;

Run karo.

Tumhe columns ke saamne constraints ke related information dikhegi.

19. Valid Data Insert karo
INSERT INTO student_constraints
(student_id, student_name, email, age)
VALUES
(1, 'Rahul', 'rahul@gmail.com', 21);

Run.

Then:

SELECT *
FROM student_constraints;

Expected:

student_id	student_name	email	age	status
1	Rahul	rahul@gmail.com	21	Active

Notice:

Humne status nahi diya.

But:

Active

automatically aa gaya.

🔥 That's DEFAULT.

20. PRIMARY KEY Test

Ab:

INSERT INTO student_constraints
(student_id, student_name, email, age)
VALUES
(1, 'Aman', 'aman@gmail.com', 22);

Run karo.

❌ Error aayega.

Reason:

student_id = 1

already exists.

21. NOT NULL Test
INSERT INTO student_constraints
(student_id, student_name, email, age)
VALUES
(2, NULL, 'aman@gmail.com', 22);

❌ Error.

Because:

student_name → NOT NULL
22. UNIQUE Test
INSERT INTO student_constraints
(student_id, student_name, email, age)
VALUES
(2, 'Aman', 'rahul@gmail.com', 22);

❌ Error.

Because Rahul ka email already exists.

23. CHECK Test
INSERT INTO student_constraints
(student_id, student_name, email, age)
VALUES
(2, 'Aman', 'aman@gmail.com', 15);

❌ Error.

Because:

age >= 18

condition fail.

24. DEFAULT Test

Ab correct data:

INSERT INTO student_constraints
(student_id, student_name, email, age)
VALUES
(2, 'Aman', 'aman@gmail.com', 22);

Then:

SELECT *
FROM student_constraints;

Result:

student_id	student_name	email	age	status
1	Rahul	rahul@gmail.com	21	Active
2	Aman	aman@gmail.com	22	Active
🧠 Ab ekdum simple memory trick
PRIMARY KEY
→ Row ki identity

NOT NULL
→ Khali nahi

UNIQUE
→ Duplicate nahi

DEFAULT
→ Value na do → default value

CHECK
→ Condition follow karo
🎯 Interview Definitions
1. What is a Constraint?

A constraint is a rule enforced on table data to maintain accuracy and integrity.

2. What is Primary Key?

A primary key uniquely identifies each row in a table and cannot contain NULL values.

3. Can a table have multiple Primary Keys?

No. A table can have only one primary key constraint, although that key can consist of multiple columns (composite primary key).

4. Can a table have multiple UNIQUE constraints?

Yes.

5. Difference between PRIMARY KEY and UNIQUE?
PRIMARY KEY
→ unique + not null
→ one primary key constraint

UNIQUE
→ prevents duplicate values
→ multiple unique constraints possible
6. What does NOT NULL do?

Column me NULL value prevent karta hai.

7. What does DEFAULT do?

Value omit hone par default value provide karta hai.

8. What does CHECK do?

Specified condition ko enforce karta hai.

📝 Practice — Pehle Khud Karo

Ab answers turant mat dekhna 😄

Q1

Ek table employees banao jisme:

employee_id → Primary Key
employee_name → NOT NULL
email → UNIQUE
salary → CHECK salary >= 10000
status → DEFAULT 'Active'
Q2

Ek valid employee insert karo.

Q3

Duplicate employee_id insert karke dekho.

Q4

Duplicate email insert karke dekho.

Q5

Salary 5000 insert karke dekho.

Q6

Employee name NULL karke dekho.

Q7

Status omit karke insert karo aur check karo ki kya aata hai.

✅ Solutions
Q1
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    salary DECIMAL(10,2) CHECK (salary >= 10000),
    status VARCHAR(20) DEFAULT 'Active'
);
Q2
INSERT INTO employees
(employee_id, employee_name, email, salary)
VALUES
(1, 'Rahul', 'rahul@gmail.com', 25000);
Q3
INSERT INTO employees
(employee_id, employee_name, email, salary)
VALUES
(1, 'Aman', 'aman@gmail.com', 30000);

❌ Duplicate Primary Key.

Q4
INSERT INTO employees
(employee_id, employee_name, email, salary)
VALUES
(2, 'Aman', 'rahul@gmail.com', 30000);

❌ Duplicate UNIQUE value.

Q5
INSERT INTO employees
(employee_id, employee_name, email, salary)
VALUES
(2, 'Aman', 'aman@gmail.com', 5000);

❌ CHECK fail.

Q6
INSERT INTO employees
(employee_id, employee_name, email, salary)
VALUES
(2, NULL, 'aman@gmail.com', 30000);

❌ NOT NULL fail.

Q7
INSERT INTO employees
(employee_id, employee_name, email, salary)
VALUES
(2, 'Aman', 'aman@gmail.com', 30000);

Then:

SELECT *
FROM employees;

status:

Active
📌 Aaj ka Core Concept

Ek table imagine karo:

┌──────────────────────────────────────┐
│           EMPLOYEES                  │
├──────────────────────────────────────┤
│ employee_id → PRIMARY KEY            │
│ employee_name → NOT NULL             │
│ email → UNIQUE                       │
│ salary → CHECK >= 10000              │
│ status → DEFAULT 'Active'            │
└──────────────────────────────────────┘

Database khud ensure karega:

ID duplicate?       ❌
ID NULL?             ❌

Name NULL?           ❌

Email duplicate?     ❌

Salary < 10000?      ❌

Status missing?      → Active

🔥 Yahi Constraints ka actual purpose hai: database ko galat data se protect karna.

📈 PHASE 12 PROGRESS
Constraints Basics       ✅
PRIMARY KEY              ✅
NOT NULL                 ✅
UNIQUE                   ✅
DEFAULT                  ✅
CHECK                    ✅

FOREIGN KEY              ⏳
Referential Integrity    ⏳
ON DELETE                ⏳
ON UPDATE                ⏳
Composite Keys           ⏳
Final Practice           ⏳

Phase 12: ~45% complete

Overall SQL: ~73% complete 🟢

अगला Lecture:

🔥 Lecture 37 — FOREIGN KEY + Primary Key vs Foreign Key + Referential Integrity

Isme hum 2 actual tables (departments + employees) bana ke relation create karenge, taaki Foreign Key sirf definition se nahi, practically crystal clear ho.