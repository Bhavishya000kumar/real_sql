# Day 2 — Revision + 30 MCQs

---

## Part 1 — Quick Revision

Before attempting the MCQs, let's quickly review all key concepts covered in `day2.md`.

### 1. Database to Table Hierarchy (`CREATE TABLE`)
- **Hierarchy:** `MySQL Server` ──► `Database` (`college`) ──► `Table` (`student`).
- **Analogy:** Database = Cupboard, Tables = Files inside cupboard.
- **Syntax:**
  ```sql
  CREATE TABLE student(
      id INT,
      name VARCHAR(50),
      age INT
  );
  ```
- **Data Types:**
  - **`INT`:** Whole integers (e.g., `1`, `20`, `100`). Decimals (`20.5`) or text strings are NOT allowed.
  - **`VARCHAR(50)`:** Variable character text up to maximum 50 characters (e.g., `'Rahul'`, `'Aman'`).
- **Verification:** Execute via `Ctrl + Enter` in MySQL Workbench, then refresh `Schemas` ➔ `college` ➔ `Tables`.

### 2. Single Row Data Insertion (`INSERT INTO`)
- **Syntax:**
  ```sql
  INSERT INTO student(id, name, age)
  VALUES (1, 'Rahul', 20);
  ```
- **Quotes Rule:**
  - Text / String values (`'Rahul'`, `'Aman'`) strictly **Single Quotes `' '`** me likhein.
  - Numeric / Integer values (`1`, `20`) **bina quotes** ke specify karein.

### 3. Data Retrieval (`SELECT` Statement)
- **Syntax:**
  - **All Columns:** `SELECT * FROM student;` (`*` = Star Wildcard for all columns).
  - **Specific Column:** `SELECT name FROM student;`
  - **Multiple Columns:** `SELECT id, name FROM student;`
- **Library Analogy:** Librarian se specific book mangna = Selecting target data columns.

### 4. Multiple Rows Insertion & Best Practices
- **Industry Standard Batch Syntax:**
  ```sql
  INSERT INTO student(id, name, age)
  VALUES
  (2, 'Aman', 21),
  (3, 'Rohit', 22),
  (4, 'Priya', 19);
  ```
  *(Tuples are separated by commas `,` and terminated with a semicolon `;`.)*
- ⚠️ **Common Trap:** Row tuples ke beech comma `,` lagana bhool jana.
- 💡 **Best Practice / Production Rule:** Always specify column names explicitly (`INSERT INTO student(id, name, age)`). Omitting column names (`INSERT INTO student VALUES(...)`) is fragile because future schema alterations will break queries.

### 5. Data Filtering (`WHERE` Clause)
- **Purpose:** Rows filter karna based on condition (Amazon filter analogy: Brand='Nike', Price < 3000).
- **Basic Syntax:**
  ```sql
  SELECT * FROM student WHERE condition;
  ```
- **Quotes Rule in `WHERE`:**
  - `WHERE name = 'Aman';` ✅ (Text value in single quotes)
  - `WHERE age = 20;` ✅ (Numeric value without quotes)

### 6. Comparison Operators in `WHERE` Clause
| Operator | Meaning | Example |
| :---: | :--- | :--- |
| `=` | Equal | `WHERE age = 20` |
| `>` | Greater Than (Excludes boundary) | `WHERE age > 20` |
| `<` | Less Than (Excludes boundary) | `WHERE age < 20` |
| `>=` | Greater Than Equal (Includes boundary) | `WHERE age >= 20` |
| `<=` | Less Than Equal (Includes boundary) | `WHERE age <= 20` |
| `!=` | Not Equal | `WHERE age != 20` |

- 🧠 **Row-by-Row Execution:** MySQL checks `WHERE` condition on each individual row. Only rows evaluating to `TRUE` are returned in the output grid.
- ⭐ **Interview Difference (`>` vs `>=`):** `>` strict inequality hai jo target boundary value (e.g. 20) ko exclude karta hai, jabki `>=` boundary value (20) ko bhi output me include karta hai.

---

## Part 2 — 30 MCQs

---

### Q1. MySQL database ke andar actual records/data kahan store hota hai?

