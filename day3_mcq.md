# Day 3 — Quick Revision + 30 MCQs

---

## Part 1 — Quick Revision

Before attempting the MCQs, let's quickly review all key concepts covered in `day3.md`.

### 1. Logical Operators (`AND`, `OR`, `NOT`)
- **Need:** Filtering table rows based on multiple conditions in a single query (`WHERE`).
- **`AND` Operator:**
  - **Rule:** **Saari / Dono conditions `TRUE`** honi mandatory hain.
  - **Syntax:** `SELECT * FROM student WHERE condition1 AND condition2;`
  - **Truth Table:** `True AND True ➔ True`. (Agar ek bhi condition False ho to outcome False hota hai).
- **`OR` Operator:**
  - **Rule:** **Kam se kam EK condition `TRUE`** hona sufficient hai.
  - **Syntax:** `SELECT * FROM student WHERE condition1 OR condition2;`
  - **Truth Table:** `False OR False ➔ False`. (Agar ek bhi condition True ho to outcome True hota hai).
- **`NOT` Operator:**
  - **Rule:** Condition ke result ko **invert/reverse** kar deta hai (`TRUE ➔ FALSE`, `FALSE ➔ TRUE`).
  - **Example:** `WHERE NOT age = 20;` is identical to `WHERE age != 20;`.

### 2. Quotes & Syntax Rules
- Text / String criteria: Single quotes compulsory (`WHERE name = 'Aman'`).
- Case Sensitivity: Database me stored exact case (`'RAHUL'`) match karna zaroori hai.
- Numeric criteria: Bina quotes ke specify karein (`WHERE age = 20`).

### 3. Data Sorting (`ORDER BY` Clause)
- **Purpose:** Table rows ko 특정 column ke basis par sort (arrange) karne ke liye (C++ `sort()` function ke similar).
- **Ascending Order (`ASC`):**
  - **Numbers:** Small ➔ Large (`19` ➔ `20` ➔ `21` ➔ `22`).
  - **Text:** Alphabetical `A` ➔ `Z`.
  - **Default Behavior:** `ORDER BY col;` automatically `ASC` order follow karta hai.
- **Descending Order (`DESC`):**
  - **Numbers:** Large ➔ Small (`22` ➔ `21` ➔ `20` ➔ `19`).
  - **Text:** Reverse Alphabetical `Z` ➔ `A`.
  - Must specify `DESC` keyword explicitly after column name (`ORDER BY age DESC;`).

### 4. Amazon E-commerce Analogies
- **Search Filters:** `Brand = 'Nike' AND Price < 3000` (AND) | `Brand = 'Nike' OR Brand = 'Adidas'` (OR).
- **Price Sort:** Low to High = `ORDER BY price ASC;` | High to Low = `ORDER BY price DESC;`.

### 5. Common Traps & Syntax Errors
- ❌ `ORDER age BY;` (Wrong keyword order)
- ❌ `ORDER BY ASC age;` (`ASC` keyword placed before column name)
- ✅ `ORDER BY age ASC;` (Correct syntax)

---

## Part 2 — 30 MCQs

---

### Q1. Multiple conditions me se jab SAARI (all) conditions TRUE hona mandatory ho, to kaunsa logical operator use hota hai?

A. `OR`  
B. `NOT`  
C. `AND`  
D. `IN`  

**Answer:** C

**Explanation:** `AND` operator tabhi `TRUE` return karta hai jab iske saare boolean expressions `TRUE` evaluate hon.

---

### Q2. Multiple conditions me se jab KAM SE KAM EK (at least one) condition TRUE hona sufficient ho, to kaunsa logical operator use hota hai?

A. `AND`  
B. `OR`  
C. `NOT`  
D. `LIKE`  

**Answer:** B

**Explanation:** `OR` operator mein agar ek bhi condition `TRUE` ho jaye, to complete expression `TRUE` evaluate ho kar record select ho jata hai.

