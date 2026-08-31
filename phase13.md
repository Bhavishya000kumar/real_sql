🚀 SQL — PHASE 13
Chapter: Foreign Key & Table Relationships
Lecture 37: FOREIGN KEY — From Basic to Practical

Haan bhai, Phase 13 start 🔥
Aaj se Phase 13 me Foreign Key aur table relationships ko properly karenge.

📊 SQL ROADMAP
Overall SQL Progress: ~73% 🟢
Phase 13 — Constraints & Relationships
1. FOREIGN KEY                     ← TODAY 🔥
2. PRIMARY KEY vs FOREIGN KEY
3. Referential Integrity
4. ON DELETE
5. ON UPDATE
6. CASCADE
7. SET NULL
8. RESTRICT / NO ACTION
9. Composite Keys
10. Constraints with ALTER TABLE
11. ADD / DROP CONSTRAINT
12. Real-world table relationships
13. Complete Practice
14. Interview Questions
1. Pehle problem samjho

Maan lo hamare paas 2 tables hain.

departments
department_id	department_name
1	CSE
2	ECE
3	ME
employees
employee_id	employee_name	department_id
101	Rahul	1
102	Aman	2
103	Rohit	1

Yahan:

departments.department_id
          ↓
employees.department_id

employees ka department_id actually departments ke kisi existing department ko refer kar raha hai.

Isi relationship ko database level par enforce karne ke liye FOREIGN KEY use hoti hai.

2. FOREIGN KEY kya hoti hai?
Interview Definition 📌

A Foreign Key is a column or set of columns in one table that references a key, usually the Primary Key, in another table.

Simple language:

Foreign Key do tables ke beech relationship banati hai aur ensure karti hai ki child table ki value parent table me valid reference ho.

3. Parent aur Child Table

Ye terminology bahut important hai.

Parent Table
departments

Isme:

department_id → PRIMARY KEY
Child Table
employees

Isme:

department_id → FOREIGN KEY

Diagram:

DEPARTMENTS
   │
   │ department_id
   ↓
EMPLOYEES
   │
   └── department_id

Ya:

Parent
departments
    ↓
    ↓ FOREIGN KEY
    ↓
Child
employees
4. Actual table banate hain

Tum MySQL Workbench use kar rahe ho, to wahi practice karenge.

Step 1 — New SQL Tab

MySQL Workbench open karo.

New SQL Tab kholo.

Step 2 — Database select karo

Apna practice database select karo.

Example:

USE sql_practice;

Agar tumhara database naam kuch aur hai, wahi naam use karna.

5. Parent Table banao
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(50) NOT NULL
);

Run karo.

Ab:

departments

table create ho gayi.

6. Department data insert karo
INSERT INTO departments
(department_id, department_name)
VALUES
(1, 'CSE'),
(2, 'ECE'),
(3, 'ME');

Run.

Check:

SELECT *
FROM departments;

Output:

department_id	department_name
1	CSE
2	ECE
3	ME
7. Ab Child Table banao 🔥
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(50) NOT NULL,
    department_id INT,
    
    FOREIGN KEY (department_id)
    REFERENCES departments(department_id)
);

Dhyan se dekho:

FOREIGN KEY (department_id)
REFERENCES departments(department_id)

Meaning:

employees.department_id
          ↓
departments.department_id
8. Ye line tod ke samjho
FOREIGN KEY (department_id)

Matlab:

Is table ka department_id Foreign Key hai.

Aur:

REFERENCES departments(department_id)

Matlab:

Ye Foreign Key departments table ke department_id ko reference karegi.

So complete:

Child Table
employees
department_id
      ↓
      ↓ references
      ↓
Parent Table
departments
department_id
9. Valid Employee Insert

Ab:

INSERT INTO employees
(employee_id, employee_name, department_id)
VALUES
(101, 'Rahul', 1);

Ye valid hai.

Kyun?

Because:

employees.department_id = 1

Aur parent table me:

departments.department_id = 1

already exist karta hai.

10. Ek aur valid insert
INSERT INTO employees
(employee_id, employee_name, department_id)
VALUES
(102, 'Aman', 2);

Valid ✅

Because department 2 exists.

11. Ab IMPORTANT test 🔥

Try:

INSERT INTO employees
(employee_id, employee_name, department_id)
VALUES
(103, 'Rohit', 99);

