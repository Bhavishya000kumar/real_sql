# SQL Practical — Day 8: Group Level Filtering (`HAVING` Clause)

> **Overview:** Is day me hum SQL ke sabse major interview topic: **`HAVING` Clause** ko seekhenge jo `GROUP BY` ke baad summary groups ko aggregate conditions (`COUNT()`, `AVG()`, `SUM()`) ke basis par filter karne ke liye use hota hai.

---

## 📌 Syllabus & Covered Topics
1. 🔍 **Lecture 21:** `HAVING` Clause (Group Filtering vs Row Filtering) ⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐
2. ⚖️ **WHERE vs HAVING:** Complete Technical & Execution Comparison
3. ⚙️ **Logical Query Execution Order:** FROM ➔ WHERE ➔ GROUP BY ➔ HAVING ➔ SELECT ➔ ORDER BY ➔ LIMIT

---

## 🔍 Lecture 21: `HAVING` Clause (Group Filtering)

### 💡 Core Concept & Need

#### 📊 Target Table (`student`)
| id | name | age | city |
| :---: | :---: | :---: | :---: |
| 1 | Rahul | 20 | Delhi |
| 2 | Aman | 21 | Delhi |
| 3 | Rohit | 22 | Mumbai |
| 4 | Priya | 19 | Delhi |
| 5 | Neha | 20 | Mumbai |
| 6 | Karan | 21 | Pune |

#### ❓ Problem Statement
If Principal asks: **"Sirf vohi cities dikhao jahan 2 ya usse zyada (>= 2) students hain."**

- `WHERE` individual rows filter karta hai (`WHERE city = 'Delhi'`).
- Lekin yahan requirement kisi single row ko nahi, **pori group ki summary metrics (student count)** ko filter karne ki hai.
- **Yahan `WHERE` fail ho jata hai!** Group filtering ke liye SQL me **`HAVING`** clause introduce hota hai.

---

### 📖 `HAVING` Definition

- **Definition:** `HAVING` clause `GROUP BY` se bane aggregated groups ko condition test ke according **filter (select/discard)** karta hai.
- 💡 **Golden Rule:** `HAVING` is almost always used together with `GROUP BY`.

---

### 🧠 Step-by-Step Execution Breakdown

Query:
```sql
SELECT city, COUNT(*) AS total_students
FROM student
GROUP BY city
HAVING COUNT(*) >= 2;
```

1. **Step 1 — Grouping (`GROUP BY city`):**
   - `Delhi Group`: Rahul, Aman, Priya (Total 3)
   - `Mumbai Group`: Rohit, Neha (Total 2)
   - `Pune Group`: Karan (Total 1)

2. **Step 2 — Aggregation (`COUNT(*)`):**
   - Delhi = 3
   - Mumbai = 2
   - Pune = 1

3. **Step 3 — Group Filtering (`HAVING COUNT(*) >= 2`):**
   - Delhi (3 >= 2) ➔ **YES ✅**
   - Mumbai (2 >= 2) ➔ **YES ✅**
   - Pune (1 >= 2) ➔ **NO ❌ (Filtered out)**

**Final Output Grid:**
| city | total_students |
| :--- | :---: |
| Delhi | 3 |
| Mumbai | 2 |

---

### ⚖️ Master Comparison Table: `WHERE` vs `HAVING` ⭐⭐⭐⭐⭐

> [!IMPORTANT]
> **This is the most asked SQL Interview Question!**

| Comparison Feature | `WHERE` Clause | `HAVING` Clause |
| :--- | :--- | :--- |
| **Primary Purpose** | Individual **Rows** ko filter karta hai | Aggregated **Groups** ko filter karta hai |
| **Execution Timing** | `GROUP BY` se **PEHLE** execute hota hai | `GROUP BY` ke **BAAD** execute hota hai |
| **Aggregate Functions** | Aggregate Functions (`COUNT`, `AVG`, `SUM`) **CANNOT** be used | Aggregate Functions (`COUNT`, `AVG`, `SUM`) **CAN** be used |
| **Dependency** | `GROUP BY` ke bina independent kaam karta hai | Normally `GROUP BY` clause par dependent hota hai |

---

### ⚙️ Logical Query Execution Hierarchy

MySQL internal execution order strictly follow karta hai:

```text
1. FROM        ➔ Table identify karo
   │
2. WHERE       ➔ Individual rows filter karo
   │
3. GROUP BY    ➔ Rows ko groups me collapse karo
   │
4. HAVING      ➔ Formed groups ko filter karo
   │
5. SELECT      ➔ Required columns / expressions pick karo
   │
6. ORDER BY    ➔ Output dataset sort karo
   │
7. LIMIT       ➔ Return rows count cap karo
```

---

### 💻 Query Examples

#### Example 1: Average Age > 20 in Cities
```sql
SELECT city, AVG(age)
FROM student
GROUP BY city
HAVING AVG(age) > 20;
```

#### Example 2: Maximum Age >= 21 in Cities
```sql
SELECT city, MAX(age)
FROM student
GROUP BY city
HAVING MAX(age) >= 21;
```

#### Example 3: E-commerce Brand Product Count > 100
```sql
SELECT brand, COUNT(*)
FROM products
GROUP BY brand
HAVING COUNT(*) > 100;
```

---

### ⚠️ Common Mistakes

> [!WARNING]
> - `WHERE COUNT(*) > 2;` ❌ *(Aggregate functions `WHERE` clause me allowed nahi hain! Always use `HAVING COUNT(*) > 2`.)*
> - `HAVING city = 'Delhi';` ❌ *(Individual row filtering condition `WHERE` clause me honi chahiye: `WHERE city = 'Delhi'`.)*
> - `SELECT city, COUNT(*) FROM student HAVING COUNT(*) >= 2;` ❌ *(`GROUP BY` clause missing hone se `HAVING` target group test nahi kar paega.)*

---

### ✍️ Practice Questions — Lecture 21

#### Q1: Sirf wahi cities dikhao jahan 2 ya usse zyada students hain.
#### Q2: Sirf wahi cities dikhao jahan average age 20 se zyada hai.
#### Q3: Sirf wahi cities dikhao jahan maximum age 22 hai.
#### Q4: Har city ke students count ko descending order me dikhao.

<details>
<summary><b>Click to reveal Answers</b></summary>

**A1:**
```sql
SELECT city, COUNT(*) FROM student GROUP BY city HAVING COUNT(*) >= 2;
```

**A2:**
```sql
SELECT city, AVG(age) FROM student GROUP BY city HAVING AVG(age) > 20;
```

**A3:**
```sql
SELECT city, MAX(age) FROM student GROUP BY city HAVING MAX(age) = 22;
```

**A4:**
```sql
SELECT city, COUNT(*) FROM student GROUP BY city ORDER BY COUNT(*) DESC;
```
</details>

---

## 🚀 What's Next? (Upcoming Teaser)
Next chapter starts **`JOINS`** (Multi-table relationships: `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL OUTER JOIN`, `SELF JOIN`, `CROSS JOIN`)! 🚀
 JOIN

itni depth me padhenge ki baad me JOIN kabhi difficult nahi lagega.

🔥 Main promise karta hoon, JOIN chapter hamare pure SQL course ka sabse best chapter hoga.

