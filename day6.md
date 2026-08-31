# SQL Practical — Day 6: Range Filtering, Deduplication, NULL Handling & CRUD Operations

> **Overview:** Is day me hum SQL ke 7 fundamental topics: `BETWEEN`, `DISTINCT`, `IS NULL` / `IS NOT NULL`, `UPDATE`, `DELETE`, `TRUNCATE`, aur `ALTER TABLE` ko complete practical breakdown ke saath seekhenge.

---

## 📌 Syllabus & Covered Topics
1. ↔️ **Lecture 17 — Topic 1:** `BETWEEN` Operator (Inclusive Range Filtering)
2. ✨ **Lecture 17 — Topic 2:** `DISTINCT` Clause (Duplicate Removal)
3. ❓ **Lecture 17 — Topic 3:** `IS NULL` / `IS NOT NULL` (Handling Unknown / Missing Data)
4. ✏️ **Lecture 18 — Topic 1:** `UPDATE` Statement (Modifying Data & Dangerous Mistakes)
5. 🗑️ **Lecture 18 — Topic 2:** `DELETE` Statement (Row Removal)
6. 🧹 **Lecture 18 — Topic 3:** `TRUNCATE` Command (Table Data Reset)
7. 🏗️ **Lecture 18 — Topic 4:** `ALTER TABLE` Command (Schema Modification: ADD, DROP, RENAME)

---

## 📚 Lecture 17: `BETWEEN`, `DISTINCT`, `IS NULL`

---

### 1️⃣ `BETWEEN` Operator (Inclusive Range Filtering)

#### 💡 Problem & Solution
Agar hume age 20 se 22 ke beech wale students chahiye hote:
```sql
-- Traditional Approach:
SELECT * FROM student WHERE age >= 20 AND age <= 22;

-- Modern Short Form (BETWEEN):
SELECT * FROM student WHERE age BETWEEN 20 AND 22;
```

#### 📜 Important Rule ⭐
> [!IMPORTANT]
> `BETWEEN` operator **INCLUSIVE** hota hai. Yani lower bound (`20`) aur upper bound (`22`) DONO output grid me include honge (`20`, `21`, `22`).

#### 💻 Query Examples
```sql
-- Example 1: Age Range
SELECT * FROM student WHERE age BETWEEN 20 AND 22;

-- Example 2: ID Range
SELECT * FROM student WHERE id BETWEEN 2 AND 4;

-- Example 3: BETWEEN with ORDER BY
SELECT * FROM student WHERE age BETWEEN 19 AND 22 ORDER BY age DESC;
```

---

### 2️⃣ `DISTINCT` Clause (Duplicate Removal)

#### 📊 Target Table (`student`)
| id | name | city |
| :---: | :---: | :---: |
| 1 | Rahul | Delhi |
| 2 | Aman | Delhi |
| 3 | Rohit | Mumbai |
| 4 | Priya | Delhi |
| 5 | Neha | Mumbai |

#### 💡 Need & Query
If we run `SELECT city FROM student;`, output displays duplicates (`Delhi`, `Delhi`, `Mumbai`, `Delhi`, `Mumbai`).  
Duplicates remove karke unique cities dekhne ke liye **`DISTINCT`** keyword use hota hai:

```sql
SELECT DISTINCT city FROM student;
```
**Output Grid:** `Delhi`, `Mumbai`

#### 🎤 Interview Question
> [!IMPORTANT]
> **Q: Difference between `SELECT city` and `SELECT DISTINCT city`?**  
> - **`SELECT city`:** Retains all values including duplicates.  
> - **`SELECT DISTINCT city`:** Returns only unique non-duplicate values.

---

### 3️⃣ `IS NULL` / `IS NOT NULL` (Handling Missing Data)

#### ❓ NULL Kya Hai?
- **NULL Definition:** Missing, unknown, or unavailable data value.
- ❌ **NULL is NOT 0.**
- ❌ **NULL is NOT an Empty String (`""`).**
- **Meaning:** Data value entered hi nahi hui hai (e.g. Aman phone number = `NULL`).

#### ⚠️ Dangerous Trap & Correct Syntax
> [!WARNING]
> - **WRONG ❌:** `WHERE phone = NULL;` *(NULL kisi bhi value ke equal nahi hota!)*
> - **CORRECT ✅:** `WHERE phone IS NULL;`

#### 💻 Query Examples
```sql
-- Fetch records with missing phone number:
SELECT * FROM student WHERE phone IS NULL;

-- Fetch records with valid phone number present:
SELECT * FROM student WHERE phone IS NOT NULL;
```

---

### ✍️ Practice Questions — Lecture 17

#### Q1: Age 19 se 21 ke beech wale students dikhao.
#### Q2: ID 2 se 4 ke beech wale students dikhao.
#### Q3: Table me se sirf unique cities dikhao.
#### Q4: Jin students ka phone number missing ho unhe dikhao.

