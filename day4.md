# SQL Practical — Day 4: Data Limitation, Pagination, Pattern Matching & Multi-Value Filtering

> **Overview:** Is day me hum SQL ke sabse important placement & interview concepts: `LIMIT` clause (Top N records), `LIMIT` with `OFFSET` (Nth Highest / Pagination), `LIKE` operator (`%` aur `_` wildcards), aur `IN` operator (Multiple `OR` alternative) ko practical breakdowns aur interview tips ke saath seekhenge.

---

## 📌 Syllabus & Covered Topics
1. ⏹️ **Lecture 11:** `LIMIT` Clause (Top N Records, Highest/Lowest Values)
2. 📑 **Lecture 12:** `LIMIT` with `OFFSET` (Nth Highest Value & Pagination) ⭐⭐⭐⭐⭐
3. 🔍 **Lecture 13:** `LIKE` Operator & `%` Wildcard (Starts with, Ends with, Contains)
4. 🎯 **Lecture 14:** `_` (Underscore) Wildcard (Single Character Matching)
5. 📥 **Lecture 15:** `IN` Operator (Multiple `OR` Alternative)

---

## ⏹️ Lecture 11: `LIMIT` (Top N Records)

### 💡 Core Concept & Need
Maan lo database table me **10 Lakh records** hain aur hume screen par sirf **pehle 5 records** dikhane hain. SQL poore 10 Lakh records fetch karne ke bajaye outputs ko limit karne ke liye **`LIMIT`** clause use karta hai.

- **Definition:** `LIMIT` decide karta hai ki query output grid me maximum kitni rows display honi chahiye.

---

### 💻 Basic Syntax & Examples

```sql
SELECT *
FROM student
LIMIT n;
```
*(Yahan `n` = Kitni rows return karni hain.)*

#### Example 1: `LIMIT 2`
```sql
SELECT *
FROM student
LIMIT 2;
```
**Output Grid:**
| id | name | age |
| :---: | :---: | :---: |
| 1 | Rahul | 20 |
| 2 | Aman | 21 |

#### Example 2: `LIMIT 3`
```sql
SELECT *
FROM student
LIMIT 3;
```
**Output Grid:**
| id | name | age |
| :---: | :---: | :---: |
| 1 | Rahul | 20 |
| 2 | Aman | 21 |
| 3 | Rohit | 22 |

---

### 🛍️ Real Life Example (Amazon Search)
Amazon par "iPhone" search karne par server ke paas 50,000 products hote hain, lekin screen par ek page par sirf 20 products dikhte hain:
```sql
SELECT *
FROM products
LIMIT 20;
```

---

### 🧠 Combining `ORDER BY` + `LIMIT` (Highest / Lowest Values)

> [!QUESTION]
> **Question:** Sabse **Highest Age** wala student kaise nikalein?  
> Kya sirf `SELECT * FROM student LIMIT 1;` run karne se Highest age record aayega?  
> ❌ **Nahi!** `LIMIT 1` bina sorting ke sirf pehli row return karega. Highest value ke liye pehle `ORDER BY` se sorting karni hogi, fir `LIMIT 1` lagana hoga.

#### 1. Highest Age Wala Student
```sql
SELECT *
FROM student
ORDER BY age DESC
LIMIT 1;
```
**Execution Breakdown:**
1. `ORDER BY age DESC` ➔ Table ko age ke descending order me arrange karega (22, 21, 20, 19, 18).
2. `LIMIT 1` ➔ Sorted table me se sabse pehle (highest) record ko return karega.

**Output Grid:**
| id | name | age |
| :---: | :---: | :---: |
| 3 | Rohit | 22 |

#### 2. Lowest Age Wala Student
```sql
SELECT *
FROM student
ORDER BY age ASC
LIMIT 1;
```
**Output:** `Neha (18)`

#### 3. Top 3 Highest Age Students
```sql
SELECT *
FROM student
ORDER BY age DESC
LIMIT 3;
```
**Output Ages:** `22`, `21`, `20`

---

### 🎤 Interview Trick: SQL Clauses Execution Order

> [!IMPORTANT]
> **Correct Clause Execution Order:**
> 1. `SELECT`
> 2. `FROM`
> 3. `WHERE`
> 4. `ORDER BY`
> 5. `LIMIT`

---

### ⚠️ Common Mistakes

