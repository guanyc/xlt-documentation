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

title: "Sqlite Insert Into Table Basic Syntax"
date: "2024-12-19 21:38:32+08:00"
lastmod: "2024-12-19 21:38:32+08:00"
draft: false

keywords: ["sqlite3"]
tags: ["sqlite3"]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

featured_image:
weight: 170
type: docs
---

### **Inserting Data into Tables: Basic Syntax**

---

**James**: XiaoMing, I’ve created my first table! Now, how do I actually put data into it?

**XiaoMing**: Ah, the fun part—`INSERT` statements! Let’s walk through the basics and build up with examples.

---

### **The Basic Syntax**

**XiaoMing**: The simplest way to add data to a table is using the `INSERT INTO` statement. Here's the general syntax:

```sql
INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);
```

**James**: Makes sense. Let’s say I have a table like this:

```sql
CREATE TABLE users (
    user_id INTEGER PRIMARY KEY,
    username TEXT NOT NULL,
    email TEXT
);
```

How would I insert a user?

**XiaoMing**: Simple! Just provide values for the columns:

```sql
INSERT INTO users (user_id, username, email) VALUES (1, 'james', 'james@example.com');
```

**James**: What happens if I skip the `email` column?

**XiaoMing**: SQLite will insert `NULL` for any column you don’t specify unless it has a `DEFAULT` value or is `NOT NULL`.

```sql
INSERT INTO users (user_id, username) VALUES (2, 'xiaoming');
```

---

### **Inserting Multiple Rows**

**James**: Can I insert multiple rows at once?

**XiaoMing**: Absolutely! It’s more efficient, especially for large datasets:

```sql
INSERT INTO users (user_id, username, email) VALUES
(3, 'alice', 'alice@example.com'),
(4, 'bob', 'bob@example.com'),
(5, 'eve', NULL);
```

**James**: Nice! That saves a lot of typing.

---

### **Skipping Column Names**

**James**: What if I just want to insert all the columns in order?

**XiaoMing**: You can skip the column names, but be careful—the order of values must exactly match the table structure:

```sql
INSERT INTO users VALUES (6, 'charlie', 'charlie@example.com');
```

**James**: What happens if I mix up the order?

**XiaoMing**: Chaos! SQLite will assign values to the wrong columns, leading to unpredictable results.

---

### **Using Default Values**

**James**: What if my table has default values?

**XiaoMing**: You can let SQLite use them by omitting the column or inserting `DEFAULT`. For example, if your table is:

```sql
CREATE TABLE inventory (
    item_id INTEGER PRIMARY KEY,
    item_name TEXT NOT NULL,
    stock INTEGER DEFAULT 10
);
```

You can do this:

```sql
INSERT INTO inventory (item_id, item_name) VALUES (1, 'Notebook');
```

Or this:

```sql
INSERT INTO inventory (item_id, item_name, stock) VALUES (2, 'Pen', DEFAULT);
```

---
### **Inserting Data Only in Specified Columns**
James: Okay, so I can insert data into just the columns I want, right?

XiaoMing: Exactly! But let me show you an explicit example to clarify. Let’s say you want to insert only the username and let user_id auto-increment:

```sql
CREATE TABLE users (
    user_id INTEGER PRIMARY KEY AUTOINCREMENT,
    username TEXT NOT NULL,
    email TEXT
);
```

Here’s how you insert data into just the username column:

```sql
sql
INSERT INTO users (username) VALUES ('alice');

```
James: Cool! So user_id will auto-increment, and email will be NULL, right?

XiaoMing: Exactly. This is very useful when you want the database to handle default or auto-generated values.

---

### **Common Pitfalls**

1. **Violating Constraints:** Inserting duplicate values into `UNIQUE` columns or omitting values for `NOT NULL` columns will throw an error.
2. **Incorrect Data Types:** If you try to insert text into an `INTEGER` column, SQLite might throw an error or silently cast the value.
3. **Column Mismatch:** Not specifying all `NOT NULL` columns will result in an error unless defaults are set.

---

### **Highlights**

1. **Basic Syntax:** Use `INSERT INTO` with column names and `VALUES` to add data.
2. **Insert Multiple Rows:** Add several rows in one `INSERT` statement for efficiency.
3. **Use Defaults:** Omit columns or use `DEFAULT` to insert default values.
4. **Column Order Matters:** Always match the value order with the table definition if skipping column names.

---

### **Exercises for James**

1. **Practice Basic Inserts:**
   - Create a `books` table:
     ```sql
     CREATE TABLE books (
         book_id INTEGER PRIMARY KEY,
         title TEXT NOT NULL,
         author TEXT,
         price REAL DEFAULT 9.99
     );
     ```
   - Insert a book with all columns specified.
   - Insert a book without specifying the `price`.

2. **Insert Multiple Rows:**
   - Add three books to the `books` table in a single `INSERT` statement.

3. **Experiment with Constraints:**
   - Try to insert a row without a `title` and observe the error.

4. **Use Default Values:**
   - Insert a row using the `DEFAULT` keyword for `price`.

---

### **References**

1. **[SQLite INSERT Statement Documentation](https://sqlite.org/lang_insert.html)**
   - Official SQLite documentation for `INSERT`.

2. **[SQLite Data Types](https://www.sqlite.org/datatype3.html)**
   - Reference for understanding how SQLite handles data types.

3. **[DB Browser for SQLite](https://sqlitebrowser.org/)**
   - A GUI tool to practice and visualize inserts.

---

**James**: Thanks, XiaoMing! I’m going to try these exercises and see if I can populate my tables without breaking anything.

**XiaoMing**: That’s the spirit! Remember, constraints are your guardrails. Happy inserting!
