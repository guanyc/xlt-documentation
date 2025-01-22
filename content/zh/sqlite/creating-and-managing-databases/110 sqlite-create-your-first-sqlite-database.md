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

title: "Sqlite Create Your First Sqlite Database"
date: "2024-12-16 21:48:32+08:00"
lastmod: "2024-12-16 21:48:32+08:00"
draft: false

keywords: [sqlite3]
tags: [sqlite3]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

featured_image:

weight: 110
type: docs

---

### **Creating Your First SQLite Database**

---

**James**: Hey David, I’m ready to dive into SQLite. Where do we start?

**David**: Alright, let’s keep it simple. Step one is creating your first SQLite database. It’s as easy as boiling water—though hopefully, you don’t burn anything while doing this.

**James**: *[Laughs]* No promises. Okay, how do I create this database?

---

### **Step 1: Using the Command Line**

**David**: The easiest way is through the SQLite command-line interface (CLI). Open your terminal or command prompt and type:

```bash
sqlite3 my_first_database.db
```

**James**: Wait, that’s it?

**David**: That’s it. Once you hit Enter, SQLite creates a file called `my_first_database.db` in your current directory.

**James**: Okay, what if I’m on Windows and get confused about the path?

**David**: No problem! Just navigate to the folder where you want the database using `cd`, then run the command.

**James**: Cool, and if I want to check if the file exists?

**David**: Use your file explorer to find it, or type:

```bash
ls   # On Linux/Mac
dir  # On Windows
```

---

### **Step 2: Adding Some Tables**

**James**: Alright, I’ve got the database. Now what?

**David**: Let’s add a table to store data. First, ensure you’re inside the SQLite CLI (you should see `sqlite>` in your terminal). Now type:

```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    age INTEGER
);
```

**James**: What’s happening here?

**David**: You’re creating a table called `users` with three columns:
1. `id`: A unique identifier for each user.
2. `name`: A text column for storing names, and it can’t be empty (`NOT NULL`).
3. `age`: A number for storing the user’s age.

**James**: Gotcha. And how do I check if the table was actually created?

**David**: Use this command:

```sql
.tables
```

This will list all the tables in your database.

---

### **Step 3: Inserting Data**

**James**: Tables are great, but empty tables are boring. How do I add some data?

**David**: Try this:

```sql
INSERT INTO users (name, age) VALUES ('Alice', 25);
INSERT INTO users (name, age) VALUES ('Bob', 30);
```

**James**: And if I want to check the data?

**David**: Use a `SELECT` query:

```sql
SELECT * FROM users;
```

This will show all rows in the `users` table.

**James**: Oh, this is starting to feel like I’m actually doing something useful!

---

### **Step 4: Saving Your Work**

**James**: So... how does saving work? Is it automatic?

**David**: Kind of. SQLite saves changes automatically unless you’re in a transaction. Just to be safe, though, use this command before exiting:

```sql
.exit
```

**James**: Got it. And what if I accidentally delete my database?

**David**: *[Grinning]* Always back it up! You can copy the `.db` file manually or use the `.backup` command.

---

### **Highlights**

1. **Creating a Database:**
   - Use `sqlite3 my_first_database.db` to create a new SQLite database.
2. **Creating a Table:**
   - Use the `CREATE TABLE` command to define table structures.
3. **Inserting Data:**
   - Use `INSERT INTO` to populate tables with data.
4. **Querying Data:**
   - Use `SELECT *` to retrieve all rows from a table.
5. **File Management:**
   - The `.db` file stores everything, so back it up if needed.

---

### **Exercises for James**

1. **Create Your Own Database:**
   - Create a database called `test_app.db`.
   - Add a table named `products` with columns for `id`, `name`, and `price`.

2. **Add Some Products:**
   - Insert at least three products into your `products` table.

3. **Query Your Data:**
   - Use a `SELECT` query to retrieve all the products you’ve added.

---

**James**: This feels really powerful but simple enough for a beginner like me.

**David**: That’s the magic of SQLite. Small steps like this will eventually lead you to master full-fledged database management. Now get on with those exercises!

**James**: Will do! Thanks, David.

---

### **References**

1. **[SQLite Official Documentation: CLI](https://sqlite.org/cli.html)**
   - Covers the command-line interface in detail.

2. **[SQLite CREATE TABLE Syntax](https://sqlite.org/lang_createtable.html)**
   - Explains the syntax for creating tables and defining columns.

3. **[SQLite Data Types](https://sqlite.org/datatype3.html)**
   - Useful for understanding SQLite’s column types.

4. **[Stack Overflow Questions About SQLite](https://stackoverflow.com/questions/tagged/sqlite)**
   - A great place to troubleshoot common issues.
