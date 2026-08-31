# SQL Practical — Day 10: INNER JOIN (Part-1 & Part-2)

> **Overview:** Is day me hum SQL ke sabse major topic **INNER JOIN** ko deep execution dry run, MySQL internal matching algorithm, Table Aliases (`s`, `d`), `SELECT *` behavior, aur Ambiguous Column errors ke saath complete practical clarity me seekhenge.

---

## 📌 Syllabus & Covered Topics
1. 🔗 **Lecture 24:** INNER JOIN (Part-1) — Core Concept, Real-Life Analogy, Syntax & Dry Run ⭐⭐⭐⭐⭐
2. ⚡ **Lecture 25:** INNER JOIN (Part-2) — Table Alias (`s`, `d`), `SELECT *`, & Ambiguous Column Error

---

## 🔗 Lecture 24: INNER JOIN (Part-1)

### 💡 Core Concept & Need

#### 📊 Target Tables Overview

**`students` Table:**
| student_id | student_name | department_id |
| :---: | :--- | :---: |
| 101 | Rahul | 1 |
| 102 | Aman | 2 |
| 103 | Rohit | 1 |
| 104 | Priya | 3 |

**`departments` Table:**
| department_id | department_name |
| :---: | :--- |
| 1 | CSE |
| 2 | ECE |
| 3 | Mechanical |
| 4 | Civil |

#### ❓ Problem Statement
> **Question:** Rahul kis department me hai?

```text
Students Table ➔ Rahul ➔ department_id = 1
                              │
                              ▼
Departments Table ➔ department_id = 1 ➔ CSE

Result: Rahul ➔ CSE
```
SQL me ye matching work **`INNER JOIN`** dwara automatically kiya jata hai!

---

### 📖 INNER JOIN Definition

- **Definition:** `INNER JOIN` do tables ke **matching records** ko combine karke unified result set return karta hai.
- **Visual Rule:**
  ```text
  [ Table A ]  +  [ Table B ]  ➔  ( Only Matching Rows )  ➔  Output Result
  ```

---

### 🧠 Real-Life Analogy

Socho tumhare paas do tables hain:

**Aadhaar Table:**
| Aadhaar | Name |
| :---: | :--- |
| 101 | Rahul |
| 102 | Aman |

**Bank Table:**
| Aadhaar | Balance |
| :---: | :---: |
| 101 | 5000 |
| 102 | 8000 |

Agar Rahul ka bank balance chahiye:
```text
Aadhaar 101 ➔ Matches Bank Aadhaar 101 ➔ Rahul = 5000
```
Ye exact logic SQL `INNER JOIN` me follow hota hai!

---

### 💻 `INNER JOIN` Syntax Breakdown

```sql
SELECT column_names
FROM table1
INNER JOIN table2
ON table1.common_column = table2.common_column;
```

#### Line-by-Line Breakdown:
- **Line 1 (`SELECT`):** Konsi columns output grid me display karni hain.
- **Line 2 (`FROM students`):** Primary / Left table identify karo.
- **Line 3 (`INNER JOIN departments`):** Right table ko connect karo.
- **Line 4 (`ON table1.common_column = table2.common_column`):** Connecting condition (Key matching criteria).

---

### ⚙️ `ON` Clause & Step-by-Step Dry Run

#### `ON` Clause Execution Logic:
```text
students.department_id = departments.department_id
```

Computer internally har row ke liye matching perform karta hai:

1. **Row 1:** `Rahul` (`department_id = 1`) ➔ `departments` me `1 = CSE` ➔ **MATCH ✅** ➔ Output: `Rahul | CSE`
2. **Row 2:** `Aman` (`department_id = 2`) ➔ `departments` me `2 = ECE` ➔ **MATCH ✅** ➔ Output: `Aman | ECE`
3. **Row 3:** `Rohit` (`department_id = 1`) ➔ `departments` me `1 = CSE` ➔ **MATCH ✅** ➔ Output: `Rohit | CSE`
4. **Row 4:** `Priya` (`department_id = 3`) ➔ `departments` me `3 = Mechanical` ➔ **MATCH ✅** ➔ Output: `Priya | Mechanical`

---

### 📊 Final Joined Output Grid

```sql
SELECT student_name, department_name
FROM students
INNER JOIN departments
ON students.department_id = departments.department_id;
```

| student_name | department_name |
| :--- | :--- |
| Rahul | CSE |
| Aman | ECE |
| Rohit | CSE |
| Priya | Mechanical |
| Neha | ECE |
| Karan | CSE |
| Ankit | Civil |
| Sneha | ECE |

---

### 📚 Table Prefix & Dot Notation (`Table.Column`)

> **Why write `students.department_id` instead of just `department_id`?**

- `department_id` column dono tables (`students` aur `departments`) me exist karta hai.
- Agar sirf `department_id` likha jaye, toh MySQL confuse ho jayega ki kaunsi table ka column use karna hai.
- **Dot (.) Notation:** `Table_Name.Column_Name` (e.g., `students.department_id` ➔ `students` table ka `department_id`).

---

### 📝 Key Notes — Part 1
- **`INNER JOIN`:** Sirf matching rows ko combine karta hai.
- **`ON`:** Connection condition specify karta hai.
- **Dot (`.`) Notation:** `Table.Column` reference system.
- **Common Column:** Matching key (`department_id`).

---

### ✍️ Practice Questions — Lecture 24

