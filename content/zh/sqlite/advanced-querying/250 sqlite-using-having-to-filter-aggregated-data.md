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

title: "Sqlite Using Having to Filter Aggregated Data"
date: "2024-12-22 22:40:00+08:00"
lastmod: "2024-12-22 22:40:00+08:00"
draft: false

keywords:
- SQLite HAVING clause tutorial
- Filtering aggregated data in SQLite
- Grouped data filtering examples
- SQLite HAVING vs WHERE
- SQL aggregate filtering techniques
tags: [sqlite3]
categories: [sqlite3]
author: "guanyc"
aliases: []

description: ""
summary:
weight: 250
type: docs



featured_image: /images/sqlite/sqlite-having-filter-aggregate.webp

---

### **Speech: Using HAVING to Filter Aggregated Data**

---

**James:** David, I’m starting to get the hang of `GROUP BY`, but what if I want to filter the grouped data? Like, say I only want to see categories with total sales above a certain amount.

**David:** Great question! That’s where the `HAVING` clause comes into play. It’s like the `WHERE` clause but specifically for filtering aggregated results.

**James:** Wait, why not just use `WHERE`?

**David:** Because `WHERE` filters rows before the grouping happens, while `HAVING` filters the grouped data after aggregation. Let me show you.

---

### **Example 1: Total Sales Above $300**

**David:** Let’s use our trusty `sales` table:

```sql
CREATE TABLE sales (
    id INTEGER PRIMARY KEY,
    category TEXT,
    amount REAL
);

INSERT INTO sales (category, amount) VALUES
('Electronics', 200.50),
('Clothing', 150.00),
('Electronics', 300.00),
('Clothing', 75.00),
('Books', 50.00);
```

Now, if you want to see only the categories where total sales exceed $300:

```sql
SELECT category, SUM(amount) AS total_sales
FROM sales
GROUP BY category
HAVING total_sales > 300;
```

This gives you:
```
category     | total_sales
--------------------------
Electronics  | 500.50
```

**James:** Oh, so the `HAVING` clause acts like a final filter on the aggregated results.

**David:** Exactly! You can use it with any aggregate function, like `COUNT()`, `AVG()`, or `MAX()`.

---

### **Example 2: Categories with More Than 1 Product**

**David:** Now, let’s try it with our `products` table:

```sql
CREATE TABLE products (
    id INTEGER PRIMARY KEY,
    category TEXT,
    name TEXT
);

INSERT INTO products (category, name) VALUES
('Electronics', 'Headphones'),
('Electronics', 'Laptop'),
('Clothing', 'T-Shirt'),
('Clothing', 'Jeans'),
('Books', 'Novel');
```

To find categories with more than one product:

```sql
SELECT category, COUNT(*) AS product_count
FROM products
GROUP BY category
HAVING product_count > 1;
```

Result:
```
category     | product_count
----------------------------
Electronics  | 2
Clothing     | 2
```

---

### **Pitfalls**

**James:** This seems straightforward. Are there any gotchas?

**David:** A few, actually:
1. **Mixing `WHERE` and `HAVING`:** Use `WHERE` for filtering raw rows before grouping and `HAVING` for filtering aggregated results.
   ```sql
   SELECT category, SUM(amount) AS total_sales
   FROM sales
   WHERE amount > 100 -- Filters raw rows
   GROUP BY category
   HAVING total_sales > 300; -- Filters grouped results
   ```
2. **Performance Issues:** The `HAVING` clause can be slow if the aggregation involves large datasets, so optimize your queries when possible.

**James:** Got it. `WHERE` first, `HAVING` after grouping!

---

### **Highlights**
- Use `WHERE` to filter raw rows and `HAVING` to filter aggregated data.
- Combine `WHERE` and `HAVING` for more precise filtering.
- Be cautious of performance when working with large datasets and complex `HAVING` conditions.

---

### **Exercises**

1. Modify the `sales` table to include a `region` column. Write a query to find regions where total sales for the "Electronics" category exceed $400.
2. Use the `products` table to find categories with product names longer than 5 characters and at least 2 products.
3. Try combining multiple conditions in `HAVING`, like filtering by both `SUM()` and `COUNT()` in the same query.

---

### **References**

1. [SQLite HAVING Documentation](https://www.sqlite.org/lang_select.html#having)
2. [SQL Aggregate Functions Tutorial](https://www.w3schools.com/sql/sql_having.asp)
3. [Advanced SQL Queries with HAVING](https://www.sqltutorial.org/sql-having/)
