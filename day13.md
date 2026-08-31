# SQL Practical — Day 13: SELF JOIN & CROSS JOIN

> **Overview:** Is day me hum SQL ke do specialized JOIN types: **`SELF JOIN`** (ek hi table ko khud se join karna for hierarchical relationships like Employee-Manager) aur **`CROSS JOIN`** (Cartesian Product — har row ko har row se combine karna), Master Join Comparison Table, aur complete JOIN Chapter milestone celebration ko detail me seekhenge.

---

## 📌 Syllabus & Covered Topics
1. 🔄 **Part 1 — SELF JOIN:** Concept, Real-World Employee-Manager Hierarchy & Syntax ⭐⭐⭐⭐⭐
2. ✖️ **Part 2 — CROSS JOIN:** Concept, Cartesian Product Formula (`A × B`), E-Commerce Product Variants & Hands-On Queries
3. 🏆 **Master Comparison Table:** All 6 SQL JOIN Types Summarized
4. 🎉 **JOIN Chapter Milestone Celebration & Roadmap Teaser**

---

## 🔄 Part 1: SELF JOIN

### 💡 Core Concept & Need

Ab tak humne dekha ki `JOIN` do alag-alag tables (e.g., `students` aur `departments`) ko connect karta hai.

> **Question:** Kya ek hi single table ko KHUD KE SAATH (`Table A` ➔ `Table A`) join kiya ja sakta hai?  
> **Answer:** **YES!** Isi technique ko SQL me **`SELF JOIN`** kehte hain.

---

### 🏢 Real-Life Example: Employee-Manager Hierarchy

Consider an `employees` table:

| emp_id | name | manager_id |
| :---: | :--- | :---: |
| 1 | Rahul | NULL *(Top Boss)* |
| 2 | Aman | 1 *(Reports to Rahul)* |
| 3 | Rohit | 1 *(Reports to Rahul)* |
| 4 | Priya | 2 *(Reports to Aman)* |

#### ❓ Problem Statement:
> **Question:** Aman ka Manager kaun hai?

- Table me `manager_id = 1` likha hai.
- Manager ka NAAM (`Rahul`) find karne ke liye computer ko usi same table me `emp_id = 1` ko search karna padega.
- Iska matlab: **Table ko khud ke saath join karna padega!**

---

### 🎨 Visual Flow & Syntax

```text
employees (e1 - Employee View)                     employees (e2 - Manager View)
+--------+-------+------------+                    +--------+-------+------------+
| emp_id | name  | manager_id |                    | emp_id | name  | manager_id |
+--------+-------+------------+                    +--------+-------+------------+
| 2      | Aman  | 1 ─────────┼───────────────────►| 1      | Rahul | NULL       |
+--------+-------+------------+                    +--------+-------+------------+
```

```sql
SELECT e1.name AS Employee,
       e2.name AS Manager
FROM employees e1
LEFT JOIN employees e2
ON e1.manager_id = e2.emp_id;
```

#### 🔍 Syntax Breakdown:
- **`employees e1`**: Table A (acting as Employee instance).
- **`employees e2`**: Table A (acting as Manager instance).
- **Aliases (`e1`, `e2`)**: Single table ko distinguish karne ke liye **Table Aliases mandatory** hote hain.
- **`ON e1.manager_id = e2.emp_id`**: Employee ka `manager_id` Manager ke `emp_id` se match hota hai.

---

### 💼 Real-World Project Use Cases for `SELF JOIN`
1. **Employee ↔ Manager** (Organizational hierarchy)
2. **Student ↔ Mentor** (Peer mentorship)
3. **Category ↔ Parent Category** (E-commerce category tree)
4. **Folder ↔ Parent Folder** (File system hierarchy)

> [!NOTE]
> Hamare current `students` table me manager/mentor column nahi hai, isliye hum is core concept ko interview and architecture perspective se mind me rakhenge.

---

## ✖️ Part 2: CROSS JOIN

### 💡 Core Concept & Definition

- **Definition:** `CROSS JOIN` Left table ki **har single row** ko Right table ki **har single row** ke saath combine karke saare possible combinations generate karta hai.
- **Mathematical Term:** Is match ko **Cartesian Product** kehte hain.

---

### 🛍️ Real-Life Example: Product Variations

