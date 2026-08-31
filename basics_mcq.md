# Basics — Revision + 30 MCQs

---

## Part 1 — Quick Revision

Before attempting the MCQs, let's quickly revise all key concepts covered in `basics.md`.

### 1. Database Creation Recap
- **Command:** `CREATE DATABASE college;`
- **Purpose:** Server par ek naya database container create karta hai.

### 2. Database Selection (`USE` Command)
- **Command:** `USE database_name;` (e.g., `USE college;`)
- **Purpose:** Server par kisi target database ko active/select karta hai.
- **Why Needed?** Server par multiple databases ho sakte hain. MySQL ko batana zaroori hai ki subsequent tables aur queries kis database ke andar execute honi chahiye.
- **Breakdown:**
  - `USE`: Command to set active context ("Ab se is database ke andar kaam karo").
  - `college`: Target database name.
- **Real-Life Analogy:** Laptop mein kisi folder (e.g., *Projects*) ko open karna taaki new files usi folder mein save hon.
- **Execution & Output:** Run via `Ctrl + Enter` in MySQL Workbench. Action Output shows `Query OK` or `Database changed`.

### 3. Check Active Database (`SELECT DATABASE();`)
- **Command:** `SELECT DATABASE();`
- **Purpose:** Current session mein kaunsa database active hai, ye check/display karta hai.
- **Breakdown:**
  - `SELECT`: Keyword used to fetch or display data/results.
  - `DATABASE()`: Built-in MySQL function returning current active database name (returns `NULL` if no database is selected).

### 4. Important Rules & Common Traps
- ⚠️ **Trap / Mistake:** Executing DDL/DML queries like `CREATE TABLE` without running `USE <database_name>;` first.
  - **Result:** Throws `Error 1046: No database selected` or creates table in an unintended database.
- 📌 **Order of Execution:**
  1. `CREATE DATABASE <db_name>;`
  2. `USE <db_name>;`
  3. `CREATE TABLE <table_name>(...);`
- 🔤 **Case Sensitivity:** SQL keywords are case-insensitive (`USE`, `use`, `Use` all work), but using UPPERCASE is standard practice for readability.
- ⚙️ **Function Syntax:** `DATABASE()` is a function, so parentheses `()` are mandatory (`SELECT DATABASE();`).

---

## Part 2 — 30 MCQs

---

### Q1. MySQL server par multiple databases hone par specific database ke andar kaam karne ke liye kaunsi command use hoti hai?

A. `OPEN database_name;`  
B. `USE database_name;`  
C. `SELECT database_name;`  
D. `SET database_name;`  

**Answer:** B

**Explanation:** `USE` command ka kaam current active database set karna hota hai taaki aage ki saari tables aur queries us database ke andar execute ho sakein.

---

### Q2. Currently active database ka naam check karne ke liye SQL mein kaunsa built-in function/command use hota hai?

A. `SHOW DATABASE;`  
B. `SELECT ACTIVE_DATABASE();`  
C. `SELECT DATABASE();`  
D. `GET DATABASE();`  

**Answer:** C

**Explanation:** `SELECT DATABASE();` command current active database ka naam return karti hai. `DATABASE()` ek built-in function hai jise `SELECT` keyword ke saath display/fetch karne ke liye call kiya jaata hai.

---

### Q3. Niche di gayi SQL command kya action perform karegi?

```sql
USE college;
```

A. Ye `college` database ko activate/select karega.  
B. Ye `college` naam ki nayi table banayega.  
C. Ye `college` database ko delete kar dega.  
D. Ye `college` database ke saare tables show karega.  

**Answer:** A

**Explanation:** `USE college;` command MySQL server ko instruct karti hai ki "ab se `college` database ko active kar do aur saari agli queries iske andar execute karo".

---

### Q4. Agar aapne koi database select nahi kiya hai (`USE` command nahi chalayi) aur seedhe `CREATE TABLE student(id INT);` run karte ho, to kya hoga?

A. Table default system database mein ban jayegi.  
B. MySQL error throw karega: `Error 1046: No database selected`.  
C. Server automatically pehla database select kar lega.  
D. Table bina kisi database ke run ho jayegi.  

**Answer:** B

**Explanation:** Jab tak koi active database select nahi hota, MySQL ko pata nahi hota ki table kis container ke andar banani hai, isliye Error 1046 ("No database selected") throw hota hai.

---

### Q5. MySQL Workbench mein active SQL query/statement ko execute karne ke liye kaunsa keyboard shortcut use hota hai?