❌ Error.

Kyun?

Employees me:

department_id = 99

but departments table me:

1
2
3

hai.

99 exist nahi karta.

Foreign Key bolti hai:

"Pehle parent table me valid department hona chahiye."

12. Foreign Key ka actual purpose

Without Foreign Key:

Employee → department_id = 99

Database shayad ye invalid reference allow kar de.

With Foreign Key:

Employee → department_id = 99
                 ↓
       Department 99 exists?
                 ↓
                NO ❌

Database invalid relationship ko prevent karta hai.

13. Isko Referential Integrity kehte hain

Ye term abhi se yaad kar lo.

Referential Integrity ensures that a foreign key value refers to a valid row in the referenced table.

Simple:

Foreign Key
      ↓
Valid Parent Reference
      ↓
Referential Integrity

Isko hum next part me aur deeply karenge.

14. NULL Foreign Key?

Important question:

Kya Foreign Key NULL ho sakti hai?

Generally haan, agar Foreign Key column par NOT NULL nahi lagaya gaya ho.

Hamare table me:

department_id INT

hai.

NOT NULL nahi hai.

So:

INSERT INTO employees
(employee_id, employee_name, department_id)
VALUES
(103, 'Rohit', NULL);

Normally allowed ho sakta hai.

Meaning:

Rohit
↓
Currently no department assigned

Foreign Key ka rule:

NULL ≠ invalid reference

NULL ka matlab ho sakta hai ki relationship value currently unknown/not assigned hai.

15. Foreign Key vs Primary Key 🔥
Primary Key	Foreign Key
Row ko uniquely identify karti hai	Dusre table ki row ko reference karti hai
Duplicate allowed nahi	Duplicate values allowed ho sakti hain
NULL allowed nahi	NULL allowed ho sakta hai, if column permits
Table me primary identity	Tables ke beech relationship
Parent side par commonly	Child side par commonly

Example:

departments
department_id → PRIMARY KEY

employees
department_id → FOREIGN KEY
16. Foreign Key duplicate ho sakti hai?

YES.

Ye bahut important hai.

Suppose:

Rahul → department 1
Aman  → department 1
Rohit → department 1

Teen employees ka:

department_id = 1

same ho sakta hai.

Kyun?

Because Foreign Key ka kaam unique identity dena nahi, relationship maintain karna hai.

17. Real-life Example

College database:

departments
1 → CSE
2 → ECE
3 → ME
students
101 → Rahul → CSE
102 → Aman  → CSE
103 → Priya → ECE

Student table me:

department_id

Foreign Key ho sakti hai.

So:

One Department
      ↓
Many Students

Isko bolte hain:

One-to-Many Relationship

Ek department ke multiple employees/students ho sakte hain.

18. Relationship diagram
departments
----------------
department_id PK
department_name
       │
       │
       │ 1
       │
       │
       │ *
employees
----------------
employee_id PK
employee_name
department_id FK

Meaning:

1 Department
      ↓
Many Employees
19. JOIN aur FOREIGN KEY ka connection

Bahut important confusion clear karo:

Foreign Key aur JOIN same cheez nahi hain.

Foreign Key:

Database relationship/rule

JOIN:

Query ke time tables ka data combine karna

Example:

Foreign Key:

FOREIGN KEY (department_id)
REFERENCES departments(department_id)

JOIN:

SELECT
    e.employee_name,
    d.department_name
FROM employees e
JOIN departments d
ON e.department_id = d.department_id;

So:

FOREIGN KEY → Relationship define/enforce
JOIN        → Data retrieve/combine

🔥 Ye interview me bahut useful distinction hai.

20. Practical JOIN

Ab run karo:

SELECT
    e.employee_id,
    e.employee_name,
    d.department_name
FROM employees e
JOIN departments d
ON e.department_id = d.department_id;

Expected:

employee_id	employee_name	department_name
101	Rahul	CSE
102	Aman	ECE
21. Foreign Key Constraint ka naam bhi de sakte hain

Instead of:

FOREIGN KEY (department_id)
REFERENCES departments(department_id)

Hum naam de sakte hain:

CONSTRAINT fk_employee_department
FOREIGN KEY (department_id)
REFERENCES departments(department_id)

Complete:

