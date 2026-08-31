# SQL Practical — Day 3: Logical Operators & Data Sorting

> **Overview:** Is day me hum SQL ke logical operators (`AND`, `OR`, `NOT`) se multiple conditions filter karna seekhenge aur `ORDER BY` clause ke saath data ko Ascending (`ASC`) / Descending (`DESC`) order me sort karna seekhenge.

---

## 📌 Syllabus & Covered Topics
1. ⚡ **Lecture 9:** Logical Operators (`AND`, `OR`, `NOT`)
2. 🔀 **Lecture 10:** `ORDER BY` Clause (Sorting Data via `ASC` & `DESC`)

---

## ⚡ Lecture 9: `AND`, `OR`, `NOT` Logical Operators (Interview Favorite ⭐⭐⭐⭐⭐)

### 💡 Core Concept & Need
Abhi tak hum single condition par filter laga rahe the (`WHERE age = 20;`). Lekin real-world scenarios me hume ek se zyada conditions par rows filter karni hoti hain (e.g. *Name = 'Aman'* AND *Age = 21*). Iske liye SQL me **Logical Operators** use hote hain.

#### 📊 Target Table (`student`)
| id | name | age |
| :---: | :---: | :---: |
| 1 | RAHUL | 20 |
| 2 | Aman | 21 |
| 3 | Rohit | 22 |
| 4 | Priya | 19 |

---

### 1️⃣ `AND` Operator

#### 📜 Rule
`AND` operator tabhi `TRUE` return karta hai jab **SAARI / DONO conditions `TRUE`** hon.

#### 💻 Syntax & Example
```sql
SELECT *
FROM student
WHERE name = 'Aman'
AND age = 21;
```

#### 🧠 MySQL Row-by-Row Execution Breakdown
- **Row 1 (RAHUL):** `name = 'Aman'` ❌ AND `age = 21` ❌ ➔ **FALSE** (Reject)
- **Row 2 (Aman):** `name = 'Aman'` ✅ AND `age = 21` ✅ ➔ **TRUE** (Selected)
- **Row 3 (Rohit):** `name = 'Aman'` ❌ AND `age = 21` ❌ ➔ **FALSE** (Reject)

**Output Grid:**
| id | name | age |
| :---: | :---: | :---: |
| 2 | Aman | 21 |

#### 📊 Truth Table — `AND` Operator
| Condition 1 | Condition 2 | Result |
| :---: | :---: | :---: |
| **True** | **True** | ✅ **True** |
| **True** | **False** | ❌ **False** |
| **False** | **True** | ❌ **False** |
| **False** | **False** | ❌ **False** |

---

### 2️⃣ `OR` Operator

#### 📜 Rule
`OR` operator me agar **EK BHI condition `TRUE`** ho jati hai, to row select ho jati hai.

#### 💻 Syntax & Example
```sql
SELECT *
FROM student
WHERE age = 19
OR age = 22;
```

**Output Grid:**
| id | name | age |
| :---: | :---: | :---: |
| 3 | Rohit | 22 |
| 4 | Priya | 19 |

#### 📊 Truth Table — `OR` Operator
| Condition 1 | Condition 2 | Result |
| :---: | :---: | :---: |
| **True** | **True** | ✅ **True** |
| **True** | **False** | ✅ **True** |
| **False** | **True** | ✅ **True** |
| **False** | **False** | ❌ **False** |

---

### 3️⃣ `NOT` Operator

#### 📜 Rule
`NOT` operator condition ke result ko **invert/reverse** kar deta hai (`TRUE` ➔ `FALSE`, `FALSE` ➔ `TRUE`).

#### 💻 Syntax & Example
```sql
SELECT *
FROM student
WHERE NOT age = 20;
```
*(Note: Ye query `WHERE age != 20;` ke identical kaam karti hai.)*

**Output Grid:**
| id | name | age |
| :---: | :---: | :---: |
| 2 | Aman | 21 |
| 3 | Rohit | 22 |
| 4 | Priya | 19 |

---

