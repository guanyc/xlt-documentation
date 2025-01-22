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

title: "Sqlite Triggers in Sqlite"
date: "2025-01-21 12:35:41+08:00"
lastmod: "2025-01-21 12:35:41+08:00"
draft: false

keywords: [sqlite3]
tags: [sqlite3]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

weight: 600
type: docs

featured_image:


---



### **SQLite Triggers: What They Are and How to Use Them**

**James:** Hey David, I was working on this database project, and I came across something called SQLite triggers. Ever heard of them? 

**David:** Yeah, I’ve heard about triggers. They’re like magic buttons in your database. When certain events happen—like inserting, updating, or deleting data—a trigger automatically runs a bit of code. Pretty handy!

**James:** Oh, that sounds cool! What’s the point of using triggers?

**David:** Triggers are great for automating repetitive tasks. For example, you can log changes in a table, enforce complex business rules, or maintain data integrity without having to manually code every time.

**James:** Got it. So how do you create a trigger in SQLite?

---

### **Creating an SQLite Trigger**

**David:** Let me break it down for you. A trigger is created using the `CREATE TRIGGER` statement. Here's the basic syntax:

```sql
CREATE TRIGGER trigger_name 
AFTER INSERT OR UPDATE OR DELETE 
ON table_name 
BEGIN
    -- your SQL statements
END;
```

**James:** Sounds simple enough. Can you show me a real example?

**David:** Sure! Say you have a `sales` table, and you want to keep a log of all updates in a `sales_log` table. Here’s how you’d do it:

```sql
CREATE TABLE sales (
    id INTEGER PRIMARY KEY,
    product TEXT,
    amount INTEGER
);

CREATE TABLE sales_log (
    log_id INTEGER PRIMARY KEY AUTOINCREMENT,
    action TEXT,
    product TEXT,
    amount INTEGER,
    timestamp DATETIME DEFAULT CURRENT_TIMESTAMP
);

CREATE TRIGGER log_sales_update
AFTER UPDATE ON sales
BEGIN
    INSERT INTO sales_log (action, product, amount)
    VALUES ('UPDATE', NEW.product, NEW.amount);
END;
```

**James:** Let me guess—whenever I update the `sales` table, it automatically logs the change in `sales_log`?

**David:** Exactly! The `NEW` keyword refers to the updated row. There’s also `OLD`, which represents the data before the update.

---

### **Pitfalls to Watch Out For**

**James:** This sounds amazing, but are there any catches? 

**David:** Absolutely. Here are some common pitfalls to avoid:  

1. **Recursive Triggers**: If you accidentally create a trigger that modifies the same table it’s attached to, you can end up in an infinite loop.
   - Example: An `AFTER INSERT` trigger that inserts into the same table can trigger itself endlessly.
   - **Fix**: Use flags or temporary tables to break the loop.

2. **Performance Issues**: Triggers add overhead to your database operations, so don’t overuse them in high-traffic tables.

3. **Debugging Difficulty**: If a trigger fails, it can be hard to pinpoint the issue since the code runs in the background.

4. **Limited Functionality in SQLite**: Unlike other databases, SQLite triggers can only execute SQL statements—no custom functions or conditional logic.

**James:** Got it. So, they’re powerful, but I should use them sparingly and carefully.

---

### **Highlights of SQLite Triggers**

**David:** Yep! Let’s summarize the cool parts:  

- **Automation**: Triggers take care of repetitive tasks without extra coding.
- **Data Integrity**: They enforce consistency rules at the database level.
- **Event-Based Execution**: You can run code on `BEFORE` or `AFTER` events for inserts, updates, or deletes.

**James:** That’s solid. I can already think of a few ways to use triggers in my project!

---

### **Exercises to Try**

1. **Exercise 1**: Create a `students` table and a `student_logs` table. Write a trigger to log all deletions from the `students` table.
   
2. **Exercise 2**: Build a trigger that prevents an `employees` table from having duplicate email addresses.

3. **Exercise 3**: Create a trigger to update an `inventory` table’s stock when an item is sold in the `sales` table.


---

### **Keywords**

- SQLite triggers
- `CREATE TRIGGER`
- `AFTER INSERT`
- `BEFORE UPDATE`
- `NEW` and `OLD` keywords
- Data integrity
- Automation in databases
- Trigger pitfalls
- SQL exercises

---

### **References**

1. [SQLite Triggers](https://www.sqlite.org/lang_createtrigger.html)


