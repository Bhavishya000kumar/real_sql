# Day 10 MCQs

## Quick Revision

Before attempting the MCQs, let's quickly review all key concepts covered in `day10.md`.

### 1. `INNER JOIN` Definition & Core Purpose
- **Purpose**: Do tables ke **matching records** ko unke common key columns (Primary Key & Foreign Key) ke basis par combine karna.
- **Rule**: `INNER JOIN` sirf aur sirf wahi rows return karta hai jinke IDs dono tables me match hote hain. Non-matching records output se discard/ignore ho jate hain.

### 2. Standard `INNER JOIN` Syntax
```sql
SELECT column_names
FROM table1
INNER JOIN table2
ON table1.common_column = table2.common_column;
```
- **`FROM`**: Primary / Left table.
- **`INNER JOIN`**: Connected Right table.
- **`ON`**: Join condition (`table1.common_column = table2.common_column`).

### 3. Table Prefix & Dot Notation (`Table.Column`)
- Multi-table queries me jab dono tables me same column name (e.g., `department_id`) ho, toh `Table.Column` notation use kiya jata hai (`students.department_id`).
- Dot notation computer ko explicit path batata hai taaki column name collision na ho.

### 4. Table Aliases (`s`, `d`)
- **Definition**: Table Aliases tables ke chhote nicknames hote hain (e.g., `students s`, `departments d`).
- **Syntax**: `FROM students s INNER JOIN departments d ON s.department_id = d.department_id;`
- **Advantage**: Queries concise, clean aur highly readable ban jaati hain without altering query behavior or performance.

### 5. `SELECT *` Behavior in JOINs
- `SELECT *` execute karne par dono tables ke saare columns combined result set me return hote hain.
- **Note**: Common join key column (e.g., `department_id`) output grid me **2 baar** display hota hai (ek `students` table ka, ek `departments` table ka).

### 6. Ambiguous Column Error (`ERROR 1052`) ⭐⭐⭐⭐⭐
- **Problem**: Selective common column (e.g., `department_id`) ko bina table prefix ya alias ke `SELECT` list me likhna (`SELECT department_id FROM students s ...` ❌).
- **Cause**: MySQL confuse ho jata hai ki column `students` se pick kare ya `departments` se.
- **Fix**: Column ke aage Table Alias / Prefix explicitly lagayein (`SELECT s.department_id ...` ✅).

---

## 30 Most Important MCQs

---

### Q1. SQL me `INNER JOIN` ka primary objective kya hota hai?

A) Sabhi rows ko delete karna  
B) Do tables ke sirf **matching records** ko combine karke output display karna  
C) Table B ki saari rows aur Table A ki NULL rows display karna  
D) Duplicate tables create karna  

**Answer:** B

**Explanation:** `INNER JOIN` do tables ke rows ko unn common key columns ke basis par combine karta hai jahan matching condition true hoti hai.

---

### Q2. `INNER JOIN` query me dono tables ko connect karne wali matching condition kis clause me specify ki jaati hai?

A) `WHERE`  
B) `GROUP BY`  
C) `ON`  
D) `HAVING`  

**Answer:** C

**Explanation:** `INNER JOIN` me connecting key equality condition (`table1.key = table2.key`) `ON` clause ke under specify ki jaati hai.

---

### Q3. Niche di gayi SQL `INNER JOIN` query ka correct clause execution sequence kya hai?

A) `INNER JOIN` ➔ `FROM` ➔ `SELECT` ➔ `ON`  
B) `SELECT` ➔ `FROM` ➔ `INNER JOIN` ➔ `ON`  
C) `ON` ➔ `SELECT` ➔ `FROM` ➔ `INNER JOIN`  
D) `FROM` ➔ `ON` ➔ `INNER JOIN` ➔ `SELECT`  

**Answer:** B

**Explanation:** SQL syntax structure: `SELECT column_names FROM table1 INNER JOIN table2 ON condition;`.

---

### Q4. SQL query me `students.department_id` likhte waqt dot (`.`) ka exact purpose kya hai?

A) String concatenation ke liye  
B) Table name aur Column name ko connect karke ambiguity finish karne ke liye (`Table.Column`)  
C) Floating point value define karne ke liye  
D) Alias delete karne ke liye  

**Answer:** B

