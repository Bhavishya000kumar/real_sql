# SQL Practical — Day 2: DDL, DML & Data Filtering

> **Overview:** Is day me hum SQL ke basic table creation (`CREATE TABLE`), data insertion (`INSERT INTO` single & multiple rows), basic data retrieval (`SELECT`), aur initial filtering (`WHERE` clause + Comparison Operators) ko practical breakdown ke saath seekhenge.

---

## 📌 Syllabus & Covered Topics
1. 🛠️ **Lecture 3:** `CREATE TABLE` Command & Data Types (`INT`, `VARCHAR`)
2. 📥 **Lecture 4:** `INSERT INTO` (Single Row Data Insertion)
3. 🔍 **Lecture 5:** `SELECT` Statement (All vs Specific Column Selection)
4. 📑 **Lecture 6:** `INSERT INTO` (Multiple Rows & Best Practices)
5. 🎯 **Lecture 7:** `WHERE` Clause Introduction (Basic Filtering)
6. ⚖️ **Lecture 8:** Comparison Operators in `WHERE` Clause (`=`, `>`, `<`, `>=`, `<=`, `!=`)

---

## 🛠️ Lecture 3: `CREATE TABLE` (SQL Ka Sabse Important DDL Command)

### 💡 Core Concept & Structure Hierarchy
Abhi tak humne Database container banaya tha:
```text
MySQL Server ──► Database (college) ──► Table (student)
```

**Database ke andar actual data kahan store hota hai?**  
👉 **Table me.**

#### 📂 Real-Life Analogy (Cupboard & Files)
- **Cupboard** = Database
- **Files inside cupboard** = Tables (`student`, `teacher`, `fees`)

---

### 📊 Target Table Schema (`student`)
Hum `student` table ka structure banayenge:

| id | name | age |
| :---: | :---: | :---: |
| 1 | Rahul | 20 |
| 2 | Aman | 21 |

*(Note: Pehle sirf structure banayenge, data baad me insert karenge.)*

---

### 💻 Syntax & Command
```sql
CREATE TABLE student(
    id INT,
    name VARCHAR(50),
    age INT
);
```

### 🧠 Command Breakdown
| Line / Syntax | Explanation & Meaning |
| :--- | :--- |
| `CREATE TABLE student(` | `CREATE` = Banao, `TABLE` = Table, `student` = Table Ka Naam. |
| `id INT,` | `id` = Column Name, `INT` = Integer Data Type (Whole numbers allowed: 1, 20, 100, 500. Decimal `20.5` ya text like `Rahul`, `ABC` allowed nahi hai). |
| `name VARCHAR(50),` | `name` = Column Name, `VARCHAR` = Variable Character Text (Maximum 50 characters allowed like 'Rahul', 'Aman', 'Bhavishya'). |
| `age INT` | `age` = Column Name, `INT` = Whole number. |
| `);` | Closing bracket & query terminator semicolon. |

---

### 🕹️ Execution & Verification
1. Editor me command likhein aur `Ctrl + Enter` dabayein.
2. Success outcome: Workbench ke Left Sidebar me `college` -> `Tables` par right-click karke **Refresh** karein. `student` table show hone lagegi.

---

### 📒 Lecture 3 Quick Summary Notes
- **`CREATE TABLE`**: Nayi table create karta hai.
- **`INT`**: Whole numbers store karta hai (e.g., `10`, `25`, `100`).
- **`VARCHAR(50)`**: Text store karta hai up to maximum 50 characters.

---

### ✍️ Practice Questions — Lecture 3

#### Question 1
`employee` naam ki table banao jisme `id`, `name`, aur `salary` columns hon.

#### Question 2
`teacher` naam ki table banao jisme `teacher_id`, `teacher_name`, aur `age` columns hon.

---

### ✅ Answers (Abhi Mat Dekhna 😄)

<details>
<summary><b>Click to reveal Answer 1</b></summary>

```sql
CREATE TABLE employee(
    id INT,
    name VARCHAR(50),
    salary INT
);
```
</details>

<details>
<summary><b>Click to reveal Answer 2</b></summary>

```sql
CREATE TABLE teacher(
    teacher_id INT,
    teacher_name VARCHAR(50),
    age INT
);
```
</details>

---

## 📥 Lecture 4: `INSERT INTO` (Single Row Data Insertion)

### 💡 Core Concept & Register Analogy
Table (`student`) structure banne ke baad wo abhi khali hai (jaise empty Student Register). Data populate karne ke liye SQL command `INSERT INTO` use hoti hai.

Register format:
```text
ID  | Name  | Age
1   | Rahul | 20
```

---

### 💻 Syntax & Command
```sql
INSERT INTO student(id, name, age)
VALUES (1, 'Rahul', 20);
```