A. Server level par  
B. Table ke andar  
C. Schema configuration file mein  
D. Workbench editor mein  

**Answer:** B

**Explanation:** Real-life analogy ke according, Database ek cupboard hai aur uske andar actual records Files i.e. Tables ke andar rows/columns me store hote hain.

---

### Q2. Table create karne ke liye kaunsi SQL DDL command use hoti hai?

A. `MAKE TABLE table_name`  
B. `BUILD TABLE table_name`  
C. `CREATE TABLE table_name(...)`  
D. `SET TABLE table_name`  

**Answer:** C

**Explanation:** SQL mein naye table structure ko define aur create karne ke liye standard syntax `CREATE TABLE table_name(...)` hota hai.

---

### Q3. SQL mein integer (poore numbers like 1, 20, 100) store karne ke liye kaunsa data type use hota hai?

A. `TEXT`  
B. `INT`  
C. `VARCHAR`  
D. `STRING`  

**Answer:** B

**Explanation:** `INT` data type whole integers store karne ke liye use hota hai. Decimals (`20.5`) ya text strings (`'Rahul'`) `INT` data type me allowed nahi hote.

---

### Q4. `VARCHAR(50)` data type ka kya matlab hai?

A. Exact 50 fixed numbers store karega  
B. Variable character text store karega jiski maximum length 50 characters tak ho sakti hai  
C. Exactly 50 rows create karega  
D. Table ko 50 seconds tak lock rakhega  

**Answer:** B

**Explanation:** `VARCHAR(50)` Variable Character text store karta hai jahan maximum 50 characters tak strings allowed hoti hain (e.g. `'Rahul'`, `'Aman'`).

---

### Q5. Niche di gayi SQL command mein line 3 ka kya role hai?

```sql
CREATE TABLE student(
    id INT,
    name VARCHAR(50),
    age INT
);
```

A. Table ka name specify karna  
B. `name` column define karna jo maximum 50 characters ka text store karega  
C. Column ko primary key banana  
D. Data insert karna  

**Answer:** B

**Explanation:** Line 3 (`name VARCHAR(50),`) `name` column define kar rahi hai variable character text data type ke saath.

---

### Q6. Single row data insert karne ke liye correct SQL command kaunsi hai?

A. `ADD INTO student VALUES (1, 'Rahul', 20);`  
B. `INSERT INTO student(id, name, age) VALUES (1, 'Rahul', 20);`  
C. `PUT INTO student VALUES (1, 'Rahul', 20);`  
D. `UPDATE student SET (1, 'Rahul', 20);`  

**Answer:** B

**Explanation:** Table mein naya data populate karne ke liye `INSERT INTO table_name(columns) VALUES(data)` syntax use hota hai.

---

### Q7. SQL mein String/Text data (like 'Rahul') aur Integer data (like 20) ko values mein kaise pass kiya jata hai?

A. String ko single quotes `' '` me aur Integer ko bina quotes ke  
B. Integer ko single quotes `' '` me aur String ko bina quotes ke  
C. Dono ko double quotes `" "` me  
D. Dono ko bina quotes ke  

**Answer:** A

**Explanation:** Rules ke according text data hamesha single quotes `'Rahul'` me likha jata hai, jabki numeric integers `20` bina quotes ke likhe jate hain.

---

### Q8. Single row insertion command run karne ke baad table me inserted data check karne ke liye verification query kya hai?

A. `SHOW DATA FROM student;`  
B. `SELECT * FROM student;`  
C. `GET * FROM student;`  
D. `FETCH student;`  

**Answer:** B

**Explanation:** `SELECT * FROM student;` query `student` table ke saare columns aur inserted rows ko fetch/display karti hai.

---

### Q9. `SELECT * FROM student;` query mein Star (`*`) symbol ka kya meaning hai?

A. First row select karna  
B. Table ke SAARE columns (`id`, `name`, `age`) fetch/display karna  
C. Random row select karna  
D. Table row count batana  

**Answer:** B

**Explanation:** `SELECT` query mein `*` wildcard ka matlab hota hai "Table ke saare columns dikhao".

---

### Q10. Library analogy ke according, librarian se bolna "DBMS book dikhao" kis SQL operation se similarity rakhta hai?

