# Day 9 MCQs

## Quick Revision

Before attempting the MCQs, let's quickly review all key concepts covered in `day9.md`.

### 1. Database Creation & Active Schema Selection
- **`CREATE DATABASE college_management;`**: Naya database schema create karta hai.
- **`USE college_management;`**: Created database ko current active session ke liye select/activate karta hai.
- **`SELECT DATABASE();`**: Verify karta hai ki filhal kaunsa database active context me hai.
- **Workbench Shortcut**: MySQL Workbench me naya query tab open karne ke liye `Ctrl + T` use hota hai.

### 2. Relational Table Schema & Structure
- **Parent Table (`departments`)**: Primary Key hold karti hai (`department_id INT PRIMARY KEY`).
- **Child Table (`students`)**: Foreign Key hold karti hai (`department_id INT`), jo parent table ke `department_id` ko point/reference karti hai.
- **`SHOW TABLES;`**: Active database schema me maujood saari tables list karta hai.

### 3. Database Normalization & Anti-Patterns
- **Monolithic Single Table (Anti-Pattern ❌)**: Single table me `student_name` ke saath `department_name` direct store karne se duplicate data (redundancy) accumulate hota hai.
- **Update Anomaly**: Agar CSE department ka naam badalkar "Computer Science" karna ho, toh Single Table me 10,000 rows par `UPDATE` chalu karna padega (high CPU load, data corruption risk).
- **Normalized Schema Solution**: Normalized multi-table architecture me sirf parent table (`departments`) me **1 single row** (`department_id = 1`) update karni padti hai. Saare students automatically reference dwara naye naam ko reflect karte hain.

### 4. Primary Key vs Foreign Key Relationship
- **Primary Key (PK)**: Parent table me har record/row ko uniquely identify karta hai (`departments.department_id`).
- **Foreign Key (FK)**: Child table me parent table ke Primary Key ko point karne wala reference column hota hai (`students.department_id`).

### 5. Why JOINs are Required (Core Interview Question)
- **Definition**: Data redundancy aur update anomalies ko khatam karne ke liye tables ko split (normalize) kar diya jata hai.
- **Purpose of JOIN**: Separated normalized tables ko key columns (`FK = PK`) ke basis par reconnect karke unified/integrated result set fetch karne ke liye **`JOIN`** ki zaroorat hoti hai.
- **Teaser Syntax**:
  ```sql
  SELECT students.student_name, departments.department_name
  FROM students
  INNER JOIN departments
  ON students.department_id = departments.department_id;
  ```

---

## 30 Most Important MCQs

---

### Q1. Active database select hone ke baad uski verification ke liye kaunsi MySQL query run ki jaati hai?

A) `SHOW DATABASE;`  
B) `SELECT DATABASE();`  
C) `USE DATABASE;`  
D) `GET DATABASE();`  

**Answer:** B

**Explanation:** `SELECT DATABASE();` query current active database schema ka naam return karti hai.

---

### Q2. MySQL Workbench me naya Query Tab open karne ke liye kaunsa keyboard shortcut use hota hai?

A) `Ctrl + N`  
B) `Ctrl + Shift + Q`  
C) `Ctrl + T`  
D) `Alt + Q`  

**Answer:** C

**Explanation:** `day9.md` me clear mention hai ki MySQL Workbench me new query tab open karne ke liye `Ctrl + T` shortcut key use hoti hai.

---

### Q3. `college_management` database me maujood saari tables ki list dekhne ke liye kaunsi command execute ki jaati hai?

A) `SELECT TABLES;`  
B) `SHOW TABLES;`  
C) `DESCRIBE DATABASE;`  
D) `LIST TABLES;`  

**Answer:** B

**Explanation:** `SHOW TABLES;` query active database schema ki saari existing tables list karti hai.

---

### Q4. `departments` table me `department_id` column par `PRIMARY KEY` constraint lagane ka main purpose kya hai?

A) Column me duplicate aur NULL values allow karna  
B) Table ke har row ko uniquely identify karna  
C) Table me duplicate rows insert karne ke liye  
D) Columns ki string length limit set karna  

**Answer:** B

**Explanation:** Parent table me `PRIMARY KEY` har row ko uniquely identify karne ke liye constraint ki tarah kaam karta hai.

---