### 🛍️ Real Life Example (Amazon Search & Filtering)
When searching for Shoes on Amazon:
- **`AND` Example:** `Brand = 'Nike' AND Price < 3000` *(Dono match hone mandatory hain)*
- **`OR` Example:** `Brand = 'Nike' OR Brand = 'Adidas'` *(Dono me se koi ek brand ho to aayega)*

---

### 🎤 Interview Trick & Difference Summary

> [!IMPORTANT]
> **Q: What is the main difference between `AND` and `OR` operators?**  
> - **`AND`:** Saari conditions `TRUE` hona mandatory hai.  
> - **`OR`:** Kam se kam ek condition ka `TRUE` hona sufficient hai.

---

### ⚠️ Common Mistakes

> [!WARNING]
> - `WHERE name = Aman;` ❌ *(Text value ke quotes missing hain)*
> - `WHERE name = 'Aman';` ✅ *(Correct string format)*
> - `WHERE age = '20';` ⚠️ *(Technically MySQL auto-converts, but numeric literals without quotes `WHERE age = 20;` is the best practice)*

---

### ✍️ Practice Questions — Lecture 9

#### Question 1
`Age = 20` ya `Age = 21` wale students dikhao.

#### Question 2
`Name = 'RAHUL'` aur `Age = 20` wala student dikhao.

#### Question 3
`Age = 19` nahi hona chahiye (`NOT` operator use karo).

#### Question 4
`Name = 'Priya'` ya `Name = 'Rohit'` wale students dikhao.

---

### ✅ Answers (Baad Me Match Karna 😄)

<details>
<summary><b>Click to reveal Answer 1</b></summary>

```sql
SELECT *
FROM student
WHERE age = 20
OR age = 21;
```
</details>

<details>
<summary><b>Click to reveal Answer 2</b></summary>

```sql
SELECT *
FROM student
WHERE name = 'RAHUL'
AND age = 20;
```
*(Note: Database me name uppercase `'RAHUL'` stored hai).*
</details>

<details>
<summary><b>Click to reveal Answer 3</b></summary>

```sql
SELECT *
FROM student
WHERE NOT age = 19;
```
</details>

<details>
<summary><b>Click to reveal Answer 4</b></summary>

```sql
SELECT *
FROM student
WHERE name = 'Priya'
OR name = 'Rohit';
```
</details>

---

### 🏆 Placement Tip
Placement test queries (TCS, Accenture, EPAM, Capgemini) me complex `WHERE` combinations widespread hote hain:
```sql
WHERE age > 20 AND name = 'Aman';
-- OR
WHERE age > 20 OR age < 18;
```

---

## 🔀 Lecture 10: `ORDER BY` (Sorting Data)

### 💡 Core Concept & Purpose
Jab interviewer ya client bole:
- *"Students ko age ke according chhote se bade order me arrange karo."*
- *"Students ko name ke according A-Z order me arrange karo."*

SQL me sorting ke liye **`ORDER BY`** clause use kiya jata hai (similar to `sort()` function in C++).

---

### 💻 Basic Syntax
```sql
SELECT *
FROM student
ORDER BY column_name;
```

---

### 1️⃣ Ascending Order (`ASC`)

#### 📜 Meaning
- **Numbers:** Small ➔ Large (`19` ➔ `20` ➔ `21` ➔ `22`)
- **Strings/Text:** Alphabetical `A` ➔ `Z`

#### 💻 Query Example
```sql
SELECT *
FROM student
ORDER BY age ASC;
```

**Output Grid:**
| id | name | age |
| :---: | :---: | :---: |
| 4 | Priya | 19 |
| 1 | RAHUL | 20 |
| 2 | Aman | 21 |
| 3 | Rohit | 22 |

> [!NOTE]
> **Default Behavior:** `ORDER BY age;` aur `ORDER BY age ASC;` bilkul SAME hain. SQL by default **Ascending Order (`ASC`)** use karta hai.

---

### 2️⃣ Descending Order (`DESC`)

