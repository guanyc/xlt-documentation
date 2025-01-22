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

title: "Sqlite Insert Using Default Values in Insert Statements"
date: "2024-12-19 22:04:36+08:00"
lastmod: "2024-12-19 22:04:36+08:00"
draft: false

keywords: ["sqlite3"]
tags: ["sqlite3"]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

featured_image:
weight: 180
type: docs

---

### **Using Default Values in Insert Statements**

---

**James**: David, I’ve been learning how to insert data, but I’ve got a question—what happens if I don’t have all the data for a row?

**David**: Great question! That’s where **default values** come in. They save the day when you don’t want to specify a value for every column.

**James**: So, it’s like setting a fallback for empty slots?

**David**: Exactly! Let’s break it down.

---

### **Understanding Default Values**

**David**: When you create a table, you can define default values for specific columns. If you don’t insert a value for that column, SQLite uses the default. Here’s a quick example:

```sql
CREATE TABLE users (
    user_id INTEGER PRIMARY KEY,
    username TEXT NOT NULL,
    email TEXT DEFAULT 'unknown@example.com',
    age INTEGER DEFAULT 18
);
```

**James**: So, in this table, if I don’t provide an `email` or `age`, they’ll get `unknown@example.com` and `18` respectively?

**David**: Bingo! Now let’s try inserting some data.

---

### **Using Default Values in Action**

**David**: Let’s start with a basic `INSERT` statement where you specify all columns:

```sql
INSERT INTO users (user_id, username, email, age)
VALUES (1, 'james', 'james@example.com', 25);
```

**James**: Got it! But what if I skip `email` and `age`?

**David**: The defaults will kick in:

```sql
INSERT INTO users (user_id, username)
VALUES (2, 'David');
```

**James**: So, this means `email` will be `'unknown@example.com'` and `age` will be `18`?

**David**: Exactly! You can also explicitly use the `DEFAULT` keyword if you want to remind yourself:

```sql
INSERT INTO users (user_id, username, email, age)
VALUES (3, 'alice', DEFAULT, DEFAULT);
```

**James**: That’s cool! I can see this being useful for optional fields.

---

### **What Happens Without Defaults?**

**James**: What if I don’t define defaults for columns in the table?

**David**: If the column is `NOT NULL`, SQLite will throw an error. If it’s not `NOT NULL`, SQLite inserts `NULL` instead.

---

### **Updating Default Values**

**James**: Can I change a column’s default after creating the table?

**David**: Unfortunately, SQLite doesn’t allow you to modify a column’s default value directly. You’d need to create a new table with the updated default and migrate the data.

**James**: Got it. That’s good to know before I lock things in.

---

### **Highlights**

1. **Default Values:** Define default values when creating a table to handle missing data gracefully.
2. **Implicit Defaults:** Skip columns during insertion, and SQLite will use their defaults.
3. **Explicit Defaults:** Use the `DEFAULT` keyword in your `INSERT` statement to make default usage clear.
4. **Constraints First:** Ensure columns that need a default value are designed accordingly.
5. **No Retroactive Changes:** Default values can’t be modified for existing columns in SQLite.

---

### **Exercises for James**

1. **Create a Table with Defaults:**
   - Create a `products` table with the following fields:
     - `product_id`: Integer, primary key.
     - `product_name`: Text, cannot be null.
     - `price`: Real, defaults to `0.0`.
     - `in_stock`: Integer, defaults to `1`.

2. **Practice Using Defaults:**
   - Insert a product specifying all columns.
   - Insert a product without specifying `price` and `in_stock`.
   - Insert a product using the `DEFAULT` keyword for `price`.

3. **Experiment with NULL Values:**
   - Insert a row without a default and observe the behavior for a nullable column.

4. **Challenge:**
   - Create a `students` table with `name`, `grade` (default `'A'`), and `attendance` (default `100`). Insert rows and verify the defaults work as expected.

---


**James**: Thanks, David! I’m going to try these exercises and experiment with defaults.

**David**: You’re welcome! Defaults are your safety net—they make your database resilient to missing data. Have fun!

---

### **References**

1. **[SQLite Default Values Documentation](https://sqlite.org/lang_createtable.html#dfltval)**
   - Official documentation on default values for table columns.

2. **[SQLite Data Types](https://www.sqlite.org/datatype3.html)**
   - Understanding SQLite data types and how they interact with defaults.

3. **[DB Browser for SQLite](https://sqlitebrowser.org/)**
   - A tool to visualize tables and test default values.