A. `CREATE TABLE`  
B. `INSERT INTO`  
C. `SELECT`  
D. `DROP DATABASE`  

**Answer:** C

**Explanation:** Jaise library se specific book mangna retrieval operation hai, waise hi SQL me data view karne ke liye `SELECT` statement execute karte hain.

---

### Q11. Agar hume `student` table se SIRF `name` column dekhna hai (baaki columns nahi), to query kya hogi?

A. `SELECT * FROM student;`  
B. `SELECT name FROM student;`  
C. `SELECT id, age FROM student;`  
D. `SHOW name FROM student;`  

**Answer:** B

**Explanation:** `*` ki jagah exact column name i.e. `SELECT name FROM student;` likhne se output grid me strictly `name` column dikhta hai.

---

### Q12. Agar hum `SELECT id, name FROM student;` run karein, to output grid mein kaunsa column NAHI aayega?

A. `id`  
B. `name`  
C. `age`  
D. Koi bhi column nahi aayega  

**Answer:** C

**Explanation:** Query mein explicitly sirf `id` aur `name` select kiye gaye hain, isliye `age` column output grid mein include nahi hoga.

---

### Q13. Single `INSERT` query se Multiple Rows insert karne ka industry standard batch syntax kaunsa hai?

A. 
```sql
INSERT INTO student(id, name, age)
VALUES (2, 'Aman', 21), (3, 'Rohit', 22);
```

B. 
```sql
INSERT INTO student(id, name, age)
VALUES (2, 'Aman', 21) AND (3, 'Rohit', 22);
```

C. 
```sql
INSERT INTO student(id, name, age)
VALUES (2, 'Aman', 21); (3, 'Rohit', 22);
```

D. 
```sql
INSERT INTO student(id, name, age)
VALUES (2, 'Aman', 21) INTO (3, 'Rohit', 22);
```

**Answer:** A

**Explanation:** Multiple rows batch insertion ke liye `VALUES` keyword ke baad har row tuple ko comma `,` se separate karke end me single semicolon `;` lagaya jata hai.

---

### Q14. Common Mistake Alert: Niche di gayi multiple row insertion query mein kya error hai?

```sql
INSERT INTO student(id, name, age)
VALUES
(2, 'Aman', 21)
(3, 'Rohit', 22);
```

A. `VALUES` keyword galat jagah hai  
B. First tuple `(2, 'Aman', 21)` ke baad comma `,` missing hai  
C. `'Aman'` ke quotes galat hain  
D. Koi error nahi hai  

**Answer:** B

**Explanation:** Row tuples ke beech comma `,` na lagane par MySQL syntax error throw karega. Correct syntax: `(2, 'Aman', 21), (3, 'Rohit', 22);`.

---

### Q15. Best Practice / Production Tip: Production environment mein `INSERT INTO student VALUES (5, 'Ankit', 23);` (bina column names likhe) execute karne ke bajaye column names specify karna kyun recommended hai?

A. Bina column names ke query slow ho jaati hai  
B. Future mein agar table schema mein naya column add ho gaya, to bina column names wali query break ho jayegi  
C. MySQL bina column names ki queries reject kar deta hai  
D. Column names me uppercase mandatory hai  

**Answer:** B

**Explanation:** Direct `INSERT INTO student VALUES(...)` schema column order par depend karta hai. Agar future me schema alter ho ya new column add ho, to position mismatch ho kar query break ho jayegi. Isliye column names explicitly specify karna industry best practice hai.

---

### Q16. Specific records ko filter karne ke liye SQL query mein kaunsa clause use hota hai?

A. `GROUP BY`  
B. `ORDER BY`  
C. `WHERE`  
D. `HAVING`  

**Answer:** C

**Explanation:** Amazon filter analogy: Specific conditions ke base par rows filter karne ke liye `WHERE` clause use kiya jata hai.

---

### Q17. `student` table se sirf `Aman` ka record nikalne ki sahi query kya hogi?

A. `SELECT * FROM student WHERE name = Aman;`  
B. `SELECT * FROM student WHERE name = 'Aman';`  
C. `SELECT * FROM student HAVING name = 'Aman';`  
D. `SELECT Aman FROM student;`  