---

### Q3. `NOT` operator ka primary rule/function kya hai?

A. Query ko execute hone se rokna  
B. Condition ke boolean result ko invert / reverse karna (`TRUE ➔ FALSE`, `FALSE ➔ TRUE`)  
C. Database ko delete karna  
D. Table merge karna  

**Answer:** B

**Explanation:** `NOT` operator true condition ko false aur false condition ko true bana deta hai.

---

### Q4. Truth Table Check (AND): Agar Condition 1 `True` hai aur Condition 2 `False` hai, to `Condition1 AND Condition2` ka outcome kya hoga?

A. True  
B. False  
C. NULL  
D. Error  

**Answer:** B

**Explanation:** `AND` operator mein ek bhi condition `False` hone par final result `False` (Reject) ho jata hai.

---

### Q5. Truth Table Check (OR): Agar Condition 1 `False` hai aur Condition 2 `True` hai, to `Condition1 OR Condition2` ka outcome kya hoga?

A. False  
B. True  
C. NULL  
D. Error  

**Answer:** B

**Explanation:** `OR` operator mein ek bhi condition `True` hone par final result `True` (Select) ho jata hai.

---

### Q6. Niche di gayi query ka output result kya show karega?

```sql
SELECT * FROM student
WHERE name = 'Aman' AND age = 21;
```
*(Dataset: Rahul-20, Aman-21, Rohit-22, Priya-19)*

A. Aman (21)  
B. Rahul (20) aur Aman (21)  
C. Blank output  
D. Saare students  

**Answer:** A

**Explanation:** `AND` operator ke liye dono condition (`name = 'Aman'` AND `age = 21`) strictly Aman ke record par True match hoti hain.

---

### Q7. Niche di gayi query ka expected output kya hoga?

```sql
SELECT * FROM student
WHERE age = 19 OR age = 22;
```
*(Dataset: Rahul-20, Aman-21, Rohit-22, Priya-19)*

A. Rohit (22)  
B. Priya (19)  
C. Rohit (22) aur Priya (19)  
D. Aman (21)  

**Answer:** C

**Explanation:** `OR` operator `age = 19` wale record (Priya) aur `age = 22` wale record (Rohit) dono ko output grid me select karega.

---

### Q8. Query `SELECT * FROM student WHERE NOT age = 20;` in me se kis query ke EXACT IDENTICAL execute karegi?

A. `SELECT * FROM student WHERE age = 20;`  
B. `SELECT * FROM student WHERE age != 20;`  
C. `SELECT * FROM student WHERE age > 20;`  
D. `SELECT * FROM student WHERE age < 20;`  

**Answer:** B

**Explanation:** `NOT age = 20` age=20 wali condition ko invert kar deta hai, jo behavior-wise exact `age != 20` ke barabar hota hai.

---

### Q9. Amazon e-commerce analogy: Search filter me jab user `Brand = 'Nike' AND Price < 3000` set karta hai, to kaunse shoes screen par dikhenge?

A. Jo shoes Nike brand ke hon YA 3000 se saste hon  
B. Strictly wahi shoes jo Nike brand ke hon AUR jin ki price 3000 se kam ho  
C. Saare shoes  
D. Sirf Adidas shoes  

**Answer:** B

**Explanation:** `AND` condition match hone par product me dono criteria (Nike brand + Price < 3000) simultaneous fulfill hone mandatory hain.

---

### Q10. Placement Scenario: Target record `name = 'RAHUL'` aur `age = 20` ko fetch karna hai. Database me name uppercase `'RAHUL'` stored hai. Sahi query chuniyen:

A. `SELECT * FROM student WHERE name = 'Rahul' AND age = 20;`  
B. `SELECT * FROM student WHERE name = 'RAHUL' AND age = 20;`  
C. `SELECT * FROM student WHERE name = RAHUL OR age = 20;`  
D. `SELECT RAHUL FROM student;`  

