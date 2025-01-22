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

title: "Sqlite Scalar, String, Number Functions"
date: "2025-01-21 21:29:31+08:00"
lastmod: "2025-01-21 21:29:31+08:00"
draft: false

keywords: [sqlite3]
tags: [sqlite3]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

weight: 385
type: docs

featured_image:


---

## Mastering SQLite Built-in Functions: String Manipulation, Numeric Functions, and Scalar Functions

SQLite is a lightweight, self-contained database engine that is popular for both desktop and mobile applications. One of its strongest features is the collection of built-in SQL functions that simplify complex operations. These functions cover everything from string manipulation to numeric calculations and even custom scalar operations. In this article, we’ll dive into the key functions available in SQLite, focusing on **String Manipulation**, **Numeric Functions**, and **Built-in Scalar Functions**.

### 1. **String Manipulation Functions**

SQLite provides several functions for manipulating and transforming string data. These are invaluable when working with text in databases, enabling you to clean, format, and extract meaningful parts of a string.

#### 1.1 **`UPPER()` and `LOWER()`**
The `UPPER()` and `LOWER()` functions are used to convert a string to uppercase or lowercase, respectively.

- **Syntax:**
  ```sql
  SELECT UPPER(name) FROM users;
  SELECT LOWER(name) FROM users;
  ```

- **Example:**
  ```sql
  SELECT UPPER('Hello World');  -- Returns 'HELLO WORLD'
  SELECT LOWER('Hello World');  -- Returns 'hello world'
  ```

#### 1.2 **`SUBSTR()` (Substring)**

The `SUBSTR()` function allows you to extract a part of a string starting from a specified position. It’s often used for cutting out specific parts of a text field.

- **Syntax:**
  ```sql
  SELECT SUBSTR(column_name, start_position, length) FROM table_name;
  ```

- **Example:**
  ```sql
  SELECT SUBSTR(name, 1, 3) FROM users;  -- Returns first 3 characters of each name
  ```

#### 1.3 **`LENGTH()`**

This function returns the length of a string in characters.

- **Syntax:**
  ```sql
  SELECT LENGTH(name) FROM users;
  ```

- **Example:**
  ```sql
  SELECT LENGTH('SQLite');  -- Returns 6
  ```

#### 1.4 **`REPLACE()`**

Use `REPLACE()` to replace all occurrences of a substring within a string.

- **Syntax:**
  ```sql
  SELECT REPLACE(name, 'old', 'new') FROM users;
  ```

- **Example:**
  ```sql
  SELECT REPLACE('Hello World', 'World', 'SQLite');  -- Returns 'Hello SQLite'
  ```

#### 1.5 **`TRIM()`**

The `TRIM()` function removes leading and trailing spaces from a string.

- **Syntax:**
  ```sql
  SELECT TRIM(string) FROM table_name;
  ```

- **Example:**
  ```sql
  SELECT TRIM('   Hello   ');  -- Returns 'Hello'
  ```

### 2. **Numeric Functions**

Numeric functions in SQLite help you perform calculations, rounding, and even generate random values. These are crucial when dealing with financial or scientific data.

#### 2.1 **`ROUND()`**

The `ROUND()` function is used to round a number to a specified number of decimal places.

- **Syntax:**
  ```sql
  SELECT ROUND(number, decimals);
  ```

- **Example:**
  ```sql
  SELECT ROUND(15.6789, 2);  -- Returns 15.68
  ```

#### 2.2 **`ABS()` (Absolute Value)**

The `ABS()` function returns the absolute (positive) value of a number.

- **Syntax:**
  ```sql
  SELECT ABS(number) FROM table_name;
  ```

- **Example:**
  ```sql
  SELECT ABS(-123);  -- Returns 123
  ```

#### 2.3 **`RANDOM()`**

The `RANDOM()` function returns a random integer. If used with a modulus operator, you can limit the random number to a certain range.

- **Syntax:**
  ```sql
  SELECT RANDOM();  -- Returns a random integer
  SELECT RANDOM() % 100;  -- Returns a random number between 0 and 99
  ```

- **Example:**
  ```sql
  SELECT RANDOM();  -- Returns, e.g., -1756056173487532800
  ```

#### 2.4 **`MIN()` and `MAX()`**