> [!WARNING]
> - **WRONG ❌:**  
>   ```sql
>   SELECT * FROM student LIMIT 2 ORDER BY age;
>   ```
> - **CORRECT ✅:**  
>   ```sql
>   SELECT * FROM student ORDER BY age LIMIT 2;
>   ```
> *(Rule: `ORDER BY` clause hamesha `LIMIT` clause se PEHLE aata hai.)*

---

### ✍️ Practice Questions — Lecture 11

#### Question 1
Sirf pehle 3 students dikhao.

#### Question 2
Sabse highest age wala student dikhao.

#### Question 3
Sabse lowest age wale 2 students dikhao.

#### Question 4
Top 2 highest age wale students dikhao.

---

### ✅ Answers (Baad Me Match Karna 😄)

<details>
<summary><b>Click to reveal Answer 1</b></summary>

```sql
SELECT *
FROM student
LIMIT 3;
```
</details>

<details>
<summary><b>Click to reveal Answer 2</b></summary>

```sql
SELECT *
FROM student
ORDER BY age DESC
LIMIT 1;
```
</details>

<details>
<summary><b>Click to reveal Answer 3</b></summary>

```sql
SELECT *
FROM student
ORDER BY age ASC
LIMIT 2;
```
</details>

<details>
<summary><b>Click to reveal Answer 4</b></summary>

```sql
SELECT *
FROM student
ORDER BY age DESC
LIMIT 2;
```
</details>

---

## 📑 Lecture 12: `LIMIT` with `OFFSET` (Nth Highest & Pagination) ⭐⭐⭐⭐⭐

### 💡 Core Concept & Need
Jab interviewer tumse puche: *"Highest Salary / Age wala student nikal liya, ab 2nd Highest Age wala student nikal kar dikhao?"*  
Iske liye hum **`OFFSET`** concept use karte hain.

- **OFFSET Definition:** `OFFSET` ka matlab hota hai **Kitni Rows Skip Karni Hain** (`OFFSET = Skip`).

---

### 💻 Syntax
```sql
LIMIT offset, count;
-- OR (Alternative syntax)
LIMIT count OFFSET offset;
```
*(Standard Placement Syntax: `LIMIT offset, count` ➔ `offset` = Skip rows, `count` = Return rows).*

#### Example: `LIMIT 1, 1`
- `1` (First number) = **1 Row Skip karo**
- `1` (Second number) = **Agli 1 Row Return karo**

---

### 🧠 2nd Highest Age Calculation Breakdown

Given Dataset:
| id | name | age |
| :---: | :---: | :---: |
| 1 | Rahul | 20 |
| 2 | Aman | 21 |
| 3 | Rohit | 22 |
| 4 | Priya | 19 |
| 5 | Neha | 18 |
| 6 | Vikas | 25 |

Query:
```sql
SELECT *
FROM student
ORDER BY age DESC
LIMIT 1, 1;
```

**Step-by-step Evaluation:**
1. `ORDER BY age DESC` ➔ Vikas (25), Rohit (22), Aman (21), Rahul (20), Priya (19), Neha (18).
2. `LIMIT 1, 1` ➔ MySQL 1st row (`Vikas 25`) ko **Skip** karega, aur 2nd row (`Rohit 22`) ko **Return** karega.

**Output Grid:**
| id | name | age |
| :---: | :---: | :---: |
| 3 | Rohit | 22 |

---

### 📊 Nth Highest Queries & General Formula

#### 1. Third Highest Age (`LIMIT 2, 1`)
```sql
SELECT *
FROM student
ORDER BY age DESC
LIMIT 2, 1;
```
*(Skip 2 highest rows, return 1 row ➔ Aman 21)*

#### 2. Fourth Highest Age (`LIMIT 3, 1`)
```sql
SELECT *
FROM student
ORDER BY age DESC
LIMIT 3, 1;
```
*(Skip 3 highest rows, return 1 row ➔ Rahul 20)*

#### ⭐ General Nth Highest Formula
> [!IMPORTANT]
> **Nth Highest Formula:** `LIMIT N-1, 1`  
> - **5th Highest:** `LIMIT 4, 1`  
> - **6th Highest:** `LIMIT 5, 1`

---

### 📱 Real Life Example (Instagram Feed Pagination)
Instagram feed scrolling ke backend pagination queries:
- **Page 1 (First 10 posts):** `LIMIT 0, 10`
- **Page 2 (Next 10 posts):** `LIMIT 10, 10`
- **Page 3 (Next 10 posts):** `LIMIT 20, 10`

