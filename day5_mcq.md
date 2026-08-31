# Day 5 — Quick Revision + 30 MCQs

---

## Quick Revision

Before attempting the MCQs, let me quickly review all key concepts covered in `day5.md`.

### 1. Set Exclusion (`NOT IN` Operator)
- **Purpose:** Specified values ki list ko query output grid me se **exclude (chhod)** karne ke liye use hota hai (`NOT IN = Exclude List`).
- **`IN` vs `NOT IN`:**
  - **`IN` (Include List):** Sirf in specified values ko fetch karo (`WHERE age IN (20, 21)` ➔ Outputs 20, 21).
  - **`NOT IN` (Exclude List):** In specified values ko chhodkar baaki sab fetch karo (`WHERE age NOT IN (20, 21)` ➔ Outputs 19, 22).

### 2. Traditional `AND` vs `NOT IN` Syntax
- **Traditional (`!=` and `AND`):** `WHERE age != 20 AND age != 21;` (Lambi queries me complex aur error-prone).
- **Modern `NOT IN` Syntax:** `WHERE age NOT IN (20, 21);` (Clean, concise, industry standard).

### 3. Execution & Rules
- **Row-by-Row Execution:** MySQL checks each row against `NOT IN` list. If row value is present in list ➔ `FALSE` ❌ (Reject). If not present ➔ `TRUE` ✅ (Return).
- **String Literals:** Single quotes compulsory (`WHERE name NOT IN ('RAHUL', 'Aman')`).
- **Numeric Literals:** Bina quotes ke (`WHERE id NOT IN (1, 4)`).
- **Parentheses:** Round brackets `()` mandatory around values list (`WHERE age NOT IN (20, 21)`).

### 4. Common Traps & Mistakes
- ❌ `WHERE age NOT 20;` (Missing `IN` keyword and parentheses `()`)
- ❌ `WHERE name NOT IN (Rahul);` (Missing single quotes on string literal)
- ✅ `WHERE age NOT IN (20);`
- ✅ `WHERE name NOT IN ('RAHUL');`

### 5. Interview Corner (`NOT IN` Equivalence & Teaser)
- 🧠 **Equivalence:** Normal non-null values ke liye `WHERE age NOT IN (20, 21)` aur `WHERE age != 20 AND age != 21` 100% same results return karte hain.
- 🚀 **Upcoming Teaser:** `BETWEEN` operator for range filtering (`WHERE age BETWEEN 20 AND 22`).

---

## 30 Most Important MCQs

---

### Q1. Specified values ki list ko query output grid me se EXCLUDE (chhodne) ke liye kaunsa SQL operator use hota hai?

A. `IN`  
B. `NOT IN`  
C. `EXCLUDE`  
D. `REMOVE`  

**Answer:** B

**Explanation:** `NOT IN` clause specified list me di hui values ko ignore/exclude karke baaki sabhi matching records ko fetch karta hai.

---

### Q2. `IN` operator aur `NOT IN` operator mein fundamental difference kya hai?

A. `IN` fast hota hai, `NOT IN` slow hota hai  
B. `IN` specified values ko INCLUDE (select) karta hai, jabki `NOT IN` specified values ko EXCLUDE (chhod) karta hai  
C. `IN` numbers ke liye hai, `NOT IN` strings ke liye hai  
D. Dono identical hain  

**Answer:** B

**Explanation:** `IN` = Include specified values list, `NOT IN` = Exclude specified values list and return rest.

---

### Q3. Repetitive query `WHERE age != 20 AND age != 21;` ka cleaner, modern alternative syntax kya hoga?

A. `WHERE age NOT (20, 21);`  
B. `WHERE age NOT IN (20, 21);`  
C. `WHERE age IN (!20, !21);`  
D. `WHERE age EXCLUDE (20, 21);`  

**Answer:** B

**Explanation:** `WHERE age NOT IN (20, 21)` repetitive `!=` AND `!=` conditions ko single line clean syntax me combine kar deta hai.

---

### Q4. Target table (`student`): Rahul-20, Aman-21, Rohit-22, Priya-19. Niche di gayi query ka output kya aayega?

```sql
SELECT * FROM student WHERE age NOT IN (20, 21);
```

A. Rahul (20), Aman (21)  
B. Rohit (22), Priya (19)  
C. Saare students  
D. Blank output  

**Answer:** B

**Explanation:** Age 20 (Rahul) aur Age 21 (Aman) filter out ho jayenge. Isliye remaining records Rohit (22) aur Priya (19) return honge.

---

### Q5. Same dataset par, query `SELECT * FROM student WHERE name NOT IN ('RAHUL', 'Aman');` ka result kya hoga?

A. Rahul (20), Aman (21)  
B. Rohit (22), Priya (19)  
C. Sirf Priya (19)  
D. Error  

**Answer:** B

