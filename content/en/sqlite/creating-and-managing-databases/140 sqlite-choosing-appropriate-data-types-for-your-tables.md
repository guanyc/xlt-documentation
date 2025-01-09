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

title: "Sqlite Choosing Appropriate Data Types for Your Tables"
date: "2024-12-19 19:51:46+08:00"
lastmod: "2024-12-19 19:51:46+08:00"
draft: false

keywords: ["sqlite3"]
tags: ["sqlite3"]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

weight: 140
type: docs


featured_image:

---

### **Choosing Appropriate Data Types for Your Tables**

---

**James**: Hey XiaoMing, I just created my first table, but I’m still not 100% sure about which data types to use. Like, when should I use `TEXT` versus `VARCHAR` or `INTEGER`?

**XiaoMing**: Great question, James. Picking the right data type is like choosing the right container for food—you don’t want to store soup in a basket, right?

**James**: Makes sense. So, how do I make the right choices?

**XiaoMing**: Let’s dive in!

---

### **Step 1: The Basics of SQLite Data Types**

**XiaoMing**: SQLite is a bit different from other databases. It uses a system called **dynamic typing**, meaning the type of data in a column doesn’t have to match its declared type perfectly. But for sanity and performance, you should still choose carefully.

**James**: Okay, what are the main types?

**XiaoMing**: SQLite has five main storage classes:
1. **NULL:** Represents missing or unknown values.
2. **INTEGER:** For whole numbers.
3. **REAL:** For floating-point numbers (decimals).
4. **TEXT:** For text strings.
5. **BLOB:** For binary data, like images or files.

---

### **Step 2: Choosing the Right Type for Your Data**

**XiaoMing**: Let’s go through some common scenarios:

1. **For IDs or counts:** Use `INTEGER`. It’s efficient and straightforward.
   - Example: `id INTEGER PRIMARY KEY`

2. **For names or descriptions:** Use `TEXT`. It’s perfect for strings of any length.
   - Example: `name TEXT NOT NULL`

3. **For prices or measurements:** Use `REAL`. It handles decimals better than `INTEGER`.
   - Example: `price REAL CHECK(price >= 0)`

4. **For dates or times:** SQLite doesn’t have a dedicated date type, so use `TEXT` or `INTEGER`.
   - Example: Store dates as `YYYY-MM-DD` in `TEXT` or as Unix timestamps in `INTEGER`.

5. **For files or images:** Use `BLOB`. It’s designed for binary data.
   - Example: `profile_picture BLOB`

---

### **Step 3: Why Constraints Matter**

**James**: What if I need to ensure a column always has data?

**XiaoMing**: That’s where constraints like `NOT NULL` come in. They add extra rules to your data. For instance:

```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    email TEXT UNIQUE,
    age INTEGER CHECK (age > 0)
);
```

**James**: So I can mix data types and constraints to enforce good data practices?

**XiaoMing**: Exactly. It’s like setting up guardrails for your database.

---

### **Step 4: Common Mistakes to Avoid**

**XiaoMing**: Here are some pitfalls to watch out for:
- **Overusing `TEXT`:** Don’t use `TEXT` for numbers just because it’s easy.
- **Ignoring `NULL`:** Decide if a column can be empty or not.
- **Forgetting constraints:** Constraints like `CHECK` and `NOT NULL` help maintain data integrity.

**James**: Got it. Always pick the type that best matches the data.

---

### **Highlights**

1. **Data Types in SQLite:**
   - `INTEGER`: Whole numbers.
   - `REAL`: Decimal numbers.
   - `TEXT`: Strings or dates.
   - `BLOB`: Binary data like files.
   - `NULL`: Missing values.

2. **Choosing Types:**
   - Use `INTEGER` for IDs and counters.
   - Use `REAL` for decimals like prices.
   - Use `TEXT` for strings and dates.

3. **Best Practices:**
   - Match the data type to the column’s purpose.
   - Use constraints like `NOT NULL` and `CHECK` to enforce rules.

---

### **Exercises for James**

1. **Create a Table with Mixed Types:**
   - Create a `products` table with:
     - `id` as `INTEGER PRIMARY KEY`.
     - `name` as `TEXT NOT NULL`.
     - `price` as `REAL CHECK(price >= 0)`.
     - `created_at` as a `TEXT` column for dates.

2. **Experiment with Constraints:**
   - Add a `CHECK` constraint to ensure the `price` is greater than zero.

3. **Store Dates Differently:**
   - Try storing the same date as `TEXT` (`YYYY-MM-DD`) and as an `INTEGER` (Unix timestamp). Query both formats to see how they behave.

---

**James**: This actually makes sense now. I like the idea of picking the right “container” for my data.

**XiaoMing**: Good! When you use the right types and constraints, your database becomes more efficient and reliable.

**James**: Time to try these exercises. I’m feeling pretty confident about this.

---

### **References**

1. **[SQLite Data Types Documentation](https://sqlite.org/datatype3.html)**
   - Official guide to SQLite’s data types and their behavior.

2. **[SQL Create Table Constraints](/post/sqlite3/sqlite-sql-create-table-constraints/)**
   - Sql create tabke constraints speeches between XiaoMing and james

3. **[Date and Time in SQLite](https://sqlite.org/lang_datefunc.html)**
   - Learn how to handle dates and times in SQLite.

4. **[SQLite3 Cheat Sheet](https://www.sqlite.org/quickstart.html)**
   - Quick reference for common SQLite commands and concepts.