---

### 🎤 Interview Favorite Question

> [!IMPORTANT]
> **Q: How to find the Second Highest Salary in SQL?**  
> **Answer:**  
> ```sql
> SELECT *
> FROM employee
> ORDER BY salary DESC
> LIMIT 1, 1;
> ```

---

### ⚠️ Common Mistake

> [!WARNING]
> - **Mistake:** Writing `LIMIT 1;` thinking it returns the 2nd Highest.  
> - ❌ `LIMIT 1;` ➔ Returns the 1st Highest.  
> - ✅ `LIMIT 1, 1;` ➔ Skips 1st row and returns the 2nd Highest.

---

### ✍️ Practice Questions — Lecture 12

#### Question 1
Highest age wala student dikhao.

#### Question 2
Second highest age wala student dikhao.

#### Question 3
Third highest age wala student dikhao.

#### Question 4
Top 3 highest age wale students dikhao.

---

### ✅ Answers (Abhi Mat Dekhna 😄)

<details>
<summary><b>Click to reveal Answer 1</b></summary>

```sql
SELECT *
FROM student
ORDER BY age DESC
LIMIT 1;
```
</details>

<details>
<summary><b>Click to reveal Answer 2</b></summary>

```sql
SELECT *
FROM student
ORDER BY age DESC
LIMIT 1, 1;
```
</details>

<details>
<summary><b>Click to reveal Answer 3</b></summary>

```sql
SELECT *
FROM student
ORDER BY age DESC
LIMIT 2, 1;
```
</details>

<details>
<summary><b>Click to reveal Answer 4</b></summary>

```sql
SELECT *
FROM student
ORDER BY age DESC
LIMIT 3;
```
</details>

---

## 🔍 Lecture 13: `LIKE` Operator & `%` Wildcard

### 💡 Core Concept & Need
Jab exact string value pata na ho (`WHERE name = 'Aman';`), lekin pattern pata ho (e.g. *"Naam 'A' se start hota hai"*, *"Naam 'a' par end hota hai"*, *"Naam me 'oh' aata hai"*), tab pattern matching ke liye **`LIKE`** operator use hota hai.

- **Real Life Analogy:** Mobile contact search me `Ra` type karne par Rahul, Raj, Ramesh, Ravi sab show ho jate hain.

---

### 1️⃣ `%` (Percentage Wildcard)

#### 📜 Rule
`%` (Percentage Symbol) represents **0 or more characters** (`% = Anything / Unlimited Characters`).

#### 💻 Query Patterns & Examples

##### Pattern 1: Starts With ('A%')
```sql
SELECT *
FROM student
WHERE name LIKE 'A%';
```
- **Breakdown:** First character `A`, uske baad `%` (kuch bhi). Matches: `Aman`, `Amit`, `Ankit`.  
- **Output:** `Aman`

##### Pattern 2: Starts With ('R%') & Case-Sensitivity Note
```sql
SELECT *
FROM student
WHERE name LIKE 'R%';
```
- **Output:** `RAHUL`, `Rohit`
- 📌 **MySQL Collation Note:** Default settings me MySQL case-insensitive collation follow karta hai, isliye `'R%'` capital `R` aur small `r` dono se matching rows return kar deta hai.

##### Pattern 3: Ends With ('%a')
```sql
SELECT *
FROM student
WHERE name LIKE '%a';
```
- **Breakdown:** Pehle `%` (kuch bhi), end me `a` fixed.  
- **Output:** `Priya`

##### Pattern 4: Contains Substring ('%oh%')
```sql
SELECT *
FROM student
WHERE name LIKE '%oh%';
```
- **Breakdown:** Beginning me `%` (kuch bhi), beech me `oh`, end me `%` (kuch bhi).  
- **Output:** `Rohit`

---

### ⚠️ Common Mistakes

> [!WARNING]
> - `WHERE name = 'A%';` ❌ *(`=` checks for literal string "A%", pattern match nahi karta)*
> - `WHERE name LIKE 'A%';` ✅ *(Correct pattern matching syntax)*

---

### ✍️ Practice Questions — Lecture 13

#### Question 1
Jinka naam `P` se start hota hai unhe dikhao.

#### Question 2
Jinka naam `t` par end hota hai unhe dikhao.

#### Question 3
Jinke naam me `ma` aata hai unhe dikhao.

