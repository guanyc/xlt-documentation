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

title: "Sqlite Preventing Errors in Data Modification in Sqlite3"
date: "2024-12-28 20:33:09+08:00"
lastmod: "2024-12-28 20:33:09+08:00"
draft: false

keywords: [SQLite3, data modification, transactions, backups, avoiding errors, SQLite pitfalls, safe queries]
tags: [sqlite3]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

weight: 330
type: docs

featured_image: /images/sqlite/sqlite-preventing-errors.jpg


---

**A Casual Chat Between David and James**  

---

**David:** James, I was playing around with SQLite3 for my project, and I accidentally deleted the wrong data! Can you teach me how to avoid such disasters?  

**James:** Haha, David, welcome to the club. But don’t worry, let’s chat about some best practices to keep your SQLite data safe and sound.  

---

### **Highlight 1: The Power of `BEGIN TRANSACTION`**  
**James:** Always use transactions when making changes. It’s like a safety net.  

**David:** Transactions? You mean like this?  

```sql
BEGIN TRANSACTION;
UPDATE students SET grade = 'A' WHERE student_id = 101;
COMMIT;
```

**James:** Exactly! If you mess up, you can just roll back:  

```sql
ROLLBACK;
```

**David:** That’s so cool! It’s like an undo button.  

---

### **Pitfall 1: Forgetting a `WHERE` Clause**  
**James:** Here’s a classic mistake:  

```sql
DELETE FROM students;
```

**David:** No way! That wipes out the whole table?  

**James:** Yep. Always add a `WHERE` clause:  

```sql
DELETE FROM students WHERE student_id = 101;
```

**David:** Got it—never delete blindly.  

---

### **Highlight 2: Backup Your Database**  
**James:** Before any big change, make a backup. SQLite makes this easy:  

```bash
sqlite3 mydatabase.db ".backup backup.db"
```

**David:** That’s super handy! So, if I mess up, I can just restore it.  

---

### **Pitfall 2: Misusing `UPDATE`**  
**James:** Updates can go wrong too. Imagine you run this:  

```sql
UPDATE students SET grade = 'B';
```

**David:** Ouch, that changes everyone’s grade!  

**James:** Exactly. Use a specific `WHERE` clause:  

```sql
UPDATE students SET grade = 'B' WHERE student_id = 102;
```

---

### **Highlight 3: Check Before You Commit**  
**James:** Always test your query with `SELECT` first.  

```sql
SELECT * FROM students WHERE student_id = 102;
```

**David:** So I know exactly what’s getting updated or deleted.  

---

### **Exercise Time!**  
1. **Scenario:**  
   You need to update a teacher’s subject in the `teachers` table. Practice these steps:  
   - Use `SELECT` to verify the data.  
   - Use `BEGIN TRANSACTION` and write an `UPDATE` query.  
   - Commit the changes safely.  

2. **Fix the Error:**  
   James accidentally ran this:  
   ```sql
   UPDATE books SET price = price * 2;
   ```
   Revert the prices back to their original values.  

---

### **References for Further Reading**  
- [SQLite Transactions - Official Documentation](https://sqlite.org/lang_transaction.html)  
- [SQLite Backup and Restore](https://sqlite.org/backup.html)  