CREATE TABLE employees2 (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(50) NOT NULL,
    department_id INT,
    
    CONSTRAINT fk_employee_department
    FOREIGN KEY (department_id)
    REFERENCES departments(department_id)
);

Yahan:

fk_employee_department

Foreign Key constraint ka naam hai.

Ye later ALTER TABLE se constraint manage karne me useful hota hai.

22. Important: Parent me referenced column kya hona chahiye?

Foreign Key usually parent table ki:

PRIMARY KEY

ya appropriate:

UNIQUE key

ko reference karti hai.

Most common pattern:

Parent:
department_id → PRIMARY KEY

Child:
department_id → FOREIGN KEY
🧠 Aaj ka Golden Concept
PRIMARY KEY
      ↓
Parent table ki identity
      ↓
        referenced by
              ↓
FOREIGN KEY
      ↓
Child table ka relationship

Example:

departments
department_id PK
       ↑
       │
       │ FK
       │
employees
department_id FK
📝 Practice — Pehle Khud Karo
Q1

courses table banao:

course_id → PRIMARY KEY
course_name → NOT NULL
Q2

students2 table banao:

student_id → PRIMARY KEY
student_name → NOT NULL
course_id → FOREIGN KEY

course_id ko courses(course_id) se connect karo.

Q3

Courses me:

1 → C++
2 → Python
3 → SQL

insert karo.

Q4

Student:

101 → Rahul → course 1
102 → Aman → course 2

insert karo.

Q5

Aisa student insert karo jiska course_id = 99 ho.

Dekho kya hota hai.

✅ Solutions
Q1
CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(50) NOT NULL
);
Q2
CREATE TABLE students2 (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50) NOT NULL,
    course_id INT,

    FOREIGN KEY (course_id)
    REFERENCES courses(course_id)
);
Q3
INSERT INTO courses
VALUES
(1, 'C++'),
(2, 'Python'),
(3, 'SQL');
Q4
INSERT INTO students2
VALUES
(101, 'Rahul', 1),
(102, 'Aman', 2);
Q5
INSERT INTO students2
VALUES
(103, 'Rohit', 99);

❌ Foreign Key constraint error.

Because:

course_id = 99

parent table me exist nahi karta.

🎯 Interview Questions
1. What is a Foreign Key?

Dusre table ki key ko reference karne wala column/columns ka set.

2. Foreign Key ka main purpose?

Tables ke beech relationship maintain karna aur invalid references prevent karna.

3. Kya Foreign Key duplicate ho sakti hai?

Yes.

4. Kya Foreign Key NULL ho sakti hai?

Yes, provided column NOT NULL nahi hai aur other constraints allow karte hain.

5. Primary Key vs Foreign Key?
PK → uniquely identifies row
FK → references another table
6. Parent table kya hoti hai?

Jiski key ko child table reference karti hai.

7. Child table kya hoti hai?

Jisme Foreign Key hoti hai.

8. Foreign Key aur JOIN same hain?

No.

FK → relationship constraint
JOIN → query operation
9. Referential Integrity kya hai?

Foreign Key references valid parent rows ko maintain karna.

10. One-to-Many relationship example?
One Department
      ↓
Many Employees
📈 PHASE 13 PROGRESS
FOREIGN KEY                  ✅
PRIMARY KEY vs FOREIGN KEY   ✅
Referential Integrity        🔜
ON DELETE                    ⏳
ON UPDATE                    ⏳
CASCADE                      ⏳
SET NULL                     ⏳
RESTRICT / NO ACTION         ⏳
Composite Keys               ⏳
ALTER TABLE Constraints      ⏳
Final Practice               ⏳
Phase 13: ~15% complete
Overall SQL: ~74% 🟢

Next Lecture → Referential Integrity + ON DELETE + ON UPDATE + CASCADE.

🚀 SQL — PHASE 13.2
FOREIGN KEY — Advanced Complete Part

Haan bhai 😄 ab Phase 13.2 me jo bhi remaining tha, sab ek hi go me karte hain. Iske baad Foreign Key/Relationships wala portion properly complete ho jayega.

📊 SQL ROADMAP
Overall SQL Progress: ~74% 🟢
Phase 13.2 — Remaining Topics
✅ Referential Integrity
✅ ON DELETE
✅ ON UPDATE
✅ CASCADE
✅ SET NULL
✅ RESTRICT / NO ACTION
✅ Composite Keys
✅ ALTER TABLE
✅ ADD CONSTRAINT
✅ DROP CONSTRAINT
✅ Real-world relationships
✅ Complete Practical
✅ Practice + Solutions
✅ Interview Questions
1. Referential Integrity 🔥

