# Day 7 — Quick Revision + 30 MCQs

---

## Quick Revision

Before attempting the MCQs, let's quickly review all key concepts covered in `day7.md`.

### 1. Aggregate Functions Overview
- **Definition:** Multiple rows of data ko process karke ek single summary result return karte hain.
- **5 Core Functions:**
  - `COUNT(*)`: Total rows (including NULLs).
  - `COUNT(column)`: Non-NULL rows count.
  - `SUM(column)`: Numeric values ka total.
  - `AVG(column)`: Numeric values ka average.
  - `MIN(column)`: Smallest value.
  - `MAX(column)`: Largest value.
- ⚠️ **Trap:** `SUM(name)` ya `AVG(name)` text columns par run nahi hote! Strictly numeric columns are required.

### 2. `GROUP BY` Clause (Data Grouping)
- **Definition:** Table ke identical/same column values ko summary groups me collapse/combine karta hai.
- **Syntax:** `SELECT column_name, AGG_FUNC() FROM table GROUP BY column_name;`
- **Use Case:** Group-wise analytics calculate karna (e.g. `SELECT city, COUNT(*) FROM student GROUP BY city;`).
- ⚠️ **Trap:** `SELECT` list me ungrouped & non-aggregated columns include karna (e.g. `SELECT city, name FROM student GROUP BY city;` ❌).

---

## 30 Most Important MCQs

---

### Q1. SQL me Multiple Rows ke values ko process karke single result value return karne wale functions ko kya kehte hain?

A. Scalar Functions  
B. Aggregate Functions  
C. User Defined Functions  
D. Mathematical Functions  

**Answer:** B

