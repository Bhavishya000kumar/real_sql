# Day 12 MCQs

## Quick Revision

Before attempting the MCQs, let's quickly review all key concepts covered in `day12.md`.

### 1. `RIGHT JOIN` Definition & Core Rules
- **Definition**: `RIGHT JOIN` right table (second table) ki **saari rows** return karta hai, chahe left table (first table) me matching record mile ya na mile.
- **Rule**: Agar left table me matching key nahi milti, toh left table ke attributes/columns output grid me **`NULL`** ho jate hain.
- **Synonym**: SQL standard me `RIGHT JOIN` ko `RIGHT OUTER JOIN` bhi kaha jata hai.

### 2. Table Reordering Equivalence (Interview Favorite ⭐⭐⭐⭐⭐)
- `SELECT * FROM A LEFT JOIN B ON A.id = B.id;`  
  **is EXACTLY identical in output to**  
  `SELECT * FROM B RIGHT JOIN A ON B.id = A.id;`  
  *(Tables ka order swap/reverse karne par `LEFT JOIN` aur `RIGHT JOIN` exact identical result set return karte hain).*

### 3. `FULL OUTER JOIN` & MySQL Limitations
- **Definition**: `FULL OUTER JOIN` Left aur Right dono tables ki **SAARI matching aur non-matching rows** return karta hai.
- **MySQL Limitation**: MySQL database engine `FULL OUTER JOIN` syntax ko **directly support nahi karta** (Syntax Error 1064).
- **MySQL Workaround (`UNION`)**:
  ```sql
  SELECT s.student_name, d.department_name
  FROM students s LEFT JOIN departments d ON s.department_id = d.department_id
  UNION
  SELECT s.student_name, d.department_name
  FROM students s RIGHT JOIN departments d ON s.department_id = d.department_id;
  ```
  `UNION` operator `LEFT JOIN` aur `RIGHT JOIN` results ko merge karke duplicate matching rows ko deduplicate/combine kar deta hai.

### 4. Venn Diagram Quick Recall
- **`INNER JOIN`**: Middle Overlap (Intersection $A \cap B$) ➔ Only Matching Rows.
- **`LEFT JOIN`**: Left Circle Complete ➔ Left All + Matching Right.
- **`RIGHT JOIN`**: Right Circle Complete ➔ Right All + Matching Left.
- **`FULL OUTER JOIN`**: Complete Both Circles (Union $A \cup B$) ➔ Everything.

### 5. Master Comparison Table
- **`INNER JOIN`**: Vikas ❌ | Electrical ❌
- **`LEFT JOIN`**: Vikas (`Vikas | NULL`) ✅ | Electrical ❌
- **`RIGHT JOIN`**: Vikas ❌ | Electrical (`NULL | Electrical`) ✅
- **`FULL OUTER JOIN`**: Vikas (`Vikas | NULL`) ✅ | Electrical (`NULL | Electrical`) ✅

---

## 30 Most Important MCQs

---

### Q1. SQL me `RIGHT JOIN` ka fundamental execution behavior kya hota hai?

A) Left table ki saari rows retain karna  
B) Right table (second table) ki **saari rows** return karna, chahe left table me match ho ya na ho  
C) Saari rows delete karna  
D) Duplicate primary keys create karna  

**Answer:** B

**Explanation:** `RIGHT JOIN` right table ke sabhi records output me preserve karta hai. Match na hone par left table columns `NULL` display hote hain.

---

### Q2. `RIGHT JOIN` me jab right table ki kisi row ka match left table me NAHI milta, toh left table columns me kya value fill hoti hai?

A) `0`  
B) `NULL`  
C) Empty string `""`  
D) Default string `'N/A'`  

**Answer:** B

**Explanation:** Left table matching row miss hone par left table attributes me `NULL` missing value return hoti hai.

---

### Q3. Day 12 dataset me Electrical department (`department_id = 5`) me zero students enrolled the. `RIGHT JOIN` output me Electrical department ke samne `student_name` column me kya output aaya?

A) `'Vikas'`  
B) `NULL`  
C) `'Rahul'`  
D) Error  

**Answer:** B

**Explanation:** Electrical department parent right table me exist karta hai par `students` me match nahi milti, isliye `student_name` = `NULL` display hota hai (`NULL | Electrical`).

---

### Q4. Interview Trick: Niche di gayi SQL queries me se konsi query `SELECT * FROM students s LEFT JOIN departments d ON s.department_id = d.department_id;` ke EXACT same output return karegi?

