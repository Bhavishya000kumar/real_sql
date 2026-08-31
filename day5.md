# SQL Practical — Day 5: Set Exclusion Filtering (`NOT IN` Operator)

> **Overview:** Is day me hum SQL ke **`NOT IN`** operator ko seekhenge jo `IN` operator ka exact opposite hai. Ye specific values ki list ko query output me se exclude / ignore karne ke liye use hota hai.

---

## 📌 Syllabus & Covered Topics
1. ⛔ **Lecture 16:** `NOT IN` Operator (Set Exclusion Filtering) ⭐⭐⭐⭐⭐

---

## ⛔ Lecture 16: `NOT IN` Operator (Set Exclusion Filtering)

### 💡 Core Concept & Need
Pichhle lecture me humne padha tha: `WHERE age IN (20, 21);` (Sirf 20 aur 21 wale students fetch karna).  
Aaj hum padhenge uski opposite requirement: **"20 aur 21 age wale students ko CHHODKAR baaki sab fetch karo."**

#### 📊 Target Table (`student`)
| id | name | age |
| :---: | :---: | :---: |
| 1 | RAHUL | 20 |
| 2 | Aman | 21 |
| 3 | Rohit | 22 |
| 4 | Priya | 19 |

---

### 🤔 Traditional `AND` vs `NOT IN` Operator

#### Traditional Approach (Using `!=` and `AND`):
```sql
SELECT *
FROM student
WHERE age != 20
AND age != 21;
```
> [!NOTE]
> Ye query sahi kaam karti hai. Lekin agar hume 10 values ko ignore karna ho (`WHERE age!=18 AND age!=19 AND age!=20 AND age!=21...`), to query bohot lambi aur complex ho jaati hai.

#### Modern / Industry Approach (Using `NOT IN`):
```sql
SELECT *
FROM student
WHERE age NOT IN (20, 21);
```

---

### 📖 `NOT IN` Definition & Syntax

- **Definition:** `NOT IN` list ke andar di hui values ko output result me se **exclude (chhod)** deta hai.

| Clause | Purpose | Action |
| :--- | :--- | :--- |
| **`IN`** | Include list | Sirf ye specified values fetch karo |
| **`NOT IN`** | Exclude list | In specified values ko chhodkar baaki sab fetch karo |

#### 💻 Syntax
```sql
SELECT *
FROM student
WHERE column_name NOT IN (value1, value2, ...);
```

---

### 🧠 MySQL Row-by-Row Execution Breakdown

Query:
```sql
SELECT *
FROM student
WHERE age NOT IN (20, 21);
```

**Execution Step-by-Step:**
- **RAHUL (Age 20):** `20 NOT IN (20, 21)` ➔ **FALSE** ❌ (Reject)
- **Aman (Age 21):** `21 NOT IN (20, 21)` ➔ **FALSE** ❌ (Reject)
- **Rohit (Age 22):** `22 NOT IN (20, 21)` ➔ **TRUE** ✅ (Return)
- **Priya (Age 19):** `19 NOT IN (20, 21)` ➔ **TRUE** ✅ (Return)

**Output Grid:**
| id | name | age |
| :---: | :---: | :---: |
| 3 | Rohit | 22 |
| 4 | Priya | 19 |

---

### 🔤 String Values Example (`NOT IN`)

```sql
SELECT *
FROM student
WHERE name NOT IN ('RAHUL', 'Aman');
```

**Output Grid:**
| id | name | age |
| :---: | :---: | :---: |
| 3 | Rohit | 22 |
| 4 | Priya | 19 |

---

### 🏫 Real Life Example (College Notice)
College me notice aaya: *"Rahul aur Aman kal presentation denge, baaki sab students free hain."*  
SQL Query:
```sql
SELECT *
FROM student
WHERE name NOT IN ('RAHUL', 'Aman');
```

---

### ⚖️ Comparison Table: `IN` vs `NOT IN`

