Awesome! 🔥 Ab hum SQL ke sabse important topic par aa gaye hain.

Phase 1 - Lecture 3

🔑 Keys in SQL (Interview Favorite ⭐⭐⭐⭐⭐)

⚠️ Sach bataun?
Agar Keys samajh gaye, to baad me Joins, Normalization, aur Relationships bahut aasaan lagne lagenge.

Isliye is lecture ko skip ya jaldi me mat padhna.

🤔 Sabse Pehle Ek Sawal

Maan lo LPU me 40,000 students hain.

Table kuch aisi hai:

Roll No	Name	Branch
101	Rahul	CSE
102	Aman	IT
103	Rahul	CSE

Ab batao...

Agar Principal bole:

"Rahul ka record dikhao."

Kaunsa Rahul? 🤔

Rahul (Roll 101)
Rahul (Roll 103)

Sirf Name se identify nahi kar sakte.

Isliye hume ek aisi value chahiye jo har student ke liye unique ho.

👉 Isi concept se Keys aayi.

🔑 Key Kya Hoti Hai?
Simple Definition

Key = Table ke record ko uniquely identify karne ka tareeka.

Yaad rakhne wali line:

"Key helps us identify a row uniquely."

Real Life Example

Tumhare paas:

Aadhaar Number
PAN Number
Passport Number
Roll Number

Ye sab unique hote hain.

Do logon ka Aadhaar same ho sakta hai?

❌ Nahi.

Isliye ye Keys ki tarah kaam karte hain.

SQL me Kitni Types ki Keys Hoti Hain?

Sabse important ye 6 hain:

Keys
│
├── Super Key
├── Candidate Key
├── Primary Key
├── Alternate Key
├── Composite Key
└── Foreign Key

Hum ek-ek karke padhenge.

1️⃣ Super Key

Sabse pehle naam se confuse mat hona.

Definition:

Aisa column ya columns ka combination jo record ko uniquely identify kar sake.

Example Table:

Roll	Email	Phone	Name
101	a@gmail.com	9876	Rahul
102	b@gmail.com	8765	Aman

Yahan unique kya hai?

Roll ✅
Email ✅
Phone ✅

Aur combinations bhi unique honge:

Roll + Name ✅
Roll + Email ✅
Email + Phone ✅

Ye sab Super Keys hain.

Important Point

Super Key me extra columns ho sakte hain.

Example:

Roll

Unique hai.

Aur

Roll + Name

Ye bhi unique hai.

Lekin Name ki zarurat nahi thi.

Phir bhi unique hai.

Isliye ye bhi Super Key hai.

2️⃣ Candidate Key

Ab socho.

Super Keys bahut saari hain.

Hume sabse chhoti (minimal) unique key chahiye.

Isi ko Candidate Key bolte hain.

Example:

Roll	Email	Phone
101	a@gmail.com	9876

Candidate Keys:

Roll
Email
Phone

Ye teeno individually unique hain.

Aur kisi extra column ki zarurat nahi.

Interview Trick ⭐

Har Candidate Key, Super Key hoti hai.

Lekin...

Har Super Key, Candidate Key nahi hoti.

Kyun?

Kyuki Super Key me extra columns ho sakte hain.

3️⃣ Primary Key

Ab maan lo Candidate Keys hain:

Roll
Email
Phone

Lekin table me Primary Key sirf ek banegi.

Hum decide karte hain:

Roll Number

Ab Roll Number ban gaya

Primary Key

Definition:

Candidate Keys me se jo key officially choose ki jaye, use Primary Key kehte hain.

Rules of Primary Key
Rule 1

Unique honi chahiye.

✅

Rule 2

NULL nahi ho sakti.

❌

Galat:

Roll
NULL

Ye allowed nahi.

Rule 3

Duplicate nahi ho sakti.

Real Life Example

College

Primary Key = Roll Number

Hospital

Primary Key = Patient ID

Amazon

Primary Key = Order ID

Bank