### 🧠 Command Breakdown
| Keyword / Part | Meaning / Role |
| :--- | :--- |
| `INSERT INTO` | Data insert karne ka SQL command. |
| `student` | Target table ka naam. |
| `(id, name, age)` | Target columns list jisme data dalna hai. |
| `VALUES` | Keyword jo actual values specify karta hai. |
| `(1, 'Rahul', 20)` | Actual data values in order: `id = 1`, `name = 'Rahul'`, `age = 20`. |

---

### 📌 String vs Number Syntax Rules

> [!IMPORTANT]
> - **Text / String (`'Rahul'`):** Text data hamesha **Single Quotes `' '`** me likhte hain.
> - **Number / Integer (`20`):** Numeric values ko **bina quotes** ke likha jata hai.
> - ❌ **Incorrect:** `'20'` (Number ko quotes me mat likho)
> - ✅ **Correct:** `20`

---

### 🔍 Data Verification Query Preview
```sql
SELECT * FROM student;
```
**Expected Output:**
| id | name | age |
| :---: | :---: | :---: |
| 1 | Rahul | 20 |

---

### 📒 Lecture 4 Quick Summary Notes
- **`INSERT INTO`**: Table me naya data row add karta hai.
- **`VALUES`**: Actual values specify karne ke liye keyword.
- **String (`'Rahul'`)**: Quotes me.
- **Integer (`20`)**: Quotes nahi.

---

### ✍️ Practice Questions — Lecture 4

#### Question 1
`student` table me ye data insert karo: `id = 2`, `name = 'Aman'`, `age = 21`.

#### Question 2
`student` table me ye data insert karo: `id = 3`, `name = 'Bhavishya'`, `age = 22`.

---

### ✅ Answers (Pehle Mat Dekhna 😄)

<details>
<summary><b>Click to reveal Answer 1</b></summary>

```sql
INSERT INTO student(id, name, age)
VALUES (2, 'Aman', 21);
```
</details>

<details>
<summary><b>Click to reveal Answer 2</b></summary>

```sql
INSERT INTO student(id, name, age)
VALUES (3, 'Bhavishya', 22);
```
</details>

---

## 🔍 Lecture 5: `SELECT` Statement (Data Retrieval)

### 💡 Core Concept & Library Analogy
`SELECT` SQL ka sabse important retrieval command hai (90% placement questions SELECT se related hote hain).
- **Library Analogy:** Library jaakar librarian se kehna *"DBMS wali book dikhao"* = Selecting specific data.

---

### 🧠 `SELECT * FROM student;` Command Breakdown
| Part | Meaning |
| :--- | :--- |
| `SELECT` | 👉 Choose karo / Dikhao |
| `*` (Star) | 👉 Saare columns (`id`, `name`, `age`) |
| `FROM` | 👉 Kis table se? |
| `student` | 👉 Target table ka naam |
| **English Translation** | "Student table se saara data dikhao." |

---

### 📊 All vs Specific Column Selection

#### 1. Select All Columns
```sql
SELECT * FROM student;
```

#### 2. Select Single Column (`name`)
```sql
SELECT name FROM student;
```
**Output:**
| name |
| :---: |
| Rahul |

#### 3. Select Single Column (`age`)
```sql
SELECT age FROM student;
```
**Output:**
| age |
| :---: |
| 20 |

#### 4. Select Multiple Specific Columns (`id, name`)
```sql
SELECT id, name FROM student;
```
**Output:**
| id | name |
| :---: | :---: |
| 1 | Rahul |

---

### ⭐ Interview Trick Summary
- `*` = All Columns.
- `id, name` = Explicitly selected columns only.

---

### ✍️ Practice Questions — Lecture 5

#### Question 1
Sirf `id` dikhane ki query likho.

#### Question 2
Sirf `name` aur `age` dikhane ki query likho.

#### Question 3
`student` table ke saare records aur saare columns dikhane ki query likho.

---

### ✅ Answers (Baad Me Match Karna 😄)

<details>
<summary><b>Click to reveal Answer 1</b></summary>

```sql
SELECT id FROM student;
```
</details>

<details>
<summary><b>Click to reveal Answer 2</b></summary>

```sql
SELECT name, age FROM student;
```
</details>

<details>
<summary><b>Click to reveal Answer 3</b></summary>

```sql
SELECT * FROM student;
```
</details>

---

## 📑 Lecture 6: `INSERT` Multiple Rows (Batch Insertion)

### 💡 Single vs Multiple Row Insertion

#### Method 1: Repeated Statements (Longer)
```sql
INSERT INTO student(id, name, age) VALUES (2, 'Aman', 21);
INSERT INTO student(id, name, age) VALUES (3, 'Rohit', 22);
INSERT INTO student(id, name, age) VALUES (4, 'Priya', 19);
```

