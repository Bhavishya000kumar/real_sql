# Day 4 — Quick Revision + 30 MCQs

---

## Quick Revision

Before attempting the MCQs, let's quickly review all key concepts covered in `day4.md`.

### 1. Data Limitation (`LIMIT` Clause)
- **Purpose:** Decide maximum number of rows returned in the output grid (`SELECT * FROM table LIMIT n;`).
- **Highest / Lowest Value:** Must combine `ORDER BY` + `LIMIT 1`:
  - **Highest:** `ORDER BY col DESC LIMIT 1;`
  - **Lowest:** `ORDER BY col ASC LIMIT 1;`
- **Clause Order Hierarchy:** `SELECT` ➔ `FROM` ➔ `WHERE` ➔ `ORDER BY` ➔ `LIMIT`. (`ORDER BY` hamesha `LIMIT` se pehle aata hai).

### 2. `LIMIT` with `OFFSET` (Nth Highest & Pagination)
- **Syntax:** `LIMIT offset, count;` (`offset` = rows to skip, `count` = rows to return).
- **2nd Highest Value:** `ORDER BY col DESC LIMIT 1, 1;` (1 row skip, 1 row return).
- **Nth Highest Formula:** `LIMIT N-1, 1;` (5th highest = `LIMIT 4, 1`, 3rd highest = `LIMIT 2, 1`).
- **Pagination Concept:** Page 1 = `LIMIT 0, 10`, Page 2 = `LIMIT 10, 10`, Page 3 = `LIMIT 20, 10`.
- ⚠️ **Trap:** `LIMIT 1;` (1st Highest) vs `LIMIT 1, 1;` (2nd Highest).

### 3. Pattern Matching (`LIKE` Operator & `%` Wildcard)
- **Purpose:** Search pattern when exact string is unknown.
- **`%` (Percentage Symbol):** Represents **0 or more (unlimited) characters** (`% = Anything`).
  - **Starts with 'A':** `WHERE name LIKE 'A%';`
  - **Ends with 'a':** `WHERE name LIKE '%a';`
  - **Contains 'oh':** `WHERE name LIKE '%oh%';`
- 📌 **Collation Note:** MySQL default collation case-insensitive matching perform karta hai (`'R%'` matches `RAHUL` and `rohit`).
- ⚠️ **Trap:** `WHERE name = 'A%'` checks exact literal string `"A%"`, NOT pattern match. Pattern match ke liye `LIKE` operator mandatory hai.

### 4. Single Character Matching (`_` Underscore Wildcard)
- **`_` (Underscore):** Represents **EXACTLY 1 character** (`_ = Exactly 1 Character`).
- **Examples:**
  - `WHERE name LIKE 'R__';` ➔ Starts with R, exactly 3 letters total (`Ram`).
  - `WHERE name LIKE '____';` ➔ Exactly 4 letters long (`Ravi`, `Neha`).
  - `WHERE name LIKE 'A___';` ➔ Starts with A, exactly 4 letters total (`Aman`).
- **`%` vs `_` Summary:** `%` = Unlimited length matching | `_` = Fixed length single-character matching.

### 5. Multi-Value Filtering (`IN` Operator)
- **Purpose:** Column value ko multiple values ki list se compare karna (`IN = Multiple OR`).
- **Syntax:** `SELECT * FROM student WHERE age IN (20, 21, 22);`
- **Quotes & Brackets Rule:**
  - Numbers: `IN (20, 21, 22)` (No quotes)
  - Strings: `IN ('RAHUL', 'Aman')` (Single quotes mandatory)
  - Parentheses `()` mandatory.
- 💡 **`OR` vs `IN`:** `WHERE age = 20 OR age = 21` is 100% identical to `WHERE age IN (20, 21)`.
- 🧠 **Bonus:** `WHERE age NOT IN (20, 21);` (List me include na hone wale records fetch karta hai).

---

## 30 Most Important MCQs

---

### Q1. MySQL query execution result grid me output rows ko limit / cap karne ke liye kaunsa clause use hota hai?

A. `TOP`  
B. `MAX`  
C. `LIMIT`  
D. `CAP`  