A. `Shift + Enter`  
B. `Ctrl + Enter`  
C. `Alt + Enter`  
D. `Tab + Enter`  

**Answer:** B

**Explanation:** MySQL Workbench mein current cursor position par written statement ko run karne ke liye `Ctrl + Enter` shortcut key use ki jaati hai.

---

### Q6. Agar `USE college;` command successfully execute ho jaati hai, to MySQL Action Output window mein kya status message show hota hai?

A. `Table Created`  
B. `Query OK` ya `Database changed`  
C. `Data Inserted`  
D. `Database Deleted`  

**Answer:** B

**Explanation:** Successful database switch par MySQL client `Query OK` ya `Database changed` output return karta hai.

---

### Q7. Agar session mein pehle se KOI database select nahi kiya gaya ho, to is command ka output kya aayega?

```sql
SELECT DATABASE();
```

A. Error throw karega  
B. `NULL` output aayega  
C. `master` output aayega  
D. `root` output aayega  

**Answer:** B

**Explanation:** Agar koi database active context mein nahi hai, to `DATABASE()` function `NULL` value return karta hai, denoting no active database.

---

### Q8. `SELECT DATABASE();` command mein `SELECT` keyword ka primary purpose kya hai?

A. Database create karna  
B. Active database ko drop/delete karna  
C. Output grid/screen par result ko fetch aur display karna  
D. Table design define karna  

**Answer:** C

**Explanation:** `SELECT` keyword SQL mein values, data, ya function evaluation results ko retrieve karke screen par display karne ke liye use hota hai.

---

### Q9. Real-life analogy ke according, `USE college;` command ko kis action se compare kiya ja sakta hai?

A. Laptop mein new folder create karne se  
B. Laptop mein kisi existing folder ko double-click karke open karne se  
C. Laptop ko restart karne se  
D. Folder ko delete karne se  

**Answer:** B

**Explanation:** Jaise laptop par kisi folder (e.g., *Projects*) ko open karne par remaining saved files us folder ke andar jaati hain, waise hi `USE college;` database context set karta hai.

---

### Q10. Niche diye gaye SQL statements mein se kaunsa statement syntax-wise BILKUL CORRECT hai?

A. `USE DATABASE college;`  
B. `USE college;`  
C. `SELECT USE college;`  
D. `USING college;`  

**Answer:** B

**Explanation:** SQL mein database select karne ka correct syntax strictly `USE <database_name>;` hai. `USE DATABASE` ek invalid syntax error generate karega.

---

### Q11. SQL keywords ki case-sensitivity ke regarding kaunsa statement sahi hai?

A. `USE college;` aur `use college;` dono valid hain kyunki SQL keywords case-insensitive hote hain.  
B. Sirf `USE` capital mein likhna mandatory hai.  
C. Sirf `use` lowercase mein likhna mandatory hai.  
D. `USE` command error dega agar lowercase mein ho.  

**Answer:** A

**Explanation:** SQL commands aur keywords case-insensitive hote hain. Isliye `USE`, `use`, ya `Use` sab kaam karenge, halanki capital letters me syntax write karna industry standard readability convention hai.

---

### Q12. Agar aapne pehle `USE college;` chalaya aur uske baad `USE school;` chalaya, to ab active database kaunsa hoga?

A. `college`  
B. `school`  
C. `college` aur `school` dono ek saath active honge  
D. Dono deactivate ho jayenge  

**Answer:** B

**Explanation:** `USE` command current session ke active database context ko overwrite kar deti hai. Isliye `USE school;` execute hone ke baad active database `school` ho jayega.

---

### Q13. Agar server par `xyz_db` naam ka database EXIST HI NAHI KARTA aur aap `USE xyz_db;` run karte ho, to kya hoga?

A. New database auto-create ho jayega.  
B. MySQL error throw karega: `Unknown database 'xyz_db'`.  
C. Query execute ho jayegi par koi table nahi dikhegi.  
D. System blank output dega.  

**Answer:** B

**Explanation:** Non-existent database ko select karne par MySQL error throw karta hai (`Error 1049: Unknown database 'xyz_db'`). Pehle `CREATE DATABASE xyz_db;` run karna hoga.

---

### Q14. Step-by-step order: Database aur table setup karne ka SAHI execution sequence kya hai?

1. `CREATE TABLE student(id INT);`  
2. `CREATE DATABASE college;`  
3. `USE college;`  

A. 1 -> 2 -> 3  
B. 2 -> 3 -> 1  
C. 3 -> 2 -> 1  
D. 2 -> 1 -> 3  

**Answer:** B

