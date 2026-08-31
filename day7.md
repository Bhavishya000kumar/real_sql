# SQL Practical — Day 7: Aggregate Functions & Data Grouping (`GROUP BY`)

> **Overview:** Is day me hum SQL ke sabse important data analysis tools: **Aggregate Functions** (`COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`) aur **`GROUP BY` Clause** (same category/attribute values wale data ko group me summarize karna) ko step-by-step practical examples ke saath seekhenge.

---

## 📌 Syllabus & Covered Topics
1. 📊 **Lecture 19:** Aggregate Functions (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`)
2. 🏷️ **Lecture 20:** `GROUP BY` Clause (Data Grouping & Summary Analytics) ⭐⭐⭐⭐⭐⭐⭐⭐⭐

---

## 📊 Lecture 19: Aggregate Functions (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`)

### 💡 Core Concept & Definition
- **Definition:** Aggregate functions multiple rows ke values ko process karke ek **single summary result** return karte hain.
- **Why Needed?** 10,000 students ki table me se total count, average age, ya max/min age bina manual calculation ke single query se nikalne ke liye.

---

### 💻 5 Primary Aggregate Functions

#### 1️⃣ `COUNT()` — Row / Record Counting
- **`COUNT(*)`:** Table me total kitni rows hain (including NULLs) unhe count karta hai.
  ```sql
  SELECT COUNT(*) FROM student;
  ```
- **`COUNT(column_name)`:** Target column me kitni **NON-NULL** values hain, sirf unhe count karta hai.
  ```sql
  SELECT COUNT(age) FROM student;
  ```

#### 2️⃣ `SUM()` — Numeric Total Calculation
- **Purpose:** Numeric column ki saari values ka sum (total) calculate karta hai.
  ```sql
  SELECT SUM(age) FROM student;
  -- Calculation: 20 + 21 + 22 + 19 = 82
  ```

#### 3️⃣ `AVG()` — Numeric Average Calculation
- **Purpose:** Numeric column ki values ka average calculate karta hai.
  ```sql
  SELECT AVG(age) FROM student;
  -- Calculation: (20 + 21 + 22 + 19) / 4 = 20.5
  ```

#### 4️⃣ `MIN()` — Minimum Value Extraction
- **Purpose:** Column me se smallest / minimum value return karta hai.
  ```sql
  SELECT MIN(age) FROM student;
  -- Output: 19
  ```

#### 5️⃣ `MAX()` — Maximum Value Extraction
- **Purpose:** Column me se largest / maximum value return karta hai.
  ```sql
  SELECT MAX(age) FROM student;
  -- Output: 22
  ```

---

### 📊 Visualizing Aggregate Functions Output
| Table Input Ages | Aggregate Function | Calculated Result |
| :---: | :---: | :---: |
| `20`, `21`, `22`, `19` | `COUNT(*)` | **4** |
| `20`, `21`, `22`, `19` | `SUM(age)` | **82** |
| `20`, `21`, `22`, `19` | `AVG(age)` | **20.5** |
| `20`, `21`, `22`, `19` | `MIN(age)` | **19** |
| `20`, `21`, `22`, `19` | `MAX(age)` | **22** |

---

### 🎯 Combining Aggregate Functions with `WHERE` Clause

```sql
-- Count students with age >= 20:
SELECT COUNT(*) FROM student WHERE age >= 20;

-- Average age of students with age >= 20:
SELECT AVG(age) FROM student WHERE age >= 20;
```

---

### ⚠️ Common Mistakes

> [!WARNING]
> - `SELECT SUM(name) FROM student;` ❌ *(SUM text/string columns par work nahi karta!)*
> - `SELECT AVG(name) FROM student;` ❌ *(AVG strictly numeric columns ke liye hota hai!)*

---

### ✍️ Practice Questions — Lecture 19

#### Q1: Student table me total kitne records hain?
#### Q2: Sabhi students ki total age nikalo.
#### Q3: Average age nikalo.
#### Q4: Minimum age nikalo.
#### Q5: Maximum age nikalo.

<details>
<summary><b>Click to reveal Answers</b></summary>

**A1:** `SELECT COUNT(*) FROM student;`  
**A2:** `SELECT SUM(age) FROM student;`  
**A3:** `SELECT AVG(age) FROM student;`  
**A4:** `SELECT MIN(age) FROM student;`  
**A5:** `SELECT MAX(age) FROM student;`  
</details>

---

## 🏷️ Lecture 20: `GROUP BY` Clause (Data Grouping)

### 💡 Core Concept & Need
Jab Principal ask kare: *"Har city me kitne students hain?"*  
Individual records filter karne ke bajaye hume **same city wale students ko ek group me collect** karna hota hai. Isi liye SQL me **`GROUP BY`** clause use hota hai.

