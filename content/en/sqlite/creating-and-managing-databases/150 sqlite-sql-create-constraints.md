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

title: "Sqlite Sql Create Table Constraints"
date: "2024-12-19 19:57:31+08:00"
lastmod: "2024-12-19 19:57:31+08:00"
draft: false

keywords: ["sqlite3"]
tags: ["sqlite3"]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

featured_image:
weight: 150
type: docs

---

### **SQL Create Constraints**

---

**James**: XiaoMing, I’ve been adding columns and data types to my tables, but how do I enforce rules? Like, making sure nobody enters a negative price or duplicates an email address?

**XiaoMing**: Ah, James, you’re talking about constraints. They’re the secret sauce that ensures your data stays clean and reliable.

**James**: Secret sauce? Sounds like something I need in my database kitchen!

---

### **Step 1: What Are Constraints?**

**XiaoMing**: Constraints are rules you set on your table’s columns to enforce specific conditions. Think of them as traffic laws for your data—keeping everything in order.

**James**: Got it. So, what kinds of rules are we talking about?

**XiaoMing**: SQLite supports several constraints:
1. **NOT NULL:** Makes sure a column always has a value.
2. **UNIQUE:** Ensures no duplicate values in a column.
3. **PRIMARY KEY:** A combination of `NOT NULL` and `UNIQUE`. Used to identify each row uniquely.
4. **CHECK:** Enforces a condition that data must satisfy.
5. **DEFAULT:** Sets a default value if none is provided.
6. **FOREIGN KEY:** Links a column to a column in another table.

---

### **Step 2: Adding Constraints in `CREATE TABLE`**

**XiaoMing**: Let’s say we’re creating a table to store products:

```sql
CREATE TABLE products (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    price REAL CHECK (price >= 0),
    stock INTEGER DEFAULT 0
);
```

**James**: Okay, let me break this down:
- `id INTEGER PRIMARY KEY`: Each product gets a unique ID.
- `name TEXT NOT NULL`: Every product must have a name.
- `price REAL CHECK (price >= 0)`: Prices can’t be negative.
- `stock INTEGER DEFAULT 0`: If no stock is provided, it defaults to 0.

**XiaoMing**: Exactly! Constraints like these save you from writing extra code to validate data.

---

### **Step 3: Using `ALTER TABLE` to Add Constraints**

**James**: What if I forget to add a constraint when creating the table?

**XiaoMing**: Unfortunately, SQLite doesn’t let you add constraints directly with `ALTER TABLE`. You’ll need to create a new table with the constraints and move your data over.

**James**: That’s… inconvenient.

**XiaoMing**: True, but planning your constraints ahead of time can save you from this hassle.

---

### **Step 4: A Real-World Example**

**XiaoMing**: Let’s create a `users` table to illustrate more constraints:

```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    username TEXT UNIQUE NOT NULL,
    email TEXT UNIQUE NOT NULL,
    age INTEGER CHECK (age >= 13),
    created_at TEXT DEFAULT (datetime('now'))
);
```

**James**: This looks solid. I see `UNIQUE` on `username` and `email`, and a `CHECK` to ensure users are at least 13 years old.

**XiaoMing**: Right, and the `DEFAULT` constraint sets the registration date automatically.

---

### **Step 5: Testing Your Constraints**

**James**: How can I confirm the constraints work?

**XiaoMing**: Try inserting some rows:

```sql
INSERT INTO users (username, email, age) VALUES ('jdoe', 'jdoe@example.com', 12);
-- This will fail because age is less than 13.

INSERT INTO users (username, email, age) VALUES ('jdoe', 'jdoe@example.com', 20);
-- This will succeed.

INSERT INTO users (username, email, age) VALUES ('jdoe', 'jdoe@example.com', 20);
-- This will fail because email and username are UNIQUE.
```

**James**: Wow, constraints are doing all the heavy lifting!


---


## SQL Create Constraints (Extended with Examples)

**James**: These constraints feel like the ultimate safety net for my database.

**XiaoMing**: That’s a great way to put it! They’re your first line of defense against bad data.

**James**: Time to get hands-on. XiaoMing, constraints are starting to make sense, but I’d love to see more examples for each one. Could we go through them in detail?

**XiaoMing**: Absolutely! Let’s tackle each of the six constraints with examples. Ready?

**James**: Always ready. Let’s go!

### **1. `NOT NULL`: Ensuring Mandatory Data**

**XiaoMing**: `NOT NULL` ensures a column can’t have empty values. For instance, every user should have a username:

```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    username TEXT NOT NULL,
    email TEXT
);
```

**James**: So, if I try this:

```sql
INSERT INTO users (id, email) VALUES (1, 'james@example.com');
```

**XiaoMing**: You’ll get an error because `username` is required.

---

### **2. `UNIQUE`: Preventing Duplicates**

**XiaoMing**: `UNIQUE` ensures no two rows have the same value in a column. Perfect for things like email addresses:

```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    username TEXT NOT NULL UNIQUE,
    email TEXT UNIQUE
);
```

**James**: So this works:

