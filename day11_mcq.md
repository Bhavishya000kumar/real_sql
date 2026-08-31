# Day 11 MCQs

## Quick Revision

Before attempting the MCQs, let's quickly review all key concepts covered in `day11.md`.

### 1. `LEFT JOIN` Definition & Fundamental Rule
- **Definition**: `LEFT JOIN` left table (first table) ki **saari rows** return karta hai, chahe right table (second table) me match mile ya na mile.
- **Rule**: Agar right table me match milta hai, toh actual data display hota hai. Match na milne par right table columns me **`NULL`** fill ho jata hai.
- **Synonym**: SQL standard me `LEFT JOIN` ko `LEFT OUTER JOIN` bhi kaha jata hai.

### 2. `INNER JOIN` vs `LEFT JOIN` Execution Difference
- **`INNER JOIN`**: Strictly only matching records return karta hai. Non-matching rows (e.g. Vikas with `department_id = 5`) ko output se **discard / hide** kar deta hai.
- **`LEFT JOIN`**: Left table ki har row ko preserve karta hai. Non-matching records (Vikas) output me **`NULL`** department ke saath include hote hain.

### 3. Day 11 Dataset Row Count Comparison
- **`students` Table**: 9 Total Students (Rahul to Sneha = 8 matching, Vikas = 1 non-matching).
- **`departments` Table**: 4 Departments (`1` CSE, `2` ECE, `3` Mechanical, `4` Civil).
- **`INNER JOIN` Output**: **8 Rows** (Vikas excluded).
- **`LEFT JOIN` Output**: **9 Rows** (Vikas included with `department_name = NULL`).

### 4. Real-World Company Use Case
- Jab requirement ho ki **"Left entity ke SAARE records dikhao"** (e.g., saare employees, saare customers, saare products) regardless of whether they have a matching record in the right table (e.g., assigned department, placed orders), tab **`LEFT JOIN`** compulsory use hota hai.

### 5. `NULL` Concept in JOINs
- `NULL` represents missing, unknown, or unassigned data in SQL.
- When `LEFT JOIN` fails to find a matching key in the right table, all right table attributes output as `NULL`.

---

## 30 Most Important MCQs

---

### Q1. SQL me `LEFT JOIN` ka fundamental execution rule kya hai?

A) Sirf Right table ke matching records return karna  
B) Left table ki **saari rows** return karna, chahe Right table me match ho ya na ho  
C) Saari rows delete kar dena  
D) Duplicate rows create karna  

**Answer:** B

**Explanation:** `LEFT JOIN` left table ke saare records output grid me preserve karta hai. Match na milne par right table columns me `NULL` aata hai.

---

### Q2. `LEFT JOIN` me jab left table ki kisi row ka matching record right table me NAHI milta, toh right table columns me kya value fill hoti hai?

A) `0`  
B) Empty string `""`  
C) `NULL`  
D) Error  

**Answer:** C

**Explanation:** Non-matching right table records ke liye SQL `NULL` (missing data placeholder) return karta hai.

---

### Q3. Day 11 dataset me non-matching student Vikas (`department_id = 5`) insert karne ke baad `INNER JOIN` query ne kitni total rows return kiye?

A) 9 rows  
B) 8 rows  
C) 5 rows  
D) 0 rows  

**Answer:** B

**Explanation:** `INNER JOIN` non-matching key (`5 ≠ 1, 2, 3, 4`) ko exclude kar deta hai, isliye sirf 8 matching rows aati hain.

---

### Q4. Day 11 dataset me non-matching student Vikas (`department_id = 5`) insert karne ke baad `LEFT JOIN` query ne kitni total rows return kiye?

A) 8 rows  
B) 9 rows  
C) 10 rows  
D) 4 rows  

**Answer:** B

**Explanation:** `LEFT JOIN` left table ke saare 9 students (8 matching + 1 Vikas) output grid me return karta hai.

---

### Q5. Vikas (`department_id = 5`) `INNER JOIN` ke result output grid se gayab/exclude kyun ho gaya?

A) Vikas ka student_id invalid tha  
B) `department_id = 5` parent table `departments` me exist nahi karta aur `INNER JOIN` sirf matching records filter karta hai  
C) Vikas Mumbai se tha  
D) Syntax error tha  

