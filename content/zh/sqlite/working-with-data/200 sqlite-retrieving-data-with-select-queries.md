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

title: "Sqlite Retrieving Data With Select Queries"
date: "2024-12-20 11:48:47+08:00"
lastmod: "2024-12-20 11:48:47+08:00"
draft: false

keywords: ["sqlite3"]
tags: ["sqlite3"]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

featured_image:
weight: 200
type: docs


---

### **Retrieving Data with SELECT Queries**

---

**James**: David, now that I know how to insert data, how do I actually get it back out?

**David**: Ah, the magic of the `SELECT` statement! It’s how you retrieve, filter, and analyze your data. Think of it like a “question” you’re asking your database, and it gives you the answer.

**James**: So, it’s like the Google search of databases?

**David**: Exactly, but with precise control over what you get back. Let’s dive into the basics.

---

### **Basic SELECT Syntax**

**David**: The simplest form of a `SELECT` query looks like this:

```sql
SELECT column1, column2 FROM table_name;
```

Here’s an example. Suppose you have a table called `users`:

```sql
CREATE TABLE users (
    user_id INTEGER PRIMARY KEY,
    username TEXT NOT NULL,
    email TEXT
);
INSERT INTO users (user_id, username, email) VALUES
(1, 'james', 'james@example.com'),
(2, 'David', 'David@example.com'),
(3, 'alice', 'alice@example.com');
```

To get all the usernames and emails, you’d write:

```sql
SELECT username, email FROM users;
```

**James**: What if I want everything in the table?

**David**: Use `*` to select all columns:

```sql
SELECT * FROM users;
```

**James**: Easy enough. What’s next?

---

### **Filtering Results with WHERE**

**David**: You can filter results using the `WHERE` clause. For example, if you only want to see James’s info:

```sql
SELECT * FROM users WHERE username = 'james';
```

**James**: What if I want users whose emails end with `example.com`?

**David**: Use the `LIKE` operator with wildcards:

```sql
SELECT * FROM users WHERE email LIKE '%example.com';
```

**James**: Ah, `%` is like “anything goes” before `example.com`!

**David**: Exactly!

---

### **Sorting Results with ORDER BY**

**David**: If you want the results in a specific order, use `ORDER BY`. For example, to sort by username:

```sql
SELECT * FROM users ORDER BY username ASC;
```

**James**: What about descending order?

**David**: Use `DESC`:

```sql
SELECT * FROM users ORDER BY username DESC;
```

---

### **Limiting Results with LIMIT**

**David**: Sometimes you only want a few rows. Use `LIMIT` for that:

```sql
SELECT * FROM users LIMIT 2;
```

**James**: So, it’ll just give me the first two rows?

**David**: Yep. Combine it with `ORDER BY` for even more control.

---

### **Common Pitfalls**

1. **Selecting Too Much Data:**
   - Avoid using `SELECT *` in production. It’s better to select only the columns you need.

2. **Forgetting WHERE Filters:**
   - Running a query like `DELETE FROM users;` without a `WHERE` is dangerous.

3. **Case Sensitivity:**
   - SQLite is case-insensitive for strings by default, but other databases might not be.

4. **Unintended Nulls:**
   - Be careful with `NULL` values. A query like `WHERE email = ''` won’t match rows where `email` is `NULL`.

---

### **Highlights**

1. **SELECT Basics:** Retrieve specific columns or all columns using `*`.
2. **WHERE Filters:** Narrow down results with conditions.
3. **Sorting with ORDER BY:** Control the order of your results using `ASC` or `DESC`.
4. **Limiting Results:** Use `LIMIT` to fetch a subset of rows.
5. **Pitfalls:** Always test queries on small datasets first, and be mindful of `NULL`.

---

### **Exercises for James**

1. **Basic Retrieval:**
   - Create a `books` table with columns `book_id`, `title`, and `author`. Insert five rows and retrieve all data.

2. **Filtering with WHERE:**
   - Query the `books` table for books written by a specific author.

3. **Sorting and Limiting:**
   - Retrieve books sorted by `title` in descending order, but only show the top two.

4. **Advanced Filters:**
   - Find books where the title contains the word “guide” using `LIKE`.

---

### **References**

1. **[SQLite SELECT Documentation](https://sqlite.org/lang_select.html)**
   - Official documentation with detailed examples.

2. **[SQLite Query Syntax](https://sqlite.org/lang.html)**
   - Comprehensive reference for all SQLite query commands.

---

**James**: This is so much better than I expected. The `SELECT` statement feels like a Swiss Army knife!

**David**: That’s a great way to think about it. Practice these exercises, and you’ll be slicing through data in no time!
