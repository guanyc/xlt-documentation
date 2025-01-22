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

title: "440 Sqlite Data Integrity Enforcing Constraits in Sqlite"
date: "2025-01-20 14:19:34+08:00"
lastmod: "2025-01-20 14:19:34+08:00"
draft: false

keywords: [sqlite3]
tags: [sqlite3]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

weight: 440
type: docs

featured_image:


---


### **Mastering Data Integrity in SQLite: Enforcing Constraints with Practical Examples, Pitfalls, and Exercises**

---

#### **What Are Constraints in SQLite?**
Constraints are rules applied to database tables that ensure the accuracy and reliability of the data. They act like guardrails to prevent invalid, inconsistent, or duplicate data from entering your tables. SQLite supports several types of constraints, such as:

1. **PRIMARY KEY**: Ensures each row is unique and serves as a unique identifier.
2. **FOREIGN KEY**: Maintains relationships between tables by linking columns.
3. **NOT NULL**: Prevents empty or null values in a column.
4. **UNIQUE**: Ensures no duplicate values in a column.
5. **CHECK**: Validates data using a specific condition.
6. **DEFAULT**: Provides a default value for a column if no value is specified.

---

#### **Practical Examples**

1. **Ensuring Product Data Integrity**
   ```sql
   CREATE TABLE Products (
       product_id INTEGER PRIMARY KEY,             
       name TEXT NOT NULL,                         
       price REAL CHECK(price > 0),                
       stock INTEGER DEFAULT 10 CHECK(stock >= 0)
   );
   ```
   - **What It Does**:
     - Each product must have a unique `product_id`.
     - `name` cannot be null.
     - `price` must be greater than 0.
     - `stock` defaults to 10 and cannot be negative.

   - **Try This**:
     ```sql
     INSERT INTO Products (name, price) VALUES ('Laptop', 1000);  -- Succeeds
     INSERT INTO Products (name, price, stock) VALUES ('Tablet', -500, -10); -- Fails
     ```

2. **Maintaining Relationships with Foreign Keys**
   ```sql
   CREATE TABLE Orders (
       order_id INTEGER PRIMARY KEY, 
       product_id INTEGER NOT NULL, 
       quantity INTEGER CHECK(quantity > 0),
       FOREIGN KEY(product_id) REFERENCES Products(product_id)
   );
   ```
   - This ensures orders can only reference valid products. Attempting to add an order with a non-existent `product_id` will fail.

---

#### **Best Practices**

1. **Plan Constraints Early**: Design constraints during schema planning to avoid migrations or updates later.
2. **Combine Constraints**: For example, combine `NOT NULL` and `CHECK`:
   ```sql
   age INTEGER NOT NULL CHECK(age >= 5);
   ```
3. **Test Constraints**: Regularly test your schema with edge cases to ensure constraints behave as expected.
4. **Keep It Simple**: Avoid overly complex constraints that may hinder performance or flexibility.

---

#### **Common Pitfalls**
1. **Overly Strict Rules**: Constraints that are too rigid might block legitimate data.
2. **Silent Failures**: Operations violating constraints are rejected by SQLite. Without proper error handling, these failures may go unnoticed.
3. **Performance Overhead**: Constraints like `FOREIGN KEY` checks may slow down large databases.
4. **Migration Challenges**: Changing or removing constraints often requires creating new tables and copying data.

---

#### **Exercises**

1. **Library Database Design**:
   - Create a `Books` table with constraints ensuring:
     - Each book has a unique ID.
     - Stock cannot be negative.
   - Add a `Borrowers` table where:
     - Name cannot be null.
   - Create a `BorrowedBooks` table to link `Books` and `Borrowers`.

2. **E-Commerce Inventory System**:
   - Create a `Products` table with:
     - Default stock values of 10.
     - Non-negative prices.
   - Create an `Orders` table referencing the `Products` table and ensuring the ordered quantity is at least 1.

---

#### **References**
1. [SQLite Documentation on Constraints](https://sqlite.org/lang_createtable.html#constraints)
2. *Learning SQL* by Alan Beaulieu
3. [SQL Zoo - Practice SQL Online](https://sqlzoo.net/)

---

#### **Keywords**
- SQLite
- Constraints
- Data Integrity
- Primary Key
- Foreign Key
- Unique Constraint
- Not Null
- Check Constraint
- Default Values
- Relational Database