**Explanation:** Dot notation `Table_Name.Column_Name` computer ko explicitly batata hai ki target column kis specific table se belong karta hai.

---

### Q5. Niche di gayi query me `s` aur `d` ko kya kaha jata hai?
```sql
SELECT s.student_name, d.department_name
FROM students s
INNER JOIN departments d
ON s.department_id = d.department_id;
```

A) Database Keys  
B) Table Aliases (Nicknames)  
C) Aggregate Functions  
D) Data Types  

**Answer:** B

**Explanation:** `students s` aur `departments d` me `s` aur `d` short nicknames (Table Aliases) hain jo query length reduce aur readability boost karte hain.

---

### Q6. Table Alias assign karne ke baad query execution / output result par kya effect padta hai?

A) Output set change ho jata hai  
B) Performance slow ho jaati hai  
C) Zero change in output; query text short aur readable ban jaati hai  
D) MySQL error return karta hai  

**Answer:** C

**Explanation:** Aliases purely readability aur code shorthand ke liye hote hain, inka query result ya execution output par koi bad prabhav nahi padta.

---

### Q7. Interview Favorite: Niche di gayi query ko execute karne par MySQL kya return karega?
```sql
SELECT department_id
FROM students s
INNER JOIN departments d
ON s.department_id = d.department_id;
```

A) Successful grid output  
B) `ERROR 1052 (23000): Column 'department_id' in field list is ambiguous`  
C) Empty set  
D) Database crash  

**Answer:** B

**Explanation:** `department_id` dono tables me exist karta hai. Select list me bina alias prefix (`s.` ya `d.`) ke likhne par MySQL ambiguity error return karta hai.

---

### Q8. Ambiguous Column Error ko resolve karne ke liye SQL query me kya fix karna chahiye?

A) `INNER JOIN` remove kar do  
B) Column ke aage explicit Table Prefix ya Alias lagayein (e.g., `s.department_id`)  
C) Table drop kar do  
D) `ON` clause hata do  

**Answer:** B

**Explanation:** Column name ke aage table alias prefix (`s.department_id` ya `d.department_id`) specify karne se ambiguous column error resolve ho jata hai.

---

### Q9. Output Check: `SELECT * FROM students s INNER JOIN departments d ON s.department_id = d.department_id;` run karne par output grid me `department_id` column kitni baar display hoga?

A) 0 baar  
B) Exactly 1 baar  
C) Exactly 2 baar  
D) 4 baar  

**Answer:** C

**Explanation:** `SELECT *` dono tables ke saare columns fetch karta hai, isliye `students` ka `department_id` aur `departments` ka `department_id` dono display hote hain (Total 2 times).

---

### Q10. Agar `students` table me student Vikas ka `department_id` 5 hai aur `departments` table me IDs (1, 2, 3, 4) hain, toh `INNER JOIN` Vikas ki row ke saath kya karega?

A) Output me Vikas ke department ko NULL dikhayega  
B) Row ko match na hone par ignore/discard kar dega (Output me nahi aayega)  
C) Default department 1 assign kar dega  
D) Query me error bhejega  

**Answer:** B

**Explanation:** `INNER JOIN` strictly only matching records ko include karta hai. Non-matching key (5) ignore kar di jaati hai.

---

### Q11. Real-Life Analogy: Aadhaar Table (101 Rahul) aur Bank Table (101 5000 Balance) par Aadhaar ID matching INNER JOIN ka output kya hoga?

A) Rahul | 5000  
B) Only Rahul  
C) Only 5000  
D) NULL | NULL  

**Answer:** A

**Explanation:** Key 101 dono tables me match hone par `INNER JOIN` combined row `Rahul | 5000` return karega.

---

### Q12. Niche di gayi SQL query me `ON s.department_id = d.department_id` ka exact role kya hai?

A) Sorting condition  
B) Filter condition jo verify karti hai ki dono tables ke `department_id` matching hain ya nahi  
C) Data insertion  
D) Grouping mechanism  

**Answer:** B

**Explanation:** `ON` clause specify karta hai ki right table ki kis row ko left table ki kis row ke saath link/match karna hai.

---

### Q13. `students` table (5 columns) aur `departments` table (2 columns) par `SELECT *` ke saath `INNER JOIN` chalane par total kitne columns return honge?

A) 5  
B) 2  
C) 7 columns  
D) 10 columns  

**Answer:** C

