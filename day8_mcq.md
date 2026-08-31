# Day 8 — Quick Revision + 30 MCQs

---

## Quick Revision

Before attempting the MCQs, let's quickly review all key concepts covered in `day8.md`.

### 1. `HAVING` Clause Overview
- **Purpose:** `GROUP BY` ke baad aggregated summary groups ko conditions ke basis par filter karna.
- **Rule:** `HAVING` behaves at the **GROUP level**, whereas `WHERE` behaves at the **ROW level**.

### 2. `WHERE` vs `HAVING` Master Differences
- **`WHERE`:** Filters individual rows BEFORE grouping. Cannot use Aggregate Functions (`WHERE COUNT(*) > 2` ❌).
- **`HAVING`:** Filters summary groups AFTER grouping. Can use Aggregate Functions (`HAVING COUNT(*) > 2` ✅).

### 3. Logical Query Execution Order
- `FROM` ➔ `WHERE` ➔ `GROUP BY` ➔ `HAVING` ➔ `SELECT` ➔ `ORDER BY` ➔ `LIMIT`.

### 4. Common Syntax Rules & Traps
- `HAVING` without `GROUP BY` cannot evaluate group metrics.
- Plain row conditions (`city = 'Delhi'`) belong in `WHERE`, not `HAVING`.
- Aggregate filtering (`HAVING AVG(age) > 20`, `HAVING COUNT(*) >= 2`, `HAVING MAX(age) >= 21`).

---

## 30 Most Important MCQs

---

### Q1. SQL me `HAVING` clause ka primary objective kya hota hai?

A. Individual rows ko filter karna  
B. `GROUP BY` se bane aggregated summary GROUPS ko filter karna  
C. Output rows ko sort karna  
D. Database table drop karna  

**Answer:** B

**Explanation:** `HAVING` clause aggregate conditions (`COUNT`, `AVG`, `SUM`) ke according formed groups ko filter karta hai.

---

### Q2. Interview Favorite Question: `WHERE` clause aur `HAVING` clause me fundamental difference kya hai?

A. `WHERE` fast hota hai, `HAVING` slow hota hai  
B. `WHERE` individual rows ko filter karta hai, jabki `HAVING` aggregated groups ko filter karta hai  
C. `HAVING` `GROUP BY` se pehle run hota hai  
D. Dono exact identical hain  

**Answer:** B

**Explanation:** `WHERE` operates on row-level before grouping, while `HAVING` operates on group-level after grouping.

---

### Q3. Aggregate functions (`COUNT(*)`, `AVG()`, `SUM()`) ko kis clause me USE NAHI KIYA JA SAKTA?

A. `HAVING`  
B. `SELECT`  
C. `WHERE` ❌  
D. `ORDER BY`  

**Answer:** C

**Explanation:** `WHERE` clause individual rows evaluate karta hai execution step me before aggregation, isliye `WHERE` me aggregate functions invalid hote hain (`WHERE COUNT(*) > 2` ❌ Syntax Error).

---

### Q4. Correct Syntax Execution Order me `HAVING` clause kis position par execute hota hai?

A. `FROM` se pehle  
B. `WHERE` se pehle  
C. `GROUP BY` ke BAAD aur `SELECT` / `ORDER BY` se PEHLE  
D. Query ke end me `LIMIT` ke baad  

**Answer:** C

**Explanation:** Execution sequence: `FROM` ➔ `WHERE` ➔ `GROUP BY` ➔ `HAVING` ➔ `SELECT` ➔ `ORDER BY` ➔ `LIMIT`.

---

### Q5. Query Error Check: Niche di gayi SQL query invalid/error-prone kyun hai?
```sql
SELECT city, COUNT(*) FROM student WHERE COUNT(*) >= 2 GROUP BY city;
```

A. `SELECT` galat hai  
B. `COUNT(*)` aggregate function `WHERE` clause me use hua hai (Use `HAVING COUNT(*) >= 2`)  
C. `GROUP BY` clause invalid hai  
D. Query 100% valid hai  

**Answer:** B

**Explanation:** Aggregate expressions `WHERE` clause me evaluate nahi ho sakte. Correct code `GROUP BY city HAVING COUNT(*) >= 2` hona chahiye.

---

### Q6. Query Error Check: Niche di gayi query me kya problem hai?
```sql
SELECT city, COUNT(*) FROM student HAVING COUNT(*) >= 2;
```

A. `WHERE` missing hai  
B. `GROUP BY` clause missing hai, so `HAVING` test target groups create hi nahi ho sake  
C. `HAVING` operator string condition hai  
D. `COUNT(*)` invalid hai  