**Explanation:** Specified list `('RAHUL', 'Aman')` me names match hone ki wajah se Rahul aur Aman reject ho jayenge. Output me Rohit aur Priya aayenge.

---

### Q6. Common Mistake Alert: Niche diye gaye query filter me kya error hai?

```sql
SELECT * FROM student WHERE age NOT 20;
```

A. `WHERE` keyword galat hai  
B. `IN` keyword aur parentheses `()` missing hain  
C. `20` ko single quotes me likhna chahiye tha  
D. Query bilkul sahi hai  

**Answer:** B

**Explanation:** Correct syntax `WHERE age NOT IN (20);` hai. Without `IN` and `()`, `WHERE age NOT 20` Syntax Error dega.

---

### Q7. Common Mistake Alert: Query `SELECT * FROM student WHERE name NOT IN (Aman);` run karne par error kyun aayega?

A. `IN` operator string accept nahi karta  
B. String literal `Aman` single quotes `' '` me missing hai  
C. Parentheses galat hain  
D. Table name galat hai  

**Answer:** B

**Explanation:** SQL parsing rules ke according text literals ko single quotes `'Aman'` me likhna compulsory hota hai (`WHERE name NOT IN ('Aman')`).

---

### Q8. College Notice Analogy: College me notice aaya ki *"Rahul aur Aman presentation denge, baaki sab students free hain."* Free students ki list nikalne ki SQL query kya hogi?

A. `SELECT * FROM student WHERE name IN ('RAHUL', 'Aman');`  
B. `SELECT * FROM student WHERE name NOT IN ('RAHUL', 'Aman');`  
C. `SELECT * FROM student WHERE name = 'RAHUL';`  
D. `SELECT * FROM student WHERE name != FREE;`  

**Answer:** B

**Explanation:** Presentation dene wale students (`'RAHUL'`, `'Aman'`) ko `NOT IN` me filter karke remaining free students fetch kiye jayenge.

---

### Q9. Row-by-Row Execution Evaluation: `NOT IN (20, 21)` criteria evaluate karte waqt, agar candidate row ki age `22` hai, to boolean result kya hoga?

A. `FALSE` (Reject)  
B. `TRUE` (Return)  
C. `NULL`  
D. `ERROR`  

**Answer:** B

**Explanation:** `22 NOT IN (20, 21)` True evaluate hoga kyunki 22 list `(20, 21)` me present nahi hai.

---

### Q10. Row-by-Row Execution Evaluation: Candidate row ki age `20` hone par `20 NOT IN (20, 21)` ka boolean outcome kya hoga?

A. `TRUE` (Return)  
B. `FALSE` (Reject)  
C. `NULL`  
D. `ERROR`  

**Answer:** B

**Explanation:** 20 target list `(20, 21)` me present hai, isliye `NOT IN` False evaluate hoga aur row reject ho jayegi.

---

### Q11. Query Output Check: Dataset (Rahul-20, Aman-21, Rohit-22, Priya-19). Query:

```sql
SELECT * FROM student WHERE age NOT IN (19, 22);
```

Output me kaun-kaun se students aayenge?

A. Rohit (22), Priya (19)  
B. RAHUL (20), Aman (21)  
C. Sirf RAHUL (20)  
D. Saare students  

**Answer:** B

**Explanation:** Age 19 (Priya) aur Age 22 (Rohit) exclude ho jayenge. Remaining rows RAHUL (20) aur Aman (21) return honge.

---

### Q12. Query Output Check: Dataset (Rahul-20, Aman-21, Rohit-22, Priya-19). Query:

```sql
SELECT * FROM student WHERE name NOT IN ('Priya');
```

Output me kitni rows return hongi?

A. 1 Row  
B. 3 Rows (RAHUL, Aman, Rohit)  
C. 4 Rows  
D. 0 Rows  

**Answer:** B

**Explanation:** Single name 'Priya' exclude hoga, baaki remaining 3 students (RAHUL, Aman, Rohit) return honge.

---

### Q13. Query Output Check: Dataset (Rahul-id 1, Aman-id 2, Rohit-id 3, Priya-id 4). Query:

```sql
SELECT * FROM student WHERE id NOT IN (1, 4);
```

Output me kaun-kaun se IDs honge?

A. ID 1, ID 4  
B. ID 2, ID 3 (Aman, Rohit)  
C. ID 1, ID 2  
D. Empty  

**Answer:** B

**Explanation:** ID 1 aur ID 4 exclude hone par ID 2 (Aman) aur ID 3 (Rohit) return honge.

---

### Q14. Interview Question (Accenture / Mass Hiring): Normal non-null values ke liye, kya `WHERE age NOT IN (20, 21)` aur `WHERE age != 20 AND age != 21` 100% same results return karte hain?