**Explanation:** `SELECT *` dono tables ke saare columns pick karta hai: 5 (students) + 2 (departments) = 7 total columns.

---

### Q14. Multi-table query me Column Ambiguity error kahan aane ke sabse high chances hote hain?

A) Jo columns dono tables me unique hain (e.g., `student_name`, `department_name`)  
B) Primary Key / Foreign Key columns jo dono tables me identical names share karte hain (e.g., `department_id`)  
C) Table Alias me  
D) `FROM` clause me  

**Answer:** B

**Explanation:** Column ambiguity tab occur hoti hai jab multiple joined tables me identical column names exist karte hain aur query me explicit table prefix miss hota hai.

---

### Q15. Day 10 ke sample dataset me `students` table ke saare 8 students ke `department_id` (1, 2, 3, 4) valid departments se match hote hain. `INNER JOIN` run karne par kitni rows output me aayengi?

A) 4 rows  
B) 8 rows  
C) 12 rows  
D) 0 rows  

**Answer:** B

**Explanation:** Chunki saare 8 students ke department IDs valid parent department IDs se match hote hain, `INNER JOIN` saari 8 rows return karega.

---

### Q16. Company DB Scenario: `employees` (e) table aur `projects` (p) table me matching project records find karne ke liye correct `INNER JOIN` condition kya hogi?

A) `ON e.proj_id = p.proj_id`  
B) `ON e.name = p.proj_id`  
C) `WHERE e.proj_id > p.proj_id`  
D) `GROUP BY e.proj_id`  

**Answer:** A

**Explanation:** Matching equality condition Foreign Key (`e.proj_id`) aur Primary Key (`p.proj_id`) ke beech `= ` operator se establish hoti hai.

---

### Q17. Statement Check: Kya `INNER JOIN` bina `ON` clause ke valid relational matching performance perform kar sakta hai?

A) Haan, `ON` clause optional hota hai  
B) Nahi, without `ON` clause condition syntax incomplete/error hota hai  
C) `ON` clause ki jagah `GROUP BY` compulsory hai  
D) `INNER JOIN` me `SELECT` optional hota hai  

**Answer:** B

**Explanation:** Relational `INNER JOIN` query ko establish hone ke liye `ON` condition block ka hona mandatory hai.

---

### Q18. MySQL me Ambiguous Column error kis error code number dwara represent hota hai?

A) `ERROR 404`  
B) `ERROR 1052`  
C) `ERROR 1000`  
D) `ERROR 500`  

**Answer:** B

**Explanation:** MySQL internal error catalog me `ERROR 1052 (23000): Column in field list is ambiguous` hota hai.

---

### Q19. Table alias assign karte waqt konsa keyword optional hota hai? (e.g., `FROM students AS s`)

A) `JOIN`  
B) `AS`  
C) `ON`  
D) `SELECT`  

**Answer:** B

**Explanation:** Table alias me `AS` keyword optional hota hai; `FROM students s` aur `FROM students AS s` dono exact identical kaam karte hain.

---

### Q20. Niche di gayi query me output list me kitni columns return hongi?
```sql
SELECT s.student_name, s.city, d.department_name
FROM students s
INNER JOIN departments d
ON s.department_id = d.department_id;
```

A) 1  
B) 2  
C) 3 columns (`student_name`, `city`, `department_name`)  
D) 7 columns  

**Answer:** C

**Explanation:** `SELECT` list me explicitly 3 columns (`s.student_name`, `s.city`, `d.department_name`) specify kiye gaye hain.

---

### Q21. Scenario-based Question: Agar Table A me 5 rows hain aur Table B me 5 rows hain, lekin unke IDs me sirf 3 records matching hain, toh `INNER JOIN` ka result size kya hoga?

A) 10 rows  
B) 5 rows  
C) 3 rows  
D) 0 rows  

**Answer:** C

**Explanation:** `INNER JOIN` purely matching records filter karta hai, isliye response me sirf 3 matching rows aayengi.

---

### Q22. Tricky Question: Table Aliases assign karne ke baad agar query me full table name (`students.department_id`) use karein toh kya hoga?

A) Query crash ho jayegi  
B) MySQL error de sakta hai ki table name recognized nahi hai kyunki alias define hone ke baad MySQL script scope me alias expect karta hai  
C) Output double ho jayega  
D) Database drop ho jayega  