**Answer:** C

**Explanation:** `LIMIT n` clause specify karta hai ki output result grid me maximum kitni rows display hongi (e.g., `LIMIT 5`).

---

### Q2. Table `student` me se sabse HIGHEST age wala student record fetch karne ke liye correct SQL query sequence kya hai?

A. `SELECT * FROM student LIMIT 1;`  
B. `SELECT * FROM student ORDER BY age DESC LIMIT 1;`  
C. `SELECT * FROM student ORDER BY age ASC LIMIT 1;`  
D. `SELECT * FROM student LIMIT 1 ORDER BY age DESC;`  

**Answer:** B

**Explanation:** Highest age value ke liye pehle `ORDER BY age DESC` se sorting karni padti hai, aur uske baad `LIMIT 1` se top record pick hota hai.

---

### Q3. Common Trap / Clause Order: SQL clauses ke syntax execution ka CORRECT order kaunsa hai?

A. `SELECT` ➔ `FROM` ➔ `LIMIT` ➔ `WHERE` ➔ `ORDER BY`  
B. `SELECT` ➔ `FROM` ➔ `WHERE` ➔ `ORDER BY` ➔ `LIMIT`  
C. `WHERE` ➔ `SELECT` ➔ `FROM` ➔ `ORDER BY` ➔ `LIMIT`  
D. `SELECT` ➔ `ORDER BY` ➔ `FROM` ➔ `LIMIT` ➔ `WHERE`  

**Answer:** B

**Explanation:** SQL clause syntax hierarchy strictly `SELECT` ➔ `FROM` ➔ `WHERE` ➔ `ORDER BY` ➔ `LIMIT` follow karti hai. `ORDER BY` hamesha `LIMIT` se pehle aata hai.

---

### Q4. Table `student` me se sabse LOWEST age wala student record fetch karne ki query kya hogi?

A. `SELECT * FROM student ORDER BY age DESC LIMIT 1;`  
B. `SELECT * FROM student ORDER BY age ASC LIMIT 1;`  
C. `SELECT * FROM student ORDER BY age LIMIT 0;`  
D. `SELECT * FROM student WHERE age = MIN;`  

**Answer:** B

**Explanation:** Lowest value ke liye `ORDER BY age ASC` (ascending) sort karke `LIMIT 1` add karte hain.

---

### Q5. `LIMIT offset, count` syntax mein `offset` keyword ka real-world meaning kya hota hai?

A. Kitni rows return karni hain  
B. Kitni rows skip karni hain  
C. Table name change karna  
D. Column count  

**Answer:** B

**Explanation:** `OFFSET` specify karta hai ki final output set return karne se pehle starting me se kitni rows ko skip (ignore) karna hai.

---

### Q6. Interview Classic Question (Accenture / Mass Hiring): `student` table se 2nd Highest Age wala record nikalne ke liye correct query kaunsi hai?

A. `SELECT * FROM student ORDER BY age DESC LIMIT 1;`  
B. `SELECT * FROM student ORDER BY age DESC LIMIT 1, 1;`  
C. `SELECT * FROM student ORDER BY age DESC LIMIT 2, 2;`  
D. `SELECT * FROM student ORDER BY age ASC LIMIT 1, 1;`  

**Answer:** B

**Explanation:** 2nd Highest ke liye pehle `ORDER BY age DESC` sort karte hain, fir `LIMIT 1, 1` (1 row skip karo, 1 row return karo) apply karte hain.

---

### Q7. Nth Highest General Formula: SQL me Nth Highest record fetch karne ka general `LIMIT` formula kya hai?

A. `LIMIT N, 1`  
B. `LIMIT N-1, 1`  
C. `LIMIT 1, N`  
D. `LIMIT N, N`  

**Answer:** B

**Explanation:** Nth Highest ke liye `LIMIT N-1, 1` formula use hota hai (e.g. 5th highest = `LIMIT 4, 1`, 3rd highest = `LIMIT 2, 1`).

---

### Q8. Tricky Output Question: Niche di gayi query ka output result kya hoga?