- **Definition:** `GROUP BY` specified column ki identical / same values ko single summary group me collapse kar deta hai.

---

### 📊 Target Table (`student`)
| id | name | age | city |
| :---: | :---: | :---: | :---: |
| 1 | Rahul | 20 | Delhi |
| 2 | Aman | 21 | Delhi |
| 3 | Rohit | 22 | Mumbai |
| 4 | Priya | 19 | Delhi |
| 5 | Neha | 20 | Mumbai |
| 6 | Karan | 21 | Pune |

---

### 💻 Basic Syntax & Grouping Example

```sql
SELECT city
FROM student
GROUP BY city;
```
**Output Grid:** `Delhi`, `Mumbai`, `Pune` *(Delhi 3 baar tha, par output me single group display hota hai.)*

---

### 🧠 Combining `GROUP BY` with Aggregate Functions ⭐

`GROUP BY` clause ki real power tab dikhti hai jab isse Aggregate Functions (`COUNT`, `AVG`, `MAX`, `MIN`, `SUM`) ke saath use kiya jaye.

#### 1. Student Count in Every City (`GROUP BY + COUNT`)
```sql
SELECT city, COUNT(*)
FROM student
GROUP BY city;
```
**Execution Breakdown:**
1. `Delhi Group` ➔ 3 Students (Rahul, Aman, Priya)
2. `Mumbai Group` ➔ 2 Students (Rohit, Neha)
3. `Pune Group` ➔ 1 Student (Karan)

**Output Grid:**
| city | COUNT(*) |
| :--- | :---: |
| Delhi | 3 |
| Mumbai | 2 |
| Pune | 1 |

#### 2. Average Age in Every City (`GROUP BY + AVG`)
```sql
SELECT city, AVG(age)
FROM student
GROUP BY city;
```
**Output Grid:**
| city | AVG(age) |
| :--- | :---: |
| Delhi | 20 |
| Mumbai | 21 |
| Pune | 21 |

#### 3. Maximum Age in Every City (`GROUP BY + MAX`)
```sql
SELECT city, MAX(age)
FROM student
GROUP BY city;
```

---

### 🛍️ Real Life Example (Ecommerce Product Analytics)
Amazon / Flipkart backend brand-wise product counts:
```sql
SELECT brand, COUNT(*)
FROM products
GROUP BY brand;
```
**Output:** Apple (25), Samsung (40), OnePlus (18).

---

### 🎤 Interview Corner: Core Definition

> [!IMPORTANT]
> **Q: What does `GROUP BY` do in SQL?**  
> **Answer:** `GROUP BY` column ke identical values ko single groups me aggregate/collapse karta hai aur summary statistics calculate karne ke liye aggregate functions (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`) ke saath combine hota hai.

---

### ⚠️ Common Syntax Mistakes

> [!WARNING]
> **WRONG ❌:**
> ```sql
> SELECT city, name
> FROM student
> GROUP BY city;
> ```
> *(Rule: `SELECT` list me koi aisa column direct include nahi hona chahiye jo `GROUP BY` list me nahi hai aur na hi par koi aggregate function apply hua hai. `name` column har group ke multiple rows ko ambiguously represent karega.)*

---

### ✍️ Practice Questions — Lecture 20

#### Q1: Har city me kitne students hain?
#### Q2: Har city ki average age nikalo.
#### Q3: Har city ki maximum age nikalo.
#### Q4: Har city ki minimum age nikalo.

<details>
<summary><b>Click to reveal Answers</b></summary>

**A1:** `SELECT city, COUNT(*) FROM student GROUP BY city;`  
**A2:** `SELECT city, AVG(age) FROM student GROUP BY city;`  
**A3:** `SELECT city, MAX(age) FROM student GROUP BY city;`  
**A4:** `SELECT city, MIN(age) FROM student GROUP BY city;`  
</details>

---

## 🚀 What's Next? (Upcoming Teaser)
Next lecture covers **`HAVING` Clause** (Group level filtering — `WHERE` vs `HAVING` interview favorite ⭐⭐⭐⭐⭐)! 🚀


ALTER TABLE student
ADD city VARCHAR(50);

ALTER TABLE student
ADD department VARCHAR(30);

Uske baad GROUP BY aur HAVING ko real data par use karenge.

🚀 Next Lecture

HAVING Clause

Ye WHERE jaisa dikhta hai, lekin kaam bilkul alag karta hai.

Bahut students WHERE aur HAVING me confuse ho jate hain.

Main tumhe itna clearly samjhaunga ki interview me agar koi pooche:

"Difference between WHERE and HAVING?"

to tum bina soche answer de paoge. 🔥  