**Answer:** B

**Explanation:** Database me data exact stored case (`'RAHUL'`) mein single quotes ke saath `AND` operator apply karke fetch hona chahiye.

---

### Q11. Scenario-based Question: Niche diye gaye query execution ko analyze karein:

```sql
SELECT * FROM student
WHERE age > 20 AND name = 'Aman';
```
*(Dataset: Rahul-20, Aman-21, Rohit-22, Priya-19)*

Output kya hoga?

A. Aman (21)  
B. Rohit (22)  
C. Aman (21) aur Rohit (22)  
D. Blank  

**Answer:** A

**Explanation:** `age > 20` is True for Aman (21) and Rohit (22). But `AND name = 'Aman'` condition strictly filter out kar ke sirf Aman ko return karegi.

---

### Q12. Scenario-based Question: Niche diye gaye query filter ka output kya hoga?

```sql
SELECT * FROM student
WHERE age > 21 OR age < 20;
```
*(Dataset: Rahul-20, Aman-21, Rohit-22, Priya-19)*

A. Aman (21), Rohit (22)  
B. Rohit (22), Priya (19)  
C. Rahul (20), Priya (19)  
D. Rohit (22)  

**Answer:** B

**Explanation:** `age > 21` gives Rohit (22). `age < 20` gives Priya (19). Dono ke beech `OR` use hua hai, isliye Rohit (22) aur Priya (19) dono select honge.

---

### Q13. SQL queries me table rows ko sort (arrange) karne ke liye kaunsa clause use hota hai?

A. `SORT BY`  
B. `ORDER BY`  
C. `ARRANGE BY`  
D. `GROUP BY`  

**Answer:** B

**Explanation:** SQL mein data ko ascending ya descending order me sort karne ke liye `ORDER BY` clause use kiya jata hai.

---

### Q14. C++ programming ke according `ORDER BY` clause kis built-in utility ke similar role perform karta hai?

A. `vector::push_back()`  
B. `sort()` function  
C. `cin` input stream  
D. `sizeof()` operator  

**Answer:** B

**Explanation:** Notes ke conceptual breakdown me bataya gaya hai ki SQL ka `ORDER BY` clause C++ ke `sort()` function jaisa sorting kaam karta hai.

---

### Q15. SQL mein `ORDER BY column_name;` (bina ASC ya DESC mention kiye) ka DEFAULT behavior kya hota hai?

A. Descending order (`DESC`)  
B. Ascending order (`ASC`)  
C. Random order  
D. Reverse insertion order  

**Answer:** B

**Explanation:** SQL `ORDER BY` by default **Ascending (`ASC`)** order follow karta hai. `ORDER BY age;` and `ORDER BY age ASC;` are identical.

---

### Q16. `ASC` (Ascending) sorting parameter numeric aur text values ko kis order me arrange karta hai?

A. Numbers: Large ➔ Small | Text: Z ➔ A  
B. Numbers: Small ➔ Large | Text: A ➔ Z  
C. Numbers: Random | Text: Length order  
D. Numbers: Negative only | Text: Lowercase only  

**Answer:** B

**Explanation:** `ASC` small numbers se large numbers (19 ➔ 20 ➔ 21 ➔ 22) aur text ko alphabetical order (A ➔ Z) me arrange karta hai.

---

### Q17. `DESC` (Descending) sorting parameter numeric aur text values ko kis order me arrange karta hai?

A. Numbers: Small ➔ Large | Text: A ➔ Z  
B. Numbers: Large ➔ Small | Text: Z ➔ A  
C. Numbers: Even ➔ Odd | Text: Vowels first  
D. Numbers: Prime numbers first  

**Answer:** B

**Explanation:** `DESC` large numbers se small numbers (22 ➔ 21 ➔ 20 ➔ 19) aur text ko reverse alphabetical order (Z ➔ A) me arrange karta hai.

---

