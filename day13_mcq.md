# Day 13 MCQs

## Quick Revision

Before attempting the MCQs, let's quickly review all key concepts covered in `day13.md`.

### 1. `SELF JOIN` Definition & Rules
- **Definition**: Jab ek hi table ko **khud ke saath (`Table A` ➔ `Table A`)** JOIN kiya jata hai, use `SELF JOIN` kehte hain.
- **Rule**: `SELF JOIN` query me **Table Aliases (e.g., `e1`, `e2`) MANDATORY** hote hain taaki computer initial table role (Employee View) aur secondary table role (Manager View) me differentiate kar sake.
- **Use Cases**:
  - Employee ↔ Manager Hierarchy (`e1.manager_id = e2.emp_id`)
  - Student ↔ Peer Mentor
  - Category ↔ Parent Category
  - Folder ↔ Parent Folder

### 2. `SELF JOIN` Query Syntax
```sql
SELECT e1.name AS Employee,
       e2.name AS Manager
FROM employees e1
LEFT JOIN employees e2
ON e1.manager_id = e2.emp_id;
```
- `e1`: Employee record instance.
- `e2`: Manager record instance.
- Using `LEFT JOIN` ensures top bosses (`manager_id IS NULL`) are retained with `Manager = NULL`.

### 3. `CROSS JOIN` Definition & Cartesian Product
- **Definition**: Left table ki **har single row** ko Right table ki **har single row** ke saath unconditionally combine karta hai.
- **Mathematical Term**: Is operation ko **Cartesian Product** kaha jata hai.
- **Formula**:
  $$	ext{Total Output Rows} = 	ext{Table1 Rows} 	imes 	ext{Table2 Rows}$$
- **Syntax**: `SELECT * FROM students CROSS JOIN departments;`
- **Day 13 DB Calculation**: $9 	ext{ students} 	imes 5 	ext{ departments} = 45 	ext{ Output Rows}$.

### 4. `CROSS JOIN` Real-World Use Case
- Generating product variants (e.g., $4 	ext{ Colors} 	imes 3 	ext{ Sizes} = 12 	ext{ Combinations}$) for e-commerce catalogs or matrix grids (Stores $	imes$ Products).

### 5. Master Comparison Table — All 6 SQL JOIN Types
1. **`INNER JOIN`**: Mutual Intersection ($A \cap B$) ➔ Only Matching Rows.
2. **`LEFT JOIN`**: Left Table Complete ($A$) ➔ All Left + Matching Right (`NULL` for non-match).
3. **`RIGHT JOIN`**: Right Table Complete ($B$) ➔ All Right + Matching Left (`NULL` for non-match).
4. **`FULL OUTER JOIN`**: Complete Union ($A \cup B$) ➔ All Left & Right (`UNION` in MySQL).
5. **`SELF JOIN`**: Same Table Join ➔ Internal hierarchical relationships via Aliases.
6. **`CROSS JOIN`**: Cartesian Product ➔ Every Row $	imes$ Every Row ($M 	imes N$).

---

## 30 Most Important MCQs

---

### Q1. SQL me `SELF JOIN` ka primary definition kya hota hai?

A) Do alag-alag databases ko join karna  
B) Ek hi single table ko **khud ke saath** (`Table A` ➔ `Table A`) join karna  
C) Primary key delete karke join karna  
D) Duplicate rows delete karna  

**Answer:** B

**Explanation:** `SELF JOIN` me same table ko multiple aliases assign karke internal hierarchical records link kiye jaate hain.

---

### Q2. `SELF JOIN` query write karte waqt SQL me kya lagana MANDATORY hota hai?

A) `WHERE` clause  
B) Table Aliases (e.g., `e1`, `e2`)  
C) `GROUP BY` clause  
D) `HAVING` clause  

**Answer:** B

**Explanation:** Single table ko distinct roles (e.g. Employee vs Manager) me clarify karne ke liye unique Table Aliases mandatory hote hain.

---

### Q3. Real-World Organizational Hierarchy me Employee ke Manager ka NAAM display karne ke liye kaunsa JOIN technique best fit hota hai?

