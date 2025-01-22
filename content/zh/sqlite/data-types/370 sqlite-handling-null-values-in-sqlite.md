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

title: "Sqlite Handling Null Values in Sqlite"
date: "2025-01-09 22:23:00+08:00"
lastmod: "2025-01-09 22:23:00+08:00"
draft: false

keywords: [SQLite NULL Handling,  SQLite IS NULL, SQLite COALESCE Function ,Handling Missing Data in SQLite  ,NULL in Aggregate Functions]

tags: [sqlite3]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

weight: 380

type: docs

featured_image:


---

### **Handling NULL Values in SQLite**  
#### **Speech Between David and James**

---

**David:**  
"Alright, James, let’s tackle something critical in SQLite—`NULL` values. It’s a concept that often confuses beginners. Do you know what a `NULL` value is?"

**James:**  
"Kind of? It means 'nothing,' right? Like an empty cell in a spreadsheet?"

**David:**  
"Close! A `NULL` value in SQLite represents the absence of a value, not an empty string or zero. It’s like saying, 'I don’t know what this value is.' It's a big deal in databases because it behaves differently from other values."

---

### **Understanding NULL**

**David:**  
"Let’s start with some basic rules about `NULL` in SQLite:  
1. `NULL` is not equal to anything, even another `NULL`.  
2. Comparisons like `NULL = NULL` or `NULL != NULL` will return `FALSE`.  
3. Most functions, when given `NULL`, will return `NULL` unless specifically handled."

**James:**  
"So, it’s like the mysterious void of databases. How do we deal with it?"

---

### **Examples of NULL in Action**

#### **1. Insert NULL Values**
```sql
CREATE TABLE students (
    id INTEGER PRIMARY KEY,
    name TEXT,
    age INTEGER
);

INSERT INTO students (id, name) VALUES (1, 'Alice');
INSERT INTO students (id, name, age) VALUES (2, 'Bob', NULL);
```

**David:**  
"Here, Bob doesn’t have an age value. The database doesn’t assume it’s zero or empty—it’s just `NULL`."

#### **2. Check for NULL Using IS NULL and IS NOT NULL**
```sql
SELECT name FROM students WHERE age IS NULL;
-- Result: Bob
```

**James:**  
"So, we can’t use `=` to compare `NULL`?"

**David:**  
"Exactly! Always use `IS NULL` or `IS NOT NULL` for such checks."

---

#### **3. Coalesce: Providing Default Values for NULL**
```sql
SELECT name, COALESCE(age, 18) AS age FROM students;
-- Result:
-- Alice | 18
-- Bob   | 18
```

**David:**  
"Here, `COALESCE` replaces `NULL` with a default value—in this case, `18`."

**James:**  
"That’s handy! But can’t we set a default when creating the table?"

---

#### **4. Default Values in Table Creation**
```sql
CREATE TABLE students (
    id INTEGER PRIMARY KEY,
    name TEXT,
    age INTEGER DEFAULT 18
);

INSERT INTO students (id, name) VALUES (3, 'Charlie');
-- Charlie will have age 18 by default.
```

**David:**  
"Yes, you can! And it works great when you don’t explicitly provide a value."

---

#### **5. NULL and Aggregate Functions**
```sql
SELECT AVG(age) AS average_age FROM students;
-- Result: Only considers non-NULL values.
```

**James:**  
"So, `NULL` values don’t mess up averages?"

**David:**  
"Right, SQLite ignores `NULL` in aggregate functions like `AVG`, `SUM`, or `COUNT`."

---

#### **6. Common Pitfall: NOT IN with NULL**
```sql
SELECT * FROM students WHERE age NOT IN (18, 20, NULL);
-- Returns no results because of NULL in the list.
```

**James:**  
"Wait, what? Why?"

**David:**  
"If `NULL` is in the list, SQLite assumes there’s uncertainty, so the entire condition fails. Avoid `NOT IN` when `NULL` is involved."

---

### **Highlights**  

1. Use `IS NULL` or `IS NOT NULL` for `NULL` checks.  
2. Handle `NULL` explicitly with functions like `COALESCE`.  
3. Be cautious with `NOT IN` when `NULL` might be present.  
4. Aggregate functions ignore `NULL` by default.  
5. Default values in table creation can help reduce `NULL` issues.  

---

### **Exercises**  

1. Create a table `employees` with columns for `id`, `name`, and `salary`. Insert some rows where `salary` is `NULL`, and write a query to replace `NULL` salaries with a default value of 50,000.  
2. Write a query to find all rows where a specific column is `NULL`.  
3. Experiment with `NULL` in aggregate functions. Try `COUNT`, `SUM`, and `AVG` on a column with `NULL` values.  

---

### **References**  

1. [SQLite Documentation on NULL Handling](https://www.sqlite.org/lang_expr.html#nulls)  
2. [SQLite Documentation on COALESCE Function](https://www.sqlite.org/lang_corefunc.html#coalesce)
3. [SQLite Documentation on Aggregate Functions](https://www.sqlite.org/lang_aggfunc.html)

---

### **Keywords**  

- SQLite NULL Handling  
- SQLite IS NULL  
- SQLite COALESCE Function  
- Handling Missing Data in SQLite  
- NULL in Aggregate Functions  