```sql
SELECT * FROM student
ORDER BY age DESC
LIMIT 2, 1;
```
*(Dataset sorted age DESC: Vikas-25, Rohit-22, Aman-21, Rahul-20, Priya-19, Neha-18)*

A. Vikas (25)  
B. Rohit (22)  
C. Aman (21)  
D. Rahul (20)  

**Answer:** C

**Explanation:** `LIMIT 2, 1` top 2 rows (`Vikas 25`, `Rohit 22`) ko skip karke 3rd highest record i.e. `Aman 21` return karega.

---

### Q9. Instagram / Amazon Pagination: Backend API request page 2 par next 10 posts fetch karne ke liye kaunsa `LIMIT` clause syntax run karegi?

A. `LIMIT 0, 10` (Page 1)  
B. `LIMIT 10, 10` (Page 2 - Skip 10, Return 10)  
C. `LIMIT 20, 10` (Page 3)  
D. `LIMIT 10`  

**Answer:** B

**Explanation:** Page 2 ke liye initial 10 posts skip hoti hain (`offset = 10`) aur next 10 posts return hoti hain (`count = 10`), i.e. `LIMIT 10, 10`.

---

### Q10. Accenture Placement Trap: Candidate ne 2nd Highest Salary query me `SELECT * FROM employee ORDER BY salary DESC LIMIT 1;` likha. Is query me kya problem hai?

A. Ye 2nd Highest nahi, balki 1st Highest (Top) Salary return karegi  
B. Query syntax error degi  
C. Output grid blank ho jayega  
D. Salary column delete ho jayega  

**Answer:** A

**Explanation:** `LIMIT 1` bina offset ke 1st row (highest) return karta hai. 2nd highest ke liye `LIMIT 1, 1` mandatory hai.

---

### Q11. SQL me pattern matching (jab exact value nahi pata ho, e.g. starts with 'A') ke liye kaunsa operator use hota hai?

A. `=`  
B. `LIKE`  
C. `IN`  
D. `MATCH`  

**Answer:** B

**Explanation:** Pattern matching ke liye `LIKE` operator wildcards (`%` aur `_`) ke saath use kiya jata hai.

---

### Q12. `LIKE` operator me `%` (Percentage) wildcard symbol ka kya meaning hai?

A. Exactly 1 character  
B. 0 ya usse zyada (unlimited) characters  
C. Exact 5 characters  
D. Only numeric digits  

**Answer:** B

**Explanation:** `%` wildcard 0 ya unlimited characters ko represent karta hai (`% = Anything`).

---

### Q13. Query `SELECT * FROM student WHERE name LIKE 'A%';` kaunse records ko match karke fetch karegi?

A. Jo naam 'A' par end hote hain  
B. Jo naam 'A' se start hote hain (e.g. Aman, Amit, Ankit)  
C. Jinke naam me exactly 1 letter 'A' ho  
D. Saare names  

**Answer:** B

**Explanation:** `'A%'` pattern ka matlab hai: Pehla letter 'A' aur uske baad `%` (kuch bhi). So 'A' se start hone wale sabhi names match honge.

---

### Q14. Query `SELECT * FROM student WHERE name LIKE '%a';` kaunse names return karegi?

A. Jo 'a' se start hote hain  
B. Jo 'a' par end hote hain (e.g. Priya, Neha)  
C. Jinke beech me 'a' ho  
D. Jinke length 1 character ho  

**Answer:** B

**Explanation:** `'%a'` pattern me pehle `%` (anything) hai aur last me `a` fixed hai, so 'a' par end hone wale names match honge.

---

### Q15. Query `SELECT * FROM student WHERE name LIKE '%oh%';` ka kya filter criteria hai?

A. Naam 'oh' se start hona chahiye  
B. Naam 'oh' par end hona chahiye  
C. Naam ke kisi bhi part ke andar 'oh' substring hona chahiye (e.g. Rohit)  
D. Naam exactly 'oh' hona chahiye  

**Answer:** C

**Explanation:** `'%oh%'` substring contains criteria hai: pehle kuch bhi, beech me 'oh', aur baad me kuch bhi.

---