A) `CROSS JOIN`  
B) `SELF JOIN`  
C) `RIGHT JOIN`  
D) `FULL OUTER JOIN`  

**Answer:** B

**Explanation:** Employee aur Manager dono exact same `employees` table me contain hote hain, isliye `SELF JOIN` hierarchically linkage perform karta hai.

---

### Q4. `employees` table me Aman (`manager_id = 1`) aur Rahul (`emp_id = 1`). `SELF JOIN` query: `ON e1.manager_id = e2.emp_id` me Aman ke manager ka Name kya fetch hoga?

A) Aman  
B) Rahul  
C) `NULL`  
D) Error  

**Answer:** B

**Explanation:** `e1.manager_id` (1) matches `e2.emp_id` (1) which belongs to Rahul, so Manager name `Rahul` print hota hai.

---

### Q5. `SELF JOIN` query: `FROM employees e1 LEFT JOIN employees e2 ON e1.manager_id = e2.emp_id;` me `e1` aur `e2` ka exact role kya hai?

A) `e1` Employee View instance hai aur `e2` Manager View instance hai  
B) `e1` Primary Key hai aur `e2` Foreign Key  
C) `e1` Database name hai aur `e2` Table name  
D) Dono separate tables hain  

**Answer:** A

**Explanation:** `e1` employee perspective represent karti hai jabki `e2` manager details fetch karne ka secondary alias perspective hota hai.

---

### Q6. E-Commerce domain me Category ↔ Parent Category (Sub-category tree) structure manage karne ke liye konsi JOIN technique use hoti hai?

A) `CROSS JOIN`  
B) `SELF JOIN`  
C) `RIGHT JOIN`  
D) `UNION`  

**Answer:** B

**Explanation:** Parent category IDs reference child category IDs within the same `categories` table via `SELF JOIN`.

---

### Q7. `CROSS JOIN` ka fundamental execution behavior kya hota hai?

A) Sirf matching records return karna  
B) Left table ki **har single row** ko Right table ki **har single row** ke saath unconditionally combine karna (Cartesian Product)  
C) Left table Delete karna  
D) Distinct values filter karna  

**Answer:** B

**Explanation:** `CROSS JOIN` every row of first table को every row of second table se pair karke Cartesian product form karta hai.

---

### Q8. Mathematical Terminology: `CROSS JOIN` dwara generate huye all-possible combination output को kya kaha jata hai?

A) Intersection  
B) Cartesian Product  
C) Venn Union  
D) Subquery  

**Answer:** B

**Explanation:** Set theory me two sets ke output pairs combination ko Cartesian Product ($A 	imes B$) kehte hain.

---

### Q9. Cartesian Product Formula: Agar Table A me $M$ rows hain aur Table B me $N$ rows hain, toh `CROSS JOIN` ka result size kitni rows hoga?

A) $M + N$  
B) $M 	imes N$  
C) $M - N$  
D) $M / N$  

**Answer:** B

**Explanation:** Total combinations formula: $	ext{Total Rows} = 	ext{Table1 Rows} 	imes 	ext{Table2 Rows}$.

---

### Q10. Day 13 dataset (`students` = 9 rows, `departments` = 5 rows) par `SELECT * FROM students CROSS JOIN departments;` query chalane par total kitni rows return hongi?

A) 14 rows  
B) 45 rows  
C) 9 rows  
D) 5 rows  

**Answer:** B

**Explanation:** $9 	ext{ students} 	imes 5 	ext{ departments} = 45 	ext{ Total Output Rows}$.

---

### Q11. Real-World Scenario: E-Commerce site par 4 Colors (Black, White, Red, Blue) aur 3 Sizes (S, M, L) ke saare SKU product combinations generate karne ke liye konsi query best hai?

A) `INNER JOIN`  
B) `CROSS JOIN` ($4 	imes 3 = 12 	ext{ combinations}$)  
C) `SELF JOIN`  
D) `LEFT JOIN`  

**Answer:** B

**Explanation:** Saare possible attribute variations (Colors $	imes$ Sizes) map karne ke liye `CROSS JOIN` ideal hai.

---