### Q5. `students` table (child table) me `department_id` column ka role kya hai?

A) Primary Key  
B) Foreign Key jo `departments` table ke `department_id` ko reference karta hai  
C) Unique Key jo auto increment hoti hai  
D) Aggregate Function placeholder  

**Answer:** B

**Explanation:** Child table (`students`) me `department_id` Foreign Key hota hai jo parent table (`departments`) ke Primary Key ko point/reference karta hai.

---

### Q6. Single Monolithic table me `student_name` ke saath `department_name` direct store karne ko database design me kya mana jata hai?

A) Best Practice  
B) Anti-Pattern  
C) Advanced Normalization  
D) Indexing Pattern  

**Answer:** B

**Explanation:** Single table me repeated textual data store karna ek Anti-Pattern hai kyunki isse data redundancy aur update anomalies paida hoti hain.

---

### Q7. Agar CSE department ka naam badalkar "Computer Science" karna ho, toh Single Monolithic table me kya problem aayegi?

A) Sirf 1 row update hogi  
B) 10,000 student rows me `UPDATE` run karna padega jisse High CPU load aur Data Corruption ka risk hoga (Update Anomaly)  
C) Query execute hi nahi hogi  
D) Database auto-delete ho jayega  

**Answer:** B

**Explanation:** Single un-normalized table me har student record me department name duplicate hota hai, isliye thousands of rows update karni padti hain jisse Update Anomaly paida hoti hai.

---

### Q8. Normalized Relational Database Architecture me CSE department ka naam badalne par `departments` table me kitni rows update karni padengi?

A) 10,000 rows  
B) Exactly 1 row (`department_id = 1`)  
C) Zero rows  
D) Sabhi tables delete karni padengi  

**Answer:** B

**Explanation:** Relational normalization ke wajah se department info parent table me ek jagah hoti hai, isliye sirf `departments` table me 1 row (`department_id = 1`) update karni padti hai.

---

### Q9. Database Normalization ke baad split hui multi-table data ko aapas me reconnect karke output fetch karne ke liye kiska use hota hai?

A) `GROUP BY`  
B) `WHERE` clause  
C) `JOIN`  
D) `HAVING` clause  

**Answer:** C

**Explanation:** Separated normalized tables ko key columns (PK/FK) ke basis par reconnect karke combined result set fetch karne ke liye `JOIN` ki zaroorat hoti hai.

---

### Q10. `students` table me `department_id` me `1` value hone ka kya matlab hai?

A) Student ka Roll No 1 hai  
B) Student CSE department se belong karta hai (referencing `departments.department_id = 1`)  
C) Student ki age 1 hai  
D) Invalid Foreign Key reference  

**Answer:** B

**Explanation:** `departments` table me `department_id = 1` CSE hai, isliye `students` table me `department_id = 1` indicate karta hai ki student CSE department se hai.

---

### Q11. Niche di gayi DDL query ka output kya hoga?
```sql
CREATE TABLE departments(
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100)
);
```

A) Ek table create hogi jisme `department_id` Primary Key hoga  
B) Rows insert ho jayengi  
C) Database drop ho jayega  
D) Query error degi kyunki Foreign Key missing hai  

**Answer:** A

**Explanation:** Yeh query `departments` naam ki table create karegi jisme `department_id` column uniquely constrainted Primary Key hoga.

---

### Q12. Multi-table relational schema me `departments` ko **Parent Table** aur `students` ko **Child Table** kyun kaha jata hai?

A) `departments` table baad me create hoti hai  
B) `students` table me Foreign Key hai jo `departments` ke Primary Key par dependent hai  
C) `departments` table me zyada rows hoti hain  
D) `students` table primary key container hai  

**Answer:** B

**Explanation:** Parent table primary key hold karti hai aur Child table foreign key ke through parent table ke PK ko reference karti hai.

---

### Q13. `CREATE DATABASE college_management;` query run karne ke baad naye database me switch karne ke liye konsi command likhi jaati hai?

A) `SELECT college_management;`  
B) `USE college_management;`  
C) `CONNECT college_management;`  
D) `OPEN college_management;`  

**Answer:** B

**Explanation:** Active database context switch/select karne ke liye `USE database_name;` command ka upyog kiya jata hai.

---