Sabse pehle iska meaning crystal clear karo.

Humare paas:

Parent
departments
----------------
department_id
1
2
3
Child
employees
----------------
employee_id | department_id
101         | 1
102         | 2

Yahan employee 101 department 1 ko refer kar raha hai.

Database ko ye ensure karna hai:

Child table me jo Foreign Key value hai, uska corresponding parent record valid hona chahiye.

Isi ko Referential Integrity kehte hain.

2. Problem: Parent row delete kar di toh?

Suppose:

departments
1 → CSE
2 → ECE
3 → ME

Aur:

employees
101 → Rahul → 1
102 → Aman  → 1

Ab hum:

DELETE FROM departments
WHERE department_id = 1;

karna chahte hain.

But employees abhi bhi department 1 ko reference kar rahe hain.

To database ko decide karna padega:

Department delete hone par employees ka kya hoga?

Isi ka control:

ON DELETE

se hota hai.

3. ON DELETE

ON DELETE define karta hai:

Parent row delete hone par related child rows ke saath kya karna hai.

Main options:

ON DELETE CASCADE
ON DELETE SET NULL
ON DELETE RESTRICT
ON DELETE NO ACTION

Ab ek-ek karke.

4. ON DELETE CASCADE 🔥

Meaning:

Parent delete → automatically related child rows bhi delete.

Example:

Department 1
    ↓
Rahul
Aman
Rohit

Agar Department 1 delete:

Department 1 ❌
     ↓
Rahul ❌
Aman ❌
Rohit ❌
5. Actual SQL

Pehle table:

CREATE TABLE employees_cascade (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(50),
    department_id INT,

    FOREIGN KEY (department_id)
    REFERENCES departments(department_id)
    ON DELETE CASCADE
);

Important part:

ON DELETE CASCADE
6. Practical

Insert:

INSERT INTO employees_cascade
VALUES
(101, 'Rahul', 1),
(102, 'Aman', 1),
(103, 'Rohit', 2);

Ab:

SELECT * FROM employees_cascade;

Result:

employee_id	employee_name	department_id
101	Rahul	1
102	Aman	1
103	Rohit	2

Ab:

DELETE FROM departments
WHERE department_id = 1;

Because:

ON DELETE CASCADE

employees 101 and 102 automatically delete ho jayenge.

7. CASCADE ko simple example se yaad rakho
Parent delete
     ↓
Child automatically delete
Shortcut:

CASCADE = Parent ke action ka effect child par bhi cascade hona.

8. ON DELETE SET NULL

Meaning:

Parent delete ho jaye, lekin child row delete na ho. Foreign Key value NULL ho jaye.

Example:

Before:

Department 1
    ↓
Rahul → 1
Aman  → 1

Department 1 delete:

Department 1 ❌

Rahul → NULL
Aman  → NULL

Employees remain karenge.

9. Important condition

SET NULL use kar rahe ho to Foreign Key column ko NULL allow karna chahiye.

Correct:

department_id INT

Not:

department_id INT NOT NULL

Otherwise NULL assign nahi ho payega.

10. Example
CREATE TABLE employees_setnull (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(50),
    department_id INT,

    FOREIGN KEY (department_id)
    REFERENCES departments(department_id)
    ON DELETE SET NULL
);
11. ON DELETE RESTRICT

Meaning:

Agar child rows parent ko reference kar rahi hain, to parent ko delete mat karo.

Example:

Department 1
    ↓
Rahul → 1
Aman  → 1

Try:

DELETE FROM departments
WHERE department_id = 1;

❌ Delete reject ho jayega.

Database bolega effectively:

Is department ko delete nahi kar sakte because child records depend on it.

12. NO ACTION

Basic level par:

NO ACTION
≈ RESTRICT

Referential constraint violation hone par parent deletion/update ko allow nahi karta.

MySQL/InnoDB context me NO ACTION effectively RESTRICT ke tarah behave karta hai.

Interview ke liye:

RESTRICT / NO ACTION
→ dependent child rows hone par parent operation prevent
13. ON DELETE — One Table
Option	Parent delete	Child
CASCADE	Allowed	Automatically delete
SET NULL	Allowed	FK becomes NULL
RESTRICT	Prevented	Remains
NO ACTION	Prevented	Remains

🔥 Ye table yaad kar lo.

14. ON UPDATE 🔥

Ab same concept UPDATE ke liye.

ON UPDATE define karta hai:

Parent key value update hone par related child rows ke saath kya hoga.

Suppose:

departments

department_id
1 → CSE

Employee:

Rahul → department_id = 1

Ab parent:

UPDATE departments
SET department_id = 10
WHERE department_id = 1;

Ab question:

Rahul ka department_id kya hoga?

Ye ON UPDATE decide karega.

15. ON UPDATE CASCADE

Agar:

ON UPDATE CASCADE

hai:

Parent:
1 → 10

Child:
1 → automatically 10

Example:

Before:

departments
1 → CSE

employees
101 → Rahul → 1

After parent ID update:

departments
10 → CSE

employees
101 → Rahul → 10
16. Complete example
CREATE TABLE employees_update (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(50),
    department_id INT,

    FOREIGN KEY (department_id)
    REFERENCES departments(department_id)
    ON UPDATE CASCADE
);
17. CASCADE both DELETE + UPDATE

Real example:

CREATE TABLE employees_full (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(50),
    department_id INT,

    FOREIGN KEY (department_id)
    REFERENCES departments(department_id)
    ON DELETE CASCADE
    ON UPDATE CASCADE
);

Meaning:

Parent DELETE
      ↓
Child DELETE

Parent KEY UPDATE
      ↓
Child FK UPDATE
18. Composite Key 🔥

Ab next important concept.

Composite Key kya hoti hai?

Jab ek key multiple columns ko combine karke row ko uniquely identify karti hai, use Composite Key kehte hain.

Example:

Suppose course enrollment:

student_id
course_id

Ek student multiple courses le sakta hai.

Aur ek course me multiple students ho sakte hain.

So:

student_id + course_id

milkar unique combination banayega.

19. Example
CREATE TABLE enrollments (
    student_id INT,
    course_id INT,
    enrollment_date DATE,

    PRIMARY KEY (student_id, course_id)
);

Yahan Primary Key:

(student_id, course_id)

hai.

Dono columns milkar key hain.

20. Example samjho

Allowed:

student_id	course_id
1	101
1	102
2	101

Kyun?

Combinations unique hain:

1 + 101
1 + 102
2 + 101

But:

1 + 101
1 + 101

❌ duplicate combination.

21. Composite Foreign Key

Foreign Key bhi multiple columns ki ho sakti hai.

Example:

Parent:

CREATE TABLE course_sections (
    course_id INT,
    section_id INT,

    PRIMARY KEY (course_id, section_id)
);

Child:

CREATE TABLE section_students (
    student_id INT,
    course_id INT,
    section_id INT,

    FOREIGN KEY (course_id, section_id)
    REFERENCES course_sections(course_id, section_id)
);

Yahan:

(course_id, section_id)

together Foreign Key relationship establish kar rahe hain.

22. ALTER TABLE se Constraint add karna 🔥

Kabhi table banate waqt constraint nahi lagaya.

Baad me add karna ho:

ALTER TABLE

use karenge.

Example:

Existing table:

CREATE TABLE employees2 (
    employee_id INT,
    employee_name VARCHAR(50),
    department_id INT
);

Ab Foreign Key add karni hai:

ALTER TABLE employees2
ADD CONSTRAINT fk_emp_dept
FOREIGN KEY (department_id)
REFERENCES departments(department_id);

Done.

23. ADD CONSTRAINT ka breakdown
ALTER TABLE employees2

→ existing table modify karo.

ADD CONSTRAINT fk_emp_dept

→ new constraint add karo.

FOREIGN KEY (department_id)

→ department_id ko FK banao.

REFERENCES departments(department_id);

→ departments ke department_id ko reference karo.

24. UNIQUE constraint later add karna

Existing table:

ALTER TABLE employees2
ADD CONSTRAINT uq_employee_email
UNIQUE (email);

⚠️ Iske liye email column table me already exist karna chahiye.

25. CHECK constraint later add karna
ALTER TABLE employees2
ADD CONSTRAINT chk_salary
CHECK (salary >= 10000);

Again, salary column existing hona chahiye.