A. Nahi, dono completely different results dete hain  
B. Haan, non-null values ke case me dono exact same result return karte hain  
C. `NOT IN` error throw karta hai  
D. `!=` AND `!=` fast hota hai  

**Answer:** B

**Explanation:** Normal non-null data par `NOT IN (20, 21)` is logically identical to `!= 20 AND != 21`.

---

### Q15. `NOT IN` clause me Multiple Numeric Values pass karte waqt valid format kya hai?

A. `WHERE age NOT IN 20 21;`  
B. `WHERE age NOT IN (20, 21);`  
C. `WHERE age NOT IN [20, 21];`  
D. `WHERE age NOT IN {20, 21};`  

**Answer:** B

**Explanation:** Numeric values comma-separated round brackets `(20, 21)` me specify ki jaati hain.

---

### Q16. `NOT IN` clause me Multiple String Values pass karte waqt valid format kya hai?

A. `WHERE name NOT IN ('Aman', 'Rohit');`  
B. `WHERE name NOT IN (Aman, Rohit);`  
C. `WHERE name NOT IN "Aman", "Rohit";`  
D. `WHERE name NOT IN ['Aman', 'Rohit'];`  

**Answer:** A

**Explanation:** Strings single quotes me parenthesized list `('Aman', 'Rohit')` me honi chahiye.

---

### Q17. Single Value Exclusion: Query `WHERE age NOT IN (21);` in me se kis expression ke identical kaam karegi?

A. `WHERE age = 21;`  
B. `WHERE age != 21;`  
C. `WHERE age > 21;`  
D. `WHERE age < 21;`  

**Answer:** B

**Explanation:** Single value list `NOT IN (21)` is identical to inequality `!= 21`.

---

### Q18. Output Table Check: Dataset (Rahul-20, Aman-21, Rohit-22, Priya-19). Query:

```sql
SELECT name FROM student WHERE age NOT IN (19, 20);
```

Output grid me kaun-kaun se names dikhenge?

A. RAHUL, Priya  
B. Aman, Rohit  
C. Aman, Priya  
D. Rohit, Priya  

**Answer:** B

**Explanation:** Age 19 (Priya) aur Age 20 (RAHUL) filter out ho jayenge. Remaining names Aman (21) aur Rohit (22) return honge.

---

### Q19. Output Table Check: Dataset (Rahul-20, Aman-21, Rohit-22, Priya-19). Query:

```sql
SELECT * FROM student WHERE id NOT IN (2, 3);
```

Output grid me kaun-kaun se IDs dikhenge?

A. ID 2, ID 3  
B. ID 1 (RAHUL), ID 4 (Priya)  
C. ID 1, ID 2  
D. ID 3, ID 4  

**Answer:** B

**Explanation:** ID 2 (Aman) aur ID 3 (Rohit) exclude hone par ID 1 (RAHUL) aur ID 4 (Priya) return honge.

---

### Q20. Tricky Scenario / Combined Clauses: Query execution evaluate karein:

```sql
SELECT name FROM student
WHERE age NOT IN (19)
ORDER BY age DESC;
```
*(Dataset: Rahul-20, Aman-21, Rohit-22, Priya-19)*

Output grid me top row par sabse pehla name kya hoga?

A. Priya (19)  
B. Rohit (22)  
C. Aman (21)  
D. Rahul (20)  

**Answer:** B

**Explanation:**  
1. `WHERE age NOT IN (19)` filters out Priya (19). Remaining: Rahul (20), Aman (21), Rohit (22).  
2. `ORDER BY age DESC` sorts remaining in descending age: Rohit (22), Aman (21), Rahul (20).  
3. Top row is Rohit.

---

### Q21. Tricky Scenario / Combined Clauses: Query execution evaluate karein:

```sql
SELECT name FROM student
WHERE age NOT IN (22)
ORDER BY age ASC
LIMIT 1;
```
*(Dataset: Rahul-20, Aman-21, Rohit-22, Priya-19)*

Output result kya hoga?

A. Rohit (22)  
B. Priya (19)  
C. Rahul (20)  
D. Aman (21)  

**Answer:** B

**Explanation:**  
1. `WHERE age NOT IN (22)` filters out Rohit (22). Remaining: Rahul (20), Aman (21), Priya (19).  
2. `ORDER BY age ASC` sorts ascending: Priya (19), Rahul (20), Aman (21).  
3. `LIMIT 1` picks the top row i.e. `Priya`.

---

### Q22. Pattern Matching + NOT IN Combination: Query execution analyze karein:

```sql
SELECT * FROM student
WHERE name LIKE 'R%' AND age NOT IN (20);
```
*(Dataset: Rahul-20, Aman-21, Rohit-22, Priya-19)*

Output me kaun aayega?

A. Rahul (20)  
B. Rohit (22)  
C. Rahul (20) aur Rohit (22)  
D. Aman (21)  