#### Question 4
Jinka naam `R` se start hota hai unhe dikhao.

---

### ✅ Answers (Baad Me Match Karna 😄)

<details>
<summary><b>Click to reveal Answer 1</b></summary>

```sql
SELECT *
FROM student
WHERE name LIKE 'P%';
```
</details>

<details>
<summary><b>Click to reveal Answer 2</b></summary>

```sql
SELECT *
FROM student
WHERE name LIKE '%t';
```
</details>

<details>
<summary><b>Click to reveal Answer 3</b></summary>

```sql
SELECT *
FROM student
WHERE name LIKE '%ma%';
```
</details>

<details>
<summary><b>Click to reveal Answer 4</b></summary>

```sql
SELECT *
FROM student
WHERE name LIKE 'R%';
```
</details>

---

## 🎯 Lecture 14: `_` (Underscore Wildcard)

### 💡 Core Concept & Definition
- **`_` (Underscore):** Represents **EXACTLY 1 character** (`_ = Exactly 1 Character`).
- **Difference:**
  - `%` ➔ `0` ya unlimited characters.
  - `_` ➔ Strictly `1` single character.

---

### 💻 Query Examples & Explanations

#### Example 1: `LIKE 'R__'`
```sql
SELECT *
FROM student
WHERE name LIKE 'R__';
```
- **Breakdown:** `R` + `_` + `_` ➔ First character `R`, followed by **exactly 2 characters** (Total length = 3 letters).
- **Match:** `Ram` ✅ (3 letters).
- **Mismatch:** `Ravi` ❌ (4 letters), `Rohit` ❌ (5 letters).

#### Example 2: `LIKE '____'`
```sql
SELECT *
FROM student
WHERE name LIKE '____';
```
- **Breakdown:** Exactly 4 underscores ➔ Names with **exactly 4 letters**.
- **Matches:** `Ravi`, `Neha`, `Aman`.

#### Example 3: `LIKE '__'`
```sql
SELECT *
FROM student
WHERE name LIKE '__';
```
- **Breakdown:** Exactly 2 letters (e.g. `Om`, `Al`).

---

### 📊 Comparison Table: `%` vs `_`

| Feature / Wildcard | `%` (Percentage) | `_` (Underscore) |
| :--- | :--- | :--- |
| **Character Count** | `0` ya unlimited characters | Strictly **Exactly 1 character** |
| **Matching Type** | Variable length matching | Fixed length matching |
| **Example Pattern** | `'A%'` ➔ `A`, `Am`, `Aman`, `Abhishek` | `'A__'` ➔ `Ary`, `Ami` (Strictly 3 letters) |

- **Real Life Analogy:** OTP verification pattern `5 _ 8 _` (Har underscore exactly single digit place karta hai).

---

### ✍️ Practice Questions — Lecture 14

#### Question 1
Exactly 5 letters wale names dikhao.

#### Question 2
`R` se start aur total 5 letters wale names dikhao.

#### Question 3
Exactly 4 letters wale names dikhao.

#### Question 4
`A` se start aur total 4 letters wale names dikhao.

---

### ✅ Answers (Baad Me Match Karna 😄)

<details>
<summary><b>Click to reveal Answer 1</b></summary>

```sql
SELECT *
FROM student
WHERE name LIKE '_____';
```
</details>

<details>
<summary><b>Click to reveal Answer 2</b></summary>

```sql
SELECT *
FROM student
WHERE name LIKE 'R____';
```
</details>

<details>
<summary><b>Click to reveal Answer 3</b></summary>

```sql
SELECT *
FROM student
WHERE name LIKE '____';
```
</details>

<details>
<summary><b>Click to reveal Answer 4</b></summary>

```sql
SELECT *
FROM student
WHERE name LIKE 'A___';
```
</details>

---

## 📥 Lecture 15: `IN` Operator (Multiple `OR` Alternative) ⭐⭐⭐⭐⭐

### 💡 Core Concept & Need
Agar hume Multiple values par equality check karni ho, to repetitive `OR` conditions likhne ke bajaye (`WHERE age=20 OR age=21 OR age=22`), cleaner way me **`IN`** operator use hota hai.

- **Definition:** `IN` ek column ki value ko multiple specified values ki list se compare karta hai (`IN = Multiple OR`).

---

### 💻 Syntax & Examples

```sql
SELECT *
FROM student
WHERE column_name IN (value1, value2, value3);
```