**Explanation:** Aggregate Functions (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`) multiple rows ko evaluate karke ek single aggregate output return karte hain.

---

### Q2. Table me Total Rows Count (including NULLs) karne ke liye kaunsa function call syntax use hota hai?

A. `COUNT(column)`  
B. `COUNT(*)`  
C. `SUM(*)`  
D. `TOTAL(*)`  

**Answer:** B

**Explanation:** `COUNT(*)` table me present saari rows ko count karta hai, chahe unme NULL values hon ya nahi.

---

### Q3. `COUNT(*)` aur `COUNT(column_name)` me main difference kya hai?

A. `COUNT(*)` slow hota hai, `COUNT(column)` fast hota hai  
B. `COUNT(*)` saari rows count karta hai, jabki `COUNT(column)` sirf Non-NULL values ko count karta hai  
C. `COUNT(column)` duplicate values skip kar deta hai  
D. Dono exact same output dete hain  

**Answer:** B

**Explanation:** `COUNT(column_name)` target column me missing/NULL values ko ignore karke sirf non-null records count karta hai.

---

### Q4. Table dataset (Ages: 20, 21, 22, 19). Query `SELECT SUM(age) FROM student;` ka calculated result kya aayega?

A. 20.5  
B. 82  
C. 4  
D. 22  

**Answer:** B

**Explanation:** `SUM(age)` = 20 + 21 + 22 + 19 = 82.

---

### Q5. Same dataset (Ages: 20, 21, 22, 19). Query `SELECT AVG(age) FROM student;` ka outcome kya hoga?

A. 82  
B. 20.5  
C. 20  
D. 21  

**Answer:** B

**Explanation:** `AVG(age)` = (20 + 21 + 22 + 19) / 4 = 82 / 4 = 20.5.

---

### Q6. Same dataset (Ages: 20, 21, 22, 19). Query `SELECT MIN(age) FROM student;` kaunsi value return karegi?

A. 22  
B. 19  
C. 20  
D. 21  

**Answer:** B

**Explanation:** `MIN(age)` dataset ki smallest value i.e. 19 return karta hai.

---

### Q7. Same dataset (Ages: 20, 21, 22, 19). Query `SELECT MAX(age) FROM student;` kaunsi value return karegi?

A. 19  
B. 22  
C. 82  
D. 20.5  

**Answer:** B

**Explanation:** `MAX(age)` dataset ki largest value i.e. 22 return karta hai.

---

### Q8. Common Error Trap: Query `SELECT SUM(name) FROM student;` execute karne par kya hoga?

A. Saare names concatenate ho jayenge  
B. Error / Warning aayegi kyunki `SUM()` text/string data type par work nahi karta  
C. Total name count return hoga  
D. Output NULL aayega  

**Answer:** B

**Explanation:** `SUM()` aur `AVG()` aggregate functions strictly numeric datatypes (`INT`, `FLOAT`, `DECIMAL`) par calculate hote hain.

---

### Q9. Identical column values (e.g. same cities) ko summary groups me collect karke collapse karne ke liye kaunsa SQL clause use hota hai?

A. `ORDER BY`  
B. `GROUP BY`  
C. `SORT BY`  
D. `COLLECT BY`  

**Answer:** B

**Explanation:** `GROUP BY` clause identical values wale records ko single summary row groups me combine karta hai.

---

### Q10. Har City me Total Kitne Students hain nikalne ki CORRECT SQL query kya hai?

A. `SELECT city, COUNT(*) FROM student GROUP BY city;`  
B. `SELECT city, SUM(*) FROM student GROUP BY city;`  
C. `SELECT city FROM student ORDER BY city;`  
D. `SELECT COUNT(city) FROM student;`  

**Answer:** A

**Explanation:** `SELECT city, COUNT(*) FROM student GROUP BY city;` same city wale students ke groups banakar har group ki total rows count karta hai.

---

### Q11. Target Dataset: (Delhi-3 students, Mumbai-2 students, Pune-1 student). Query `SELECT city, COUNT(*) FROM student GROUP BY city;` output result table me kitni rows hongi?

A. 6 Rows  
B. 3 Rows (Delhi: 3, Mumbai: 2, Pune: 1)  
C. 1 Row  
D. 4 Rows  

**Answer:** B

**Explanation:** `GROUP BY city` total unique cities count ke equal (3 rows: Delhi, Mumbai, Pune) output result grid banayega.

---

### Q12. Query `SELECT city, AVG(age) FROM student GROUP BY city;` ka main objective kya hai?

A. Saare cities ke students ki overall single average age nikalna  
B. Har city ke group ki ALAG-ALAG (individual) average age nikalna  
C. Cities list ko sort karna  
D. Error dega  

**Answer:** B

**Explanation:** `GROUP BY city` har city group ke members ki average age separate calculate karta hai.

---

### Q13. Syntax Error Check: MySQL me niche di gayi query invalid kyun consider hoti hai?
```sql
SELECT city, name FROM student GROUP BY city;
```

A. `city` keyword invalid hai  
B. `name` column `GROUP BY` list me missing hai aur us par koi Aggregate Function apply nahi hua hai  
C. `FROM` missing hai  
D. Query 100% ideal standard hai  

**Answer:** B

**Explanation:** Standard SQL rules ke according, `SELECT` clause me sirf vohi columns aa sakte hain jo `GROUP BY` clause me ho ya fir aggregate functions ke andar wrap huye hon.

---

### Q14. Real-life E-commerce Scenario: Amazon backend par "Har Brand ke Total Kitne Products hain" query likhne ke liye correct SQL code kya hoga?

A. `SELECT brand, COUNT(*) FROM products GROUP BY brand;`  
B. `SELECT brand, SUM(*) FROM products GROUP BY brand;`  
C. `SELECT brand FROM products ORDER BY brand;`  
D. `SELECT COUNT(brand) FROM products;`  

**Answer:** A

**Explanation:** Brands ke according products count karne ke liye `GROUP BY brand` ke saath `COUNT(*)` use hota hai.

---

### Q15. Aggregate Functions + `WHERE` Clause: Sirf Age >= 20 wale students ka total count batane ki correct query kya hai?

A. `SELECT COUNT(*) FROM student WHERE age >= 20;`  
B. `SELECT COUNT(*) FROM student HAVING age >= 20;`  
C. `SELECT SUM(age) FROM student WHERE age >= 20;`  
D. `SELECT AVG(*) FROM student WHERE age >= 20;`  

**Answer:** A

**Explanation:** `WHERE age >= 20` criteria filter apply hone ke baad `COUNT(*)` overall matching rows return karta hai.

---

### Q16. `AVG()` Aggregate Function null values ke saath kaise behave karta hai?

A. Null values ko 0 treat karke total count me include karta hai  
B. Null values ko completely ignore (exclude) kar deta hai  
C. Error throw karta hai  
D. Result NULL kar deta hai  

**Answer:** B

**Explanation:** Standard SQL aggregate functions (`AVG`, `SUM`, `COUNT(col)`, `MIN`, `MAX`) calculation se NULL values ko ignore kar dete hain.

---

### Q17. Group Summary Check: Dataset (Delhi: Rahul-20, Aman-21, Priya-19). Query: `SELECT city, MAX(age) FROM student WHERE city = 'Delhi' GROUP BY city;` Output result kya hoga?

A. Delhi | 20  
B. Delhi | 21  
C. Delhi | 19  
D. Delhi | 60  

**Answer:** B

**Explanation:** Delhi group me present ages (20, 21, 19) me se maximum age 21 hai.

---

### Q18. Group Summary Check: Same Delhi dataset (Rahul-20, Aman-21, Priya-19). Query: `SELECT city, MIN(age) FROM student WHERE city = 'Delhi' GROUP BY city;` Output result kya hoga?

A. Delhi | 19  
B. Delhi | 20  
C. Delhi | 21  
D. Delhi | 60  

**Answer:** A

**Explanation:** Delhi group me present smallest age 19 is outputted.

---

### Q19. `GROUP BY` clause ke saath usually in me se kin functions ko combine kiya jata hai?

A. Comparison Operators (`=`, `>`, `<`)  
B. Aggregate Functions (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`)  
C. Logical Operators (`AND`, `OR`)  
D. `LIKE` wildcards  