**Answer:** B

**Explanation:**  
1. `name LIKE 'R%'` matches Rahul (20) and Rohit (22).  
2. `AND age NOT IN (20)` excludes Rahul (20).  
3. Final output is strictly Rohit (22).

---

### Q23. Common Mistake Check: Which of the following SQL statements will cause a SYNTAX ERROR in MySQL?

A. `SELECT * FROM student WHERE age NOT IN (20, 21);`  
B. `SELECT * FROM student WHERE age NOT IN (20);`  
C. `SELECT * FROM student WHERE age NOT (20, 21);`  
D. `SELECT * FROM student WHERE name NOT IN ('Aman');`  

**Answer:** C

**Explanation:** `WHERE age NOT (20, 21)` me `IN` keyword missing hai, isliye syntax error aayega.

---

### Q24. Comparison Check: `WHERE age IN (20, 21)` aur `WHERE age NOT IN (20, 21)` ke results par kaunsa statement sahi hai?

A. Dono ke results 100% overlap karte hain  
B. Dono ke results mutually exclusive (ek dusre ke opposite) hain aur milkar complete dataset cover karte hain  
C. Dono identical rows return karte hain  
D. Dono syntax errors hain  

**Answer:** B

**Explanation:** `IN` target list ki rows fetch karta hai, jabki `NOT IN` remaining rows fetch karta hai.

---

### Q25. Placement Level Question: Agar database table me 1,000 employees hain aur hume Departments 10 aur 20 ke employees ko CHHODKAR baaki sabhi departments ke employees fetch karne hain, to efficient query filter kya hoga?

A. `WHERE dept_id = 10 AND dept_id = 20;`  
B. `WHERE dept_id NOT IN (10, 20);`  
C. `WHERE dept_id IN (10, 20);`  
D. `WHERE dept_id = 1020;`  

**Answer:** B

**Explanation:** Department IDs 10 aur 20 ko ignore/exclude karne ke liye `WHERE dept_id NOT IN (10, 20)` correct syntax hai.

---

### Q26. Dataset Check: Dataset (Rahul-20, Aman-21, Rohit-22, Priya-19). Query:

```sql
SELECT COUNT(*) FROM student WHERE age NOT IN (21);
```

Output count kya hoga?

A. 1  
B. 3  
C. 4  
D. 0  

**Answer:** B

**Explanation:** Age 21 (Aman) exclude hoga, bache huye 3 records (Rahul-20, Rohit-22, Priya-19) count honge.

---

### Q27. Syntax Check: Multiple String Exclusion query:

```sql
SELECT * FROM student WHERE name NOT IN ('Aman', 'Rohit');
```

Output me kaun-kaun se names return honge?  
*(Dataset: Rahul-20, Aman-21, Rohit-22, Priya-19)*

A. Aman, Rohit  
B. RAHUL, Priya  
C. RAHUL, Aman  
D. Rohit, Priya  

**Answer:** B

**Explanation:** Aman aur Rohit exclude kiye gaye hain, so RAHUL aur Priya return honge.

---

### Q28. Upcoming Topic Teaser Check: Day 5 notes ke end teaser ke according, Next Lecture me kaunsa range filtering operator padhaya jayega?

A. `LIKE`  
B. `BETWEEN` (e.g., `WHERE age BETWEEN 20 AND 22`)  
C. `GROUP BY`  
D. `HAVING`  

**Answer:** B

**Explanation:** Day 5 notes ke teaser section ke according, next upcoming topic `BETWEEN` range operator hai.

---

### Q29. Data Flow Check: Complete student dataset (19, 20, 21, 22) par `NOT IN (20, 21)` apply karne par filtered output array values kya hongi?

A. `(20, 21)`  
B. `(19, 22)`  
C. `(19, 20, 21, 22)`  
D. `()`  

**Answer:** B

**Explanation:** Values 20 aur 21 remove hone par array `(19, 22)` remain rahta hai.

---

### Q30. Final Synthesis Question: Niche diye gaye script ko analyze karke final output table ka result determine karein:

```sql
-- Student table: Rahul(20), Aman(21), Rohit(22), Priya(19)
SELECT name, age
FROM student
WHERE age NOT IN (19, 21)
ORDER BY age ASC;
```

Resulting output grid mein rows ka correct sequence kya hoga?

A. Rahul (20), then Rohit (22)  
B. Rohit (22), then Rahul (20)  
C. Aman (21), then Priya (19)  
D. Priya (19), then Rahul (20)  

**Answer:** A

**Explanation:**  
1. `WHERE age NOT IN (19, 21)` excludes Priya (19) and Aman (21). Remaining: Rahul (20), Rohit (22).  
2. `ORDER BY age ASC` sorts in ascending order: Rahul (20) first, then Rohit (22).  
Final output grid contains Rahul (20), followed by Rohit (22).