26. Constraint DROP karna

Agar constraint ka naam pata hai:

ALTER TABLE employees2
DROP CONSTRAINT fk_emp_dept;

MySQL me constraint type ke hisaab se syntax important hai.

Foreign Key specifically remove karne ke liye:

ALTER TABLE employees2
DROP FOREIGN KEY fk_emp_dept;

🔥 MySQL Workbench me Foreign Key remove karte waqt ye distinction yaad rakho.

27. Primary Key remove karna

MySQL:

ALTER TABLE employees2
DROP PRIMARY KEY;
28. UNIQUE constraint remove karna

Agar UNIQUE ko index ke form me create kiya gaya hai, MySQL me commonly:

ALTER TABLE employees2
DROP INDEX uq_employee_email;

Isliye constraint/index ka actual name check karna important hota hai.

29. Real-world Example 🔥

Let's design:

DEPARTMENT
----------------
department_id PK
department_name

        ↓

EMPLOYEE
----------------
employee_id PK
employee_name
email UNIQUE
department_id FK
salary CHECK
status DEFAULT

SQL:

CREATE TABLE department (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(50) NOT NULL
);

Then:

CREATE TABLE employee (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    department_id INT,
    salary DECIMAL(10,2) CHECK (salary >= 10000),
    status VARCHAR(20) DEFAULT 'Active',

    FOREIGN KEY (department_id)
    REFERENCES department(department_id)
    ON DELETE SET NULL
    ON UPDATE CASCADE
);

Ab ek hi table me:

PRIMARY KEY     ✅
NOT NULL        ✅
UNIQUE          ✅
CHECK           ✅
DEFAULT         ✅
FOREIGN KEY     ✅
ON DELETE       ✅
ON UPDATE       ✅

🔥 Ye actual database design jaisa pattern hai.

30. Kab CASCADE use karna chahiye?

CASCADE useful hai jab child record ka existence parent se strongly dependent ho.

Example:

Order
 ↓
Order Items

Order delete:

Order delete
    ↓
Order items bhi delete

Yahan CASCADE logical ho sakta hai.

31. Kab SET NULL?

Jab child record ko retain karna hai but parent association hata deni hai.

Example:

Employee
   ↓
Department

Department delete ho gaya, employee ko delete nahi karna.

So:

department_id → NULL

useful ho sakta hai.

32. Kab RESTRICT?

Jab parent ko delete karna hi nahi chahte agar dependent records exist karte hain.

Example:

Department
   ↓
Employees

Employees present hain:

Department delete ❌

Admin ko pehle employees ko reassign/delete karna padega.

🧠 GOLDEN TABLE
ON DELETE

CASCADE
→ Parent delete
→ Child delete

SET NULL
→ Parent delete
→ Child remains
→ FK = NULL

RESTRICT
→ Child exists
→ Parent delete blocked

NO ACTION
→ Parent operation blocked if relationship violated

And:

ON UPDATE CASCADE
→ Parent key changes
→ Child FK automatically changes
🧪 COMPLETE PRACTICAL

Ab actual practice ke liye fresh tables bana lo.

Step 1 — Parent
CREATE TABLE departments_p13 (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(50) NOT NULL
);
Step 2 — Data
INSERT INTO departments_p13
VALUES
(1, 'CSE'),
(2, 'ECE'),
(3, 'ME');
Step 3 — Child
CREATE TABLE employees_p13 (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(50) NOT NULL,
    department_id INT,

    FOREIGN KEY (department_id)
    REFERENCES departments_p13(department_id)
    ON DELETE SET NULL
    ON UPDATE CASCADE
);
Step 4 — Employees
INSERT INTO employees_p13
VALUES
(101, 'Rahul', 1),
(102, 'Aman', 1),
(103, 'Rohit', 2);
Step 5 — Check
SELECT *
FROM employees_p13;
Step 6 — UPDATE test

Run:

UPDATE departments_p13
SET department_id = 10
WHERE department_id = 1;

Then:

SELECT *
FROM employees_p13;

Because:

ON UPDATE CASCADE

employees:

Rahul → 10
Aman  → 10

automatically ho jayenge.

Step 7 — DELETE test

Run:

DELETE FROM departments_p13
WHERE department_id = 10;

Then:

SELECT *
FROM employees_p13;

Rahul aur Aman delete nahi honge.