**Answer:** B

**Explanation:** `GROUP BY` clause majorly aggregate functions ke saath grouped analytics metrics calculate karne ke liye combine kiya jata hai.

---

### Q20. Interview Definition Question: `COUNT(*)` result datatype kya hota hai?

A. `VARCHAR`  
B. `INTEGER` (Number of rows count)  
C. `FLOAT`  
D. `BOOLEAN`  

**Answer:** B

**Explanation:** Row counts naturally non-negative whole numbers (Integers) hote hain.

---

### Q21. Query Output Check: Table has 5 rows. 2 rows have age = 20, 2 rows have age = 21, 1 row has age = NULL. Query: `SELECT COUNT(age) FROM student;` Output kya hoga?

A. 5  
B. 4 (Ignoring 1 NULL value)  
C. 2  
D. Error  

**Answer:** B

**Explanation:** `COUNT(column_name)` NULL values ko count nahi karta, so 5 - 1 = 4 return hoga.

---

### Q22. Same Table (5 rows, 1 NULL age). Query: `SELECT COUNT(*) FROM student;` Output kya hoga?

A. 4  
B. 5 (Including NULL row)  
C. 0  
D. Error  

**Answer:** B

**Explanation:** `COUNT(*)` total rows in table count karta hai irrespective of null values, so output is 5.

---

### Q23. Har Department ki Average Salary nikalne ke liye correct SQL code template kya hoga?

A. `SELECT dept, AVG(salary) FROM employee GROUP BY dept;`  
B. `SELECT dept, SUM(salary) FROM employee;`  
C. `SELECT AVG(salary) FROM employee;`  
D. `SELECT dept FROM employee GROUP BY salary;`  

**Answer:** A