Suppose a clothing brand has:
- **Table A (Colors):** Red, Blue (2 rows)
- **Table B (Sizes):** S, M (2 rows)

#### Combinations Output:
| Color | Size |
| :--- | :--- |
| Red | S |
| Red | M |
| Blue | S |
| Blue | M |

> 📐 **Cartesian Product Formula:**  
> $	ext{Total Output Rows} = 	ext{Table1 Rows} 	imes 	ext{Table2 Rows}$  
> Calculation: $2 	imes 2 = 4 	ext{ Rows}$.

---

### 💻 `CROSS JOIN` Hands-On Query & DB Calculation

In our Database:
- `students` Table: **9 Rows**
- `departments` Table: **5 Rows**

$$	ext{Expected Output Rows} = 9 	imes 5 = 45 	ext{ Rows}$$

```sql
SELECT *
FROM students
CROSS JOIN departments;
```

#### ⚙️ Result Grid Behavior:
- **Rahul** ➔ Combined with CSE, ECE, Mechanical, Civil, Electrical (5 rows)
- **Aman** ➔ Combined with CSE, ECE, Mechanical, Civil, Electrical (5 rows)
- ... (Repeated for all 9 students) = **Total 45 Rows**.

---

## 🏆 Master Comparison Table — All 6 SQL JOIN Types

| JOIN Type | Core Definition / Behavior | Result Formula / Behavior |
| :--- | :--- | :--- |
| **`INNER JOIN`** | Only matching records | Intersection ($A \cap B$) |
| **`LEFT JOIN`** | All rows from Left table + matching Right | Left Complete ($A$) |
| **`RIGHT JOIN`** | All rows from Right table + matching Left | Right Complete ($B$) |
| **`FULL OUTER JOIN`** | All rows from Both tables (`UNION` in MySQL) | Union ($A \cup B$) |
| **`SELF JOIN`** | Table joined with **itself** via aliases | Hierarchical links ($e1.fk = e2.pk$) |
| **`CROSS JOIN`** | Every row $	imes$ every row (Cartesian Product) | $m 	imes n 	ext{ Rows}$ |

---

### ✍️ Practice Questions — Lecture 28

#### Q1: `SELECT * FROM students CROSS JOIN departments;` query run karke row count verify karo.
#### Q2: Agar Table A me 10 rows hain aur Table B me 6 rows hain, toh `CROSS JOIN` kitni output rows return karega?

<details>
<summary><b>Click to reveal Answers</b></summary>

**A1:** Output: **45 Rows** ($9 	ext{ students} 	imes 5 	ext{ departments}$).  
**A2:** Output: **60 Rows** ($10 	imes 6 = 60$).  
</details>

---

## 🎉 JOIN Chapter Complete! 🥳

Congratulations! 🥳 Tumne SQL ke saare major JOINs successfully master kar liye hain:
- ✅ `INNER JOIN`
- ✅ `LEFT JOIN`
- ✅ `RIGHT JOIN`
- ✅ `FULL OUTER JOIN` (MySQL `UNION` way)
- ✅ `SELF JOIN`
- ✅ `CROSS JOIN`

---

## 📊 SQL Overall Progress Summary
- **Basics:** ✅ 100%
- **Filtering (`WHERE`):** ✅ 100%
- **Aggregate Functions:** ✅ 100%
- **`GROUP BY` / `HAVING`:** ✅ 100%
- **JOINs (All 6 Types):** ✅ 100%

**Overall SQL Mastery Course:** $pprox 65-70\%$ Complete! 🚀

---

## 🚀 What's Next? (Advanced Interview Roadmap)

Upcoming chapters start **Advanced SQL Interview Topics**:
- ⭐ **Subqueries** (Single-row, Multi-row, Correlated Subqueries)
- ⭐ **`EXISTS` / `NOT EXISTS`** Operators
- ⭐ **`ANY` / `ALL`** Operators
- ⭐ **`UNION` / `UNION ALL`** Deep Dive
- ⭐ **Constraints** (`PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, `CHECK`, `DEFAULT`)
- ⭐ **Views & Indexes**
- ⭐ **Transactions** (`COMMIT`, `ROLLBACK`, `SAVEPOINT`)
- ⭐ **Top 50 SQL Interview Questions & LeetCode Practice**