**Answer:** B

**Explanation:** `WHERE` clause me text criteria string single quotes `'Aman'` ke andar honi chahiye. Without quotes `WHERE name = Aman` error throw karega.

---

### Q18. Common Mistake: Query `SELECT * FROM student WHERE name = Aman;` mein kya mistake hai?

A. `WHERE` clause galat hai  
B. `'Aman'` text single quotes `' '` me nahi hai  
C. `SELECT *` me space missing hai  
D. Semicolon missing hai  

**Answer:** B

**Explanation:** SQL parser `Aman` ko identifier/column name samajh leta hai agar single quotes na lagaye jayein. Isliye string text values ko single quotes `'Aman'` me specify karna compulsory hai.

---

### Q19. SQL mein Comparison Operator `=` ka kya primary meaning hai?

A. Value assign karna  
B. Column value match / equal check karna  
C. Greater than check karna  
D. String concatenate karna  

**Answer:** B

**Explanation:** SQL mein `=` comparison operator candidate row ki column value ko targeted value se equality check karta hai.

---

### Q20. SQL Comparison Operators list mein `!=` symbol ka kya meaning hota hai?

A. Equal to  
B. Not Equal to  
C. Greater than  
D. Division  

**Answer:** B

**Explanation:** `!=` operator SQL me "Not Equal to" condition evaluate karta hai (i.e. specified value ko छोड़कर baaki rows select karta hai).

---

### Q21. Scenario-based Question: Niche diye gaye dataset ko dekhein:

**Dataset (`student` table):**
- Rahul (Age 20)
- Aman (Age 21)
- Rohit (Age 22)
- Priya (Age 19)

**Query:**
```sql
SELECT * FROM student WHERE age > 20;
```

Output mein kitni rows aur kaun-kaun se students aayenge?

A. 3 Rows (Rahul, Aman, Rohit)  
B. 2 Rows (Aman, Rohit)  
C. 1 Row (Priya)  
D. 4 Rows (Sabhi students)  

**Answer:** B

**Explanation:** `age > 20` strict greater than condition hai. Rahul (age 20) exclude ho jayega kyunki `20 > 20` FALSE hai. Aman (21) aur Rohit (22) TRUE honge. Total 2 rows output me aayengi.

---

### Q22. Scenario-based Question: Same dataset par agar query ye hoti:

```sql
SELECT * FROM student WHERE age >= 20;
```

To output mein Rahul include hoga ya nahi?

A. Nahi, Rahul exclude hoga  
B. Haan, Rahul include hoga kyunki `>=` equal boundary value (20) ko bhi include karta hai  
C. Query error degi  
D. Output blank aayega  

**Answer:** B

**Explanation:** `>=` (Greater Than Equal) operator boundary value `20` ko include karta hai (`20 >= 20` is TRUE). Isliye Rahul result set me select hoga.

---

### Q23. Interview Question: `>` (Greater Than) aur `>=` (Greater Than Equal) mein main difference kya hai?

A. `>` fast hota hai, `>=` slow hota hai  
B. `>` boundary value ko exclude karta hai, jabki `>=` boundary value ko include karta hai  
C. `>` text ke liye use hota hai, `>=` numbers ke liye  
D. Dono bilkul identical hain  

**Answer:** B

**Explanation:** `>` strict inequality hai jo boundary value ko reject karta hai, jabki `>=` boundary value matching par TRUE return karta hai.

---

### Q24. Query Output Check: Niche di gayi query ka result kya hoga?

```sql
SELECT * FROM student WHERE age < 20;
```
*(Dataset: Rahul-20, Aman-21, Rohit-22, Priya-19)*

A. Rahul, Priya  
B. Sirf Priya (19)  
C. Aman, Rohit  
D. Blank  

**Answer:** B

**Explanation:** `age < 20` condition strictly 20 se kam values check karegi. Priya (19) is TRUE. Rahul (20) is FALSE. Isliye output me sirf Priya aayegi.

---

### Q25. Query Output Check: Niche di gayi query ka result kya hoga?

```sql
SELECT * FROM student WHERE age != 20;
```
*(Dataset: Rahul-20, Aman-21, Rohit-22, Priya-19)*