<details>
<summary><b>Click to reveal Answers</b></summary>

**A1:** `SELECT * FROM student WHERE age BETWEEN 19 AND 21;`  
**A2:** `SELECT * FROM student WHERE id BETWEEN 2 AND 4;`  
**A3:** `SELECT DISTINCT city FROM student;`  
**A4:** `SELECT * FROM student WHERE phone IS NULL;`  
</details>

---

## 🚀 Lecture 18: `UPDATE`, `DELETE`, `TRUNCATE`, `ALTER TABLE`

---

### ✏️ Topic 1: `UPDATE` Statement

#### 💡 Concept & Need
Existing row ke data me changes karne ke liye `UPDATE` statement use kiya jata hai.

#### 💻 Syntax & Single Column Update
```sql
UPDATE student
SET age = 21
WHERE id = 1;
```

#### 💻 Multiple Columns Update
```sql
UPDATE student
SET name = 'Rahul Kumar', age = 22
WHERE id = 1;
```

#### ⚠️ Sabse Dangerous Mistake Alert

> [!CAUTION]
> If you forget the `WHERE` clause:
> ```sql
> UPDATE student SET age = 50;
> ```
> 😨 **Poori table ke saare students ki age 50 ho jayegi!** Hamesha `UPDATE` query execute karne se pehle `WHERE` clause verify karein.

---

### 🗑️ Topic 2: `DELETE` Statement

#### 💡 Concept & Need
Table me se specific record/row ko permanently remove karne ke liye `DELETE` statement use hota hai.

#### 💻 Syntax & Example
```sql
DELETE FROM student
WHERE id = 4;
```

> [!CAUTION]
> `DELETE FROM student;` (without `WHERE` clause) table ka saara data delete kar deta hai!

---

### 🧹 Topic 3: `TRUNCATE` Command

#### 💡 Concept & Definition
```sql
TRUNCATE TABLE student;
```
- **Definition:** Table ke saare records ko ek hi shot me delete/empty kar deta hai. Fast performance execute karta hai. Table structure aur columns remain intact.

---

### 🏗️ Topic 4: `ALTER TABLE` Command (Schema Modification)

Table design create hone ke baad uske structure me changes (Column add, drop, rename) karne ke liye `ALTER TABLE` command use hoti hai:

```sql
-- 1. New Column Add:
ALTER TABLE student ADD phone VARCHAR(15);

-- 2. Column Delete:
ALTER TABLE student DROP COLUMN phone;

-- 3. Column Rename:
ALTER TABLE student RENAME COLUMN name TO student_name;

-- 4. Table Rename:
ALTER TABLE student RENAME TO students;
```

---

### 📊 Master Comparison Table: `DELETE` vs `TRUNCATE` vs `DROP TABLE`

| Command | Command Category | Table Structure | Data Rows | Performance Speed | Rollback / Behavior |
| :--- | :--- | :---: | :---: | :---: | :--- |
| **`DELETE`** | DML | Retained | Selected / All rows deleted | Slower (Row-by-row) | Can be filtered with `WHERE` |
| **`TRUNCATE`** | DDL | Retained | ALL rows deleted (Reset) | Faster | Resets table data instantly |
| **`DROP TABLE`** | DDL | **Deleted** | ALL rows deleted | Fast | Deletes table schema + data completely |

---

### ✍️ Practice Questions — Lecture 18

#### Q1: ID = 2 wale student ki age 25 kar do.
#### Q2: ID = 3 wale student ka naam 'Rohan' kar do.
#### Q3: ID = 2 wale student ko delete karo.
#### Q4: Student table me `email` naam ka column add karo (`VARCHAR(100)`).
#### Q5: `email` column ko delete karo.

<details>
<summary><b>Click to reveal Answers</b></summary>

**A1:** `UPDATE student SET age = 25 WHERE id = 2;`  
**A2:** `UPDATE student SET name = 'Rohan' WHERE id = 3;`  
**A3:** `DELETE FROM student WHERE id = 2;`  
**A4:** `ALTER TABLE student ADD email VARCHAR(100);`  
**A5:** `ALTER TABLE student DROP COLUMN email;`  
</details>

---

## 🚀 What's Next? (Upcoming Teaser)
Next lectures cover **Aggregate Functions** (`COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`), `GROUP BY`, `HAVING`, aur uske baad **`JOINS`**! 🚀
HERE
Comparison Operators (=, >, <, >=, <=, !=)
AND / OR / NOT
ORDER BY
LIMIT
LIKE (%, _)
IN / NOT IN
BETWEEN
DISTINCT
IS NULL / IS NOT NULL
UPDATE
DELETE
ALTER TABLE
TRUNCATE

Ab hum SQL ke next major chapter me enter kar rahe hain.