#### Example 1: Numeric List (`age IN (20, 22)`)
```sql
SELECT *
FROM student
WHERE age IN (20, 22);
```
**Output Grid:**
| id | name | age |
| :---: | :---: | :---: |
| 1 | RAHUL | 20 |
| 3 | Rohit | 22 |

#### Example 2: String List (`name IN ('RAHUL', 'Priya')`)
```sql
SELECT *
FROM student
WHERE name IN ('RAHUL', 'Priya');
```
**Output Grid:**
| id | name | age |
| :---: | :---: | :---: |
| 1 | RAHUL | 20 |
| 4 | Priya | 19 |

---

### ⚖️ Comparison: `OR` vs `IN`

```sql
-- Using OR (Longer):
SELECT * FROM student WHERE age = 20 OR age = 21 OR age = 22;

-- Using IN (Clean & Industry Standard):
SELECT * FROM student WHERE age IN (20, 21, 22);
```

> [!IMPORTANT]
> **Interview Question:** Is `WHERE age = 20 OR age = 21` identical to `WHERE age IN (20, 21)`?  
> **Answer:** **Yes!** Result 100% identical aayega. `IN` clause syntax readability aur query cleanliness improve karta hai.

---

### ⚠️ Common Mistakes

> [!WARNING]
> - `WHERE age IN 20, 21;` ❌ *(Parentheses `()` missing hain)*
> - `WHERE age IN (20, 21);` ✅ *(Correct)*
> - `WHERE name IN (Rahul, Aman);` ❌ *(Text values me single quotes missing hain)*
> - `WHERE name IN ('RAHUL', 'Aman');` ✅ *(Correct)*

---

### ✍️ Practice Questions — Lecture 15

#### Question 1
Age 20, 21 aur 22 wale students dikhao.

#### Question 2
Name `Aman` aur `Priya` wale students dikhao.

#### Question 3
ID 1 aur 3 wale students dikhao.

#### Question 4
Age 19 aur 20 wale students dikhao.

---

### ✅ Answers (Baad Me Match Karna 😄)

<details>
<summary><b>Click to reveal Answer 1</b></summary>

```sql
SELECT *
FROM student
WHERE age IN (20, 21, 22);
```
</details>

<details>
<summary><b>Click to reveal Answer 2</b></summary>

```sql
SELECT *
FROM student
WHERE name IN ('Aman', 'Priya');
```
</details>

<details>
<summary><b>Click to reveal Answer 3</b></summary>

```sql
SELECT *
FROM student
WHERE id IN (1, 3);
```
</details>

<details>
<summary><b>Click to reveal Answer 4</b></summary>

```sql
SELECT *
FROM student
WHERE age IN (19, 20);
```
</details>

---

### 🧠 Bonus Knowledge Teaser (`NOT IN`)
Agar 20 aur 21 ko **chhodkar** baaki sab students fetch karne hon:
```sql
SELECT *
FROM student
WHERE age NOT IN (20, 21);
```

---

## 📚 SQL Roadmap Summary
- ✅ Database & Table Creation (`CREATE DATABASE`, `USE`, `CREATE TABLE`)
- ✅ Data Operations (`INSERT`, `SELECT`, `WHERE`)
- ✅ Comparison & Logical Operators (`=`, `>`, `<`, `>=`, `<=`, `!=`, `AND`, `OR`, `NOT`)
- ✅ Data Sorting & Limitation (`ORDER BY ASC/DESC`, `LIMIT`, `LIMIT with OFFSET`)
- ✅ Pattern & Set Filtering (`LIKE '%'`, `LIKE '_'`, `IN`)
- 🚀 **Next Topics:** `NOT IN`, `BETWEEN`, `IS NULL`, `DISTINCT`, `UPDATE`, `DELETE`, `ALTER TABLE`, Aggregate Functions (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`).
/ OR / NOT
✅ ORDER BY
✅ LIMIT
✅ LIKE (%, _)
✅ IN

Next Lecture:

NOT IN
BETWEEN
IS NULL
DISTINCT

Uske baad hum UPDATE, DELETE, ALTER TABLE, aur phir Aggregate Functions (COUNT, SUM, AVG, MIN, MAX) start karenge.

Ek request: Ab se har naye topic me main purane topics ko mix karke queries dunga. Isi se tumhari SQL thinking develop hogi, jo interviews aur real projects dono me bahut kaam aati hai. 🚀