**Answer:** B

**Explanation:** Jab table ko alias (e.g. `students s`) diya jata hai, tab target scope me alias (`s.department_id`) use karna strict standard rule hota hai.

---

### Q23. Enterprise level par production queries me Table Aliases use karne ka main reason kya hai?

A) Query parsing speed slow karne ke liye  
B) Code brevity, query clean design, aur column ambiguity prevent karne ke liye  
C) Primary Key delete karne ke liye  
D) Automatic backup lene ke liye  

**Answer:** B

**Explanation:** Production queries complex multiple joins hold karti hain jahan Aliases code readability maintain rakhte hain aur ambiguity avoid karte hain.

---

### Q24. Niche di gayi code snippet me correct modification kya hona chahiye?
```sql
SELECT student_name, age, department_name
FROM students s
INNER JOIN departments d
ON s.department_id = d.department_id;
```

A) `student_name` par `s.` aur `department_name` par `d.` alias prefix lagana best engineering practice hai  
B) Query invalid hai  
C) `ON` clause ko drop kar do  
D) `age` column par `INNER JOIN` allow nahi hota  

**Answer:** A

**Explanation:** Although `student_name` ambiguous nahi hai, production standard code me sabhi SELECT columns ke aage respective table alias prefix (`s.student_name`, `s.age`, `d.department_name`) lagana clean practice hoti hai.

---

### Q25. SQL me `ON` clause aur `WHERE` clause ke beech primary difference kya hai in JOIN context?

A) `ON` clause join matching condition define karta hai; `WHERE` clause combined results par row filtering apply karta hai  
B) `ON` clause duplicate values delete karta hai  
C) `WHERE` clause tables ko connect karta hai  
D) Dono exact identical function hain  

**Answer:** A

**Explanation:** `ON` clause relational matching condition form karta hai, jabki `WHERE` clause join hone ke baad records filter karne ke liye use hota hai.

---

### Q26. Practical Query check: Student Name ke saath unka City fetch karne ke liye JOIN ki zaroorat kyun nahi hoti?

A) Kyunki City aur Student Name dono akele `students` table me available hain  
B) City column illegal hai  
C) `JOIN` sirf numbers par chalta hai  
D) Workbench single column block karta hai  

**Answer:** A

**Explanation:** Jab saare required columns ek single table (`students`) me exist karte hain, tab multi-table `JOIN` query chalane ki zaroorat nahi hoti.

---

### Q27. Accenture Trap Question: Kya Table Alias humesha single character (`s`, `d`) hi hona chahiye?

A) Haan, rules strict hain  
B) Nahi, alias koi bhi meaningful string ya abbreviation ho sakta hai (e.g., `stu`, `dept`)  
C) Alias maximum 2 letters ka hota hai  
D) Alias Humesha Numbers hona chahiye  

**Answer:** B

**Explanation:** Table Alias koi bhi valid identifier name ho sakta hai (e.g. `students stu`, `departments dept`). Single character simple shorthand convention hai.

---

### Q28. If a student row in `students` table has `department_id = NULL`, will `INNER JOIN` output include that student?

A) Yes, with NULL department name  
B) No, because `NULL = department_id` comparison fails in INNER JOIN  
C) Yes, with default CSE department  
D) Query will crash  

**Answer:** B

**Explanation:** `INNER JOIN` matching equality check karta hai; `NULL` value parent table primary key se match nahi hoti, isliye record exclude ho jata hai.

---

### Q29. Interview Question: SQL queries me agar keyword `INNER JOIN` ki jagah sirf `JOIN` likha jaye, toh MySQL konsa join type execute karta hai?

A) `LEFT JOIN`  
B) Default `INNER JOIN`  
C) `CROSS JOIN`  
D) Error return karega  

**Answer:** B

**Explanation:** SQL standard me plain `JOIN` write karne par MySQL default `INNER JOIN` hi perform karta hai.

---

### Q30. Placement Core Question: `ON s.department_id = d.department_id` condition me `=` operator ka main function kya hai?

A) Assignment operator  
B) Equality comparison operator jo foreign key aur primary key ke matching values filter karta hai  
C) Increment operator  
D) String concatenation  

**Answer:** B

**Explanation:** `=` comparison operator verification karta hai ki child table ka `department_id` aur parent table ka `department_id` equal/matched hain ya nahi.