**Explanation:** Correct logical sequence is: Pehle database create karo (`CREATE DATABASE`), fir usko select karo (`USE`), aur uske baad us database ke andar table create karo (`CREATE TABLE`).

---

### Q15. `SELECT DATABASE();` query run karne par output grid mein Column Header ka kya naam show hota hai?

A. `ACTIVE_DB`  
B. `DATABASE()`  
C. `CURRENT_DB`  
D. `NAME`  

**Answer:** B

**Explanation:** Jab aap `SELECT function_name()` run karte ho, to MySQL output grid ke header mein exact function syntax `DATABASE()` hi header label ki tarah display karta hai.

---

### Q16. Niche di gayi SQL query mein kya syntax error hai?

```sql
SELECT DATABASE;
```

A. Semicolon missing hai  
B. Function Call ke parentheses `()` missing hain  
C. `SELECT` ki jagah `SHOW` keyword hona chahiye  
D. Query bilkul sahi hai  

**Answer:** B

**Explanation:** MySQL mein `DATABASE()` ek built-in function hai. Function call ke liye parentheses `()` lagana mandatory hota hai. Without `()`, MySQL `DATABASE` ko column name treat karne ki koshish karega aur syntax/unknown column error dega.

---

### Q17. `company` naam ke database ko active karne ki correct SQL query kaunsi hai?

A. `USE company;`  
B. `SELECT company;`  
C. `CREATE company;`  
D. `GO company;`  

**Answer:** A

**Explanation:** Active database context set karne ka single proper SQL command `USE company;` hai.

---

### Q18. Agar SQL client terminal par aap command likhte ho: `use school` (bina semicolon `;` ke), to client execute kyun nahi karta?

A. Command completely wrong hai  
B. SQL statement termination symbol (semicolon `;`) missing hai  
C. Terminal crash ho gaya hai  
D. `use` keyword capitalized nahi hai  

**Answer:** B

**Explanation:** SQL clients (like MySQL CLI / Workbench) multiline queries accept karte hain aur jab tak terminating semicolon `;` nahi milta, tab tak execution trigger nahi karte.

---

### Q19. Once `USE college;` command execute ho jaati hai, to iska effect kin queries par padta hai?

A. Sirf agli 1 query par  
B. Current session mein aage execute honi wali sabhi table aur data queries par  
C. Sirf `SELECT` queries par  
D. Server ke sabhi logged-in users par globally  

**Answer:** B

**Explanation:** `USE` command current connection session ke active schema/database को change kar deti hai. Iske baad run hone wali saari DDL (e.g. `CREATE TABLE`) aur DML (e.g. `INSERT`) queries usi active database par execute hoti hain.

---

### Q20. Interview Question: `USE` command ka core objective single line mein kya hai?

A. Database ko permanently remove karna  
B. Current session ke liye active working database set/specify karna  
C. Table structure ko alter karna  
D. Database ka backup create karna  

**Answer:** B

**Explanation:** `USE` command ka primary objective current session context ke liye active working database point karna hai.

---

### Q21. Tricky Question: Niche diye gaye script execution ko analyze karo:

```sql
CREATE DATABASE hospital;
SELECT DATABASE();
```

Agar step 1 ke baad `USE hospital;` run NAHI kiya gaya, to `SELECT DATABASE();` ka output kya hoga (assuming isse pehle koi DB active nahi tha)?

A. `hospital`  
B. `NULL`  
C. `master`  
D. Error 1046  

**Answer:** B

**Explanation:** Trap Alert! Database ko sirf `CREATE DATABASE` karne se wo automatically active (`USE`) nahi ho jata. Step 2 par active database check karne par output `NULL` hi aayega jab tak explicit `USE hospital;` command na chalayi jaye.

---

### Q22. Consider the following output grid:

```text
+------------------+
| DATABASE()       |
+------------------+
| tech_db          |
+------------------+
```

Is output ka kya meaning hai?

A. `tech_db` database drop/delete ho gaya hai.  
B. `tech_db` currently active selected database hai.  
C. `tech_db` ke andar 0 tables hain.  
D. Query mein error hai.  

**Answer:** B

**Explanation:** `SELECT DATABASE();` query ke result array mein `tech_db` aana confirm karta hai ki `tech_db` active database context hai.

---

### Q23. Tricky Question: Kya ek MySQL session mein ek saath 2 databases active ho sakte hain (e.g., `USE db1, db2;`)?