### Q16. MySQL default collation settings mein `'R%'` pattern query uppercase `'RAHUL'` aur lowercase `'rohit'` dono ko select kar leti hai. Why?

A. MySQL LIKE operator broken hai  
B. Default MySQL collation case-insensitive hota hai  
C. `R` aur `r` numbers hain  
D. Query me error hai  

**Answer:** B

**Explanation:** Standard MySQL default collation case-insensitive matching follow karta hai.

---

### Q17. Common Trap: Query `SELECT * FROM student WHERE name = 'A%';` ka kya result aayega?

A. Aman, Amit return honge  
B. MySQL exact literal string "A%" search karega (jo shayad table me na ho)  
C. Error aa jayega  
D. Saare students return honge  

**Answer:** B

**Explanation:** `=` comparison operator pattern matching nahi karta, wo exact literal text `"A%"` match karta hai. Pattern matching ke liye `LIKE` operator zaroori hai (`WHERE name LIKE 'A%'`).

---

### Q18. `LIKE` operator me Underscore (`_`) wildcard symbol ka kya strictly defined rule hai?

A. 0 ya unlimited characters  
B. Exactly 1 single character (`_ = 1 Character`)  
C. Exact 10 characters  
D. Spaces only  

**Answer:** B

**Explanation:** `_` (Underscore) strictly single character place match karta hai.

---

### Q19. Query `SELECT * FROM student WHERE name LIKE 'R__';` kaunse names ko match karegi?

A. R se start hone wale saare names (regardless of length)  
B. R se start hone wale EXACTLY 3 letters wale names (e.g. Ram)  
C. R par end hone wale names  
D. Exactly 2 letters wale names  

**Answer:** B

**Explanation:** `'R__'` means `R` + `1 char` + `1 char` = Strictly 3 letters total starting with R.

---

### Q20. Query `SELECT * FROM student WHERE name LIKE '____';` (4 underscores) ka expected result kya hai?

A. Exactly 4 letters wale sabhi names (e.g. Ravi, Neha, Aman)  
B. 4 se zyada letters wale names  
C. 4 se kam letters wale names  
D. Error  

**Answer:** A

**Explanation:** 4 underscores (`____`) strictly 4-letter long names matching return karegi.

---

### Q21. Difference Check (`%` vs `_`): `LIKE 'A%'` aur `LIKE 'A__'` me kya main difference hai?

A. Dono bilkul same hain  
B. `'A%'` A se start hone wale kisi bhi length ke names match karega, jabki `'A__'` strictly A se start hone wale 3-letter names match karega  
C. `'A__'` fast execute hota hai  
D. `'A%'` syntax error hai  

**Answer:** B

**Explanation:** `%` unlimited length matching deta hai, jabki `_` fixed-length single-character matching deta hai.

---

### Q22. Real-world OTP Analogy: Pattern `5 _ 8 _` kis wildcard concept ko illustrate karta hai?

A. Percentage `%` wildcard  
B. Underscore `_` wildcard (jahan har `_` exactly 1 digit/character place ko fill karta hai)  
C. `IN` operator  
D. `ORDER BY`  

**Answer:** B

**Explanation:** Har `_` single character placeholder ki tarah behave karta hai.

---

### Q23. Query `SELECT * FROM student WHERE name LIKE 'A___';` (A followed by 3 underscores) ka target match kya hoga?

A. Aman (4 letters starting with A)  
B. Abhishek (8 letters)  
C. Al (2 letters)  
D. Rahul (5 letters)  

**Answer:** A

**Explanation:** `'A___'` total 4-letter long names search karega starting with A (e.g., Aman).

---

### Q24. Multiple `OR` conditions ko concise, clean aur readable syntax me convert karne ke liye kaunsa SQL operator use hota hai?

A. `LIKE`  
B. `IN`  
C. `BETWEEN`  
D. `LIMIT`  

**Answer:** B

**Explanation:** `IN` operator column value ko list of values se equality check karta hai (`IN = Multiple OR`).

---

### Q25. Query `SELECT * FROM student WHERE age IN (20, 22);` ka equivalent `OR` syntax query kya hoga?