#### 📜 Meaning
- **Numbers:** Large ➔ Small (`22` ➔ `21` ➔ `20` ➔ `19`)
- **Strings/Text:** Reverse Alphabetical `Z` ➔ `A`

#### 💻 Query Example
```sql
SELECT *
FROM student
ORDER BY age DESC;
```

**Output Grid:**
| id | name | age |
| :---: | :---: | :---: |
| 3 | Rohit | 22 |
| 2 | Aman | 21 |
| 1 | RAHUL | 20 |
| 4 | Priya | 19 |

---

### 🔤 Sorting by Name Column

#### Alphabetical (A ➔ Z)
```sql
SELECT *
FROM student
ORDER BY name ASC;
```
**Output Order:** `Aman` ➔ `Priya` ➔ `RAHUL` ➔ `Rohit`

#### Reverse Alphabetical (Z ➔ A)
```sql
SELECT *
FROM student
ORDER BY name DESC;
```

---

### 📊 Visualizing `ASC` vs `DESC`
- **`ASC` (Ascending):** `19` ➔ `20` ➔ `21` ➔ `22` ⬆️ *(Chhote se bada / A-Z)*
- **`DESC` (Descending):** `22` ➔ `21` ➔ `20` ➔ `19` ⬇️ *(Bade se chhota / Z-A)*

---

### 🎤 Interview Question

> [!IMPORTANT]
> **Q: What is the difference between `ASC` and `DESC` in `ORDER BY`?**
> | Property | `ASC` (Ascending) | `DESC` (Descending) |
> | :--- | :--- | :--- |
> | **Number Direction** | Small ➔ Large | Large ➔ Small |
> | **Text Direction** | A ➔ Z | Z ➔ A |
> | **Default Status** | Default in SQL | Must specify explicitly |

---

### 🛍️ Real Life Example (Ecommerce Price Filter)
- **Price: Low to High:** `ORDER BY price ASC;`
- **Price: High to Low:** `ORDER BY price DESC;`

---

### ⚠️ Common Syntax Mistakes

> [!WARNING]
> - `ORDER age BY;` ❌ *(Wrong keyword placement)*
> - `ORDER BY age;` ✅ *(Correct)*
> - `ORDER BY ASC age;` ❌ *(`ASC` placed before column name)*
> - `ORDER BY age ASC;` ✅ *(Correct)*

---

### ✍️ Practice Questions — Lecture 10

#### Question 1
Students ko `age` ke according ascending order me dikhao.

#### Question 2
Students ko `age` ke according descending order me dikhao.

#### Question 3
Students ko `name` ke according A-Z me dikhao.

#### Question 4
Students ko `name` ke according Z-A me dikhao.

---

### ✅ Answers (Baad Me Match Karna 😄)

<details>
<summary><b>Click to reveal Answer 1</b></summary>

```sql
SELECT *
FROM student
ORDER BY age ASC;
```
</details>

<details>
<summary><b>Click to reveal Answer 2</b></summary>

```sql
SELECT *
FROM student
ORDER BY age DESC;
```
</details>

<details>
<summary><b>Click to reveal Answer 3</b></summary>

```sql
SELECT *
FROM student
ORDER BY name ASC;
```
</details>

<details>
<summary><b>Click to reveal Answer 4</b></summary>

```sql
SELECT *
FROM student
ORDER BY name DESC;
```
</details>

---

### 🎯 Homework (Real Placement Style)
Apni current `student` table me 3 naye students insert karo:
```sql
INSERT INTO student(id, name, age)
VALUES
(5, 'Karan', 23),
(6, 'Neha', 18),
(7, 'Vikas', 20);
```
Uske baad query chalao:
```sql
SELECT *
FROM student
ORDER BY age DESC;
```
*(Data zyada hone par sorting clearly visualize hogi!)*

---

## 🚀 What's Next? (Upcoming Teaser)
Next lecture covers **`LIMIT` Clause** (Interview & LeetCode/HackerRank Favorite ⭐⭐⭐⭐⭐):
- Top N Records
- First 3 Students
- Highest Age wala Student
- Lowest Age wale 2 Students