### Q14. Niche di gayi SQL command ka purpose kya hai?
```sql
INSERT INTO departments (department_id, department_name)
VALUES (1, 'CSE'), (2, 'ECE');
```

A) Table delete karna  
B) `departments` table me 2 new department records populate/insert karna  
C) Table column count check karna  
D) Existing records update karna  

**Answer:** B

**Explanation:** `INSERT INTO` statement table ke specified columns me naye rows insert/populate karta hai.

---

### Q15. Day 9 sample dataset ke according, `students` table me Ankit (student_id 107) ka `department_id` 4 hai. `departments` table me `department_id = 4` kis department ko belong karta hai?

A) CSE  
B) ECE  
C) Mechanical  
D) Civil  

**Answer:** D

**Explanation:** `departments` table sample data me `department_id = 4` Civil department ka record hai.

---

### Q16. Interview Scenario: Agar ek company database me `employees` table me `dept_id` hai aur `departments` table me `dept_id` Primary Key hai, toh matching records retrieve karne ke liye matching condition kya hogi?

A) `employees.dept_id = departments.dept_id`  
B) `employees.name = departments.dept_id`  
C) `employees.dept_id > departments.dept_id`  
D) `employees.dept_id + departments.dept_id`  

**Answer:** A

**Explanation:** JOINs me matching records Foreign Key aur Primary Key columns ke equality comparison (`FK = PK`) par based hote hain.

---

### Q17. Single table me data redundancy se konsi major problem paida hoti hai?

A) Update Anomaly  
B) Data Inconsistency & Corruption Risk  
C) High Storage & Memory CPU Load during Updates  
D) All of the above  

**Answer:** D

**Explanation:** Un-normalized single table design me duplicate text values hone se storage waste hota hai, updates expensive hote hain (CPU load), aur inconsistency/anomalies paida hoti hain.

---

### Q18. Day 9 sample dataset me total kitne students `students` table me insert kiye gaye hain aur kitne departments `departments` table me hain?

A) 6 Students, 3 Departments  
B) 8 Students, 4 Departments  
C) 10 Students, 5 Departments  
D) 5 Students, 2 Departments  

**Answer:** B

**Explanation:** `day9.md` me `departments` table me 4 rows (CSE, ECE, Mechanical, Civil) aur `students` table me 8 rows (Rahul to Sneha) insert kiye gaye hain.

---

### Q19. `SHOW TABLES;` command run karne par agar output empty set aata hai, toh iska kya reason ho sakta hai?

A) Database delete ho gaya  
B) Select kiye gaye active database me koi table create nahi hui hai  
C) SQL syntax broken hai  
D) Workbench crash ho gaya  

**Answer:** B

**Explanation:** Jab active database schema me koi table build nahi hoti, tab `SHOW TABLES;` empty output return karta hai.

---

### Q20. Output Check: `SELECT DATABASE();` run karne par agar `college_management` return hota hai, toh iska exact matlab kya hai?

A) Server down hai  
B) `college_management` filhal active/selected schema hai jiske upar queries execute hongi  
C) Database me 0 tables hain  
D) Queries disable hain  

**Answer:** B

**Explanation:** `SELECT DATABASE();` currently selected active database schema ka naam display karta hai.

---

### Q21. Tricky Question: `students` table me `department_id` column me numeric values (1, 2, 3, 4) kyun rakhi gayi hain, bajaye direct 'CSE', 'ECE' string store karne ke?

A) Numbers store karne me memory kam lagti hai aur Normalization maintain hota hai  
B) Strings SQL me banned hain  
C) Numbers speed increase nahi karte  
D) MySQL Workbench string format support nahi karta  

**Answer:** A

**Explanation:** Foreign key me numeric ID reference karne se data repetition khatam hota hai, storage compute optimize hota hai aur update anomaly avoid hoti hai.

---

### Q22. Niche di gayi JOIN teaser query me `ON` clause ka primary work kya hai?
```sql
SELECT students.student_name, departments.department_name
FROM students
INNER JOIN departments
ON students.department_id = departments.department_id;
```

A) Output rows ko sort karna  
B) Table A (child) aur Table B (parent) ke beech common matching key condition specify karna  
C) Rows count limit karna  
D) New column create karna  

**Answer:** B

**Explanation:** `ON` clause specify karta hai ki dono tables ke konse key columns match hone chahiye (yahan `students.department_id = departments.department_id`).