**Answer:** B

**Explanation:** `HAVING` clause target groups ko filter karne ke liye `GROUP BY` clause par dependent hota hai.

---

### Q7. Query Output Evaluation: Dataset (Delhi-3 students, Mumbai-2 students, Pune-1 student). Query:
```sql
SELECT city, COUNT(*) FROM student GROUP BY city HAVING COUNT(*) >= 2;
```
Output result me kaun-kaun se cities aayenge?

A. Delhi, Mumbai, Pune  
B. Delhi, Mumbai (Pune is filtered out because count 1 < 2)  
C. Sirf Delhi  
D. Pune  

**Answer:** B

**Explanation:** `HAVING COUNT(*) >= 2` Pune (count 1) ko filter out kar dega. Delhi (3) aur Mumbai (2) return honge.

---

### Q8. Average Age Filter: Sirf un cities ko display karne ki query jahan average age > 20 ho:

A. `SELECT city, AVG(age) FROM student GROUP BY city HAVING AVG(age) > 20;`  
B. `SELECT city, AVG(age) FROM student WHERE AVG(age) > 20 GROUP BY city;`  
C. `SELECT city FROM student WHERE age > 20;`  
D. `SELECT AVG(age) FROM student HAVING city > 20;`  

**Answer:** A

**Explanation:** Grouped average age condition `HAVING AVG(age) > 20` correct syntax is option A.

---

### Q9. Maximum Age Filter: Sirf un cities ko fetch karne ki query jahan max age >= 21 ho:

A. `SELECT city, MAX(age) FROM student GROUP BY city HAVING MAX(age) >= 21;`  
B. `SELECT city, MAX(age) FROM student WHERE MAX(age) >= 21 GROUP BY city;`  
C. `SELECT city FROM student HAVING age >= 21;`  
D. `SELECT MAX(age) FROM student WHERE city >= 21;`  

**Answer:** A

**Explanation:** `HAVING MAX(age) >= 21` after `GROUP BY city` gives maximum age filtering per city.

---

### Q10. E-commerce Backend Query: Sirf un Brands ko fetch karna jinke Total Products > 100 hon:

A. `SELECT brand, COUNT(*) FROM products GROUP BY brand HAVING COUNT(*) > 100;`  
B. `SELECT brand, COUNT(*) FROM products WHERE COUNT(*) > 100 GROUP BY brand;`  
C. `SELECT brand FROM products WHERE products > 100;`  
D. `SELECT COUNT(*) FROM products HAVING brand > 100;`  

**Answer:** A

**Explanation:** Brand level count filtering requires `GROUP BY brand HAVING COUNT(*) > 100`.

---

### Q11. Which SQL clause is evaluated FIRST by MySQL?

A. `WHERE`  
B. `FROM`  
C. `HAVING`  
D. `SELECT`  

**Answer:** B

**Explanation:** Logical Execution Hierarchy starts with `FROM` clause to identify the data source table.

---

### Q12. Which SQL clause is evaluated LAST among the following?

A. `WHERE`  
B. `GROUP BY`  
C. `HAVING`  
D. `LIMIT`  

**Answer:** D

**Explanation:** `LIMIT` clause execution pipeline ke sabse end me output rows cap karta hai.

---

### Q13. Plain Row Filter vs Group Filter Best Practice: Query `WHERE city = 'Delhi'` vs `HAVING city = 'Delhi'` ke regarding kaunsa statement TRUE hai?

A. `HAVING city = 'Delhi'` accurate & fast performance hai  
B. Row filtering conditions (`city = 'Delhi'`) ko `WHERE` clause me likhna industry best practice hai (Performance optimal)  
C. Dono invalid syntax hain  
D. `HAVING` row filtering me fast hota hai  

**Answer:** B

**Explanation:** Row level static column filters `WHERE` me evaluate karne chahiye taaki grouping se pehle unwanted rows discard ho skein (faster performance).

---

### Q14. Combined Query Breakdown: Query analyze karein:
```sql
SELECT city, COUNT(*)
FROM student
WHERE age >= 20
GROUP BY city
HAVING COUNT(*) >= 2;
```
First step execution kya hoga?

A. `HAVING COUNT(*) >= 2`  
B. `FROM student` (Table load)  
C. `WHERE age >= 20` (Row filtering)  
D. `GROUP BY city`  

**Answer:** B

**Explanation:** Logical execution strictly starts with `FROM student`.

---

### Q15. Same Combined Query: `WHERE age >= 20` filter kis step ke pehle apply hoga?