### Q12. Standard `CROSS JOIN` SQL query syntax kaunsa hai?

A) `SELECT * FROM table1 CROSS JOIN table2;`  
B) `CROSS JOIN table1 WITH table2;`  
C) `SELECT * FROM table1 ON table2;`  
D) `JOIN CROSS table1, table2;`  

**Answer:** A

**Explanation:** Standard ANSI SQL syntax: `SELECT columns FROM table1 CROSS JOIN table2;`.

---

### Q13. If Table A has 10 rows and Table B has 6 rows, how many rows will `SELECT * FROM A CROSS JOIN B;` return?

A) 16 rows  
B) 60 rows  
C) 10 rows  
D) 4 rows  

**Answer:** B

**Explanation:** Calculation: $10 	imes 6 = 60 	ext{ rows}$.

---

### Q14. Statement Check: Kya standard `CROSS JOIN` query me `ON` clause matching condition ki zaroorat hoti hai?

A) Haan, `ON` clause mandatory hai  
B) Nahi, `CROSS JOIN` unconditional Cartesian product perform karta hai (No `ON` clause required)  
C) `ON` clause ki jagah `GROUP BY` compulsory hai  
D) None of the above  

**Answer:** B

**Explanation:** `CROSS JOIN` har row ko har row se pair karta hai, isliye isme key matching `ON` condition ki zaroorat nahi hoti.

---

### Q15. Master Comparison: Single table ko internal hierarchical parent-child linking ke liye join karne ko kya kehte hain?

A) `CROSS JOIN`  
B) `SELF JOIN`  
C) `FULL JOIN`  
D) `RIGHT JOIN`  

**Answer:** B

**Explanation:** Single table internal reference linking = `SELF JOIN`.

---

### Q16. Master Comparison: Har single row ko har possible row ke saath pair karne ko kya kehte hain?

A) `INNER JOIN`  
B) `CROSS JOIN`  
C) `LEFT JOIN`  
D) `SELF JOIN`  

**Answer:** B

**Explanation:** All-pairs combination generator = `CROSS JOIN`.

---

### Q17. Statement Check: Kya `SELF JOIN` me `LEFT JOIN` or `INNER JOIN` keyword combine ho sakta hai?

A) Haan, e.g. `FROM employees e1 LEFT JOIN employees e2 ON e1.manager_id = e2.emp_id`  
B) Nahi, `SELF JOIN` alag keyword hai  
C) `SELF JOIN` SQL me illegal hai  
D) Only `RIGHT JOIN` allowed hai  

**Answer:** A

**Explanation:** `SELF JOIN` concept hai jisme join operator (`LEFT JOIN`, `INNER JOIN`) single table aliases ke saath implement hota hai.

---

### Q18. Employee-Manager hierarchy me Top Boss Rahul (`manager_id = NULL`) ko output me retain karne ke liye `SELF JOIN` me konsa join type use karna chahiye?

A) `INNER JOIN`  
B) `LEFT JOIN` (`FROM employees e1 LEFT JOIN employees e2`)  
C) `CROSS JOIN`  
D) `DELETE JOIN`  

**Answer:** B

**Explanation:** `LEFT JOIN` top boss (`manager_id = NULL`) ko preserve rakhta hai, outputting `Manager = NULL`.

---

### Q19. Master Progress Check: Day 13 tak total kitne primary SQL JOIN types complete ho chuke hain?

A) 2 Types  
B) 6 Types (`INNER`, `LEFT`, `RIGHT`, `FULL OUTER`, `SELF`, `CROSS`)  
C) 10 Types  
D) 1 Type  

**Answer:** B

**Explanation:** Day 13 tak saare 6 fundamental RDBMS JOIN types cover ho chuke hain.

---

### Q20. If Table A has 0 rows and Table B has 100 rows, how many rows will `SELECT * FROM A CROSS JOIN B;` return?

A) 100 rows  
B) 0 rows ($0 	imes 100 = 0$)  
C) 50 rows  
D) Error  

**Answer:** B

**Explanation:** Multiplied size: $0 	imes 100 = 0 	ext{ rows}$.

---