A) `SELECT * FROM departments d RIGHT JOIN students s ON s.department_id = d.department_id;`  
B) `SELECT * FROM students s RIGHT JOIN departments d ON s.department_id = d.department_id;`  
C) `SELECT * FROM departments d INNER JOIN students s ON s.department_id = d.department_id;`  
D) None of the above  

**Answer:** A

**Explanation:** Table positions ko reverse (`departments d RIGHT JOIN students s`) karne par `RIGHT JOIN` exact `LEFT JOIN` ka result produce karta hai.

---

### Q5. `FULL OUTER JOIN` ka primary objective kya hota hai?

A) Sirf common matching records return karna  
B) Dono tables ki **SAARI matching aur non-matching rows** ek saath single result set me return karna  
C) Database clear karna  
D) Rows count zero karna  

**Answer:** B

**Explanation:** `FULL OUTER JOIN` complete union output represent karta hai jisme left aur right dono tables ke non-matching records `NULL` placeholders ke saath include hote hain.

---

### Q6. MySQL database engine me `FULL OUTER JOIN` keyword ke baare me kaunsa statement 100% TRUE hai?

A) MySQL direct `FULL OUTER JOIN` keyword ko native support karta hai  
B) MySQL `FULL OUTER JOIN` keyword ko **directly support nahi karta**  
C) MySQL me `FULL OUTER JOIN` likhne se database format ho jata hai  
D) MySQL `FULL OUTER JOIN` ko `GROUP BY` me convert karta hai  

**Answer:** B

**Explanation:** MySQL engine me direct `FULL OUTER JOIN` keyword unavailable hai; run karne par syntax error return hota hai.

---

### Q7. MySQL me `FULL OUTER JOIN` jaisa complete result set derive karne ke liye kin do JOIN queries ko combine kiya jata hai?

A) `INNER JOIN` aur `CROSS JOIN`  
B) `LEFT JOIN` aur `RIGHT JOIN` via `UNION`  
C) `WHERE` aur `HAVING`  
D) `DELETE` aur `UPDATE`  

**Answer:** B

**Explanation:** MySQL me `LEFT JOIN` (left non-matches) aur `RIGHT JOIN` (right non-matches) ko `UNION` operator se merge karke `FULL OUTER JOIN` simulate kiya jata hai.

---

### Q8. MySQL me `LEFT JOIN` aur `RIGHT JOIN` queries ko merge karke duplicate matching rows remove karne ke liye kaunsa operator use hota hai?

A) `JOIN`  
B) `UNION`  
C) `LIKE`  
D) `BETWEEN`  

**Answer:** B

**Explanation:** `UNION` operator dono query result sets ko combine karta hai aur automatic distinct deduplication perform karta hai.

---

### Q9. `UNION` operator `LEFT JOIN` aur `RIGHT JOIN` results ko merge karte waqt matching rows (e.g. Rahul, Aman) ke saath kya karta hai?

A) Duplicate matching rows ko double kar deta hai  
B) Duplicate matching rows ko deduplicate karke single time display karta hai  
C) Matching rows delete kar deta hai  
D) Error de deta hai  

**Answer:** B

**Explanation:** `UNION` standard set operator hai jo combined output me duplicate identical rows ko deduplicate karke single entry retain karta hai.

---

### Q10. Day 12 dataset par MySQL `UNION` approach se `FULL OUTER JOIN` run karne par result grid me kaun-kaun se non-matching records ek saath dikhenge?

A) Sirf Vikas (`Vikas | NULL`)  
B) Sirf Electrical (`NULL | Electrical`)  
C) Vikas (`Vikas | NULL`) AUR Electrical (`NULL | Electrical`) DONO  
D) Koyi bhi nahi  

**Answer:** C

**Explanation:** `FULL OUTER JOIN` left side non-matching (Vikas) aur right side non-matching (Electrical) dono records ko result set me show karta hai.

---

### Q11. Venn Diagram Representation: `INNER JOIN` Venn Diagram ke kis portion ko represent karta hai?

A) Complete Left Circle  
B) Complete Right Circle  
C) Dono circles ka middle overlapping intersection ($A \cap B$)  
D) External background  

**Answer:** C

**Explanation:** `INNER JOIN` strictly mutual intersection region ($A \cap B$) ko represent karta hai.

---

### Q12. Venn Diagram Representation: `FULL OUTER JOIN` Venn Diagram ke kis portion ko represent karta hai?

A) Complete Both Circles (Union $A \cup B$)  
B) Only Middle  
C) Only Left Outer  
D) Only Right Outer  

**Answer:** A