A. `GROUP BY city` se PEHLE  
B. `HAVING` ke BAAD  
C. `SELECT` ke BAAD  
D. `LIMIT` ke BAAD  

**Answer:** A

**Explanation:** `WHERE` clause individual rows ko grouping se PEHLE filter out kar deta hai.

---

### Q16. Syntax Check: Which statement is 100% VALID SQL?

A. `SELECT city, SUM(age) FROM student GROUP BY city HAVING SUM(age) > 50;`  
B. `SELECT city, SUM(age) FROM student WHERE SUM(age) > 50 GROUP BY city;`  
C. `SELECT city FROM student HAVING SUM(age) > 50;` (Missing GROUP BY)  
D. `HAVING SUM(age) > 50 SELECT city FROM student;`  

**Answer:** A

**Explanation:** Option A follows exact syntax hierarchy: `SELECT ... FROM ... GROUP BY ... HAVING ...`.

---

### Q17. Alias in HAVING Clause (MySQL Feature): Query `SELECT city, COUNT(*) AS total FROM student GROUP BY city HAVING total >= 2;` MySQL me executable hai?

A. Haan, MySQL `HAVING` clause me column alias (`total`) permit karta hai  
B. Nahi, syntax error aayega  
C. Only Oracle allows it  
D. SQL me aliases forbidden hote hain  

**Answer:** A

**Explanation:** Standard MySQL extensions allow using column aliases declared in `SELECT` list inside `HAVING` and `ORDER BY` clauses.

---

### Q18. Count Ascending/Descending: Grouped counts ko Highest to Lowest display karne ki query:

A. `SELECT city, COUNT(*) FROM student GROUP BY city ORDER BY COUNT(*) DESC;`  
B. `SELECT city, COUNT(*) FROM student GROUP BY city HAVING COUNT(*) DESC;`  
C. `SELECT city FROM student SORT BY COUNT(*);`  
D. `SELECT COUNT(*) FROM student ORDER BY city;`  

**Answer:** A

**Explanation:** Sorting grouped output set requires `ORDER BY COUNT(*) DESC` after `GROUP BY city`.

---

### Q19. `HAVING` Clause without Aggregate Function: Query `SELECT city FROM student GROUP BY city HAVING city = 'Delhi';` ka behavior kya hoga?

A. Error dega  
B. Valid execution hai par poor design practice hai (Row condition `WHERE` me honi chahiye)  
C. Data corrupt kar dega  
D. Table drop ho jayegi  

**Answer:** B

**Explanation:** Technically valid in MySQL, but bad design practice because non-aggregate row filters should be placed in `WHERE` clause before grouping.

---

### Q20. Placement Scenario: Find departments having Total Salary expenditure > 500,000:

A. `SELECT dept, SUM(salary) FROM emp GROUP BY dept HAVING SUM(salary) > 500000;`  
B. `SELECT dept, SUM(salary) FROM emp WHERE SUM(salary) > 500000 GROUP BY dept;`  
C. `SELECT dept FROM emp WHERE salary > 500000;`  
D. `SELECT SUM(salary) FROM emp HAVING dept > 500000;`  

**Answer:** A

**Explanation:** Department total salary threshold filtering strictly uses `GROUP BY dept HAVING SUM(salary) > 500000`.

---

### Q21. Complete Execution Chain Order Check: Correct sequence is:

A. `FROM` ➔ `WHERE` ➔ `GROUP BY` ➔ `HAVING` ➔ `SELECT` ➔ `ORDER BY` ➔ `LIMIT`  
B. `SELECT` ➔ `FROM` ➔ `WHERE` ➔ `HAVING` ➔ `GROUP BY`  
C. `FROM` ➔ `SELECT` ➔ `WHERE` ➔ `GROUP BY` ➔ `HAVING`  
D. `WHERE` ➔ `FROM` ➔ `GROUP BY` ➔ `HAVING` ➔ `SELECT`  

**Answer:** A

**Explanation:** Standard MySQL logical query execution hierarchy starts at `FROM` and ends at `LIMIT`.

---

### Q22. Practice Question Answer Check: Q1 answer (`jahan 2 ya usse zyada students hain`):

A. `SELECT city, COUNT(*) FROM student GROUP BY city HAVING COUNT(*) >= 2;`  
B. `SELECT city FROM student WHERE COUNT(*) >= 2;`  
C. `SELECT COUNT(*) FROM student GROUP BY city;`  
D. `SELECT city FROM student HAVING count >= 2;`  

**Answer:** A

**Explanation:** Option A specifies `GROUP BY city HAVING COUNT(*) >= 2`.

---

### Q23. Practice Question Answer Check: Q2 answer (`average age 20 se zyada hai`):