#### Method 2: Single Query Batch Insertion (Industry Standard)
```sql
INSERT INTO student(id, name, age)
VALUES
(2, 'Aman', 21),
(3, 'Rohit', 22),
(4, 'Priya', 19);
```
*(Notice: `INSERT INTO` sirf ek baar likha, aur tuples comma `,` se separate hain.)*

---

### 📊 Verification Output (`SELECT * FROM student;`)
| id | name | age |
| :---: | :---: | :---: |
| 1 | Rahul | 20 |
| 2 | Aman | 21 |
| 3 | Rohit | 22 |
| 4 | Priya | 19 |

---

### 🧠 Omitting Column Names List & Best Practice

```sql
-- Query without specifying column names:
INSERT INTO student
VALUES (5, 'Ankit', 23);
```

> [!NOTE]
> Ye query tabhi chalegi agar values ka order table ke original schema order (`id` -> `name` -> `age`) se 100% match karta ho.

> [!IMPORTANT]
> **⭐ Interview Tip / Best Practice:** Industry me hamesha column names explicitly likhna (`INSERT INTO student(id, name, age)`) recommended hai. Agar future me table me naya column add ho gaya, to bina column names wali queries break ho jayengi.

---

### ⚠️ Common Mistakes

> [!WARNING]
> **Galti:** Row tuples ke beech comma `,` bhool jana.
> ```sql
> -- WRONG ❌
> VALUES
> (2, 'Aman', 21)
> (3, 'Rohit', 22)
> 
> -- CORRECT ✅
> VALUES
> (2, 'Aman', 21),
> (3, 'Rohit', 22);
> ```

---

### ✍️ Practice Questions — Lecture 6

#### Question 1
Ek hi query me ye students insert karo:  
`5 | Sohan | 18`  
`6 | Neha | 20`

#### Question 2
Single query se ek student insert karo:  
`7 | Bhavishya | 21`

#### Question 3
Ab poori table print karne ki query likho.

---

### ✅ Answers (Baad Me Dekhna 😄)

<details>
<summary><b>Click to reveal Answer 1</b></summary>

```sql
INSERT INTO student(id, name, age)
VALUES
(5, 'Sohan', 18),
(6, 'Neha', 20);
```
</details>

<details>
<summary><b>Click to reveal Answer 2</b></summary>

```sql
INSERT INTO student(id, name, age)
VALUES (7, 'Bhavishya', 21);
```
</details>

<details>
<summary><b>Click to reveal Answer 3</b></summary>

```sql
SELECT * FROM student;
```
</details>

---

## 🎯 Lecture 7: `WHERE` Clause Introduction (Basic Filtering)

### 💡 Why `WHERE` Clause? (Amazon Filter Analogy)
Agar table me thousands of rows hain aur hume specific row chaiye (e.g., Amazon par Shoes filter: `Brand = Nike`, `Price < 3000`), tab hum `WHERE` clause ka filter lagate hain.

---

### 💻 Syntax & Examples

```sql
SELECT *
FROM student
WHERE condition;
```

#### Example 1: Filter by Name (`name='Aman'`)
```sql
SELECT *
FROM student
WHERE name = 'Aman';
```
**Output:**
| id | name | age |
| :---: | :---: | :---: |
| 2 | Aman | 21 |

#### Example 2: Filter by Age (`age=20`)
```sql
SELECT *
FROM student
WHERE age = 20;
```
**Output:**
| id | name | age |
| :---: | :---: | :---: |
| 1 | Rahul | 20 |

#### Example 3: Filter by ID (`id=3`)
```sql
SELECT *
FROM student
WHERE id = 3;
```
**Output:**
| id | name | age |
| :---: | :---: | :---: |
| 3 | Rohit | 22 |

---

### ⚠️ Common Mistake in `WHERE`

> [!WARNING]
> - `WHERE name = Aman;` ❌ *(Text value me quotes missing hain)*
> - `WHERE name = 'Aman';` ✅ *(Correct: String values in single quotes)*
> - `WHERE age = 20;` ✅ *(Correct: Numeric values without quotes)*

---

### ✍️ Practice Questions — Lecture 7

#### Question 1
Sirf `Priya` ka record dikhao.

#### Question 2
Sirf `Rohit` ka record dikhao.

#### Question 3
Jiski `age = 21` hai uska record dikhao.

#### Question 4
Jiski `id = 4` hai uska record dikhao.

---

### ✅ Answers (Pehle Khud Karna 😄)

<details>
<summary><b>Click to reveal Answer 1</b></summary>

```sql
SELECT * FROM student WHERE name = 'Priya';
```
</details>

<details>
<summary><b>Click to reveal Answer 2</b></summary>

```sql
SELECT * FROM student WHERE name = 'Rohit';
```
</details>

