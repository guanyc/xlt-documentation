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

title: "Sqlite Alter Table Adding Column and Removing Column"
date: "2024-12-19 20:33:31+08:00"
lastmod: "2024-12-19 20:33:31+08:00"
draft: false

keywords: ["sqlite3"]
tags: ["sqlite3"]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

featured_image:
weight: 160
type: docs


---


## **Altering Tables: Adding and Removing Columns**


**James**: David, I made a mistake in my database design again. I forgot to add a column to one of my tables. Is it too late to fix?

**David**: No worries, James! Adding and even removing columns is a breeze in SQLite. Let me show you how to alter tables.

---

### **Adding a Column**

**David**: First, let’s talk about adding a column. Say you have a `users` table:

```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    username TEXT NOT NULL
);
```

And now you realize you need an `email` column. You can add it like this:

```sql
ALTER TABLE users ADD COLUMN email TEXT;
```

**James**: Wait, just like that? No need to rewrite the whole table?

**David**: Exactly! However, the new column will be `NULL` for all existing rows unless you assign a `DEFAULT` value.

---

### **Adding a Column with a Default Value**

**James**: What if I want all new users to have a default email, like "unknown@example.com"?

**David**: You can do that too.

```sql
ALTER TABLE users
ADD COLUMN email TEXT DEFAULT 'unknown@example.com';
```

Now any new rows will automatically get that value unless specified otherwise.

---

### **Removing a Column(Drop Column)**

**James**: Okay, but what if I added a column I don’t need anymore? Can I remove it?

**David**: Yes, you can use Drop Column to remove a column.

**James**: So, what do I do?

**David**: Here’s an example, suppose you want to delete the email Column added above.

```sql
ALTER TABLE users
DROP Column email
```

---
### **Renaming a Column**

**James**: and what if I made a typo, how can I modify the wrong column name?

**David**: just use Alter Table RENAME COLUMN to rename a column.
suppose you want to change the email column to e-mail:

```sql
ALTER TABLE users
RENAME Column "email" to e-mail
```
**David**: but this is only valid with SQLite version 3.25.0 or later,
if unluckily,  you met older versions of sqlite , to rename a column could be done in the folllowing buggy way:

Step 1: Create a new table with desired column name:

```sql
CREATE TABLE users_new(
    id INTEGER PRIMARY KEY,
    username TEXT NOT NULL
    e-mail TEXT
);
```

Step 2: Copy Data :

```sql
```sql
INSERT INTO users_new(username, e-mail)
SELECT username, email FROM users;
``````
Note: The above command should be all one line.

Step 3: Drop the old table:

```sql
DROP TABLE users;
```

Step 4: rename the new talbe to the old using:

```sql
ALTER TABLE users_new RENAME TO users;
```

---

### **Highlights**

1. **Adding Columns:**
   - Use `ALTER TABLE ... ADD COLUMN` to add a new column to a table.
   - You can specify a `DEFAULT` value for the new column.

2. **Direct Column Removal:**
   - SQLite support removing columns directly now
   - The old buggy way: create a new table, copy the data, and rename it.

3. **Plan Your Schema:**
   - Avoid frequent structural changes by planning your database schema carefully upfront.

---

### **Exercises for James**

1. **Add a Column:**
   - Start with a `products` table:
     ```sql
     CREATE TABLE products (
         id INTEGER PRIMARY KEY,
         product_name TEXT NOT NULL
     );
     ```
   - Add a `price` column with a default value of `0.0`.

2. **Remove a Column:**
   - Modify the `products` table by removing the `price` column. Use the process of creating a new table, copying data, and renaming.

3. **Rename a Table:**
   - Rename the `products` table to `items`.
---

**James**: Got it. I’ll try out these exercises. Renaming and restructuring tables doesn’t sound too bad now!

**David**: You’re getting the hang of it, James. Keep going—you’re building great database skills!

---

### **References**

1. **[SQLite ALTER TABLE Documentation](https://www.sqlite.org/lang_altertable.html)**
   - Official guide for altering tables in SQLite.

2. **[SQLite Table Redesign](https://www.sqlite.org/lang_altertable.html#otheralter)**
   - Learn more about the workaround for removing columns.

3. **[Backup and Restore in SQLite](https://www.sqlite.org/backup.html)**
   - Ensure data safety before making significant changes.

4. **[DB Browser for SQLite(DB4S)](https://sqlitebrowser.org/)**
   - This graphics took allows you to alter table in a user friendly way