### Q18. Amazon e-commerce analogy: Search result me jab user "Price: Low to High" select karta hai, to underlying SQL query me kya syntax apply hoga?

A. `ORDER BY price DESC;`  
B. `ORDER BY price ASC;`  
C. `WHERE price = LOW;`  
D. `GROUP BY price;`  

**Answer:** B

**Explanation:** "Low to High" price sorting ke liye `ORDER BY price ASC;` (ya simple `ORDER BY price;`) execute hota hai.

---

### Q19. Amazon e-commerce analogy: Search result me "Price: High to Low" ke liye SQL query kya hogi?

A. `ORDER BY price ASC;`  
B. `ORDER BY price DESC;`  
C. `WHERE price > HIGH;`  
D. `SELECT price DESC;`  

**Answer:** B

**Explanation:** "High to Low" price sorting ke liye `ORDER BY price DESC;` execute hota hai.

---

### Q20. Common Mistake Alert: Niche di gayi queries me se kaunsa syntax WRONG (Incorrect) hai?

A. `SELECT * FROM student ORDER BY age ASC;`  
B. `SELECT * FROM student ORDER BY age DESC;`  
C. `SELECT * FROM student ORDER BY ASC age;`  
D. `SELECT * FROM student ORDER BY age;`  

**Answer:** C

**Explanation:** `ASC` ya `DESC` keyword column name ke BAAD likha jata hai. `ORDER BY ASC age` Syntax Error dega.

---

### Q21. Common Mistake Alert: Niche diye gaye syntax options me se kaunsa option galat keyword order ki wajah se error dega?

A. `ORDER BY age;`  
B. `ORDER age BY;`  
C. `ORDER BY age DESC;`  
D. `ORDER BY name ASC;`  

**Answer:** B

**Explanation:** Correct SQL clause `ORDER BY` hota hai. `ORDER age BY` invalid keyword ordering error throw karega.

---

### Q22. Output Grid Check: Niche di gayi query ka output row sequence kya hoga?

```sql
SELECT * FROM student ORDER BY age ASC;
```
*(Dataset: Rahul-20, Aman-21, Rohit-22, Priya-19)*

A. Rohit (22), Aman (21), Rahul (20), Priya (19)  
B. Priya (19), Rahul (20), Aman (21), Rohit (22)  
C. Rahul (20), Aman (21), Rohit (22), Priya (19)  
D. Aman (21), Priya (19), Rahul (20), Rohit (22)  

**Answer:** B

**Explanation:** Ascending order (`ASC`) small to large numbers arrange karega: 19 (Priya) ➔ 20 (Rahul) ➔ 21 (Aman) ➔ 22 (Rohit).

---

### Q23. Output Grid Check: Niche di gayi query ka output row sequence kya hoga?

```sql
SELECT * FROM student ORDER BY age DESC;
```
*(Dataset: Rahul-20, Aman-21, Rohit-22, Priya-19)*

A. Priya (19), Rahul (20), Aman (21), Rohit (22)  
B. Rohit (22), Aman (21), Rahul (20), Priya (19)  
C. Rahul (20), Aman (21), Rohit (22), Priya (19)  
D. Aman (21), Rohit (22), Priya (19), Rahul (20)  

**Answer:** B

**Explanation:** Descending order (`DESC`) large to small numbers arrange karega: 22 (Rohit) ➔ 21 (Aman) ➔ 20 (Rahul) ➔ 19 (Priya).

---

### Q24. String Sorting Check: Query `SELECT * FROM student ORDER BY name ASC;` par names (`Aman`, `Priya`, `RAHUL`, `Rohit`) ka correct Alphabetical output order kya hoga?

A. Rohit, RAHUL, Priya, Aman  
B. Aman, Priya, RAHUL, Rohit  
C. Priya, Aman, Rohit, RAHUL  
D. RAHUL, Rohit, Aman, Priya  

**Answer:** B