<details>
<summary><b>Click to reveal Answer 3</b></summary>

```sql
SELECT * FROM student WHERE age = 21;
```
</details>

<details>
<summary><b>Click to reveal Answer 4</b></summary>

```sql
SELECT * FROM student WHERE id = 4;
```
</details>

---

## ⚖️ Lecture 8: Comparison Operators in `WHERE` Clause

### 📊 Comparison Operators Table
| Operator | Meaning | Example |
| :---: | :--- | :--- |
| `=` | Equal | `WHERE age = 20` |
| `>` | Greater Than | `WHERE age > 20` |
| `<` | Less Than | `WHERE age < 20` |
| `>=` | Greater Than Equal | `WHERE age >= 20` |
| `<=` | Less Than Equal | `WHERE age <= 20` |
| `!=` | Not Equal | `WHERE age != 20` |

---

### 🧠 How MySQL Evaluates `WHERE` (Row-by-Row Execution)

Consider Table:
| id | name | age |
| :---: | :---: | :---: |
| 1 | Rahul | 20 |
| 2 | Aman | 21 |
| 3 | Rohit | 22 |
| 4 | Priya | 19 |

Query: `SELECT * FROM student WHERE age > 20;`
- **Rahul (20):** `20 > 20` ➔ **FALSE** ❌ (Reject)
- **Aman (21):** `21 > 20` ➔ **TRUE** ✅ (Select)
- **Rohit (22):** `22 > 20` ➔ **TRUE** ✅ (Select)
- **Priya (19):** `19 > 20` ➔ **FALSE** ❌ (Reject)

**Output:**
| id | name | age |
| :---: | :---: | :---: |
| 2 | Aman | 21 |
| 3 | Rohit | 22 |

---

### 💻 Operator Examples & Outputs

#### 1. Less Than (`<`)
```sql
SELECT * FROM student WHERE age < 20;
```
**Output:** `Priya (19)`

#### 2. Greater Than Equal (`>=`)
```sql
SELECT * FROM student WHERE age >= 20;
```
**Output:** `Rahul (20)`, `Aman (21)`, `Rohit (22)`

#### 3. Less Than Equal (`<=`)
```sql
SELECT * FROM student WHERE age <= 20;
```
**Output:** `Rahul (20)`, `Priya (19)`

#### 4. Not Equal (`!=`)
```sql
SELECT * FROM student WHERE age != 20;
```
**Output:** `Aman (21)`, `Rohit (22)`, `Priya (19)`

---

### 🎤 Interview Question

> [!IMPORTANT]
> **Q: Difference between `>` and `>=` operators in SQL?**  
> **Answer:**  
> - `>` (Greater Than) boundary value ko include **nahi** karta (`age > 20` gives 21, 22...).  
> - `>=` (Greater Than Equal) boundary value ko bhi output set me **include** karta hai (`age >= 20` gives 20, 21, 22...).

---

### ✍️ Practice Questions — Lecture 8

#### Question 1
Age 21 se zyada wale students dikhao (`age > 21`).

#### Question 2
Age 21 ya usse kam wale students dikhao (`age <= 21`).

#### Question 3
Age 19 nahi honi chahiye (`age != 19`).

#### Question 4
Age 22 ya usse zyada wale students dikhao (`age >= 22`).

---

### ✅ Answers (Baad Me Match Karna 😄)

<details>
<summary><b>Click to reveal Answer 1</b></summary>

```sql
SELECT * FROM student WHERE age > 21;
```
</details>

<details>
<summary><b>Click to reveal Answer 2</b></summary>

```sql
SELECT * FROM student WHERE age <= 21;
```
</details>

<details>
<summary><b>Click to reveal Answer 3</b></summary>

```sql
SELECT * FROM student WHERE age != 19;
```
</details>

<details>
<summary><b>Click to reveal Answer 4</b></summary>

```sql
SELECT * FROM student WHERE age >= 22;
```
</details>

---

## 🚀 What's Next? (Upcoming Teaser)
Next lecture me hum padhenge:
- Logical Operators: `AND`, `OR`, `NOT`
- Filtering clauses: `ORDER BY`, `LIMIT`, `LIKE`, `IN`, `BETWEEN`
- Data Operations: `UPDATE` & `DELETE`
la Lecture (SQL ka Bahut Important Topic)

Ab hum padhenge:

AND
OR
NOT

Ye teen operators har placement company (TCS, Accenture, Capgemini, EPAM, Infosys) ke SQL rounds me bahut frequently use hote hain.

Uske baad hum ORDER BY, LIMIT, LIKE, IN, BETWEEN aur phir UPDATE aur DELETE ki taraf badhenge. Ye sab milkar tumhe SQL ke interview-level questions solve karne layak bana denge. 🚀