These functions return the smallest and largest values, respectively, from a set of numbers.

- **Syntax:**
  ```sql
  SELECT MIN(price) FROM products;
  SELECT MAX(price) FROM products;
  ```

- **Example:**
  ```sql
  SELECT MIN(price) FROM products;  -- Returns the lowest price
  SELECT MAX(price) FROM products;  -- Returns the highest price
  ```

### 3. **Scalar Functions**

Scalar functions perform operations on individual data values and return a single result. These are among the most common functions used in SQL queries.

#### 3.1 **`COALESCE()`**

`COALESCE()` returns the first non-NULL value in a list of expressions. This function is useful when dealing with potential NULL values in your data.

- **Syntax:**
  ```sql
  SELECT COALESCE(value1, value2, value3, ...) FROM table_name;
  ```

- **Example:**
  ```sql
  SELECT COALESCE(NULL, NULL, 'Hello');  -- Returns 'Hello'
  ```

#### 3.2 **`IFNULL()`**

`IFNULL()` checks if a value is NULL and returns a specified value if it is. This is similar to `COALESCE()` but for two values.

- **Syntax:**
  ```sql
  SELECT IFNULL(column, 'default_value') FROM table_name;
  ```

- **Example:**
  ```sql
  SELECT IFNULL(name, 'No Name') FROM users;  -- Returns 'No Name' if name is NULL
  ```

#### 3.3 **`LIKE` (Pattern Matching)**

SQLite’s `LIKE` operator is used to perform pattern matching on strings. It’s case-insensitive by default and supports wildcards (`%` and `_`).

- **Syntax:**
  ```sql
  SELECT column FROM table_name WHERE column LIKE pattern;
  ```

- **Example:**
  ```sql
  SELECT name FROM users WHERE name LIKE 'A%';  -- Returns all names starting with 'A'
  ```

#### 3.4 **`CAST()`**

`CAST()` is used to convert a value from one type to another. For example, converting a string to an integer.

- **Syntax:**
  ```sql
  SELECT CAST(expression AS datatype) FROM table_name;
  ```

- **Example:**
  ```sql
  SELECT CAST('123' AS INTEGER);  -- Returns 123 as an integer
  ```

#### 3.5 **`DATE()` and `TIME()`**

SQLite provides date and time functions to manipulate date and time values. These functions are essential for handling time-based data.

- **Syntax:**
  ```sql
  SELECT DATE('now');
  SELECT TIME('now');
  ```

- **Example:**
  ```sql
  SELECT DATE('now');  -- Returns the current date in YYYY-MM-DD format
  SELECT TIME('now');  -- Returns the current time in HH:MM:SS format
  ```

### Pitfalls to Watch Out For
While SQLite functions are incredibly powerful, there are some common pitfalls you should avoid:
1. **NULL Handling**: Be careful with `NULL` values. Many functions return `NULL` if any operand is `NULL`. Always check for `NULL` before performing operations.
2. **Type Compatibility**: SQLite is dynamically typed, but mixing incompatible data types in calculations (like trying to sum a string with a number) can lead to unexpected results.
3. **Precision**: When working with floating-point numbers, be cautious with rounding errors. Use `ROUND()` appropriately when precision matters.
4. **Case Sensitivity**: SQLite’s string functions like `LIKE` are case-insensitive by default, but this behavior can change depending on the collation used.

### Conclusion

SQLite provides a wide range of built-in functions to help you manipulate strings, perform numerical calculations, and operate on data efficiently. Whether you’re cleaning up user input, analyzing prices, or working with dates and times, these functions save time and effort by allowing you to perform complex tasks directly within your SQL queries.

By mastering functions like `UPPER()`, `ROUND()`, `COALESCE()`, and others, you can streamline your database interactions, making your queries more powerful and flexible. However, always be mindful of edge cases like `NULL` values and type compatibility to avoid unexpected results.

### References:
- [SQLite Documentation](https://www.sqlite.org/lang_aggfunc.html) 
  
### Featured Image :

--- 

### Keywords:
- **SQLite functions**
- **String manipulation**
- **Numeric functions**
- **Scalar functions**
- **Rounding in SQLite**
- **Substring function**
- **NULL handling**
- **SQLite tutorials**