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

title: "Sqlite Filtering Results With Where Clauses"
date: "2024-12-20 12:15:24+08:00"
lastmod: "2024-12-20 12:15:24+08:00"
draft: false

keywords: [sqlite3]
tags: [sqlite3]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

featured_image: images/sqlite/sqlite-filtering-where.png
weight: 210

type: docs


---

### **Filtering Results with WHERE Clauses**

---

**James**: Alright, David, I can pull data from a table, but what if I don’t need *all* the data?

**David**: That’s where the `WHERE` clause comes in! It’s like a filter that lets you pinpoint exactly what you’re looking for.

**James**: So it’s like searching for specific songs in a playlist?

**David**: Exactly! Imagine your table as the playlist and `WHERE` as your search bar. Let’s dive in.

---

### **The Basics of WHERE**

**David**: The `WHERE` clause is added to a `SELECT` statement to filter rows. Here’s the basic syntax:

```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

Let’s say we have a `products` table:

```sql
CREATE TABLE products (
    product_id INTEGER PRIMARY KEY,
    product_name TEXT NOT NULL,
    price REAL,
    stock INTEGER
);

INSERT INTO products (product_id, product_name, price, stock) VALUES
(1, 'Laptop', 999.99, 10),
(2, 'Mouse', 25.50, 100),
(3, 'Keyboard', 49.99, 50),
(4, 'Monitor', 150.00, 20),
(5, 'USB Cable', 5.99, 200);
```

Now, if you want to find products with a price above $50:

```sql
SELECT product_name, price
FROM products
WHERE price > 50;
```

**James**: So, this will only return the Laptop, Keyboard, and Monitor?

**David**: Exactly. You can use operators like `>`, `<`, `>=`, `<=`, `=`, and `!=` to set your conditions.

---

### **Combining Conditions with AND and OR**

**James**: What if I want to find products above $50 that are also in stock?

**David**: Use `AND`:

```sql
SELECT product_name, price, stock
FROM products
WHERE price > 50 AND stock > 0;
```

**James**: Makes sense. What about finding products below $10 *or* products with more than 100 in stock?

**David**: For that, use `OR`:

```sql
SELECT product_name, price, stock
FROM products
WHERE price < 10 OR stock > 100;
```

**James**: So `AND` is stricter, while `OR` is more flexible.

---

### **Filtering with LIKE**

**David**: The `LIKE` operator is great for partial matching. Use `%` as a wildcard for any number of characters.

To find all products with “USB” in their name:

```sql
SELECT product_name
FROM products
WHERE product_name LIKE '%USB%';
```

**James**: `%` is like saying, “I don’t care what comes before or after ‘USB’.”

**David**: Exactly! You can also use `_` for a single character wildcard.

---

### **NULL Values and IS NULL**

**David**: What if you’re looking for rows where a column has no value? That’s where `NULL` comes in.

If a column in your table has `NULL` values, filter them like this:

```sql
SELECT product_name
FROM products
WHERE stock IS NULL;
```

**James**: And if I want rows that aren’t `NULL`?

**David**: Use `IS NOT NULL`:

```sql
SELECT product_name
FROM products
WHERE stock IS NOT NULL;
```

---

### **Common Pitfalls**

1. **Forgetting Operator Precedence:**
   - Conditions with `AND` and `OR` can behave unpredictably without parentheses:
     ```sql
     SELECT * FROM products
     WHERE price > 50 OR stock < 10 AND stock > 0;
     ```
     Always group with parentheses for clarity:
     ```sql
     SELECT * FROM products
     WHERE price > 50 OR (stock < 10 AND stock > 0);
     ```

2. **Misunderstanding NULL:**
   - `NULL` isn’t the same as an empty string or zero. A query like `price = NULL` will fail. Use `IS NULL` instead.

3. **Case Sensitivity with LIKE:**
   - `LIKE` is case-insensitive in SQLite, but some databases might not be.

---

### **Highlights**

1. **Basic Filters:** Use `WHERE` with operators like `=`, `!=`, `<`, and `>`.
2. **Combining Filters:** Use `AND` and `OR` to refine queries.
3. **Pattern Matching:** Use `LIKE` and wildcards (`%` and `_`) for flexible searches.
4. **NULL Handling:** Use `IS NULL` and `IS NOT NULL` for null value filtering.
5. **Parentheses:** Always group conditions clearly when mixing `AND` and `OR`.

---

### **Exercises for James**

1. **Basic Filtering:**
   - Write a query to find all products with a price below $50.

2. **Combining Conditions:**
   - Find products with a stock greater than 20 and a price under $100.

3. **Using LIKE:**
   - Retrieve all products with “Cable” in their name.

4. **NULL Handling:**
   - Add a product with `NULL` stock and query all rows where `stock` is `NULL`.

5. **Precedence Practice:**
   - Write a query mixing `AND` and `OR`, and test how parentheses affect the results.

---

### **References**

1. **[SQLite WHERE Clause Documentation](https://www.sqlite.org/lang_select.html#whereclause)**
   - Official reference for `WHERE` clause usage.

2. **[SQLite Tutorial: Querying Data](https://www.sqlitetutorial.net/sqlite-select/)**
   - Examples and exercises for querying data with `WHERE`.

3. **[SQL Pattern Matching](https://www.sqltutorial.org/sql-like/)**
   - Guide to `LIKE` operator and wildcards.

---

**James**: Filtering feels like unlocking the power of a database. It’s way more useful than I expected!

**David**: Exactly! Once you master filters, you’ll feel like a detective solving data mysteries.
