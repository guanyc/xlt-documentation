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

title: "Sqlite Understanding Dynamic Typing System"
date: "2024-12-28 21:11:36+08:00"
lastmod: "2024-12-28 21:11:36+08:00"
draft: false

keywords: SQLite, dynamic typing, storage classes, type affinity, data integrity, CHECK constraints, implicit type conversion  
tags: [sqlite3]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

weight: 340
type: docs

featured_image:


---

### SQLite’s Dynamic Typing System Explained  
*A Casual Chat Between David and James*  

---

**David:** James, I was working with SQLite, and I noticed I could insert a string into a column I thought was supposed to store numbers. Isn’t that a bug?  

**James:** Haha, nope! That’s just SQLite’s dynamic typing at work. It’s flexible like that, but you have to be careful. Let me explain.  

---

### **Highlight 1: SQLite’s Dynamic Typing**  
**James:** Unlike other databases, SQLite doesn’t enforce strict data types for columns. Instead, it uses something called *storage classes*.  

**David:** Storage classes? What are those?  

**James:** Think of them as categories like `INTEGER`, `REAL`, `TEXT`, `BLOB`, and `NULL`. A column might suggest a type, but SQLite doesn’t insist on it.  

**Example:**  

```sql
CREATE TABLE demo (id INTEGER, data TEXT);
INSERT INTO demo (id, data) VALUES (1, 'Hello'); -- Works as expected
INSERT INTO demo (id, data) VALUES ('ABC', 123); -- Still works!
```

---

### **Pitfall 1: Data Integrity Risks**  
**David:** Wait a second. Doesn’t this make it easy to mess up data?  

**James:** Absolutely! For example:  

```sql
INSERT INTO demo (id) VALUES ('Hello');
```

**David:** But that should’ve been a number!  

**James:** That’s why you need to validate data at the application level or use `CHECK` constraints:  

```sql
CREATE TABLE demo (
  id INTEGER CHECK(typeof(id) = 'integer')
);
```

---

### **Highlight 2: Type Affinity**  
**James:** SQLite does try to behave predictably with something called *type affinity*.  

**David:** What’s that?  

**James:** When you declare a column type, SQLite interprets it loosely. For example:  

```sql
CREATE TABLE demo (price NUMERIC);
```

- SQLite uses the `NUMERIC` affinity, so it tries to store values as `INTEGER` or `REAL`.  
- If it can’t, it falls back to `TEXT`.  

---

### **Pitfall 2: Implicit Type Conversion**  
**James:** Watch out for unexpected conversions!  

```sql
INSERT INTO demo (price) VALUES ('100abc');
SELECT price + 1 FROM demo;
```

**David:** Oh no! Instead of failing, it treats `'100abc'` as `0`.  

**James:** Exactly. Always sanitize input and validate data.  

---

### **Exercise Time!**  

1. **Identify Issues:**  
   - Create a table with a `TEXT` column. Try inserting numbers, strings, and mixed types. Observe how SQLite handles each case.  

2. **Add Constraints:**  
   - Modify a table to enforce that a column only accepts integers using a `CHECK` constraint.  

3. **Debug Query:**  
   - James ran this query:  
     ```sql
     INSERT INTO demo (price) VALUES ('abc123');
     ```
     Write a query to find and clean up invalid rows.  

---

### **References for Further Reading**  
- [SQLite Data Types - Official Documentation](https://sqlite.org/datatype3.html)  
- [Type Affinity in SQLite](https://sqlite.org/datatype3.html#type_affinity)  

---

### **Keywords:**  
SQLite, dynamic typing, storage classes, type affinity, data integrity, CHECK constraints, implicit type conversion  
