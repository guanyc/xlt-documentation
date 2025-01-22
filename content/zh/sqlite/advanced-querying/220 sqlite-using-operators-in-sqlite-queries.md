---
# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: true
autoCollapseToc: false
postMetaInFooter: false
hiddenFromHomePage: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
contentCopyright: false
reward: false
mathjax: false
mathjaxEnableSingleDollar: false
mathjaxEnableAutoNumber: false

# You unlisted posts you might want not want the header or footer to show
hideHeaderAndFooter: false

# You can enable or disable out-of-date content warning for individual post.
# Comment this out to use the global config.
#enableOutdatedInfoWarning: false

flowchartDiagrams:
  enable: false
  options: ""

sequenceDiagrams:
  enable: false
  options: ""

title: "Sqlite Using Operators in Sqlite Queries"
date: "2024-12-20 14:34:42+08:00"
lastmod: "2024-12-20 14:34:42+08:00"
draft: false

keywords: [sqlite3]
tags: [sqlite3]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

featured_image: images/sqlite/using-operators.png
weight: 220
type: docs
---

### **Using Operators in SQLite Queries**

---

**James**: David, I keep seeing all these operators in SQL: `=`, `>`, `<`, `!=`, and even some weird ones like `IN` and `BETWEEN`. Do I need to know all of them?

**David**: Oh, definitely! Operators are the tools that make your queries powerful. Think of them as your Swiss Army knife for working with data.

**James**: So, they’re like filters and comparisons?

**David**: Exactly! Let’s break them down into categories and tackle them one at a time.

---

### **1. Comparison Operators**

**David**: These operators help you compare values. The basics include:

- `=`: Equal to
- `!=` or `<>`: Not equal to
- `<`, `>`, `<=`, `>=`: Less than, greater than, etc.

**James**: Got an example?

**David**: Sure! Say we have a `students` table:

```sql
CREATE TABLE students (
    id INTEGER PRIMARY KEY,
    name TEXT,
    age INTEGER,
    grade TEXT
);

INSERT INTO students (id, name, age, grade) VALUES
(1, 'Alice', 15, 'A'),
(2, 'Bob', 16, 'B'),
(3, 'Charlie', 15, 'C'),
(4, 'Diana', 17, 'A');
```

If you want students who are older than 15:

```sql
SELECT name, age
FROM students
WHERE age > 15;
```

**James**: Easy enough. What’s next?

---

### **2. Logical Operators**

**David**: These combine multiple conditions:

- `AND`: All conditions must be true.
- `OR`: At least one condition must be true.
- `NOT`: Negates a condition.

For instance, to find students older than 15 and with a grade of 'A':

```sql
SELECT name, age, grade
FROM students
WHERE age > 15 AND grade = 'A';
```

**James**: And if I want students older than 15 *or* with a grade of 'A'?

**David**: That’s an `OR`:

```sql
SELECT name, age, grade
FROM students
WHERE age > 15 OR grade = 'A';
```

---

### **3. Range and Membership Operators**

**James**: You mentioned `BETWEEN` and `IN`. What are those for?

**David**:
- `BETWEEN`: Checks if a value is within a range (inclusive).
- `IN`: Checks if a value matches one of several options.

Example for `BETWEEN`:

```sql
SELECT name, age
FROM students
WHERE age BETWEEN 15 AND 16;
```

And for `IN`:

```sql
SELECT name, grade
FROM students
WHERE grade IN ('A', 'B');
```

**James**: So `BETWEEN` is for ranges, and `IN` is for a specific set of values.

**David**: Exactly!

---

### **4. Pattern Matching Operators**

**David**: Don’t forget `LIKE` for pattern matching.

If you want students whose names start with 'A':

```sql
SELECT name
FROM students
WHERE name LIKE 'A%';
```

---

### **5. Arithmetic Operators**

**David**: SQLite also supports arithmetic in queries. You can add, subtract, multiply, and divide.

For example, if you want to calculate an age difference:

```sql
SELECT name, 18 - age AS years_to_adulthood
FROM students;
```

---

### **6. Null Handling**

**James**: And what about checking for missing data?

**David**: For `NULL`, use `IS NULL` or `IS NOT NULL`.

```sql
SELECT name
FROM students
WHERE grade IS NULL;
```

---

### **Common Pitfalls**

1. **Misusing `=` with `NULL`:**
   - Never use `= NULL`; it won’t work. Use `IS NULL`.

2. **Confusing `AND` and `OR`:**
   - Parentheses help clarify precedence when combining conditions.

3. **Overusing `LIKE` Wildcards:**
   - `%` can be expensive performance-wise if overused in large datasets.

---

### **Highlights**

1. **Comparison Operators:** Use for basic equality and range checks.
2. **Logical Operators:** Combine conditions with `AND`, `OR`, and `NOT`.
3. **Range and Membership:** Use `BETWEEN` for ranges and `IN` for specific values.
4. **Pattern Matching:** Use `LIKE` for partial matches with `%` and `_`.
5. **Arithmetic Operators:** Perform calculations in your queries.
6. **Null Handling:** Use `IS NULL` and `IS NOT NULL` for missing data.

---

### **Exercises for James**

1. Write a query to find students with a grade of 'B' or 'C'.
2. Find all students between the ages of 15 and 16.
3. Select students whose names contain the letter 'i'.
4. Calculate how many years each student has until they turn 18.
5. Identify students whose grade column is `NULL`.

---

### **References**

1. **[SQLite Operators Documentation](https://www.sqlite.org/lang_expr.html)**
   - Official documentation on supported operators.

2. **[SQL Logical Operators - W3Schools](https://www.w3schools.com/sql/sql_and_or.asp)**
   - A beginner-friendly guide to logical operators.

3. **[SQLite Pattern Matching](https://www.sqlitetutorial.net/sqlite-like/)**
   - Learn more about `LIKE` and wildcards.

4. **[SQL Arithmetic Operators](https://www.tutorialspoint.com/sql/sql-arithmetic-operators.htm)**
   - Overview of arithmetic operators in SQL.

---

**James**: This feels like leveling up my SQL powers. Combining operators is so satisfying.

**David**: It is! Once you master these, querying data becomes second nature. You’re doing great!
