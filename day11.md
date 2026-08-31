# SQL Practical — Day 11: LEFT JOIN

> **Overview:** Is day me hum SQL ke sabse major interview topic **`LEFT JOIN`** ko, `INNER JOIN` vs `LEFT JOIN` ke actual execution difference, `NULL` values handling, real-world non-matching record scenarios, aur company use cases ke saath step-by-step seekhenge.

---

## 📌 Syllabus & Covered Topics
1. 👈 **Lecture 26:** `LEFT JOIN` (Concept, Non-Matching Records, `NULL` Handling & Master Comparison) ⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐
2. ⚖️ **INNER JOIN vs LEFT JOIN:** Complete Row Count & Execution Analysis
3. 🎯 **Interview Corner:** Top Most Asked JOIN Question & Real-World Use Case

---

## 👈 Lecture 26: `LEFT JOIN`

### 💡 The Core Problem Statement

Abhi tak hamare database me sabhi students ke department IDs valid (`1`, `2`, `3`, `4`) the. Is waja se `INNER JOIN` aur `LEFT JOIN` dono exact identical output de rahe the.

`LEFT JOIN` ke real power aur difference ko samajhne ke liye, hum ek naya student insert karenge jiska department exist hi nahi karta!

---

### 🪜 Step 1: Insert Non-Matching Sample Student

Run this query in your editor:

```sql
INSERT INTO students (student_id, student_name, age, city, department_id)
VALUES (109, 'Vikas', 22, 'Jaipur', 5);
```

#### 🔍 Analysis:
- `departments` table me existing IDs: `1` (CSE), `2` (ECE), `3` (Mechanical), `4` (Civil).
- Vikas ko humne `department_id = 5` diya hai jo parent table me exist hi nahi karta!

---

### 🪜 Step 2: Verify `students` Table

```sql
SELECT * FROM students;
```

**Last Row Output:**
| student_id | student_name | age | city | department_id |
| :---: | :--- | :---: | :--- | :---: |
| 109 | Vikas | 22 | Jaipur | 5 |

---

### 🪜 Step 3: Run `INNER JOIN` (Observe Behavior)

```sql
SELECT s.student_name, d.department_name
FROM students s
INNER JOIN departments d
ON s.department_id = d.department_id;
```

**`INNER JOIN` Result Grid:**
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

#### 🤔 Vikas Kahan Gaya?
Vikas output me nahi aaya! **Reason:** Vikas ka `department_id = 5` parent table me match nahi hua (`5 ≠ 1, 2, 3, 4`).

> [!IMPORTANT]
> **Rule No. 1:** `INNER JOIN` ➔ Sirf **Matching Records** return karta hai. Non-matching records discard ho jate hain.

---

### 🪜 Step 4: Run `LEFT JOIN` (Observe Magic ✨)

```sql
SELECT s.student_name, d.department_name
FROM students s
LEFT JOIN departments d
ON s.department_id = d.department_id;
```

**`LEFT JOIN` Result Grid:**
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
| **Vikas** | **NULL** |

#### 😲 What Changed?
Vikas output grid me include ho gaya! Right table (`departments`) me matching department nahi mila, isliye department column me **`NULL`** fill ho gaya.

---

### 📖 `LEFT JOIN` Definition

- **Definition:** `LEFT JOIN` left table (first table) ki **saari rows** return karta hai, chahe right table (second table) me matching record mile ya na mile.
- **Rule:** Right table me match milne par detailed data aayega; match na milne par right table columns me **`NULL`** placeholder set hoga.

---

### 🎨 Internal Visualization & Logic