### Q21. Master Comparison: Match na hone par Right side attributes me `NULL` fill karne wala Join?

A) `LEFT JOIN`  
B) `RIGHT JOIN`  
C) `CROSS JOIN`  
D) `INNER JOIN`  

**Answer:** A

**Explanation:** `LEFT JOIN` left rows preserve karta hai aur missing right attributes ko `NULL` set karta hai.

---

### Q22. Master Comparison: Match na hone par Left side attributes me `NULL` fill karne wala Join?

A) `LEFT JOIN`  
B) `RIGHT JOIN`  
C) `CROSS JOIN`  
D) `INNER JOIN`  

**Answer:** B

**Explanation:** `RIGHT JOIN` right rows preserve karta hai aur missing left attributes ko `NULL` set karta hai.

---

### Q23. Query Breakdown: `SELECT e1.name FROM employees e1 LEFT JOIN employees e2 ON e1.manager_id = e2.emp_id;` me `e1` table kis role ko represent karti hai?

A) Manager Role  
B) Employee Role  
C) Company Name Role  
D) Department Role  

**Answer:** B

**Explanation:** `e1` driving left table list hai jo employee names (`e1.name`) extract karti hai.

---

### Q24. Query Breakdown: Above query me `ON e1.manager_id = e2.emp_id` me `e2` table kis role ko represent karti hai?

A) Employee Role  
B) Manager Role  
C) Project Role  
D) Location Role  

**Answer:** B

**Explanation:** `e2` target lookup table hai jahan `emp_id` match karke manager का details (`e2.name`) nikalte hain.

---

### Q25. Folder ↔ Parent Folder directory file system representation ke liye konsa JOIN model apply hota hai?

A) `CROSS JOIN`  
B) `SELF JOIN`  
C) `FULL OUTER JOIN`  
D) `UNION`  

**Answer:** B

**Explanation:** Self-referencing tree structure (Folder ➔ Parent Folder ID) `SELF JOIN` se query hota hai.

---

### Q26. Retail inventory tracking (5 Stores $	imes$ 4 Products = 20 initial inventory tracking pairs) generate karne ke liye konsa JOIN model standard hai?

A) `CROSS JOIN`  
B) `SELF JOIN`  
C) `INNER JOIN`  
D) `WHERE`  

**Answer:** A

**Explanation:** All-store to all-product complete Cartesian grid generation ke liye `CROSS JOIN` ideal setup method hai.

---

### Q27. Accenture Trap Question: Kya `CROSS JOIN` me `ON` clause na likhne se syntax error aata hai?

A) Haan, syntax error aayega  
B) Nahi, `CROSS JOIN` without `ON` condition Cartesian product evaluate karta hai  
C) Workbench crash ho jata hai  
D) Query drop ho jaati hai  

**Answer:** B

**Explanation:** `CROSS JOIN` inherently unconditional Cartesian product perform karta hai, so `ON` clause is not required.

---

### Q28. Progress Assessment: Day 13 tak complete hone par overall SQL Course Mastery approximate kitne percentage par pahunch chuka hai?

A) 10%  
B) 65–70%  
C) 100%  
D) 30%  

**Answer:** B

**Explanation:** Basics, Filtering, Aggregation, Grouping, aur saare 6 JOINs complete hone se course $pprox 65-70\%$ complete ho gaya hai.

---

### Q29. Upcoming Roadmap: All 6 JOINs complete hone ke baad SQL ka next major advanced interview topic kaunsa start hone wala hai?

A) HTML Tags  
B) Subqueries & Correlated Subqueries  
C) Basic Arithmetic  
D) Operating System  

**Answer:** B

**Explanation:** JOINs ke baad SQL ka most crucial advanced topic Subqueries (Nested Queries) hota hai.

---

### Q30. Placement Master Question: Which SQL query produces a complete grid of all possible pairs between two sets of data without filtering?

A) `INNER JOIN`  
B) `CROSS JOIN`  
C) `LEFT JOIN`  
D) `SELF JOIN`  

**Answer:** B

**Explanation:** `CROSS JOIN` produces an unfiltered complete grid of all possible pairs (Cartesian Product) between two datasets.