Instead:

department_id → NULL

because:

ON DELETE SET NULL

🔥 Ab tumne ON UPDATE CASCADE + ON DELETE SET NULL actual practical me dekh liya.

📝 Practice Questions

Pehle khud solve karna. Answers neeche hain.

Q1

customers table banao:

customer_id → PK
customer_name → NOT NULL
email → UNIQUE
Q2

orders table banao:

order_id → PK
customer_id → FK

Customer delete hone par uske orders bhi automatically delete hone chahiye.

Q3

Agar customer ID change ho to orders me bhi automatically change ho.

Q4

Composite Primary Key ka example banao:

student_id
subject_id
Q5

Existing table me Foreign Key ALTER TABLE se add karo.

✅ Solutions
Q1
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE
);
Q2 + Q3
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,

    FOREIGN KEY (customer_id)
    REFERENCES customers(customer_id)
    ON DELETE CASCADE
    ON UPDATE CASCADE
);
Q4
CREATE TABLE student_subject (
    student_id INT,
    subject_id INT,

    PRIMARY KEY (student_id, subject_id)
);
Q5
ALTER TABLE orders
ADD CONSTRAINT fk_order_customer
FOREIGN KEY (customer_id)
REFERENCES customers(customer_id);
🎯 Interview Questions — Phase 13.2
Q1. Referential Integrity kya hai?

Foreign Key relationship me valid parent-child references maintain karna.

Q2. ON DELETE CASCADE kya karta hai?

Parent row delete hone par related child rows automatically delete karta hai.

Q3. ON DELETE SET NULL?

Child row retain hoti hai aur Foreign Key NULL ho jati hai.

Q4. RESTRICT kya karta hai?

Dependent child records hone par parent deletion/update ko prevent karta hai.

Q5. ON UPDATE CASCADE?

Parent key update hone par corresponding child Foreign Key automatically update hoti hai.

Q6. Foreign Key duplicate ho sakti hai?

Yes.

Q7. Composite Key kya hai?

Multiple columns ko combine karke banayi gayi key jo combined values ke basis par row ko uniquely identify karti hai.

Q8. Kya Composite Foreign Key possible hai?

Yes.

Q9. Foreign Key ALTER TABLE se add kar sakte hain?

Yes.

ALTER TABLE table_name
ADD CONSTRAINT constraint_name
FOREIGN KEY (...)
REFERENCES ...;
Q10. Foreign Key aur JOIN me difference?
FOREIGN KEY
→ relationship/constraint

JOIN
→ query ke time data combine
Q11. CASCADE kab dangerous ho sakta hai?

Jab accidentally parent delete karne se bahut saare child records automatically delete ho sakte hain. Isliye CASCADE carefully use karna chahiye.

Q12. Parent aur Child table?
Parent
→ referenced table

Child
→ Foreign Key wali table
🧠 PHASE 13 — FINAL REVISION
PRIMARY KEY
↓
Unique row identity

FOREIGN KEY
↓
Another table ko reference

REFERENTIAL INTEGRITY
↓
Reference valid rakho

ON DELETE
↓
Parent delete ka child par effect

CASCADE
↓
Child automatically delete/update

SET NULL
↓
Child rahega, FK NULL

RESTRICT
↓
Operation block

ON UPDATE
↓
Parent key update ka effect

COMPOSITE KEY
↓
Multiple columns = one key

ALTER TABLE
↓
Existing table me constraint add/remove
📊 SQL ROADMAP UPDATE
Phase 13 — 100% COMPLETE ✅🔥
FOREIGN KEY                  ✅
PRIMARY KEY vs FOREIGN KEY   ✅
Referential Integrity        ✅
ON DELETE                    ✅
ON UPDATE                    ✅
CASCADE                      ✅
SET NULL                     ✅
RESTRICT / NO ACTION         ✅
Composite Keys               ✅
ALTER TABLE                  ✅
ADD CONSTRAINT               ✅
DROP CONSTRAINT              ✅
Real-world relationships     ✅
Complete Practical           ✅
Interview Questions          ✅
Practice + Solutions         ✅
🟢 Overall SQL Progress: ~78% COMPLETE

Phase 13 officially DONE. ✅

Next hum Phase 14 se start karenge, aur usme bhi related topics ko possible ho to ek hi phase me properly group karke karenge.