A. `SELECT * FROM student WHERE age = 20 AND age = 22;`  
B. `SELECT * FROM student WHERE age = 20 OR age = 22;`  
C. `SELECT * FROM student WHERE age LIKE (20, 22);`  
D. `SELECT * FROM student WHERE age = 2022;`  

**Answer:** B

**Explanation:** `WHERE age IN (20, 22)` is logically identical to `WHERE age = 20 OR age = 22`.

---

### Q26. Syntax Check: `IN` operator me String list pass karte waqt konsa format 100% CORRECT hai?

A. `WHERE name IN (Rahul, Aman);` ❌  
B. `WHERE name IN ('RAHUL', 'Aman');` ✅  
C. `WHERE name IN 'RAHUL', 'Aman';` ❌  
D. `WHERE name IN ['RAHUL', 'Aman'];` ❌  

**Answer:** B

**Explanation:** `IN` clause me string literals single quotes me parenthesized list `('RAHUL', 'Aman')` me hone chahiye.

---

### Q27. Syntax Check: `IN` operator me Numeric list pass karte waqt konsa format 100% CORRECT hai?

A. `WHERE age IN 20, 21;` ❌  
B. `WHERE age IN (20, 21);` ✅  
C. `WHERE age IN [20, 21];` ❌  
D. `WHERE age IN '20, 21';` ❌  

**Answer:** B

**Explanation:** Numeric values bina quotes ke round parentheses `(20, 21)` me specify honi chahiye.

---

### Q28. Real Project Combined Query Scenario: Niche di gayi SQL query ka result aur clause ordering check karein:

```sql
SELECT name, age
FROM student
WHERE age IN (20, 21)
ORDER BY age DESC
LIMIT 2;
```

Kya ye query syntax-wise 100% valid hai?

A. Nahi, `IN` aur `LIMIT` ek saath use nahi ho sakte  
B. Haan, bilkul valid hai aur correct execution order (`SELECT` ➔ `FROM` ➔ `WHERE` ➔ `ORDER BY` ➔ `LIMIT`) follow karti hai  
C. Nahi, `WHERE` se pehle `ORDER BY` aana chahiye  
D. Nahi, `LIMIT` start me hona chahiye  

**Answer:** B

**Explanation:** Query 100% valid hai aur multiple clauses se combine hokar correct standard order me structured hai.

---

### Q29. Bonus Knowledge Check (`NOT IN`): Agar hume age 20 aur 21 ko CHHODKAR baaki saare students fetch karne hon, to query kya hogi?

A. `SELECT * FROM student WHERE age IN (20, 21);`  
B. `SELECT * FROM student WHERE age NOT IN (20, 21);`  
C. `SELECT * FROM student WHERE age != (20, 21);`  
D. `SELECT * FROM student WHERE NOT age;`  

**Answer:** B

**Explanation:** `NOT IN` clause specified list me include na hone wale records ko filter out kar ke baaki rows select karta hai.

---

### Q30. Synthesis Scenario: Niche diye gaye 3 execution steps ko evaluate karke final output identify karein:

```sql
-- Table contains: Rahul-20, Aman-21, Rohit-22, Priya-19, Neha-18, Vikas-25
SELECT name
FROM student
WHERE name LIKE '%a%' OR name LIKE '%A%'
ORDER BY age DESC
LIMIT 1, 1;
```

Query ka outcome kya hoga?

A. Vikas (25)  
B. Aman (21)  
C. Rahul (20)  
D. Priya (19)  

**Answer:** B

**Explanation:**  
1. `WHERE name LIKE '%a%' OR name LIKE '%A%'` filters names containing 'a'/'A': Vikas (25), Aman (21), Rahul (20), Priya (19), Neha (18). (Rohit has no 'a'/'A' so filtered out).  
2. `ORDER BY age DESC` sorts remaining filtered: Vikas (25), Aman (21), Rahul (20), Priya (19), Neha (18).  
3. `LIMIT 1, 1` skips 1st row (`Vikas 25`) and returns 2nd row i.e. `Aman (21)`.  
Final output is strictly `Aman`.
