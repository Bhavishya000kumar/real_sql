# Day 6 — Quick Revision + 30 MCQs

---

## Quick Revision

Before attempting the MCQs, let's quickly review all key concepts covered in `day6.md`.

### 1. Range Filtering (`BETWEEN` Operator)
- **Purpose:** Range ke andar values fetch karne ke liye (`WHERE col BETWEEN val1 AND val2;`).
- **Inclusive Nature:** `BETWEEN` lower bound aur upper bound **DONO ko include** karta hai (`BETWEEN 20 AND 22` ➔ Includes 20, 21, 22).
- ⚠️ **Trap:** `WHERE age BETWEEN 20 TO 22;` ❌ (Use `AND`, not `TO`).

### 2. Deduplication (`DISTINCT` Clause)
- **Purpose:** Query output result set me se duplicate values ko eliminate karna (`SELECT DISTINCT col FROM table;`).
- **Comparison:** `SELECT city` (returns duplicates) vs `SELECT DISTINCT city` (returns unique values only).

### 3. Missing Data (`IS NULL` / `IS NOT NULL`)
- **NULL Definition:** Missing, unknown, or unavailable data value (NOT 0, NOT empty string `""`).
- ⚠️ **Dangerous Trap:** `WHERE phone = NULL;` ❌ (NULL kisi value ke equal nahi hota! Always use `WHERE phone IS NULL;` or `WHERE phone IS NOT NULL;`).

### 4. Data Modification (`UPDATE` Statement)
- **Syntax:** `UPDATE table_name SET column_name = value WHERE condition;`
- **Multiple Columns:** `UPDATE student SET name = 'Rahul', age = 22 WHERE id = 1;`
- ⚠️ **Dangerous Trap:** Executing `UPDATE student SET age = 50;` without `WHERE` clause updates EVERY ROW in the table to 50!

### 5. Data Removal (`DELETE` vs `TRUNCATE` vs `DROP TABLE`)
- **`DELETE` (DML):** Specific rows delete karta hai (`DELETE FROM student WHERE id = 4;`). Without `WHERE`, deletes all rows slowly row-by-row. Structure remains.
- **`TRUNCATE` (DDL):** Table ke saare rows ko instantly reset/empty kar deta hai (`TRUNCATE TABLE student;`). Faster than DELETE. Structure remains intact.
- **`DROP TABLE` (DDL):** Table structure + table schema + all data permanently delete kar deta hai.

### 6. Schema Alteration (`ALTER TABLE`)
- **Add Column:** `ALTER TABLE student ADD phone VARCHAR(15);`
- **Drop Column:** `ALTER TABLE student DROP COLUMN phone;`
- **Rename Column:** `ALTER TABLE student RENAME COLUMN name TO student_name;`
- **Rename Table:** `ALTER TABLE student RENAME TO students;`

---

## 30 Most Important MCQs

---

### Q1. Range filtering ke liye `BETWEEN` operator ke regarding kaunsa statement TRUE hai?

A. `BETWEEN` boundary values ko exclude karta hai  
B. `BETWEEN` boundary values ko INCLUSIVELY include karta hai  
C. `BETWEEN` string values par kaam nahi karta  
D. `BETWEEN` me `OR` keyword use hota hai  

**Answer:** B

**Explanation:** `BETWEEN val1 AND val2` inclusive hota hai, matlab `val1` aur `val2` dono output result me include honge.

---

### Q2. Query `SELECT * FROM student WHERE age BETWEEN 20 AND 22;` ka equivalent `AND` syntax query kya hoga?

A. `SELECT * FROM student WHERE age = 20 OR age = 22;`  
B. `SELECT * FROM student WHERE age >= 20 AND age <= 22;`  
C. `SELECT * FROM student WHERE age > 20 AND age < 22;`  
D. `SELECT * FROM student WHERE age IN (20, 22);`  

**Answer:** B