#### Q1: `students` table se Student Name aur City display karne ki query likho.
#### Q2: Student Name aur Unka Department Name dikhane ki INNER JOIN query likho.
#### Q3: Student Name, City aur Department Name saath me fetch karne ki query likho.

<details>
<summary><b>Click to reveal Answers</b></summary>

**A1:**
```sql
SELECT student_name, city
FROM students;
```

**A2:**
```sql
SELECT student_name, department_name
FROM students
INNER JOIN departments
ON students.department_id = departments.department_id;
```

**A3:**
```sql
SELECT student_name, city, department_name
FROM students
INNER JOIN departments
ON students.department_id = departments.department_id;
```
</details>

---

## ⚡ Lecture 25: INNER JOIN (Part-2)

---

### 🏷️ Topic 1: Table Aliases (`s`, `d`)

#### ❓ Need for Aliases
Badi production queries me `students.department_id = departments.department_id` baar-baar likhna repetitive aur lengthy ho jata hai. Iska clean solution **Table Aliases (Nicknames)** hai.

#### 📖 Alias Definition & Syntax
Alias matlab table ka chhota nickname (e.g., `students` ➔ `s`, `departments` ➔ `d`).

```sql
SELECT s.student_name, d.department_name
FROM students s
INNER JOIN departments d
ON s.department_id = d.department_id;
```

- `FROM students s` ➔ `students` table ko alias `s` assign hua.
- `INNER JOIN departments d` ➔ `departments` table ko alias `d` assign hua.
- `ON s.department_id = d.department_id` ➔ Query short, clean aur highly readable ban gayi!

---

### 📋 Topic 2: `SELECT *` with JOIN

Agar dono tables ke saare columns ek saath fetch karne hon:

```sql
SELECT *
FROM students s
INNER JOIN departments d
ON s.department_id = d.department_id;
```

**Output Grid:**
| student_id | student_name | age | city | department_id | department_id | department_name |
| :---: | :--- | :---: | :--- | :---: | :---: | :--- |
| 101 | Rahul | 20 | Delhi | 1 | 1 | CSE |
| 102 | Aman | 21 | Delhi | 2 | 2 | ECE |

> [!NOTE]
> `department_id` column output me **2 baar** aata hai kyunki ek `students` table ka column hai aur ek `departments` table ka.

---

### ⚠️ Topic 3: Ambiguous Column Error ⭐⭐⭐⭐⭐

> [!WARNING]
> **Interview Trap:** Niche di gayi SQL query run karne par kya hoga?

```sql
SELECT department_id
FROM students
INNER JOIN departments
ON students.department_id = departments.department_id;
```

#### ❌ Error Result:
```text
ERROR 1052 (23000): Column 'department_id' in field list is ambiguous
```

#### 💡 Reason & Resolution:
- **Reason:** Computer confuse ho jata hai ki field list me `department_id` `students` table se pick karna hai ya `departments` table se.
- **Fix:** Always explicitly specify table prefix or alias:
  ```sql
  SELECT s.department_id -- ✅ Explicit table alias
  FROM students s
  INNER JOIN departments d
  ON s.department_id = d.department_id;
  ```

---

### 🔍 Topic 4: Computer Internal Matching Visualization

```text
STUDENTS TABLE                                      DEPARTMENTS TABLE
+------------+--------------+---------------+       +---------------+-----------------+
| student_id | student_name | department_id |       | department_id | department_name |
+------------+--------------+---------------+       +---------------+-----------------+
| 101        | Rahul        | 1 ────────────┼──────►| 1             | CSE             |
| 102        | Aman         | 2 ────────────┼──────►| 2             | ECE             |
| 103        | Rohit        | 1 ────────────┼──────►| 3             | Mechanical      |
| 104        | Priya        | 3 ────────────┼──────►| 4             | Civil           |
+------------+--------------+---------------+       +---------------+-----------------+
```

---

### 📝 Key Notes — Part 2
- **Table Alias (`students s`, `departments d`):** Code readability aur brevity ke liye nicknames.
- **`SELECT *`:** Combined dataset ke saare columns fetch karta hai (duplicate key columns ke saath).
- **Ambiguous Column Error:** Single column name jo multiple tables me common ho, uske pehle table alias/prefix lagana mandatory hai (`s.department_id`).

---

### ✍️ Practice Questions — Lecture 25

#### Q1: Alias (`s`, `d`) ka use karke Student Name aur Department Name display karo.
#### Q2: Alias ka use karke JOIN ke baad saari columns (`SELECT *`) fetch karo.
#### Q3: Alias ka use karke Student Name, City aur Department Name display karo.

<details>
<summary><b>Click to reveal Answers</b></summary>

**A1:**
```sql
SELECT s.student_name, d.department_name
FROM students s
INNER JOIN departments d
ON s.department_id = d.department_id;
```

**A2:**
```sql
SELECT *
FROM students s
INNER JOIN departments d
ON s.department_id = d.department_id;
```

**A3:**
```sql
SELECT s.student_name, s.city, d.department_name
FROM students s
INNER JOIN departments d
ON s.department_id = d.department_id;
```
</details>

---

## 🚀 What's Next? (Upcoming Teaser)
Next lecture covers **`LEFT JOIN`** (What happens when a student has an unassigned or non-matching department ID? Why `INNER JOIN` hides non-matching rows and how `LEFT JOIN` retains all left-table rows with `NULL`s)! 🚀
