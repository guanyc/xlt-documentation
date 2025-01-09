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

title: "Sqlite3 Data Storage How It Works Internally"
date: "2024-12-15 22:15:40+08:00"
date: "2024-12-15 22:15:40+08:00"
draft: false

keywords: ["sqlite3"]
tags: ["sqlite3"]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

featured_image:

weight: 70
type: docs

---

### **SQLite3 Data Storage: How It Works Internally**

**James:** Hey XiaoMing, I’ve been playing around with SQLite, and it’s great so far. But I’m curious—how does it actually store data? Like, what’s happening under the hood?

**XiaoMing:** Oh, now you’re asking the deep questions, James! Okay, imagine your SQLite database file as a neat little storage box. Inside, everything is packed into a specific structure that makes it easy and fast to find and update data.

**James:** A storage box? What’s in the compartments?

**XiaoMing:** Great question! Think of the database file as being divided into **pages**—these are like little compartments. Each page is a fixed size, usually 4KB, and they hold different types of data, like tables, indexes, and more.

**James:** So, each page has its own role?

**XiaoMing:** Exactly. Pages can be:
1. **Table B-Trees:** Store your actual data in rows.
2. **Index B-Trees:** Help SQLite quickly look up data.
3. **Free Pages:** Empty space waiting to be filled.
4. **Overflow Pages:** When a table or index grows too big for a single page.

**James:** Overflow pages sound like when my desk gets too cluttered, and I have to pile stuff on the floor!

**XiaoMing:** (Laughs) Kind of like that, yeah. But SQLite is super organized about it. It uses a structure called a **B-Tree** to keep track of everything.

---

**James:** B-Trees, huh? Sounds like something out of a math class.

**XiaoMing:** It’s not as scary as it sounds. A B-Tree is just a way to organize data hierarchically so SQLite can find things fast. Imagine a family tree where each person has a fixed number of children—kind of like that.

**James:** Okay, so SQLite isn’t just throwing data randomly into the file.

**XiaoMing:** Not at all! Every time you insert, update, or delete data, SQLite carefully updates the right pages and keeps the B-Tree balanced. That’s why it’s fast and efficient, even with big datasets.

**James:** And this all happens in that one `.db` file?

**XiaoMing:** Yep! That one file is like a self-contained universe for your database. It stores your data, schema, indexes, and even keeps track of free space.

**James:** That’s impressive. What about when I make a mistake or if the power goes out?

**XiaoMing:** Great point! SQLite uses a **write-ahead log** (WAL) to ensure your data stays safe. Before making changes to the database, it writes the changes to a separate file first. If something goes wrong, SQLite can recover using that log.

**James:** That’s like a safety net. I love it.

---

**James:** So, how can I see this in action?

**XiaoMing:** Here’s an exercise for you. You’ll need a little script for this, but it’s a great way to explore:

### **Exercises:**

1. **Create a New Database and Table:**
   - Create a table called `library` with columns: `id` (INTEGER PRIMARY KEY), `title` (TEXT), and `author` (TEXT).
   - Insert a few rows of book data into it.

2. **Explore the File Size:**
   - Check the size of your `.db` file before and after inserting data.
   - Use `.dump` in the SQLite CLI to see the raw SQL that represents your database.

3. **Experiment with WAL Mode:**
   - Enable WAL mode with this command:
     ```sql
     PRAGMA journal_mode = WAL;
     ```
   - Make some changes to your database, then observe the new `.db-wal` file created alongside your database file.

4. **Inspect Free Space:**
   - Delete a few rows from your table.
   - Use the `VACUUM` command to clean up the database and observe how it affects the file size.

---

**James:** This is awesome, XiaoMing! I’ll give these a try and report back.

**XiaoMing:** Sounds good. Understanding SQLite’s storage mechanics isn’t just cool—it’ll help you design better databases. Go ahead and poke around. You’ll learn a ton!

---

### **Main Takeaways:**
1. SQLite stores data in **pages** within a single `.db` file, each with a specific role (e.g., storing table data, indexes, or free space).
2. Data is organized using **B-Trees**, which balance speed and efficiency for inserts, updates, and lookups.
3. The **write-ahead log (WAL)** ensures data integrity during crashes or power failures.
4. Commands like `.dump`, `PRAGMA journal_mode`, and `VACUUM` let you peek into how SQLite handles and optimizes storage.


### **References**

1. **[SQLite File Format](https://sqlite.org/fileformat.html)**
   - This document provides a detailed explanation of SQLite's database file format, including pages, B-Trees, and the role of each component.

2. **[Overview of SQLite B-Tree Structures](https://sqlite.org/btree.html)**
   - Understand how SQLite organizes data within B-Trees and why they are crucial for efficient data retrieval.

3. **[Write-Ahead Logging (WAL)](https://sqlite.org/wal.html)**
   - A comprehensive overview of how the WAL mechanism ensures data integrity and improves performance during transactions.

4. **[VACUUM Command](https://sqlite.org/lang_vacuum.html)**
   - Explains how the `VACUUM` command works to clean up unused space in the database and optimize file size.

5. **[SQLite’s Page Cache](https://sqlite.org/malloc.html)**
   - Discusses how SQLite uses a page cache to manage memory and improve read/write performance.

6. **[SQLite Journal Modes](https://sqlite.org/pragma.html#pragma_journal_mode)**
   - Provides information about the different journal modes, including WAL and DELETE, and their impact on data storage.

7. **SQLite Source Code – Pager Module:**
   - For a deep dive into how SQLite reads and writes data at the file level, look at the **Pager** source code in the [SQLite Repository](https://sqlite.org/src).

8. **"Using SQLite" by Jay A. Kreibich:**
   - Chapter on "File and Storage Details" offers an accessible yet thorough explanation of how SQLite handles data internally.

9. **[SQLite Forum](https://sqlite.org/forum/):**
   - A place to ask specific questions or find detailed discussions on how SQLite stores and manages data.

10. **[SQLite BLOB Internals](https://sqlite.org/intern-v-extern-blob.html):**
    - Learn how large binary objects (BLOBs) are stored internally and the distinction between inline and external storage.
