# SQL Practical — Day 9: Real Relational Schema Setup & JOIN Foundation

> **Overview:** Is day me hum SQL ke sabse major chapter **JOINS** ke liye complete multi-table relational database (`college_management`) build karenge aur Relational Database Normalization, Primary Key vs Foreign Key relationships, aur JOINs ki foundational necessity ko step-by-step seekhenge.

---

## 📌 Syllabus & Covered Topics
1. 🔍 **Lecture 22:** Relational Database & Multi-Table Schema Setup (`students` & `departments`)
2. 🔗 **Lecture 23:** JOIN Foundation (Why split data? Database Normalization & Foreign Keys)

---

## 🔍 Lecture 22: Relational Database & Multi-Table Schema Setup

### 🛠️ Step 0: Workbench Setup & Shortcut Keys
- Open **MySQL Workbench** ➔ Connect to Local Instance.
- Open New Query Tab: `Ctrl + T`.

---

### 🗄️ Step 1: Create Database & Select Active Schema

```sql
-- 1. Create Database:
CREATE DATABASE college_management;

-- 2. Select Database:
USE college_management;

-- 3. Verify Active Database:
SELECT DATABASE();
-- Output: college_management
```

---

### 🏗️ Step 2: Create Relational Tables Schema

#### 1. `departments` Table Creation
```sql
CREATE TABLE departments(
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100)
);
```

#### 2. `students` Table Creation
```sql
CREATE TABLE students(
    student_id INT PRIMARY KEY,
    student_name VARCHAR(100),
    age INT,
    city VARCHAR(50),
    department_id INT
);
```

#### 3. Verify Tables Structure
```sql
SHOW TABLES;
-- Expected Output: departments, students
```

---

### 📥 Step 3: Insert Production-Grade Sample Data

#### 1. Populate `departments` Table
```sql
INSERT INTO departments (department_id, department_name)
VALUES
(1, 'CSE'),
(2, 'ECE'),
(3, 'Mechanical'),
(4, 'Civil');

-- Verify Inserted Data:
SELECT * FROM departments;
```

**`departments` Table Output Grid:**
| department_id | department_name |
| :---: | :--- |
| 1 | CSE |
| 2 | ECE |
| 3 | Mechanical |
| 4 | Civil |

#### 2. Populate `students` Table
```sql
INSERT INTO students (student_id, student_name, age, city, department_id)
VALUES
(101, 'Rahul', 20, 'Delhi', 1),
(102, 'Aman', 21, 'Delhi', 2),
(103, 'Rohit', 22, 'Mumbai', 1),
(104, 'Priya', 19, 'Delhi', 3),
(105, 'Neha', 20, 'Mumbai', 2),
(106, 'Karan', 21, 'Pune', 1),
(107, 'Ankit', 23, 'Lucknow', 4),
(108, 'Sneha', 20, 'Patna', 2);

-- Verify Inserted Data:
SELECT * FROM students;
```

**`students` Table Output Grid:**
| student_id | student_name | age | city | department_id |
| :---: | :--- | :---: | :--- | :---: |
| 101 | Rahul | 20 | Delhi | 1 |
| 102 | Aman | 21 | Delhi | 2 |
| 103 | Rohit | 22 | Mumbai | 1 |
| 104 | Priya | 19 | Delhi | 3 |
| 105 | Neha | 20 | Mumbai | 2 |
| 106 | Karan | 21 | Pune | 1 |
| 107 | Ankit | 23 | Lucknow | 4 |
| 108 | Sneha | 20 | Patna | 2 |

---

### 🏛️ Schema Architecture Overview
```text
college_management Database
│
├── 📁 departments (Parent Table)
│   ├── department_id   [PRIMARY KEY]
│   └── department_name
│
└── 📁 students (Child Table)
    ├── student_id      [PRIMARY KEY]
    ├── student_name
    ├── age
    ├── city
    └── department_id   [FOREIGN KEY ➔ references departments(department_id)]
```

---

## 🔗 Lecture 23: JOIN Foundation (Concepts & Architecture)

---

### ❓ Why Split Data into Multiple Tables? (Database Normalization)

> **Question:** Single Table me `student_name` ke saath `department_name` direct kyun nahi store karte? Why create 2 tables?

#### ⚠️ Single Monolithic Table Structure (Anti-Pattern ❌):
| student_name | department_name |
| :--- | :--- |
| Rahul | CSE |
| Aman | ECE |
| Rohit | CSE |
| ... (10,000 rows) | CSE |

#### 🔄 Real-World Update Anomaly Problem
If CSE department is renamed to *"Computer Science"*:
- **Single Table:** 10,000 individual student rows require `UPDATE` modifications ⚠️ *(High CPU load, data corruption risk, update anomaly)*.
- **Relational Tables:** Only 1 single row in `departments` table gets updated (`department_id = 1`)! All 10,000 students automatically reflect the new name via key reference! 🎉✨

---

### 🔑 Primary Key vs Foreign Key Relationship

- **Primary Key (`departments.department_id`):** Uniquely identifies each department row in the parent table.
- **Foreign Key (`students.department_id`):** Reference column in child table pointing to the Primary Key of the parent table.

```text
+------------------------+             +--------------------------+
|        students        |             |       departments        |
+------------------------+             +--------------------------+
| student_id  (PK)       |             | department_id   (PK)     |
| student_name           |             | department_name          |
| department_id (FK) ────┼────────────►|                          |
+------------------------+             +--------------------------+
```

---

### 🎯 Interview Corner: Core Definition

> [!IMPORTANT]
> **Q: Why are JOINs required in Relational Databases (RDBMS)?**  
> **Answer:** JOINs are required to reconnect normalized tables that have been separated to eliminate data redundancy and update anomalies. They retrieve integrated result sets by matching records across tables using common key columns (Primary Key / Foreign Key).

---

### ✍️ Practice Questions — Lecture 22 & 23

#### Q1: Database `college_management` list me tables check karne ki query run karo.
#### Q2: `students` table ka full content display karo.
#### Q3: `departments` table ka full content display karo.
#### Q4: Rahul ka department_name fetch karne ke liye hum kaunsi technique use karenge?

<details>
<summary><b>Click to reveal Answers</b></summary>

**A1:** `SHOW TABLES;`  
**A2:** `SELECT * FROM students;`  
**A3:** `SELECT * FROM departments;`  
**A4:** We use **`JOIN`** (matching `students.department_id = departments.department_id`).  
</details>

---

## 🚀 What's Next? (Upcoming Teaser)
Next lecture covers **`INNER JOIN`** (Hands-on Syntax & MySQL internal row matching dry run)! 🚀

```sql
SELECT students.student_name, departments.department_name
FROM students
INNER JOIN departments
ON students.department_id = departments.department_id;
```

Itni depth me padhenge ki baad me JOIN kabhi difficult nahi lagega.

🔥 Main promise karta hoon, JOIN chapter hamare pure SQL course ka sabse best chapter hoga.