**Explanation:** `BETWEEN 20 AND 22` is logically identical to `>= 20 AND <= 22`.

---

### Q3. Syntax Check: `BETWEEN` operator ka CORRECT syntax kaunsa hai?

A. `WHERE age BETWEEN 20 TO 22;` ❌  
B. `WHERE age BETWEEN 20 AND 22;` ✅  
C. `WHERE age BETWEEN (20, 22);` ❌  
D. `WHERE age BETWEEN 20 - 22;` ❌  

**Answer:** B

**Explanation:** `BETWEEN` clause me values ke beech `AND` keyword specify kiya jata hai (`BETWEEN lower AND upper`).

---

### Q4. Table result grid me se Duplicate values ko remove karke sirf Unique values dekhne ke liye kaunsa keyword use hota hai?

A. `UNIQUE`  
B. `DISTINCT`  
C. `DIFFERENT`  
D. `SINGLE`  

**Answer:** B

**Explanation:** `SELECT DISTINCT column_name FROM table;` duplicate rows/values ko filter out kar ke unique records return karta hai.

---

### Q5. Database में `NULL` value ka real meaning kya hota hai?

A. Integer `0`  
B. Empty String `""`  
C. Missing / Unknown / Unavailable data  
D. String `"NULL"`  

**Answer:** C

**Explanation:** `NULL` denotes missing or unknown data. It is NOT zero and NOT an empty string.

---

### Q6. Dangerous Trap Alert: Database me phone number missing hone par filter karne ki CORRECT query kya hogi?

A. `SELECT * FROM student WHERE phone = NULL;` ❌  
B. `SELECT * FROM student WHERE phone IS NULL;` ✅  
C. `SELECT * FROM student WHERE phone == NULL;` ❌  
D. `SELECT * FROM student WHERE phone EQUALS NULL;` ❌  

**Answer:** B

**Explanation:** SQL me NULL kisi bhi value ke equal check nahi hota (`= NULL` is invalid). NULL check karne ke liye strictly `IS NULL` use hota hai.

---

### Q7. Existing table record ke data values me changes karne ke liye kaunsi SQL DML command use hoti hai?

A. `CHANGE`  
B. `MODIFY`  
C. `UPDATE`  
D. `ALTER`  

**Answer:** C

**Explanation:** Existing rows ke attributes update/modify karne ke liye `UPDATE table_name SET col = val WHERE condition;` command use hoti hai.

---

### Q8. Single record update: Student ID = 1 ki age ko 21 update karne ki correct SQL query kya hai?

A. `UPDATE student SET age = 21 WHERE id = 1;`  
B. `MODIFY student SET age = 21 WHERE id = 1;`  
C. `UPDATE student AGE = 21 WHERE id = 1;`  
D. `ALTER TABLE student SET age = 21 WHERE id = 1;`  

**Answer:** A

**Explanation:** Correct syntax `UPDATE table_name SET column_name = value WHERE condition;` hota hai.

---

### Q9. Dangerous Mistake Alert: Candidate ne query chalayi `UPDATE student SET age = 50;` (without WHERE clause). Outcome kya hoga?

A. Query syntax error degi  
B. Table ke SAARE students ki age 50 ho jayegi  
C. Pehle student ki age 50 hogi  
D. Kuch nahi hoga  

**Answer:** B

**Explanation:** `UPDATE` query me `WHERE` clause omit karne par table ki target column ki SAARI rows update ho jaati hain.

---

### Q10. Ek hi query me Multiple Columns update karne ka correct syntax kaunsa hai?

A. `UPDATE student SET name = 'Rahul', age = 22 WHERE id = 1;`  
B. `UPDATE student SET name = 'Rahul' AND age = 22 WHERE id = 1;`  
C. `UPDATE student SET name = 'Rahul' SET age = 22 WHERE id = 1;`  
D. `UPDATE student (name = 'Rahul', age = 22) WHERE id = 1;`  

**Answer:** A