**Explanation:** `ASC` text ko Alphabetical A ➔ Z arrange karta hai: Aman ➔ Priya ➔ RAHUL ➔ Rohit.

---

### Q25. Interview Question: Placement round me question: "What is the difference between `ASC` and `DESC` in `ORDER BY`?" ka perfect answer kya hoga?

A. `ASC` table create karta hai, `DESC` table drop karta hai  
B. `ASC` default sorting (Small ➔ Large / A ➔ Z) hai, jabki `DESC` explicit reverse sorting (Large ➔ Small / Z ➔ A) hai  
C. `ASC` string ke liye hai, `DESC` integers ke liye hai  
D. Dono keywords interchangeable hain  

**Answer:** B

**Explanation:** `ASC` Ascending default sorting strategy hai aur `DESC` Descending explicit reverse sorting strategy hai.

---

### Q26. Scenario-based Question: Agar student table me ye records hon:
- Karan (23)
- Neha (18)
- Vikas (20)

Query: `SELECT name FROM student ORDER BY age ASC;`  
Sabse pehle (Top row) par kaunsa student name aayega?

A. Karan  
B. Neha  
C. Vikas  
D. None  

**Answer:** B

**Explanation:** `ORDER BY age ASC` lowest age value (18) ko top par rakhega. Age 18 wala student Neha hai, to Neha pehli row me aayegi.

---

### Q27. Combined Clause Order: Real-world queries me `WHERE` aur `ORDER BY` ek saath run hote hain. Correct execution sequence syntax kya hota hai?

A. `ORDER BY` pehle, `WHERE` baad me  
B. `WHERE` clause pehle, `ORDER BY` clause baad me  
C. Dono kisi bhi order me likh sakte hain  
D. Dono ek query me use nahi ho sakte  

**Answer:** B

**Explanation:** SQL syntax rule ke according filter (`WHERE`) pehle apply hota hai, aur filtered output set par sorting (`ORDER BY`) baad me apply hota hai (`SELECT * FROM table WHERE condition ORDER BY col;`).

---

### Q28. Homework Query Check: Homework me naye records insert kiye gaye:
```sql
INSERT INTO student(id, name, age) VALUES (5, 'Karan', 23), (6, 'Neha', 18), (7, 'Vikas', 20);
SELECT * FROM student ORDER BY age DESC;
```
Top row par sabse pehla record kaunsa dikhega?

A. Neha (18)  
B. Karan (23)  
C. Rohit (22)  
D. Vikas (20)  

**Answer:** B

**Explanation:** Total dataset me largest age Karan (23) ki hai. `ORDER BY age DESC` largest age ko sabse upar (top row) display karega.

---

### Q29. Logical Trap Check: Niche di gayi query ka outcome batayein:

```sql
SELECT * FROM student
WHERE NOT (age = 20 OR age = 21);
```
*(Dataset: Rahul-20, Aman-21, Rohit-22, Priya-19)*

Output me kaun-kaun se students aayenge?

A. Rahul (20) aur Aman (21)  
B. Rohit (22) aur Priya (19)  
C. Saare students  
D. Blank  

**Answer:** B

**Explanation:** `(age = 20 OR age = 21)` Rahul aur Aman par `TRUE` deta hai. Outer `NOT` operator us `TRUE` ko `FALSE` bana kar filter out kar dega. So remaining rows i.e. Rohit (22) and Priya (19) result set me return honge.

---

### Q30. Upcoming Topic Teaser Check: Day 3 notes ke end teaser ke according, Next Lecture me LeetCode/HackerRank placement favorite kaunsa topic padhaya jayega?

A. `JOIN`  
B. `LIMIT` (Top N Records / First N Students)  
C. `GROUP BY`  
D. `ALTER TABLE`  

**Answer:** B

**Explanation:** Day 3 notes ke concluding section ke according, next upcoming main topic `LIMIT` clause hai (Top N records, highest/lowest age students).
