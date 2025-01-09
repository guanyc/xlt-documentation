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

title: "Sqlite Combining Results With Union and Intersect"
date: "2024-12-22 20:01:21+08:00"
lastmod: "2024-12-22 20:01:21+08:00"
draft: false

keywords:
- SQLite UNION and INTERSECT tutorial
- Combining query results in SQLite
- UNION vs UNION ALL in SQLite
- Examples of INTERSECT in SQL
- Common pitfalls in SQL set operators
tags: [sqlite3]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

featured_image: "/images/sqlite/sqlite-union-and-intersect.jpg"

weight: 260
type: docs

---

### **Speech: Combining Results with UNION and INTERSECT**

---

**James:** XiaoMing, I keep hearing about combining results from multiple queries with things like `UNION` and `INTERSECT`. But honestly, it sounds kind of intimidating.

**XiaoMing:** Ah, don’t worry, James. These are just tools for merging query results in different ways. Let me break it down for you.

---

### **Understanding UNION**

**XiaoMing:** Let’s start with `UNION`. It’s used when you want to combine results from two queries into a single result set, removing duplicates by default.

**James:** Sounds like a way to “stack” data, right?

**XiaoMing:** Exactly! Here’s an example.

**Example 1: Combining Employees from Two Departments**

```sql
CREATE TABLE department1 (
    id INTEGER,
    name TEXT
);

CREATE TABLE department2 (
    id INTEGER,
    name TEXT
);

INSERT INTO department1 VALUES (1, 'Alice'), (2, 'Bob');
INSERT INTO department2 VALUES (2, 'Bob'), (3, 'Charlie');

SELECT name FROM department1
UNION
SELECT name FROM department2;
```

**Result:**
```
name
------
Alice
Bob
Charlie
```

**James:** So it combines the lists, but without duplicates?

**XiaoMing:** Right! If you want duplicates included, use `UNION ALL`.

---

### **Understanding INTERSECT**

**XiaoMing:** Now, let’s talk about `INTERSECT`. It finds the common rows between two queries.

**James:** Like finding overlapping areas in a Venn diagram?

**XiaoMing:** Exactly! Here’s an example.

**Example 2: Common Employees Between Departments**

```sql
SELECT name FROM department1
INTERSECT
SELECT name FROM department2;
```

**Result:**
```
name
------
Bob
```

**James:** Ah, so Bob is in both departments!

**XiaoMing:** You’ve got it.

---

### **Pitfalls**

**James:** This all seems pretty straightforward. Are there any gotchas?

**XiaoMing:** A few:
1. **Column Order Matters:** The queries combined by `UNION` or `INTERSECT` must have the same number of columns and compatible data types.
2. **Performance:** These operations can be slow on large datasets since they may require sorting and comparisons.
3. **Duplicates in `UNION`:** Always specify `UNION ALL` if duplicates are okay, as removing them takes extra processing.

---

### **Highlights**

- `UNION`: Combines results, removes duplicates by default.
- `UNION ALL`: Combines results, keeps duplicates.
- `INTERSECT`: Returns only the common rows between queries.
- Use column order and data types carefully to avoid errors.

---

### **Exercises**

1. Create two tables: `city_europe` and `city_asia`. Use `UNION` to combine all unique city names from both tables.
2. Modify the first exercise to use `UNION ALL`. Observe the difference.
3. Write a query using `INTERSECT` to find cities present in both `city_europe` and `city_asia`.

---

### **References**

1. [SQLite UNION Documentation](https://www.sqlite.org/lang_select.html#union)
2. [SQLite INTERSECT Documentation](https://www.sqlite.org/lang_select.html#intersect)
3. [SQL Set Operators Tutorial](https://www.sqltutorial.org/sql-union-intersect-except/)