**Answer:** B

**Explanation:** `INNER JOIN` strictly `FK = PK` matching records par depend karta hai. Match na hone par row output se discard ho jaati hai.

---

### Q6. Enterprise Real-World Scenario: Audit team ne kaha "Company ke SAARE 500 employees dikhao, chahe unhe department assign hua ho ya na ho". Aap konsa join use karenge?

A) `INNER JOIN`  
B) `LEFT JOIN`  
C) `CROSS JOIN`  
D) `DELETE JOIN`  

**Answer:** B

**Explanation:** `LEFT JOIN` ensure karta hai ki left table (`employees`) ka ek bhi record audit report se miss na ho.

---

### Q7. Agar Audit team ke kehne par galati se `INNER JOIN` chalayein, toh report me kya mistake aayegi?

A) Database drop ho jayega  
B) Jis employee ko department assign nahi hua hai, wo employee report se HIDE/MISSING ho jayega  
C) Output me 1000 rows aayengi  
D) Saari names uppercase ho jayengi  

**Answer:** B

**Explanation:** `INNER JOIN` unassigned employees (non-matching rows) ko discard kar dega, jisse audit report incomplete aayegi.

---

### Q8. Beginner Misconception Check: Kya `LEFT JOIN` ka matlab sirf Left table ka data display karna hai?

A) Haan, right table data exclude ho jata hai  
B) Nahi, `LEFT JOIN` Left table ki saari rows PLUS Right table ka matching data display karta hai  
C) Haan, `LEFT JOIN` column delete kar deta hai  
D) None of the above  

**Answer:** B

**Explanation:** `LEFT JOIN` left table ki saari rows aur right table ke matching columns return karta hai; match na milne par right side `NULL` hota hai.

---

### Q9. Correct `LEFT JOIN` SQL syntax order kaunsa hai?

A) `SELECT ... FROM students s LEFT JOIN departments d ON s.department_id = d.department_id;`  
B) `SELECT ... LEFT JOIN students ON s.department_id = d.department_id;`  
C) `FROM students LEFT JOIN ON s.department_id = d.department_id;`  
D) `LEFT JOIN s.department_id = d.department_id;`  

**Answer:** A

**Explanation:** Standard syntax: `SELECT columns FROM table1 s LEFT JOIN table2 d ON s.key = d.key;`.

---

### Q10. Day 11 ke `LEFT JOIN` output grid me Vikas ke samne `department_name` column me kya output print hua?

A) `'CSE'`  
B) `'Civil'`  
C) `NULL`  
D) `'Unknown'`  

**Answer:** C

**Explanation:** Department 5 `departments` table me missing hone par right table attribute `department_name` me `NULL` print hota hai.

---

### Q11. MySQL internal execution dry run according, `LEFT JOIN` me Vikas (`dept_id = 5`) process hote waqt kya steps perform hote hain?

A) `dept_id = 5` search in `departments` ➔ Not Found ➔ Return `Vikas | NULL`  
B) Error 404 trigger hota hai  
C) Row auto delete ho jaati hai  
D) Department 1 force update ho jata hai  

**Answer:** A

**Explanation:** Computer right table me key 5 search karta hai, na milne par left record Vikas ko `NULL` right values ke saath return karta hai.

---

### Q12. Agar Left table me 10 rows hain aur saare 10 rows Right table me exact match hote hain, toh `INNER JOIN` aur `LEFT JOIN` ke row counts me kya relationship hoga?

A) `LEFT JOIN` me zyada rows aayengi  
B) `INNER JOIN` me zyada rows aayengi  
C) Dono exact SAME (10 rows) return karenge  
D) Dono 0 rows return karenge  

**Answer:** C

**Explanation:** Jab 100% rows match hoti hain, tab `INNER JOIN` aur `LEFT JOIN` exact identical output grid aur row count return karte hain.

---

### Q13. Day 11 Query: `SELECT s.student_name, s.city, d.department_name FROM students s LEFT JOIN departments d ON s.department_id = d.department_id;` Vikas row me `city` column me kya aayega?

A) `NULL`  
B) `'Jaipur'`  
C) `'Delhi'`  
D) Error  

**Answer:** B

