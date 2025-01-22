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

title: "Sqlite Create Tables Syntax and Examples"
date: "2024-12-16 22:20:51+08:00"
lastmod: "2024-12-16 22:20:51+08:00"
draft: false

keywords: ["sqlite3"]
tags: ["sqlite3"]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

weight: 130
type: docs

featured_image:

---

### **Creating Tables: Syntax and Examples**

---

**James**: Alright, David, I’ve got my SQLite database set up, but… it’s feeling a little empty. Time to build some tables, right?

**David**: Exactly! A database without tables is like a notebook without pages. Let’s add some structure to your database by creating tables.

**James**: I hope this isn’t too complicated…

**David**: Not at all. SQLite makes it pretty straightforward. Let’s jump in.

---

### **Step 1: The Basic Syntax**

**David**: To create a table, you use the `CREATE TABLE` statement. Here’s the simplest form:

```sql
CREATE TABLE table_name (
    column1 datatype constraints,
    column2 datatype constraints,
    ...
);
```

**James**: Okay, but what are “datatypes” and “constraints”?

**David**: Good question.
- **Datatypes** tell SQLite what kind of data the column will hold, like `TEXT`, `INTEGER`, or `REAL`.
- **Constraints** enforce rules, like making sure a column isn’t empty (`NOT NULL`) or assigning a unique identifier (`PRIMARY KEY`).

---

### **Step 2: Creating Your First Table**

**David**: Let’s say we’re building a table to store user information. Try this:

```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    email TEXT UNIQUE,
    age INTEGER
);
```

**James**: Okay, let me break this down:
- `id`: A unique identifier for each user.
- `name`: The user’s name, and it can’t be blank.
- `email`: A unique email address for each user.
- `age`: Their age as a number.

**David**: Spot on! The `PRIMARY KEY` on `id` ensures each user has a unique ID.

---

### **Step 3: Checking Your Table**

**James**: How do I know if the table was created successfully?

**David**: Just use the `.tables` command in the SQLite CLI. It’ll list all tables in your database.
Want to see the structure of your `users` table? Use this:

```sql
PRAGMA table_info(users);
```

**James**: Ooh, fancy.

---

### **Step 4: Handling Mistakes**

**James**: What if I mess up the table and need to start over?

**David**: No worries. You can delete a table with:

```sql
DROP TABLE users;
```

**James**: And then I can recreate it?

**David**: Exactly. Just be careful—`DROP TABLE` deletes all the data in the table too.

---

### **Step 5: Advanced Table Features**

**James**: What if I want to add extra rules? Like making sure age is always positive?

**David**: You can use `CHECK` constraints. For example:

```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    age INTEGER CHECK (age > 0)
);
```

**James**: Nice! What happens if someone tries to enter a negative age?

**David**: SQLite will reject it. Constraints are like database bodyguards—they enforce your rules.

---

### **Highlights**

1. **Basic Syntax:** Use `CREATE TABLE` to define tables.
2. **Common Column Types:**
   - `TEXT` for text data.
   - `INTEGER` for whole numbers.
   - `REAL` for decimal numbers.
3. **Constraints:**
   - `PRIMARY KEY` ensures unique identifiers.
   - `NOT NULL` enforces mandatory fields.
   - `CHECK` adds custom rules.
4. **Dropping Tables:** Use `DROP TABLE` to delete tables.

---

### **Exercises for James**

1. **Create Your Own Table:**
   - Create a table called `products` with columns for `id`, `name`, `price`, and `stock`.
   - Add constraints: `id` as `PRIMARY KEY`, `name` as `NOT NULL`, and `price` to ensure it’s greater than 0.

2. **Experiment with Constraints:**
   - Try adding a `CHECK` constraint on the `stock` column to ensure it’s always non-negative.

3. **Drop and Recreate:**
   - Drop the `products` table and recreate it with an additional column for `category`.

---

**James**: Okay, I think I’ve got the hang of this. Tables are like the skeleton of the database, right?

**David**: Exactly! Once you have tables, you can start adding data and building relationships between them. But for now, master these basics.

**James**: Got it. Time to put these exercises to work!

---

### **References**

1. **[SQLite CREATE TABLE Documentation](https://sqlite.org/lang_createtable.html)**
   - Official reference for creating tables and defining columns.

2. **[SQLite Data Types](https://sqlite.org/datatype3.html)**
   - Overview of supported data types in SQLite.

3. **[SQLite Constraints](https://sqlite.org/syntax/column-constraint.html)**
   - Details on constraints like `PRIMARY KEY`, `NOT NULL`, and `CHECK`.

4. **[DB Browser for SQLite](https://sqlitebrowser.org/)**
   - A graphical tool for creating and managing tables.

5. **[SQL Style Guide](https://www.sqlstyle.guide/)**
   - Best practices for writing clean and consistent SQL.
