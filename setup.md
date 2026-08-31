🚀 SQL Phase 2 - Lecture 2
Installation + First Database + First Command (100% Practical)

Aaj ka Goal:

MySQL install karna
MySQL Workbench open karna
Server se connect hona
Pehla Database banana
Har command ka meaning samajhna
📌 Step 1 - MySQL Install Hai Ya Nahi?

Sabse pehle check karte hain.

Windows me

Keyboard se

Windows Key

Press karo.

Search karo

MySQL Workbench
Agar ye aa gaya
MySQL Workbench 8.0

To install hai.

Agar nahi aaya

To install karna padega.

📌 Step 2 - Agar Install Nahi Hai

Download karna hai:

Browser open karo (Chrome/Edge).
Search karo:
MySQL Community Download
Official MySQL website open karo.
MySQL Installer for Windows download karo.
Installer run karo.
Developer Default select karo.
Next → Next → Execute.
Root password set karo (example: root123).
Finish.

⚠️ Password yaad rakhna. Roz isi se login karna hoga.

📌 Step 3 - MySQL Workbench Open Karna

Desktop ya Start Menu se

MySQL Workbench

Open karo.

Screen kuch is type ki dikhegi:

+----------------------------+

Local instance MySQL80

+----------------------------+

Us par double click karo.

📌 Step 4 - Password

Password maangega.

Example:

Password

********

Yahan wahi password likho jo installation ke time diya tha.

Example:

root123

Login ho jaoge.

📌 Step 5 - Screen Samjho

Ab jo screen khulegi usme generally ye parts honge:

----------------------------------------

Navigator

Schemas

----------------------------------------

SQL Editor

Yahi commands likhenge.

----------------------------------------

Output

Yahan result dikhega.

----------------------------------------

Ye teen jagah yaad rakhna:

1️⃣ SQL Editor

Yahan hum commands likhenge.

2️⃣ Output

Yahan success ya error dikhega.

3️⃣ Schemas

Yahan databases dikhenge.

📌 Step 6 - Pehli SQL Command

SQL Editor me click karo.

Likho:

SHOW DATABASES;

Abhi execute mat karo.

Pehle samajhte hain.

SHOW DATABASES Ka Matlab

Maan lo MySQL ke andar already kuch databases hain.

Jaise:

mysql
sys
performance_schema
information_schema

Ye sab dekhna hai.

To hum likhte hain

SHOW DATABASES;
Syntax Breakdown
SHOW

Matlab

"Dikhao"

DATABASES

Matlab

"Saare databases"

;

Statement khatam.

Is Command Ka Output

Kuch is tarah aa sakta hai:

information_schema

mysql

performance_schema

sys

Ye system databases hain.

Inhe delete nahi karna.

📌 Step 7 - Command Execute Kaise Karein?

Workbench me do tareeke hain:

Method 1

Keyboard

Ctrl + Enter

Ye current query execute karega.

Method 2

Upar ⚡ (Lightning) icon hota hai.

Us par click karo.

Agar Successfully Chala

Neeche Output me likha aayega

Query OK

Ya result grid me databases dikh jayenge.

📌 Step 8 - Apna Database Banate Hain

Ab SQL Editor me likho:

CREATE DATABASE college;
Samajhte Hain
CREATE

Matlab

"Banao"

DATABASE

Matlab

"Database"

college

Ye database ka naam hai.

Tum kuch bhi rakh sakte ho.

Example

lpu

hospital

amazon

flipkart

school
Execute

Phir

Ctrl + Enter
Output
Query OK

1 row affected

Matlab

Database ban gaya.

📌 Step 9 - Verify

Ab dubara likho

SHOW DATABASES;

Execute karo.

Ab list me

college

bhi dikhega.

📌 Step 10 - Database Select Karna

Ab database bana liya.

Lekin kaam uske andar kaise karenge?

Likho:

USE college;

Execute.

Matlab

Ab jitni bhi tables banaoge

Wo

college

database ke andar banengi.

📌 Step 11 - Current Database Check

Likho

SELECT DATABASE();

Execute.

Output

college

Matlab

Abhi hum

college

database ke andar hain.

Ab Tak Humne Kya Kiya?
MySQL Workbench Open

↓

SHOW DATABASES;

↓

CREATE DATABASE college;

↓

SHOW DATABASES;

↓

USE college;

↓

SELECT DATABASE();

Ye har SQL project ka starting sequence hota hai.

🔥 Ek Bahut Important Cheez

Agar tum galti se likh do:

CREATE DATABASE college;

Aur database pehle se bana hua ho.

To error aayega:

Database 'college' already exists

Is problem se bachne ke liye industry me likhte hain:

CREATE DATABASE IF NOT EXISTS college;
Iska matlab:

Agar database nahi bana hai, tabhi banao. Agar pehle se bana hua hai, to error mat do.

Ye best practice hai.

📝 Lecture Notes (Revision)
Commands
SHOW DATABASES;

➡️ Saare databases dikhata hai.

CREATE DATABASE college;

➡️ Naya database banata hai.

CREATE DATABASE IF NOT EXISTS college;

➡️ Database sirf tab banata hai jab pehle se exist na karta ho.

USE college;

➡️ Current database select karta hai.

SELECT DATABASE();

➡️ Batata hai ki abhi kaunsa database active hai.

🎤 Interview Questions
Q1. SHOW DATABASES; kya karta hai?

➡️ MySQL server ke sabhi databases ki list dikhata hai.

Q2. USE command ka kya kaam hai?

➡️ Current active database ko select karta hai.

Q3. CREATE DATABASE IF NOT EXISTS kyun use karte hain?

➡️ Taaki agar database pehle se bana ho to error na aaye.

🎯 Homework (Practical)

Aaj sirf ye 5 commands khud chalao:

SHOW DATABASES;
CREATE DATABASE college;
SHOW DATABASES;
USE college;
SELECT DATABASE();
🚀 Next Lecture (SQL Coding Ka Actual Start)

Agle lecture me hum seekhenge:

CREATE TABLE
Data Types (INT, VARCHAR, CHAR, DATE, DECIMAL, BOOLEAN)
Column ka matlab
Constraints ka introduction
Apni pehli Students table banayenge aur har line ka meaning samjhenge.
📌 Ek Request

Next lecture start karne se pehle mujhe batao:

👉 Kya tumhare laptop me MySQL + MySQL Workbench pehle se install hai, ya hume installation se hi start karna hai?

Isse main bilkul tumhare setup ke hisaab se guide karunga.