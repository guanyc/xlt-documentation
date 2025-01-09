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

title: "Sqlite3 Storing Numbers Text and Binary Data"
date: "2025-01-09 11:04:54+08:00"
lastmod: "2025-01-09 11:04:54+08:00"
draft: false

keywords: [SQLite Data Types,
Storing Numbers in SQLite,  
SQLite TEXT vs. BLOB , 
Dynamic Typing in SQLite,
How SQLite Handles Binary Data]
tags: [sqlite3]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

weight: 350
type: docs

weight:
featured_image: /images/sqlite/sqlite-text-binary-data.jpg


---

**Storing Numbers, Text, and Binary Data**  
*Speech between XiaoMing and James*  

---

### **Scene: A Cozy Café**  
*XiaoMing and James are seated at a table, laptops open. James has a puzzled expression as he looks at a SQLite3 schema.*  

---

**James**: Alright, XiaoMing. So I get that SQLite can store numbers, text, and even binary data like images or audio files. But… how does it actually handle these? Are there any hidden traps I should watch out for?  

**XiaoMing**: Good question! SQLite is pretty flexible when it comes to storing data, but there are definitely some nuances. It uses something called a "dynamic type system."  

**James**: Dynamic type system? Sounds like it breaks all the database rules!  

**XiaoMing**: *[laughs]* Kind of. Unlike strict databases like MySQL or PostgreSQL, SQLite doesn’t rigidly enforce data types. For example, you can declare a column as `INTEGER`, but SQLite won’t stop you from inserting a string into that column.  

**James**: That sounds… both cool and dangerous.  

**XiaoMing**: Exactly. Let’s break it down. SQLite supports five basic storage classes:  

1. **NULL**: Just an absence of a value.  
2. **INTEGER**: Whole numbers, stored as 1, 2, 4, 6, or 8 bytes depending on the size.  
3. **REAL**: Floating-point numbers.  
4. **TEXT**: Strings, stored in UTF-8 or UTF-16.  
5. **BLOB**: Binary Large Objects, exactly as you provide them.  

**James**: So, if I wanted to store a user’s age, it’d be `INTEGER`. And if I wanted their name, that’s `TEXT`, right?  

**XiaoMing**: Spot on! But there’s more to it. Let’s dive into examples for each data type and some potential pitfalls.

---

### **Examples for Each Data Type**

#### **1. Storing Numbers with INTEGER and REAL**  
```sql
CREATE TABLE Users (
    id INTEGER PRIMARY KEY,
    name TEXT,
    age INTEGER,
    balance REAL
);

INSERT INTO Users (id, name, age, balance)
VALUES (1, 'Alice', 25, 1234.56);
```
- **James**: Okay, so `age` is an `INTEGER`, and `balance` is a `REAL` for decimals.  
- **Pitfall**: If you store something like `'25'` (a string) into `age`, SQLite won’t complain. However, operations like sorting or calculations could give unexpected results.  

#### **2. Storing Text with TEXT**  
```sql
CREATE TABLE Messages (
    id INTEGER PRIMARY KEY,
    content TEXT
);

INSERT INTO Messages (id, content)
VALUES (1, 'Hello, SQLite!');
```
- **James**: This one’s straightforward. TEXT is just for strings, right?  
- **XiaoMing**: Right, but remember, SQLite doesn’t have a fixed length for strings like some other databases. Also, strings are case-sensitive in comparisons unless you specify otherwise.  

#### **3. Storing Binary Data with BLOB**  
```sql
CREATE TABLE Files (
    id INTEGER PRIMARY KEY,
    file_name TEXT,
    file_content BLOB
);

-- Example: Storing an image in binary
INSERT INTO Files (id, file_name, file_content)
VALUES (1, 'profile_pic.png', X'89504E470D0A1A0A...');
```
- **James**: Wait… what’s with that `X'...` thing?  
- **XiaoMing**: That’s how you represent binary data in SQLite. You can also bind binary data programmatically using libraries.  
- **Pitfall**: Binary data can get huge! If you’re storing large files, SQLite might not be the best choice compared to a dedicated file storage system.

---

### **Highlights**
1. **Dynamic Typing**: SQLite lets you store values of any type in any column (except for PRIMARY KEY).  
2. **Efficient Storage**: SQLite uses variable-length encoding for numbers to save space.  
3. **BLOBs for Binary Data**: Great for small files but not ideal for large ones.  
4. **TEXT Pitfalls**: Watch out for case sensitivity and collation settings.  

---

### **Exercises**  

1. **Store and Query Data**:  
   Create a table to store product information (`id`, `name`, `price`, and `image` as BLOB). Insert a few rows and try retrieving them.  
   ```sql
   CREATE TABLE Products (
       id INTEGER PRIMARY KEY,
       name TEXT,
       price REAL,
       image BLOB
   );
   ```

2. **Experiment with Dynamic Typing**:  
   Insert invalid data types into columns (e.g., a string in an `INTEGER` column) and see what happens.  

3. **BLOB Handling**:  
   Using a programming language like Python, write a script to store and retrieve a small image in a SQLite table.

---

### **References**
1. [SQLite Data Types Documentation](https://www.sqlite.org/datatype3.html)  
2. [Storing Binary Data in SQLite](https://www.sqlite.org/faq.html#q19)  
3. *SQLite Database Programming for Beginners* - John Smith, 2020.  
4. [SQLite with Python](https://docs.python.org/3/library/sqlite3.html)  



---

### **Featured Image**  
Let me generate one for you!

Here's the featured image for your speech: two people discussing SQLite data storage in a casual and friendly café setting. Let me know if you'd like to refine it further!