A. Sirf Rahul  
B. Aman, Rohit, Priya  
C. Rahul, Priya  
D. Error  

**Answer:** B

**Explanation:** `age != 20` condition 20 ke ilawa saare records select karegi. Rahul (20) filter out ho jayega, isliye Aman (21), Rohit (22), aur Priya (19) return honge.

---

### Q26. Tricky Concept: MySQL engine `WHERE` clause ko internal level par kaise evaluate karta hai?

A. Saare records ko ek saath merge karke  
B. Table ke HAR ROW par condition evaluate karke boolean (`TRUE`/`FALSE`) check karta hai, aur sirf `TRUE` rows ko output me deta hai  
C. Table name change karke  
D. Column count count karke  

**Answer:** B

**Explanation:** MySQL engine target table ki har single row par `WHERE` expression evaluate karta hai. Jiss row ke liye expression `TRUE` hota hai, wo row output grid me appear hoti hai.

---

### Q27. Syntax Check: `teacher` table mein multiple rows insert karne ke liye kaunsa code block 100% CORRECT hai?

A. 
```sql
INSERT INTO teacher(teacher_id, teacher_name, age)
VALUES
(101, 'Karan', 35),
(102, 'Sneha', 30);
```

B. 
```sql
INSERT INTO teacher(teacher_id, teacher_name, age)
VALUES
(101, 'Karan', 35)
(102, 'Sneha', 30);
```

C. 
```sql
INSERT INTO teacher(teacher_id, teacher_name, age)
VALUES
(101, Karan, 35),
(102, Sneha, 30);
```

D. 
```sql
CREATE teacher VALUES (101, 'Karan', 35);
```

**Answer:** A

**Explanation:** Option A mein correct comma separation hai aur text names `'Karan'`, `'Sneha'` single quotes mein formatted hain. Option B me comma missing hai, aur Option C me text bina quotes ke hai.

---

### Q28. Schema Design Check: `CREATE TABLE` command mein agar hum `age VARCHAR(50)` define kar dein to kya problem hogi?

A. Error aa jayega, column hi nahi banega  
B. `age` numerical values ke bajaye text/string treat hoga, jo numbers (age) ke liye bad database design practice hai  
C. System automatically `INT` me convert kar dega  
D. Table delete ho jayegi  

**Answer:** B

**Explanation:** `VARCHAR` text datatypes ke liye hota hai. Numbers like age/salary ke liye `INT` datatype use karna correct design practice hai taaki numerical filtering aur operations properly ho sakein.

---

### Q29. Higher Placement Scenario: Agar company database mein 1,00,000 employees ka record hai aur aapko specific Employee `id = 5042` ka record chahiye, to correct aur efficient query kya hogi?

A. `SELECT * FROM employee;` aur manually search karna  
B. `SELECT * FROM employee WHERE id = 5042;`  
C. `CREATE TABLE employee WHERE id = 5042;`  
D. `INSERT INTO employee VALUES(5042);`  

**Answer:** B

**Explanation:** `WHERE` clause DB server level par row filter apply karta hai jisse targeted record (`id = 5042`) efficiently return hota hai (`SELECT * FROM employee WHERE id = 5042;`).

---

### Q30. Final Synthesis Question: Niche diye gaye 3 SQL statements ko analyze karke batayein ki sequential execution ka final result kya hoga?

```sql
CREATE TABLE student(id INT, name VARCHAR(50), age INT);

INSERT INTO student(id, name, age) 
VALUES (1, 'Rahul', 20), (2, 'Aman', 21);

SELECT name FROM student WHERE age <= 20;
```

A. Output grid mein `Rahul`  
B. Output grid mein `Aman`  
C. Output grid mein `Rahul` aur `Aman` dono  
D. Error 1046  

**Answer:** A

**Explanation:** Step 1 table banata hai. Step 2 me Rahul (20) aur Aman (21) insert hote hain. Step 3 me `WHERE age <= 20` filter lagaya hai (`20 <= 20` is TRUE for Rahul, `21 <= 20` is FALSE for Aman) aur sirf `name` column select kiya hai. So final result grid mein strictly `Rahul` single row return hoga.