**Explanation:** Department-wise average salary calculate karne ke liye `GROUP BY dept` ke saath `AVG(salary)` select kiya jata hai.

---

### Q24. Clause Sequence Rule: `GROUP BY` clause SQL query structure me kis position par aata hai?

A. `SELECT` se pehle  
B. `FROM` ya `WHERE` clause ke BAAD  
C. `ORDER BY` clause ke BAAD  
D. Query ke starting me  

**Answer:** B

**Explanation:** SQL Syntax Hierarchy: `SELECT` ➔ `FROM` ➔ `WHERE` ➔ `GROUP BY` ➔ `HAVING` ➔ `ORDER BY` ➔ `LIMIT`.

---

### Q25. Multiple Column Grouping: Query `SELECT department, city, COUNT(*) FROM student GROUP BY department, city;` kya return karegi?

A. Syntax error  
B. Unique combinations of Department AND City ke summary group counts  
C. Department wise counts ignore karke sirf city counts  
D. Plain table list  

**Answer:** B

**Explanation:** `GROUP BY col1, col2` dataset ko unique pairs of (Department, City) ke subgroups me group kar ke summary return karta hai.

---

### Q26. Practice Question Check: Student table me sabhi students ki total age ka sum nikalne ki query kya hai?

A. `SELECT COUNT(age) FROM student;`  
B. `SELECT SUM(age) FROM student;`  
C. `SELECT AVG(age) FROM student;`  
D. `SELECT MAX(age) FROM student;`  

**Answer:** B

**Explanation:** Total sum calculation ke liye `SUM(age)` function call kiya jata hai.

---

### Q27. Practice Question Check: Har city ki minimum age display karne wali correct query kya hai?

A. `SELECT city, MIN(age) FROM student GROUP BY city;`  
B. `SELECT city, MAX(age) FROM student GROUP BY city;`  
C. `SELECT MIN(age) FROM student;`  
D. `SELECT city FROM student WHERE age = MIN;`  

**Answer:** A

**Explanation:** City-wise minimum age output karne ke liye `SELECT city, MIN(age) FROM student GROUP BY city;` syntax correct hai.

---

### Q28. Aggregate Function Math: If ages are (20, 20, 20), what is `AVG(age)`?

A. 60  
B. 20  
C. 3  
D. 0  

**Answer:** B

**Explanation:** (20 + 20 + 20) / 3 = 60 / 3 = 20.

---

### Q29. Placement Question: 10,000 records wali employee table se Highest Salary nikalne ke liye O(N) single line query kya hogi?

A. `SELECT * FROM employee ORDER BY salary DESC LIMIT 1;`  
B. `SELECT MAX(salary) FROM employee;`  
C. Both A and B give the maximum salary scalar value  
D. `SELECT SUM(salary) FROM employee;`  

**Answer:** C

**Explanation:** Maximum salary value fetch karne ke liye `MAX(salary)` function or `ORDER BY salary DESC LIMIT 1` dono valid strategies hain.

---

### Q30. Synthesis Scenario: Niche di gayi SQL script ka output grid identify karein:
```sql
-- Table contains: Rahul(20, Delhi), Aman(21, Delhi), Rohit(22, Mumbai)
SELECT city, SUM(age)
FROM student
WHERE age >= 21
GROUP BY city;
```
Output result kya aayega?

A. Delhi: 41, Mumbai: 22  
B. Delhi: 21, Mumbai: 22  
C. Delhi: 20, Mumbai: 22  
D. Delhi: 41  

**Answer:** B

**Explanation:**  
1. `WHERE age >= 21` filters out Rahul (20). Remaining: Aman (21, Delhi) and Rohit (22, Mumbai).  
2. `GROUP BY city`:  
   - Delhi Group ➔ Aman (21) ➔ SUM = 21  
   - Mumbai Group ➔ Rohit (22) ➔ SUM = 22  
Output grid is Delhi: 21, Mumbai: 22.