**Explanation:** `UPDATE` me multiple columns comma `,` se separate karke `SET col1 = val1, col2 = val2` format me likhe jate hain.

---

### Q11. Specific row (e.g. ID = 4) ko table me se delete karne ki correct query kya hai?

A. `REMOVE FROM student WHERE id = 4;`  
B. `DELETE FROM student WHERE id = 4;`  
C. `DROP FROM student WHERE id = 4;`  
D. `TRUNCATE FROM student WHERE id = 4;`  

**Answer:** B

**Explanation:** Specific row deletion ke liye `DELETE FROM table_name WHERE condition;` syntax use hota hai.

---

### Q12. Dangerous Mistake: `DELETE FROM student;` query run karne par kya hoga?

A. Table structure delete ho jayega  
B. Table ka SAARA data rows delete ho jayega (lekin table structure bacha rahega)  
C. Syntax error aayega  
D. Sirf pehli row delete hogi  

**Answer:** B

**Explanation:** Without `WHERE` clause, `DELETE FROM table;` table ke saare records slowly row-by-row delete kar deta hai, par table schema intact rehta hai.

---

### Q13. `TRUNCATE TABLE student;` command ke regarding kaunsa statement TRUE hai?

A. Ye table schema aur structure ko bhi delete kar deta hai  
B. Ye table ke saare rows ko ek baar me fast empty kar deta hai, jabki table structure remain karta hai  
C. Ye `WHERE` clause accept karta hai  
D. Ye DML command hai  

**Answer:** B

**Explanation:** `TRUNCATE` ek DDL command hai jo table ki saari rows ko instantly reset kar ke table empty kar deti hai, while preserving schema structure.

---

### Q14. Interview Master Question: `DELETE`, `TRUNCATE`, aur `DROP TABLE` ke differences par correct pair select karein:

A. `DELETE` = DDL, `TRUNCATE` = DML, `DROP` = DCL  
B. `DELETE` = Row-by-row DML, `TRUNCATE` = Fast table reset DDL (Structure remains), `DROP` = Deletes structure + data DDL  
C. `DELETE` aur `TRUNCATE` dono table schema drop kar dete hain  
D. `DROP TABLE` `WHERE` clause accept karta hai  

**Answer:** B

**Explanation:** `DELETE` row-level DML hai, `TRUNCATE` table-level reset DDL hai (schema bacha rehta hai), aur `DROP TABLE` schema + data dono ko drop kar deta hai.

---

### Q15. Table structure me NAYA COLUMN (`phone VARCHAR(15)`) add karne ki correct command kya hai?

A. `UPDATE TABLE student ADD phone VARCHAR(15);`  
B. `ALTER TABLE student ADD phone VARCHAR(15);`  
C. `INSERT INTO student ADD phone VARCHAR(15);`  
D. `MODIFY TABLE student ADD phone VARCHAR(15);`  

**Answer:** B

**Explanation:** Table schema alter/modify karne ke liye `ALTER TABLE table_name ADD col_name datatype;` use hota hai.

---

### Q16. Table structure me se existing column (`phone`) ko REMOVE/DELETE karne ki command kya hai?

A. `ALTER TABLE student DROP COLUMN phone;`  
B. `DELETE COLUMN phone FROM student;`  
C. `REMOVE COLUMN phone FROM student;`  
D. `ALTER TABLE student DELETE phone;`  

**Answer:** A

**Explanation:** Column drop karne ke liye `ALTER TABLE table_name DROP COLUMN column_name;` command execute hoti hai.

---

### Q17. Table ke column ka naam rename karne (`name` ➔ `student_name`) ki correct command kya hai?

A. `ALTER TABLE student RENAME COLUMN name TO student_name;`  
B. `UPDATE student RENAME name TO student_name;`  
C. `RENAME COLUMN name TO student_name IN student;`  
D. `ALTER COLUMN name TO student_name;`  

**Answer:** A