```text
LEFT TABLE (students)                                RIGHT TABLE (departments)
+-----------------------+                            +-------------------------+
| Rahul   (dept_id = 1) | ──────────────────────────►| 1 ➔ CSE                 |
| Aman    (dept_id = 2) | ──────────────────────────►| 2 ➔ ECE                 |
| Priya   (dept_id = 3) | ──────────────────────────►| 3 ➔ Mechanical          |
| Ankit   (dept_id = 4) | ──────────────────────────►| 4 ➔ Civil               |
| Vikas   (dept_id = 5) | ─────────► [ Not Found ] ➔ | NULL                    |
+-----------------------+                            +-------------------------+
```

#### MySQL Internal Thinking:
1. **Rahul** (`dept_id = 1`): Match found ➔ `CSE`
2. **Aman** (`dept_id = 2`): Match found ➔ `ECE`
3. **Vikas** (`dept_id = 5`): Search in `departments` ➔ Not Found ➔ Return `Vikas | NULL`

---

### ⚖️ Master Comparison: `INNER JOIN` vs `LEFT JOIN`

| Metric / Scenario | `INNER JOIN` | `LEFT JOIN` |
| :--- | :--- | :--- |
| **Matching Rows** | Output me aate hain | Output me aate hain |
| **Non-Matching Left Rows (Vikas)** | Discarded / Hidden ❌ | Included with `NULL` ✅ |
| **Total Rows Returned (Day 11)** | **8 Rows** | **9 Rows** |
| **Primary Focus** | Mutual Intersect | Complete Left Table |

---

### 🏢 Real-World Company Scenario

#### Scenario: Employee Department Report
Suppose Boss asks: **"Mujhe company ke SAARI EMPLOYEES ki list aur unke departments dikhao (bhale hi kisi naye employee ko abhi tak department assign na hua ho)."**

- **If you use `INNER JOIN`:** Unassigned employees hidden ho jayenge ❌ *(Boss ko incomplete audit report milegi)*.
- **If you use `LEFT JOIN`:** Saare employees list honge, aur jinko department nahi mila unke aage `NULL` aayega ✅ *(Perfect complete report)*.

---

### ⚠️ Common Mistake

> [!WARNING]
> **Common Beginner Misconception:** "LEFT JOIN matlab sirf Left side ki table ka data aayega."  
> **Fact:** `LEFT JOIN` left table ki saari rows **PLUS** right table ka matching data return karta hai. Match na hone par right side `NULL` ho jata hai.

---

### 🎯 Interview Corner ⭐⭐⭐⭐⭐

> [!IMPORTANT]
> **Q: What is the main difference between `INNER JOIN` and `LEFT JOIN`?**  
> **Answer:**  
> - **`INNER JOIN`** returns ONLY records that have matching values in both tables. Non-matching records are excluded.  
> - **`LEFT JOIN`** returns ALL records from the left table, and the matched records from the right table. If no match is found in the right table, `NULL` values are returned for the right table columns.

---

### ✍️ Practice Questions — Lecture 26

#### Q1: `INNER JOIN` run karke verify karo kitni total rows aa rahi hain.
#### Q2: `LEFT JOIN` run karke verify karo kitni total rows aa rahi hain.
#### Q3: Student Name, City aur Department Name display karne ki `LEFT JOIN` query likho.

<details>
<summary><b>Click to reveal Answers</b></summary>

**A1:**
```sql
SELECT *
FROM students s
INNER JOIN departments d
ON s.department_id = d.department_id;
-- Output: 8 Rows (Vikas excluded)
```

**A2:**
```sql
SELECT *
FROM students s
LEFT JOIN departments d
ON s.department_id = d.department_id;
-- Output: 9 Rows (Vikas included with NULLs)
```

**A3:**
```sql
SELECT s.student_name, s.city, d.department_name
FROM students s
LEFT JOIN departments d
ON s.department_id = d.department_id;
```
</details>

---

## 🚀 What's Next? (Upcoming Teaser)
Next lecture covers **`RIGHT JOIN`**, **`FULL OUTER JOIN`** (and how to simulate FULL OUTER JOIN in MySQL using `UNION`), plus Venn Diagram visual shortcuts to master all JOIN types permanently! 🚀