A. Haan, comma se separate karke kar sakte hain.  
B. Nahi, ek session mein ek time par EXACTLY ONE active database hi ho sakta hai.  
C. Haan, `AND` operator apply karke.  
D. Haan, sub-query format mein.  

**Answer:** B

**Explanation:** MySQL connection session mein at any given moment strictly single database context active ho sakta hai. Naya `USE` command execution purane active database context ko replace kar deta hai.

---

### Q24. Study notes (`basics.md`) ke according, Database selection seekhne ke baad agla main practical concept kya padhaya jayega?

A. `DROP DATABASE`  
B. `CREATE TABLE`  
C. `ALTER TABLE`  
D. `DELETE FROM`  

**Answer:** B

**Explanation:** Notes ke end teaser section ke according, next upcoming main topic `CREATE TABLE` hai, jisme data types (`INT`, `VARCHAR`) aur constraints (`PRIMARY KEY`, `NOT NULL`) cover honge.

---

### Q25. Niche diye gaye options mein se `SELECT DATABASE();` ke baare mein kaunsa statement GALAT (Incorrect) hai?

A. Ye active database ka naam display karta hai.  
B. `DATABASE()` ek built-in function hai.  
C. Ye current database ko change ya select karne ke liye use hota hai.  
D. Agar koi database active nahi hai to ye `NULL` return karta hai.  

**Answer:** C

**Explanation:** Option C statement wrong hai. Current database ko select/change karne ke liye `USE` command hoti hai, jabki `SELECT DATABASE();` sirf current status inspect/check karne ke liye read-only function hai.

---

### Q26. Tricky Question: Niche diye gaye execution flow ka final output kya aayega?

```sql
CREATE DATABASE test1;
CREATE DATABASE test2;
USE test1;
USE test2;
SELECT DATABASE();
```

A. `test1`  
B. `test2`  
C. `NULL`  
D. Error 1049  

**Answer:** B

**Explanation:** Line 3 par `USE test1;` run hone se `test1` active hua, lekin Line 4 par `USE test2;` run hone se active context switch hokar `test2` ho gaya. Isliye Line 5 par `SELECT DATABASE();` ka final output `test2` aayega.

---

### Q27. Standard MySQL syntax rules ke according, valid identifier for database selection kya hai?

```sql
USE college;
```

A. Sahi hai, standard unquoted database identifier syntax hai.  
B. Incorrect hai, hamesha double quotes mandatory hain.  
C. Incorrect hai, string identifier query nahi ho sakti.  
D. Incorrect hai, syntax syntax error dega.  

**Answer:** A

**Explanation:** MySQL mein standard database selection syntax without quotes (`USE college;`) use hota hai.

---

### Q28. MySQL Workbench mein `Database changed` Action Output message kis command execution ke baad return hota hai?

A. `CREATE DATABASE`  
B. `USE` command  
C. `SELECT DATABASE()`  
D. `DROP TABLE`  

**Answer:** B

**Explanation:** CLI / Workbench interface par jab `USE <db_name>;` command run karke active database badla jata hai, tab status message `Database changed` (ya `Query OK`) receive hota hai.

---

### Q29. Concept Alignment Check: Niche diye gaye key-value pairs mein se correct match choose karein:

A. `USE` = Query Data | `SELECT DATABASE()` = Change Active DB  
B. `USE` = Set Active Database Context | `SELECT DATABASE()` = Fetch Active Database Name  
C. `USE` = Delete Database | `SELECT DATABASE()` = Create Database  
D. `USE` = Create Table | `SELECT DATABASE()` = Insert Values  

**Answer:** B

**Explanation:** `USE` active database set karta hai aur `SELECT DATABASE()` active database ka naam fetch/display karta hai.

---

### Q30. Higher-Level Execution Check: Niche diye gaye SQL scripts mein se kaunsa script WITHOUT ANY ERROR complete execute hoga (fresh database server par)?

A. 
```sql
CREATE TABLE emp(id INT);
CREATE DATABASE company;
USE company;
```

B. 
```sql
CREATE DATABASE company;
USE company;
CREATE TABLE emp(id INT);
```

C. 
```sql
USE company;
CREATE DATABASE company;
```

D. 
```sql
SELECT DATABASE();
CREATE TABLE emp(id INT);
```

**Answer:** B

**Explanation:** Script B bilkul correct sequence follow karti hai: First create database (`CREATE DATABASE company;`), then activate it (`USE company;`), and finally create table inside it (`CREATE TABLE emp(id INT);`). Script A aur D mein database select kiye bina table create karne par Error 1046 aayega. Script C mein non-existing DB par `USE` chalane par Error 1049 aayega.