**Explanation:** Column rename karne ka standard syntax `ALTER TABLE table_name RENAME COLUMN old_name TO new_name;` hota hai.

---

### Q18. Entire Table ka naam rename karne (`student` ➔ `students`) ki correct syntax command kya hai?

A. `ALTER TABLE student RENAME TO students;`  
B. `RENAME TABLE student TO students;`  
C. Both A and B are valid SQL statements  
D. `UPDATE TABLE student NAME = students;`  

**Answer:** C

**Explanation:** MySQL me `ALTER TABLE student RENAME TO students;` aur `RENAME TABLE student TO students;` dono valid execution commands hain.

---

### Q19. Range Check Query: Dataset (Rahul-20, Aman-21, Rohit-22, Priya-19). Query:
```sql
SELECT * FROM student WHERE age BETWEEN 19 AND 21;
```
Output me kitni rows aayengi?

A. 2 Rows  
B. 3 Rows (Priya-19, Rahul-20, Aman-21)  
C. 4 Rows  
D. 1 Row  

**Answer:** B

**Explanation:** `BETWEEN 19 AND 21` includes 19, 20, aur 21. Isliye Priya (19), Rahul (20), aur Aman (21) return honge (3 rows).

---

### Q20. Range Check Query: Dataset (Rahul-id 1, Aman-id 2, Rohit-id 3, Priya-id 4). Query:
```sql
SELECT * FROM student WHERE id BETWEEN 2 AND 4;
```
Output me kaun-kaun se IDs honge?

A. ID 2, ID 3  
B. ID 2, ID 3, ID 4 (Aman, Rohit, Priya)  
C. ID 3, ID 4  
D. ID 1, ID 2, ID 3, ID 4  

**Answer:** B

**Explanation:** `BETWEEN 2 AND 4` inclusive check me ID 2, ID 3, aur ID 4 (Aman, Rohit, Priya) return karega.

---

### Q21. Duplicate City Query: Table me values hain (`Delhi`, `Delhi`, `Mumbai`, `Delhi`, `Mumbai`). Query: `SELECT DISTINCT city FROM student;` Output grid me kya dikhega?

A. Delhi, Delhi, Mumbai, Delhi, Mumbai  
B. Delhi, Mumbai  
C. Delhi  
D. Mumbai  

**Answer:** B

**Explanation:** `DISTINCT` keyword duplicates ko filter karke single unique occurrences (`Delhi`, `Mumbai`) return karega.

---

### Q22. Null Filter Query: Table contains (Rahul-Phone: 987, Aman-Phone: NULL, Rohit-Phone: 986). Query:
```sql
SELECT name FROM student WHERE phone IS NOT NULL;
```
Output me kaun-kaun se names aayenge?

A. Aman  
B. Rahul, Rohit  
C. Rahul, Aman, Rohit  
D. Blank  

**Answer:** B

**Explanation:** `IS NOT NULL` filter sirf un records ko fetch karta hai jinka phone number missing nahi hai (Rahul aur Rohit).

---

### Q23. Update Query Outcome: Table row (ID 3, Name: Rohit, Age 22). Query run ki gayi:
```sql
UPDATE student SET name = 'Rohan' WHERE id = 3;
```
Table record me kya change aayega?

A. Record delete ho jayega  
B. ID 3 par name 'Rohit' change hokar 'Rohan' ho jayega (Age 22 same rahegi)  
C. Saari rows ka name Rohan ho jayega  
D. Error aayega  

**Answer:** B

**Explanation:** `UPDATE` strictly target row (`id = 3`) ke name attribute ko 'Rohan' me modify kar dega.

---

### Q24. Delete Query Outcome: Table (Rahul-1, Aman-2, Rohit-3, Priya-4). Query:
```sql
DELETE FROM student WHERE id = 2;
```
Select query run karne par kya dikhega?

A. Aman delete ho jayega, Rahul (1), Rohit (3), Priya (4) rahenge  
B. Saare students delete ho jayenge  
C. Table structure drop ho jayega  
D. ID 2 ki age 0 ho jayegi  