**Explanation:** `FULL OUTER JOIN` complete union ($A \cup B$) ko represent karta hai.

---

### Q13. Niche di gayi query me Right Table kaunsi hai?
```sql
SELECT s.student_name, d.department_name
FROM students s
RIGHT JOIN departments d
ON s.department_id = d.department_id;
```

A) `students`  
B) `departments`  
C) `s`  
D) `ON`  

**Answer:** B

**Explanation:** `RIGHT JOIN` keyword ke baad specify ki gayi table (`departments d`) Right Table hoti hai.

---

### Q14. Beginner Misconception Check: Kya `RIGHT JOIN` execute karne par Right Table ke columns ke alawa baki columns drop ho jate hain?

A) Haan, left columns remove ho jate hain  
B) Nahi, `RIGHT JOIN` **ROWS** ki completeness par work karta hai, columns select list ke according exact intact rehte hain  
C) `RIGHT JOIN` table drop kar deta hai  
D) None of the above  

**Answer:** B

**Explanation:** Joins row preservation rules manage karte hain; columns output display purely `SELECT` list dwara determine hoti hai.

---

### Q15. E-Commerce Real-World Scenario: `products` (Left) `RIGHT JOIN` `categories` (Right). Naye Category "Sports" me 0 products hain. Output grid me `product_name` column me kya output print hoga?

A) `'Sports'`  
B) `NULL`  
C) `'No Product'`  
D) Row discard ho jayegi  

**Answer:** B

**Explanation:** Non-matching left side attributes (`product_name`) ke liye `RIGHT JOIN` `NULL` fill karta hai.

---

### Q16. Above E-Commerce scenario me agar requirement ho ki "Saari Categories list karo bhale hi unme 0 products hon", toh `categories` ko RIGHT table banakar konsa join use karenge?

A) `INNER JOIN`  
B) `RIGHT JOIN`  
C) `CROSS JOIN`  
D) `SELF JOIN`  

**Answer:** B

**Explanation:** Right table (`categories`) ki Complete visibility ensure karne ke liye `RIGHT JOIN` use kiya jayega.

---

### Q17. Table A me 5 rows hain aur Table B me 10 rows hain. Query: `SELECT * FROM A RIGHT JOIN B ON A.id = B.id;` ka result grid MINIMUM kitni rows return karega?

A) Minimum 5 rows  
B) Minimum 10 rows  
C) Minimum 15 rows  
D) 0 rows  

**Answer:** B

**Explanation:** `RIGHT JOIN` Right table (Table B) ke saare 10 records preserve karta hai, isliye result size minimum 10 rows hoga.

---

### Q18. SQL me `UNION` aur `UNION ALL` ke beech primary difference kya hota hai?

A) `UNION` duplicate rows remove karta hai; `UNION ALL` duplicates retain/include karta hai  
B) `UNION` slow hota hai, `UNION ALL` error deta hai  
C) `UNION` columns delete karta hai  
D) Dono exact identical hain  

**Answer:** A

**Explanation:** `UNION` set operation output deduplicate karta hai, jabki `UNION ALL` combined queries ke saare rows (including duplicates) combine kar deta hai.

---

### Q19. Day 12 database setup step 1 me Electrical department (`department_id = 5`) insert karne ke baad `departments` table me total kitni rows ho gayi thin?

A) 4 rows  
B) 5 rows  
C) 9 rows  
D) 1 row  

**Answer:** B

**Explanation:** Initially 4 departments (CSE, ECE, Mechanical, Civil) the; Electrical add hone ke baad count 5 ho gaya.

---

### Q20. Standard ANSI SQL me `RIGHT JOIN` ka formal extended name kya hota hai?

A) `RIGHT INNER JOIN`  
B) `RIGHT OUTER JOIN`  
C) `RIGHT CROSS JOIN`  
D) `RIGHT FULL JOIN`  

**Answer:** B

**Explanation:** SQL syntax me `RIGHT JOIN` aur `RIGHT OUTER JOIN` inter-changeable synonyms hain.

---

### Q21. Master Comparison Check: Konsa JOIN non-matching right rows ko retain karta hai lekin non-matching left rows ko discard kar deta hai?

A) `LEFT JOIN`  
B) `RIGHT JOIN`  
C) `INNER JOIN`  
D) `FULL OUTER JOIN`  

**Answer:** B

**Explanation:** `RIGHT JOIN` strictly Right table records ko preserve karta hai aur left non-matches ko discard karta hai.

---

### Q22. Master Comparison Check: Konsa JOIN dono sides (Left & Right) ke non-matching records ko output se EXCLUDE/DISCARD kar deta hai?