**Explanation:** `city` column `students` table ka Part hai, aur Vikas ki city `students` table me `'Jaipur'` stored hai, isliye `'Jaipur'` print hoga.

---

### Q14. Tricky Question: Agar Left Table me 9 rows hain, toh `LEFT JOIN` ka result set MINIMUM kitni rows guarantee karta hai?

A) Minimum 0 rows  
B) Minimum 9 rows  
C) Minimum 4 rows  
D) Minimum 18 rows  

**Answer:** B

**Explanation:** `LEFT JOIN` left table ke har single record ko preserve karta hai, isliye result size minimum left table row count (9) ke barabar hota hai.

---

### Q15. Real-World Scenario: `customers` (Left Table) `LEFT JOIN` `orders` (Right Table). Customer "Rahul" ne past me 0 orders place kiye hain. Output grid me Rahul ke `order_id` column me kya value aayegi?

A) `0`  
B) `NULL`  
C) `'No Order'`  
D) Record skip ho jayega  

**Answer:** B

**Explanation:** Matching order record na hone par `orders` table ke columns (`order_id`) `NULL` display honge.

---

### Q16. Above E-Commerce scenario me agar aapko un customers ki list chahiye jinhone "Abhi tak 0 orders place kiye hain", toh aap konsa join use karke `WHERE order_id IS NULL` lagayein?

A) `INNER JOIN`  
B) `LEFT JOIN`  
C) `CROSS JOIN`  
D) `SELF JOIN`  

**Answer:** B

**Explanation:** Unmatched/zero order customers identify karne ke liye `LEFT JOIN` ke baad `WHERE order_id IS NULL` filtering pattern use hota hai.

---

### Q17. `INSERT INTO students (student_id, student_name, age, city, department_id) VALUES (109, 'Vikas', 22, 'Jaipur', 5);` Run karne par `departments` table par kya effect hua?

A) `departments` me 1 row add ho gayi  
B) `departments` table completely untouched aur unchanged rahi  
C) `departments` me error aaya  
D) `departments` table reset ho gayi  

**Answer:** B

**Explanation:** `INSERT INTO students` sirf `students` child table me record add karta hai; parent `departments` table me zero change hota hai.

---

### Q18. SQL Standard me `LEFT JOIN` ka full formal synonym name kya hai?

A) `LEFT INNER JOIN`  
B) `LEFT OUTER JOIN`  
C) `LEFT FULL JOIN`  
D) `LEFT CROSS JOIN`  

**Answer:** B

**Explanation:** ANSI SQL standard me `LEFT JOIN` aur `LEFT OUTER JOIN` exact identical keywords hain.

---

### Q19. Interview Question: `INNER JOIN` aur `LEFT JOIN` me main difference kya hai?

A) `INNER JOIN` matching rows deta hai; `LEFT JOIN` left table ki ALL rows deta hai (unmatched rows ke liye `NULL` ke saath)  
B) `INNER JOIN` fast hota hai, `LEFT JOIN` slow  
C) `LEFT JOIN` duplicate rows delete karta hai  
D) Dono exact identical hain  

**Answer:** A

**Explanation:** Core interview distinction: `INNER JOIN` intersection matches only; `LEFT JOIN` preserves all left table records with `NULL` fallbacks.

---

### Q20. `FROM students s LEFT JOIN departments d ON s.department_id = d.department_id` me Left Table kaunsi hai?

A) `departments`  
B) `students`  
C) `d`  
D) `ON`  

**Answer:** B

**Explanation:** `FROM` clause ke aage first specify ki gayi table (`students`) `LEFT JOIN` scope me Left Table kehalati hai.

---

### Q21. Output Check: `SELECT COUNT(*) FROM students s LEFT JOIN departments d ON s.department_id = d.department_id;` Day 11 DB state par run karne par kya output dega?

A) 8  
B) 9  
C) 4  
D) 5  

**Answer:** B

**Explanation:** Total 9 students (8 matching + 1 Vikas) hain, isliye `COUNT(*)` = 9 return hoga.

---

### Q22. Output Check: `SELECT COUNT(*) FROM students s INNER JOIN departments d ON s.department_id = d.department_id;` Day 11 DB state par run karne par kya output dega?