```sql
INSERT INTO users (id, username, email) VALUES (1, 'james', 'james@example.com');
```

**XiaoMing**: But this fails:

```sql
INSERT INTO users (id, username, email) VALUES (2, 'james', 'james@example.com');
```

**James**: Right, because both `username` and `email` must be unique.

---

### **3. `PRIMARY KEY`: Unique Row Identifiers**

**XiaoMing**: A `PRIMARY KEY` uniquely identifies each row and combines `NOT NULL` with `UNIQUE`. Typically, it’s used for IDs:

```sql
CREATE TABLE orders (
    order_id INTEGER PRIMARY KEY,
    product_name TEXT NOT NULL,
    quantity INTEGER
);
```

**James**: So if I try this:

```sql
INSERT INTO orders (order_id, product_name, quantity) VALUES (1, 'Laptop', 2);
```

**XiaoMing**: It works. But this:

```sql
INSERT INTO orders (order_id, product_name, quantity) VALUES (1, 'Phone', 1);
```

**James**: Fails, because `order_id` must be unique.

---

### **4. `CHECK`: Enforcing Conditions**

**XiaoMing**: `CHECK` ensures column values meet specific conditions. For instance, prices should be non-negative:

```sql
CREATE TABLE products (
    product_id INTEGER PRIMARY KEY,
    product_name TEXT NOT NULL,
    price REAL CHECK (price >= 0)
);
```

**James**: So this works:

```sql
INSERT INTO products (product_id, product_name, price) VALUES (1, 'Book', 10.99);
```

**XiaoMing**: But this fails:

```sql
INSERT INTO products (product_id, product_name, price) VALUES (2, 'Pen', -5);
```

---

### **5. `DEFAULT`: Setting Default Values**

**XiaoMing**: `DEFAULT` sets a column’s value automatically if none is provided. For instance, a default stock of 0 for new products:

```sql
CREATE TABLE inventory (
    item_id INTEGER PRIMARY KEY,
    item_name TEXT NOT NULL,
    stock INTEGER DEFAULT 0
);
```

**James**: So, if I run this:

```sql
INSERT INTO inventory (item_id, item_name) VALUES (1, 'Notebook');
```

**XiaoMing**: The stock will be set to `0`.

---

### **6. `FOREIGN KEY`: Linking Tables**

**XiaoMing**: `FOREIGN KEY` links a column in one table to a column in another, enforcing relational integrity. For instance, linking orders to users:

```sql
CREATE TABLE users (
    user_id INTEGER PRIMARY KEY,
    username TEXT NOT NULL
);

CREATE TABLE orders (
    order_id INTEGER PRIMARY KEY,
    user_id INTEGER,
    order_details TEXT,
    FOREIGN KEY (user_id) REFERENCES users (user_id)
);
```

**James**: So, I can do this:

```sql
INSERT INTO users (user_id, username) VALUES (1, 'james');
INSERT INTO orders (order_id, user_id, order_details) VALUES (1, 1, 'Laptop');
```

**XiaoMing**: But this fails:

```sql
INSERT INTO orders (order_id, user_id, order_details) VALUES (2, 99, 'Tablet');
```

**James**: Because there’s no user with `user_id = 99` in the `users` table.

---


### **Highlights**

1. **Types of Constraints:**
   - `NOT NULL`: Mandatory fields.
   - `UNIQUE`: Prevent duplicates.
   - `PRIMARY KEY`: Unique identifier for rows.
   - `CHECK`: Custom rules for values.
   - `DEFAULT`: Set default values for columns.
   - `FOREIGN KEY`: Link tables together.

2. **Plan Ahead:** Adding constraints during table creation avoids data migration headaches later.

3. **Automatic Enforcement:** Constraints ensure data integrity without extra validation logic in your application code.

---

### **Exercises for James**

1. **Create a `students` Table:**
   - Include `id` (integer, primary key), `name` (text, not null), `grade` (integer, check that grade is between 0 and 100), and `registration_date` (text, default to the current date).

2. **Experiment with UNIQUE:**
   - Create a table where both `email` and `phone_number` are unique, and try inserting duplicate values to see what happens.

3. **Use CHECK Constraints:**
   - Add a `CHECK` constraint to ensure that a column for `stock` in a table always has a value of 0 or higher.

---

### **References**

1. **[SQLite Constraints Documentation](https://sqlite.org/syntax/column-constraint.html)**
   - Official reference for understanding constraints in SQLite.

2. **[SQLite CHECK Constraint](https://sqlite.org/lang_createtable.html#ckconst)**
   - Details on how to use the `CHECK` constraint effectively.

3. **[SQLite Default Values](https://sqlite.org/lang_createtable.html#dfltval)**
   - Explanation of the `DEFAULT` constraint and its uses.

4. **[DB Browser for SQLite](https://sqlitebrowser.org/)**
   - Tool to visualize and experiment with constraints.

5. **[Sqlite Choosing Appropriate Data Types for Your Tables](/post/sqlite3/sqlite-choosing-appropriate-data-types-for-your-tables/)**
   - choose the right data type.