A. `SELECT city, AVG(age) FROM student GROUP BY city HAVING AVG(age) > 20;`  
B. `SELECT city FROM student WHERE age > 20;`  
C. `SELECT AVG(age) FROM student HAVING age > 20;`  
D. `SELECT city FROM student GROUP BY city WHERE AVG(age) > 20;`  

**Answer:** A

**Explanation:** Option A correctly combines `GROUP BY city` with `HAVING AVG(age) > 20`.

---

### Q24. Practice Question Answer Check: Q3 answer (`maximum age 22 hai`):

A. `SELECT city, MAX(age) FROM student GROUP BY city HAVING MAX(age) = 22;`  
B. `SELECT city FROM student WHERE age = 22;`  
C. `SELECT MAX(age) FROM student HAVING age = 22;`  
D. `SELECT city FROM student GROUP BY MAX(age) = 22;`  

**Answer:** A

**Explanation:** Option A specifies `GROUP BY city HAVING MAX(age) = 22`.

---

### Q25. Group Filter Evaluation: Dataset (Delhi avg age: 20, Mumbai avg age: 21, Pune avg age: 21). Query:
```sql
SELECT city, AVG(age) FROM student GROUP BY city HAVING AVG(age) > 20;
```
Output me kaun-kaun se cities aayenge?

A. Delhi, Mumbai, Pune  
B. Mumbai, Pune (Delhi is 20, not > 20)  
C. Sirf Delhi  
D. None  

**Answer:** B

**Explanation:** Delhi average age is 20. Condition is strictly `> 20`, so Delhi is excluded. Mumbai (21) and Pune (21) return.

---

### Q26. Can `WHERE` and `HAVING` be used TOGETHER in the same query?

A. No, never  
B. Yes, `WHERE` filters rows before grouping and `HAVING` filters groups after grouping  
C. Only in subqueries  
D. Only with `LIMIT`  

**Answer:** B

**Explanation:** `WHERE` and `HAVING` can be seamlessly combined in a single query (e.g. `WHERE age >= 18 GROUP BY city HAVING COUNT(*) >= 2`).

---

### Q27. Interview Definition: `HAVING` clause execution sequence timing:

A. Before `FROM`  
B. After `GROUP BY` and before `SELECT`  
C. After `ORDER BY`  
D. Before `WHERE`  

**Answer:** B

**Explanation:** `HAVING` executes right after `GROUP BY` aggregates formed groups, and before `SELECT` projects final output columns.

---

### Q28. What happens if `HAVING` condition evaluates to `FALSE` for a group?

A. The entire table is deleted  
B. That specific group is discarded/omitted from the output result set  
C. An error is returned  
D. NULL is printed  

**Answer:** B

**Explanation:** `HAVING` filters out groups whose condition evaluates to FALSE or UNKNOWN.

---

### Q29. Output Count Check: Table has 3 cities (Delhi-5, Mumbai-4, Pune-1). Query: `SELECT city FROM student GROUP BY city HAVING COUNT(*) > 3;` How many rows in output grid?

A. 3  
B. 2 (Delhi: 5, Mumbai: 4)  
C. 1  
D. 0  

**Answer:** B

**Explanation:** Delhi (5 > 3) and Mumbai (4 > 3) pass. Pune (1 > 3) fails. Output has 2 rows.

---

### Q30. Synthesis Scenario: Evaluate execution result of following query:
```sql
-- Student table: Rahul(20, Delhi), Aman(21, Delhi), Priya(19, Delhi), Rohit(22, Mumbai), Neha(20, Mumbai)
SELECT city, COUNT(*) AS count
FROM student
WHERE age >= 20
GROUP BY city
HAVING COUNT(*) >= 2;
```
Output grid contains:

A. Delhi: 2, Mumbai: 2  
B. Delhi: 3, Mumbai: 2  
C. Delhi: 2  
D. Mumbai: 2  

**Answer:** A

**Explanation:**  
1. `WHERE age >= 20` removes Priya (19). Remaining: Rahul (20, Delhi), Aman (21, Delhi), Rohit (22, Mumbai), Neha (20, Mumbai).  
2. `GROUP BY city`:  
   - Delhi Group ➔ Rahul(20), Aman(21) ➔ Count = 2  
   - Mumbai Group ➔ Rohit(22), Neha(20) ➔ Count = 2  
3. `HAVING COUNT(*) >= 2`:  
   - Delhi (2 >= 2) ➔ PASS  
   - Mumbai (2 >= 2) ➔ PASS  
Output grid is Delhi: 2, Mumbai: 2.