| Query | Condition | Output Ages |
| :--- | :--- | :---: |
| `WHERE age IN (20, 21)` | Select ONLY age 20 and 21 | `20`, `21` |
| `WHERE age NOT IN (20, 21)` | Exclude age 20 and 21 (Select rest) | `19`, `22` |

---

### 📊 Data Flow Visualization
```text
All Students (19, 20, 21, 22)
          │
          ▼
   WHERE NOT IN (20, 21)
          │
          ▼
   Filtered Output (19, 22)
```

---

### 🕹️ Workbench Practical Queries

#### Query 1: Exclude Age 19 & 22
```sql
SELECT *
FROM student
WHERE age NOT IN (19, 22);
```
**Expected Output:** `RAHUL (20)`, `Aman (21)`

#### Query 2: Exclude Single Name ('Priya')
```sql
SELECT *
FROM student
WHERE name NOT IN ('Priya');
```

#### Query 3: Exclude IDs (1, 4)
```sql
SELECT *
FROM student
WHERE id NOT IN (1, 4);
```

---

### 📒 Quick Cheatsheet / Notes

- **`NOT IN` General Syntax:**
  ```sql
  SELECT * FROM student WHERE age NOT IN (20, 21);
  ```
- **String Filtering:**
  ```sql
  SELECT * FROM student WHERE name NOT IN ('Aman');
  ```
- **Numeric Filtering:**
  ```sql
  SELECT * FROM student WHERE id NOT IN (1, 2);
  ```

---

### ⚠️ Common Mistakes

> [!WARNING]
> - `WHERE age NOT 20;` ❌ *(Missing `IN` keyword and parentheses `()`)*
> - `WHERE age NOT IN (20);` ✅ *(Correct)*
> - `WHERE name NOT IN (Rahul);` ❌ *(Missing single quotes on string literal)*
> - `WHERE name NOT IN ('RAHUL');` ✅ *(Correct)*

---

### ✍️ Practice Questions — Lecture 16

#### Question 1
Age `19` aur `20` ko chhodkar baaki students dikhao.

#### Question 2
Name `Aman` aur `Rohit` ko chhodkar baaki students dikhao.

#### Question 3
ID `2` aur `3` ko chhodkar baaki students dikhao.

#### Question 4
Age `21` ko chhodkar baaki students dikhao.

---

### ✅ Answers (Khud Karne Ke Baad Dekhna 😄)

<details>
<summary><b>Click to reveal Answer 1</b></summary>

```sql
SELECT *
FROM student
WHERE age NOT IN (19, 20);
```
</details>

<details>
<summary><b>Click to reveal Answer 2</b></summary>

```sql
SELECT *
FROM student
WHERE name NOT IN ('Aman', 'Rohit');
```
</details>

<details>
<summary><b>Click to reveal Answer 3</b></summary>

```sql
SELECT *
FROM student
WHERE id NOT IN (2, 3);
```
</details>

<details>
<summary><b>Click to reveal Answer 4</b></summary>

```sql
SELECT *
FROM student
WHERE age NOT IN (21);
```
</details>

---

### 🧠 Interview Corner

> [!IMPORTANT]
> **Q: Are `WHERE age NOT IN (20, 21);` and `WHERE age != 20 AND age != 21;` identical?**  
> **Answer:** **Yes!** Normal non-null values ke case me dono exact same result return karte hain.  
> *(Note: Jab database me `NULL` values hoti hain, tab `NOT IN` ka behavior change ho sakta hai, jise hum `NULL` chapter me detail me padhenge.)*

---

## 🚀 What's Next? (Upcoming Teaser)
Next lecture covers **`BETWEEN` Operator** (Range Filtering):
```sql
SELECT *
FROM student
WHERE age BETWEEN 20 AND 22;
```
*(Ye query Age = 20, 21, 22 ko single line range filtering me fetch karti hai.)*

Is topic ke baad hum `DISTINCT`, `IS NULL`, `UPDATE`, aur `DELETE` start karenge. 🚀