Primary Key = Account Number

4️⃣ Alternate Key

Candidate Keys me se jo Primary Key nahi bani...

Wahi Alternate Keys hoti hain.

Example:

Candidate Keys:

Roll
Email
Phone

Primary Key:

Roll

Alternate Keys:

Email
Phone

Bas itna hi.

5️⃣ Composite Key

Kabhi-kabhi ek column se uniqueness nahi aati.

Tab do ya zyada columns ko mila kar key banate hain.

Example:

Attendance Table

Student_ID	Subject	Date
101	DBMS	10-Jul
101	OS	10-Jul

Sirf Student_ID unique nahi.

Sirf Subject bhi unique nahi.

Lekin:

Student_ID + Subject + Date

Ye combination unique hai.

Isliye ye Composite Key hai.

6️⃣ Foreign Key (⭐⭐⭐⭐⭐ Most Important)

Ab tak hum ek hi table dekh rahe the.

Ab do tables dekhte hain.

Students
Student_ID	Name
101	Rahul
102	Aman
Fees
Receipt	Student_ID	Amount
1	101	50000
2	102	45000

Notice kiya?

Fees table me jo Student_ID hai...

Wo Students table ki Primary Key ko refer kar raha hai.

Isi ko Foreign Key kehte hain.

Definition

Foreign Key ek table ka column hota hai jo doosri table ki Primary Key ko refer karta hai.

Real Life Analogy

Students Table

Student ID

↓

Fees Table

Student ID

↓

Dono connected.

Isi connection ki wajah se SQL me relationships bante hain.

Aur isi wajah se baad me hum JOIN use karte hain.

🔥 Summary Diagram
Super Key
     │
     ▼
Candidate Key
     │
     ▼
Primary Key

Aur

Candidate Keys
      │
Primary Key ko hata do
      │
      ▼
Alternate Keys

Aur

Do Tables

Students
    │
Primary Key
    │
    ▼
Foreign Key
    │
Fees
📒 Lecture Notes (Revision)
Key
Record ko uniquely identify karti hai.
Super Key
Unique + extra columns ho sakte hain.
Candidate Key
Minimal Super Key.
Primary Key
Candidate Key me se selected key.
Unique.
NULL nahi.
Duplicate nahi.
Alternate Key
Candidate Keys jo Primary Key nahi bani.
Composite Key
Do ya zyada columns milkar uniqueness dete hain.
Foreign Key
Dusri table ki Primary Key ko refer karti hai.
🎤 Interview Questions
Q1. Primary Key aur Candidate Key me difference?

Answer:

Candidate Keys multiple ho sakti hain.
Primary Key sirf ek hoti hai aur Candidate Keys me se choose ki jati hai.
Q2. Kya Primary Key NULL ho sakti hai?

❌ Nahi.

Q3. Kya ek table me multiple Primary Keys ho sakti hain?

❌ Nahi.

Ek hi Primary Key hoti hai.

Q4. Composite Key kab use karte hain?

Jab ek single column record ko uniquely identify na kar paaye.

Q5. Foreign Key ka purpose kya hai?

Do tables ke beech relationship establish karna aur data consistency maintain karna.

🎯 Homework (Concept Building)

Ek Library Management System imagine karo.

Socho usme ye tables hongi:

Books
Students
Book_Issue

Ab khud identify karne ki koshish karo:

Books table ki Primary Key kya hogi?
Students table ki Primary Key kya hogi?
Book_Issue table me kaun-kaun si Foreign Keys hongi?

Ye exercise karoge to Foreign Key ka concept bahut strongly baith jayega.

⏭️ Next Lecture (Phase 1 - Lecture 4)

Ab hum SQL Environment me entry karenge:

MySQL kya hai?
SQL aur MySQL me difference.
MySQL Workbench kya hai?
Database kaise create karte hain?
CREATE DATABASE
USE
Pehla database aur pehli table banayenge.

Yahin se hum actual SQL queries likhna start karenge. 🚀