---

### Q23. Real-World Scenario: E-Commerce system me `orders` table aur `users` table alag-alag split hoti hain. `orders` table me `user_id` hota hai. Yahan `user_id` kya hai?

A) `users` table ka Foreign Key  
B) `orders` table ka Foreign Key jo `users.user_id` (Primary Key) ko refer karta hai  
C) Monolithic column  
D) Composite Aggregate Key  

**Answer:** B

**Explanation:** Child table (`orders`) me `user_id` Foreign Key hota hai jo parent table (`users`) ke Primary Key `user_id` ko point karta hai.

---

### Q24. Target Schema Check: Day 9 ke `students` table DDL command me `department_id` column define karte waqt kya datatype set kiya gaya tha?
```sql
CREATE TABLE students(
    student_id INT PRIMARY KEY,
    student_name VARCHAR(100),
    age INT,
    city VARCHAR(50),
    department_id INT
);
```

A) `VARCHAR(50)`  
B) `INT`  
C) `FLOAT`  
D) `TEXT`  

**Answer:** B

**Explanation:** DDL script me `department_id INT` explicitly numeric integer datatype ke roop me set kiya gaya tha.

---

### Q25. Database Relational Design me Foreign Key rule ke according, kya child table ka Foreign Key value parent table ke existing Primary Key value se match hona chahiye?

A) Haan, Referencing Foreign Key values parent table ke Primary Key values par base hoti hain  
B) Nahi, koi bhi random string daal sakte hain  
C) Foreign Key humesha negative numbers hona chahiye  
D) Relational DB me Foreign Keys allow nahi hote  

**Answer:** A

**Explanation:** Foreign Key child table me valid parent Primary Key ID ko reference karta hai taaki relational integrity maintain rahe.

---

### Q26. `students` table me `Rahul` (student_id 101) aur `Rohit` (student_id 103) dono ka `department_id = 1` hai. Iska kya matlab hai?

A) Rahul aur Rohit dono CSE department se hain  
B) CSE department delete ho gaya  
C) Rahul aur Rohit identical twin hain  
D) Data duplication error hai  

**Answer:** A

**Explanation:** Multiple child rows (Rahul, Rohit) parent key 1 ko reference kar rahi hain, yaani dono CSE department me enrolled hain.

---

### Q27. Key Comparison: Primary Key aur Foreign Key ke beech main difference kya hai?

A) Primary Key parent table me unique row identifier hai; Foreign Key child table me parent PK ko reference karti hai  
B) Primary Key child table me hoti hai, Foreign Key parent table me  
C) Primary Key hamesha text hoti hai, Foreign Key numeric  
D) Dono exact identical hoti hain  

**Answer:** A

**Explanation:** Primary Key parent table me row uniqueness ensure karti hai, jabki Foreign Key child table me table relationship define karti hai.

---

### Q28. Relational Schema me `students` table query: `SELECT * FROM students;` ka output grid kitne columns return karega?

A) 3 Columns  
B) 5 Columns (`student_id`, `student_name`, `age`, `city`, `department_id`)  
C) 2 Columns  
D) 1 Column  

**Answer:** B

**Explanation:** `students` table schema me 5 columns defined hain: `student_id`, `student_name`, `age`, `city`, `department_id`.

---

### Q29. Placement Question: Database Normalization ka primary goal kya hota hai?

A) Data Redundancy aur Anomalies (Insert/Update/Delete) ko remove karke relational integrity build karna  
B) Data storage capacity ko fill karna  
C) SQL queries ki length ko double karna  
D) Tables ko delete kar dena  

**Answer:** A

**Explanation:** Normalization data redundancy reduce karne aur Update/Insert/Delete anomalies ko eliminate karne ke liye database schema design process hai.

---

### Q30. Accenture Trap Question: Agar `college_management` database activate kiye bina (`USE college_management;` run kiye bina) `CREATE TABLE departments...` query run karein toh kya hoga?

A) Table automatically default system database me create ho jayegi  
B) `ERROR 1046 (3D000): No database selected` aayega  
C) Workbench background me silently database create kar dega  
D) Query execute ho jayegi bina kisi issue ke  

**Answer:** B

**Explanation:** Active database context select (`USE db_name;`) kiye bina table creation query execute karne par MySQL `No database selected` error return karta hai.
