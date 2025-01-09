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

title: "Sqlite Grouping and Aggregating Data With Group By"
date: "2024-12-22 12:34:38+08:00"
lastmod: "2024-12-22 12:34:38+08:00"
draft: false

keywords:
- SQLite GROUP BY tutorial
- Aggregating data in SQLite
- SQLite aggregate functions
- Grouping data with SQL
- SQLite GROUP BY examples
tags: [sqlite3]
categories: [tech]
author: "guanyc"
aliases: []


description: ""
summary:

weight: 240
type: docs

featured_image: /images/sqlite/sqlite group by.png


---

### **Speech: Grouping and Aggregating Data with GROUP BY**

---

**James:** XiaoMing, I’ve been working with `SELECT` queries, but now I need to analyze grouped data. What’s this `GROUP BY` thing I keep hearing about?

**XiaoMing:** `GROUP BY` is your best friend when you want to group rows that have the same values in specific columns and then perform aggregate calculations, like sums or averages, on those groups.

**James:** Sounds handy! Can we jump into an example?

---

### **Example 1: Total Sales per Category**
**XiaoMing:** Let’s say you have a `sales` table:

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

Now, if you want to know the total sales for each category, you can use `GROUP BY`:

```sql
SELECT category, SUM(amount) AS total_sales
FROM sales
GROUP BY category;
```

The result is:
```
category     | total_sales
--------------------------
Electronics  | 500.50
Clothing     | 225.00
Books        | 50.00
```

**James:** So, `GROUP BY` organizes the data into groups, and `SUM()` calculates the total for each group?

**XiaoMing:** Exactly! You can also use other aggregate functions like `AVG()`, `COUNT()`, `MAX()`, or `MIN()`.

---

### **Example 2: Counting Products per Category**
**XiaoMing:** Here’s another one. Let’s add a `products` table:

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

If you want to count how many products are in each category:

```sql
SELECT category, COUNT(*) AS product_count
FROM products
GROUP BY category;
```

The result:
```
category     | product_count
----------------------------
Electronics  | 2
Clothing     | 2
Books        | 1
```

**James:** This is cool! But what happens if I forget to include all non-aggregated columns in the `GROUP BY` clause?

---

### **Pitfalls**
**XiaoMing:** Great question! If you try something like this:

```sql
SELECT category, name, COUNT(*) AS product_count
FROM products
GROUP BY category;
```

SQLite will let it slide, but the `name` column in the result might not make sense because it’s not grouped or aggregated. Other databases, like MySQL in strict mode or PostgreSQL, will throw an error. Always make sure your selected columns are either in the `GROUP BY` clause or wrapped in an aggregate function.

**James:** Got it—no shortcuts there!

---

### **Highlight**
- Use `GROUP BY` to organize data into groups for aggregation.
- Include all non-aggregated columns in the `GROUP BY` clause.
- Be cautious with databases that allow loose grouping—your results may be inconsistent.

---

### **Exercise**
1. Modify the `sales` table to include a `date` column. Write a query that calculates the total sales for each category per day.
2. Using the `products` table, find the category with the highest number of products.
3. Try adding another column (e.g., `region`) to the `sales` table. Group by multiple columns (`category` and `region`) to see the combined effects.

---

**James:** This is so useful, XiaoMing. I feel like I can analyze my data way better now!

**XiaoMing:** That’s the idea. Keep experimenting, and soon `GROUP BY` will feel like second nature!

---

### **References**
1. [SQLite GROUP BY Documentation](https://www.sqlite.org/lang_select.html#resultset)
2. [SQL Aggregate Functions](https://www.w3schools.com/sql/sql_count_avg_sum.asp)
3. [SQLite Tutorial – GROUP BY](https://www.sqlitetutorial.net/sqlite-group-by/)
