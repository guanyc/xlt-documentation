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

title: "Sqlite3 Commnd Line Basics"
date: "2024-12-15 22:05:40+08:00"
lastmod: "2024-12-15 22:05:40+08:00"
draft: false

keywords: ["sqlite3"]
tags: ["sqlite3"]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

featured_image:

weight: 50
type: docs

---

### **SQLite3 Command-Line Basics**

**James:** Alright, David, I’ve got SQLite installed! Now what? How do I actually use this thing?

**David:** Awesome, James! Let’s start with the SQLite3 command-line interface, or CLI for short. It’s like your direct hotline to the database.

**James:** Hotline, huh? Sounds powerful. How do I open it?

**David:** Just type `sqlite3` in your terminal or command prompt, and hit Enter. If you want to open a specific database, include the file name, like this:
```bash
sqlite3 my_database.db
```

**James:** What if the database file doesn’t exist yet?

**David:** No problem! SQLite will create it for you if it doesn’t exist.

**James:** Oh, that’s nice. So, I can just type `sqlite3 test.db` and it’ll set everything up?

**David:** Exactly. Once you’re in, you’ll see the SQLite prompt—something like this:
```
sqlite>
```
That’s where you enter all your commands.

---

**James:** Cool. What kind of commands can I run?

**David:** Let’s start with the basics. To see a list of tables in your database, use:
```sql
.tables
```
If you want detailed information about a specific table, try:
```sql
.schema table_name
```

**James:** What if I mess up and forget the commands?

**David:** Don’t worry. Just type `.help` and SQLite will show you all the available commands. It’s like a cheat sheet built into the CLI.

**James:** That’s a lifesaver. How do I actually add data, though?

**David:** First, you need a table. Let’s create one. Type this at the SQLite prompt:
```sql
CREATE TABLE budget (id INTEGER PRIMARY KEY, description TEXT, amount REAL);
```

**James:** Wait, so `id` is the primary key, `description` is a text column, and `amount` is for numbers, right?

**David:** Nailed it! After that, you can insert data like this:
```sql
INSERT INTO budget (description, amount) VALUES ('Groceries', 150.75);
```

**James:** Simple enough. How do I check if it worked?

**David:** Use a SELECT query:
```sql
SELECT * FROM budget;
```

**James:** Oh, nice! That shows all the rows in the table, right?

**David:** Exactly. By the way, if you want to exit the CLI, just type `.exit` or `.quit`.

---

**James:** Okay, this is starting to make sense. Anything else I should know?

**David:** A few tips:
1. Use semicolons (`;`) to end SQL commands.
2. For multi-line commands, you can press Enter, and SQLite will wait for the semicolon before executing.
3. And always remember to save your work! Your changes are automatically saved to the database file, but it’s good practice to keep backups.

**James:** Got it! Sounds like I’m ready to give this a shot.

**David:** That’s the spirit! Let me give you a few exercises to practice.

---

### **Main Takeaways:**
1. **Starting SQLite CLI:** Open it with `sqlite3 database_name.db`. SQLite creates the database file if it doesn’t exist.
2. **Basic Commands:**
   - `.tables` to list all tables.
   - `.schema table_name` to see table structure.
   - `.help` for a list of CLI commands.
3. **SQL Basics:**
   - `CREATE TABLE` to define a table.
   - `INSERT INTO` to add data.
   - `SELECT * FROM table_name` to retrieve data.
4. **Exiting the CLI:** Use `.exit` or `.quit`.

---

### **Exercises for James:**
1. **Create a New Table:**
   Create a table called `expenses` with the following columns:
   - `id` (INTEGER PRIMARY KEY)
   - `category` (TEXT)
   - `cost` (REAL)

2. **Insert Data:**
   Add at least three rows of data into the `expenses` table.

3. **Query Data:**
   Use a `SELECT` statement to display all rows in the `expenses` table.

4. **Explore Table Info:**
   Use `.tables` to confirm your table was created and `.schema expenses` to see its structure.

**James:** These exercises sound fun! I’ll try them out and let you know how it goes.

**David:** Perfect! Let me know if you hit any roadblocks—I’ll be here to help.