**Answer:** A

**Explanation:** `DELETE FROM ... WHERE id = 2` sirf Aman (ID 2) ki row ko remove karega.

---

### Q25. Common Syntax Error: Niche di gayi commands me se kaunsa statement Syntax Error dega?

A. `ALTER TABLE student ADD email VARCHAR(100);`  
B. `ALTER TABLE student DROP COLUMN email;`  
C. `ALTER student ADD email VARCHAR(100);` ❌  
D. `UPDATE student SET age = 25 WHERE id = 2;`  

**Answer:** C

**Explanation:** `ALTER` statement me `TABLE` keyword mandatory hai (`ALTER TABLE student...`). Option C me `TABLE` keyword missing hai.

---

### Q26. DDL vs DML Check: `UPDATE` aur `DELETE` kis SQL command category me aate hain?

A. DDL (Data Definition Language)  
B. DML (Data Manipulation Language)  
C. DCL (Data Control Language)  
D. TCL (Transaction Control Language)  

**Answer:** B

**Explanation:** Data values ko insert, update, aur delete karne wali commands `DML` (Data Manipulation Language) hoti hain.

---

### Q27. DDL vs DML Check: `CREATE`, `ALTER`, `TRUNCATE`, aur `DROP` kis SQL command category me aate hain?

A. DML  
B. DDL (Data Definition Language)  
C. DCL  
D. TCL  

**Answer:** B

**Explanation:** Table structure, schema definition, aur reset karne wali commands `DDL` (Data Definition Language) hoti hain.

---

### Q28. Practice Question Answer Check: Query `SELECT * FROM student WHERE age BETWEEN 19 AND 22 ORDER BY age DESC;` ka top record kaunsa student hoga?
(Dataset: Rahul-20, Aman-21, Rohit-22, Priya-19)

A. Priya (19)  
B. Rohit (22)  
C. Aman (21)  
D. Rahul (20)  

**Answer:** B

**Explanation:** `BETWEEN 19 AND 22` saare students select karta hai. `ORDER BY age DESC` largest age (22 - Rohit) ko top row me display karega.

---

### Q29. Practice Question Answer Check: `student` table me `email VARCHAR(100)` column add karke, apply baad me use remove karne ki 2 commands ka sahi pair chuniyen:

A. `ALTER TABLE student ADD email VARCHAR(100);` AND `ALTER TABLE student DROP COLUMN email;`  
B. `UPDATE student ADD email;` AND `DELETE email FROM student;`  
C. `CREATE email;` AND `DROP email;`  
D. `INSERT email;` AND `REMOVE email;`  

**Answer:** A

**Explanation:** Schema me column add karne ke liye `ALTER TABLE ... ADD ...` aur drop karne ke liye `ALTER TABLE ... DROP COLUMN ...` correct SQL syntax hai.

---

### Q30. Synthesis Scenario: Niche diye gaye 3 operations ka cumulative result kya hoga?
```sql
-- Step 1: Table student (Rahul-20, Aman-21, Rohit-22, Priya-19)
UPDATE student SET age = 25 WHERE name = 'Aman';
DELETE FROM student WHERE age < 20;
SELECT COUNT(*) FROM student WHERE age BETWEEN 21 AND 25;
```
Output count kya return hoga?

A. 1  
B. 2 (Aman-25, Rohit-22)  
C. 3  
D. 0  

**Answer:** B

**Explanation:**  
1. Step 1: Aman ki age 21 ➔ 25 ho gayi. (Rahul-20, Aman-25, Rohit-22, Priya-19).  
2. Step 2: `DELETE WHERE age < 20` removes Priya (19). Remaining: Rahul (20), Aman (25), Rohit (22).  
3. Step 3: `WHERE age BETWEEN 21 AND 25` matches Rohit (22) and Aman (25). (Rahul-20 is excluded).  
Count is strictly 2.