A) 9  
B) 8  
C) 4  
D) 0  

**Answer:** B

**Explanation:** Vikas exclude hone ke waja se `INNER JOIN` me sirf 8 matching rows count honge.

---

### Q23. `LEFT JOIN` query me `SELECT *` execute karne par Vikas wali row me `departments.department_id` column value kya aayegi?

A) `5`  
B) `NULL`  
C) `0`  
D) `1`  

**Answer:** B

**Explanation:** Right table (`departments`) me ID 5 exist nahi karti, isliye right table `department_id` column me `NULL` missing value fill hoti hai.

---

### Q24. Placement Scenario: Company me 100 Employees hain aur 10 Departments. Sabhi employees me valid `dept_id` hai. `LEFT JOIN` query chalane par output me kitni rows aayengi?

A) 10 rows  
B) 100 rows  
C) 110 rows  
D) 0 rows  

**Answer:** B

**Explanation:** Saare 100 employees left table me hain aur match hote hain, isliye result set exact 100 rows ka banega.

---

### Q25. Trap Question: Kya SQL me `NULL` value number `0` ya empty string `""` ke equal hoti hai?

A) Haan, `NULL = 0` hota hai  
B) Nahi, `NULL` missing / unknown value ko represent karta hai jo `0` ya `""` se completely different hai  
C) `NULL` space character hota hai  
D) `NULL` negative number hota hai  

**Answer:** B

**Explanation:** SQL me `NULL` zero ya empty string nahi hota; `NULL` state ka matlab value unassigned ya unknown hai.

---

### Q26. `SELECT s.student_name FROM students s LEFT JOIN departments d ON s.department_id = d.department_id;` Yahan Vikas result list me aayega ya nahi?

A) Nahi aayega  
B) Aayega (Total 9 student names list honge)  
C) Error aayega  
D) Duplicate names aayenge  

**Answer:** B

**Explanation:** `LEFT JOIN` Left table `students` ke har name (including Vikas) ko SELECT result list me retain karta hai.

---

### Q27. Accentue Alignment: Agar `ON s.department_id = d.department_id` me `s.department_id` NULL ho, toh `LEFT JOIN` use karne par output row me kya display hoga?

A) Student row output me aayegi aur right table columns NULL honge  
B) Student row delete ho jayegi  
C) Query error throw karegi  
D) Database drop ho jayega  

**Answer:** A

**Explanation:** `LEFT JOIN` left row preserve karta hai. `department_id = NULL` right table me match nahi hoga, isliye right side NULLs display honge.

---

### Q28. Master Rule: Konsa JOIN guarantee karta hai ki Left Table ka EK BHI record final output set se lost/exclude NAHI hoga?

A) `INNER JOIN`  
B) `LEFT JOIN` (ya `LEFT OUTER JOIN`)  
C) `RIGHT JOIN`  
D) `CROSS JOIN`  

**Answer:** B

**Explanation:** `LEFT JOIN` primary design purpose hi left table rows preservation ensure karna hai.

---

### Q29. Practice Question A3 check: Student Name, City, aur Department Name fetch karne ke liye correct `LEFT JOIN` code snippet kya tha?

A) `SELECT s.student_name, s.city, d.department_name FROM students s LEFT JOIN departments d ON s.department_id = d.department_id;`  
B) `SELECT * WHERE city = 'Jaipur';`  
C) `LEFT JOIN city FROM students;`  
D) `SELECT department_name FROM departments;`  

**Answer:** A

**Explanation:** Proper explicit alias select format `s.student_name, s.city, d.department_name` ke saath `LEFT JOIN` query run ki jaati hai.

---

### Q30. Summary Question: `INNER JOIN` vs `LEFT JOIN` ka core difference summarized:

A) `INNER JOIN` = Intersection (Only Matches) | `LEFT JOIN` = Left Table All + Right Matches (`NULL` for missing)  
B) `INNER JOIN` = Left All | `LEFT JOIN` = Intersection  
C) Dono identical hain  
D) `LEFT JOIN` SQL me deprecated hai  

**Answer:** A

**Explanation:** `INNER JOIN` is strictly intersection of matching records; `LEFT JOIN` preserves all left table records with right-side `NULL` fallbacks.