A) `INNER JOIN`  
B) `LEFT JOIN`  
C) `RIGHT JOIN`  
D) `FULL OUTER JOIN`  

**Answer:** A

**Explanation:** `INNER JOIN` strictly only matching records retain karta hai; non-matches from both sides ignore ho jate hain.

---

### Q23. Output Check: Day 12 DB state (9 students, 5 departments) par `SELECT COUNT(*) FROM students s RIGHT JOIN departments d ON s.department_id = d.department_id;` ka output count kya hoga?

A) 8  
B) 9 rows (8 matching + 1 Electrical with NULL student)  
C) 10  
D) 5  

**Answer:** B

**Explanation:** Right side `departments` ke 5 rows match hote hain: CSE (3 students), ECE (3 students), Mech (1), Civil (1), Electrical (1 with NULL) = Total 9 output rows.

---

### Q24. Correct MySQL `FULL OUTER JOIN` query template check:

A) `SELECT * FROM A FULL OUTER JOIN B ON A.id = B.id;`  
B) `SELECT * FROM A LEFT JOIN B ON A.id = B.id UNION SELECT * FROM A RIGHT JOIN B ON A.id = B.id;`  
C) `SELECT * FROM A INNER JOIN B UNION ALL;`  
D) `SELECT * FROM A CROSS JOIN B;`  

**Answer:** B

**Explanation:** Option B standard MySQL workaround query hai for FULL OUTER JOIN.

---

### Q25. Interview Question: `SELECT * FROM A RIGHT JOIN B ON A.id = B.id` aur `SELECT * FROM B LEFT JOIN A ON B.id = A.id` exact identical kyun hote hain?

A) Kyunki `FROM` aur `JOIN` me tables swap karne se Left aur Right table references exchange ho jate hain  
B) Kyunki MySQL syntax check skip kar deta hai  
C) Kyunki dono `INNER JOIN` ban jate hain  
D) Memory cache ke waja se  

**Answer:** A

**Explanation:** Table ordering swap karne se `RIGHT JOIN B` exactly `LEFT JOIN A` ke equal logic represent karta hai.

---

### Q26. Output Check: `SELECT d.department_name FROM students s RIGHT JOIN departments d ON s.department_id = d.department_id;` me Electrical department display hoga ya nahi?

A) Nahi, kyunki koi student nahi hai  
B) Haan, `'Electrical'` display hoga  
C) Syntax Error dega  
D) `'NULL'` string aayega  

**Answer:** B

**Explanation:** `department_name` Right table (`departments`) ka column hai, isliye `'Electrical'` clear print hoga.

---

### Q27. Accenture Trap Question: Agar koi developer Direct MySQL me query likhe: `SELECT * FROM students FULL OUTER JOIN departments ON ...` toh kya hoga?

A) Query perfectly run hogi  
B) `ERROR 1064 (42000): You have an error in your SQL syntax`  
C) Database shut down ho jayega  
D) `INNER JOIN` run ho jayega  

**Answer:** B

**Explanation:** MySQL engine direct `FULL OUTER JOIN` keyword parse nahi kar pata aur syntax error return karta hai.

---

### Q28. Day 12 `RIGHT JOIN` query result grid me NULL student name ke aage kaunsa department name print hua?

A) `CSE`  
B) `Electrical`  
C) `Civil`  
D) `Mechanical`  

**Answer:** B

**Explanation:** Electrical department me student missing hone par row `NULL | Electrical` banti hai.

---

### Q29. `LEFT JOIN` (includes Vikas `Vikas | NULL`) aur `RIGHT JOIN` (includes Electrical `NULL | Electrical`) ko `UNION` karne par total DISTINCT output rows kitni aati hain Day 12 DB me?

A) 8 rows  
B) 10 rows (8 matching + 1 Vikas + 1 Electrical)  
C) 15 rows  
D) 5 rows  

**Answer:** B

**Explanation:** 8 mutual matching rows + 1 left unmatched (Vikas) + 1 right unmatched (Electrical) = Total 10 unique rows in FULL OUTER JOIN.

---

### Q30. Placement Master Question: Overlapping (matching) + Non-overlapping (unmatched left & right) complete dataset 360-degree visibility ke liye RDBMS feature ko kya kehte hain?

A) `INNER JOIN`  
B) `FULL OUTER JOIN`  
C) `CROSS JOIN`  
D) `SELF JOIN`  

**Answer:** B

**Explanation:** `FULL OUTER JOIN` complete 360-degree dataset visibility provide karta hai combining matched and unmatched rows from both tables.
