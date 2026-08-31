# SQL Basics — Practical Day 1 (Database Selection)

> **Context / Recap:** Pichhle lecture me humne database banaya tha:  
> `CREATE DATABASE college;`  
> Ab agla step hai database ko select karke uske andar kaam karna.

---

## 📌 Study Pattern Overview
- 📖 **Theory (Very Basic)**
- 💻 **Practical**
- 🧠 **Har Command Ka Meaning**
- ⚠️ **Common Mistakes**
- 🎤 **Interview Point**
- ✍️ **Practice Questions & Answers**

---

## 1. Step 1 — Database Ko Use Karna (`USE` Command)

### 💡 Database Select Kyun Karte Hain?
Agar server me 50 databases hain, to MySQL ko kaise pata chalega ki table kis database ke andar banani hai?  
Isliye sabse pehle hum database ko select / active karte hain.

### 💻 Command
```sql
USE college;
```

### 🧠 Is Command Ko Todte Hain
| Part / Command | Meaning |
| :--- | :--- |
| `USE` | "Ab se isi database ke andar kaam karo." |
| `college` | Database ka naam |
| **Poora Matlab** | "MySQL, ab `college` database ko active kar do." |

---

### 📂 Real Life Example
Socho laptop me multiple folders hain:
- Documents
- Photos
- **Projects** 👈 *(Tum is folder ko open karte ho)*
- Movies

Tum **Projects** folder open karte ho. Ab jo bhi file save karoge, wo Projects ke andar hi jayegi.  
Bilkul waise hi `USE college;` chalane ke baad jitni bhi tables banengi, wo `college` database ke andar banengi.

---

### 🕹️ Run Kaise Karen? & Success Verification

1. **Write:**  
   ```sql
   USE college;
   ```
2. **Run:**  
   Press `Ctrl + Enter`

3. **Success Kaise Pata Chalega?**  
   Neeche **Action Output** window me likha aayega:  
   `Query OK`  ya  `Database changed`  
   Matlab command successfully chal gayi hai!

---

## 2. Step 2 — Check Karen Ki Database Active Hai Ya Nahi (`SELECT DATABASE();`)

### 💻 Command
```sql
SELECT DATABASE();
```

### 📊 Expected Output
```text
+------------------+
| DATABASE()       |
+------------------+
| college          |
+------------------+
```
*(Agar output me `college` aaya to matlab wahi active database hai.)*

---

### 🧠 `SELECT DATABASE()` Ka Meaning Breakdown
| Part | Meaning |
| :--- | :--- |
| `SELECT` | 👉 Nikalo / Dikhao |
| `DATABASE()` | 👉 Current active database function |
| **Poora Matlab** | "Mujhe batao abhi kaunsa database active hai." |

---

## 3. 📒 Summary Notes

| Goal | SQL Command | Kaam / Function |
| :--- | :--- | :--- |
| **Database Select Karna** | `USE college;` | `college` database ko active karta hai. |
| **Current Database Check Karna** | `SELECT DATABASE();` | Abhi kaunsa database active hai, ye batata hai. |

---

## 4. ⚠️ Common Mistake

> [!WARNING]
> **Galti:** Database select kiye bina table create karne ki koshish karna.
> ```sql
> CREATE TABLE student(
>     id INT
> );
> ```
> Agar tum `USE college;` chalana bhool gaye, to error aa sakta hai (`Error 1046: No database selected`) ya table galat database me ban sakti hai.  
>  
> **Rule:** Isliye database create karne ke baad sabse pehle `USE` command chalate hain.

---

## 5. 🎤 Interview Question

> [!IMPORTANT]
> **Q. `USE` command ka kya kaam hai?**  
>  
> **Answer:** `USE` command kisi database ko current active database bana deti hai, jiske andar baad ki saari tables aur operations perform hote hain.

---

## 6. 🧑‍💻 Practice Questions

### Question 1
`school` naam ka database active karne ki command likho.

### Question 2
Current active database dekhne ki command likho.

### Question 3
`company` database ko active karne ki command likho.

---

### ✅ Answers (Pehle Mat Dekhna 😄)

<details>
<summary><b>Click to reveal Answer 1</b></summary>

```sql
USE school;
```
</details>

<details>
<summary><b>Click to reveal Answer 2</b></summary>

```sql
SELECT DATABASE();
```
</details>

<details>
<summary><b>Click to reveal Answer 3</b></summary>

```sql
USE company;
```
</details>

---

## 🚀 Next Lecture (Bahut Important)
Iske baad hum SQL ka sabse pehla aur sabse important command seekhenge: **`CREATE TABLE`**

Usme hum padhenge:
- Table kya hoti hai (practical)
- Columns kaise banate hain
- `INT` kya hota hai
- `VARCHAR(50)` kya hota hai
- `PRIMARY KEY`
- `NOT NULL`
- Aur apni pehli `Student` table banayenge.

*Ye SQL ka asli coding start hoga. Yahin se tum database design karna seekh jaoge.*