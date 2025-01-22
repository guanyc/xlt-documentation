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

title: "Measure Performace of Sql Command"
date: "2025-01-20 22:50:40+08:00"
lastmod: "2025-01-20 22:50:40+08:00"
draft: false

keywords: [sqlite3]
tags: [sqlite3]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

weight: 550
type: docs

featured_image:


---

To measure the performance of SQL commands in SQLite, especially when working with indexes, you can use a few techniques to track and analyze how fast your queries are executing. Here's how you can go about it:

---

### 1. **Using `EXPLAIN QUERY PLAN`**
SQLite provides the `EXPLAIN QUERY PLAN` statement, which can show you the query execution plan and help you understand how the query is being executed (whether indexes are being used, for example).

**How it works:**

You can run `EXPLAIN QUERY PLAN` before your query to see how SQLite plans to execute it. This will help you identify if your index is being used, or if SQLite is performing a full table scan.

#### Example:

```sql
EXPLAIN QUERY PLAN
SELECT * FROM Products WHERE Category = 'Electronics' AND Price > 100;
```

Output will show something like:

```
0|0|0|SEARCH TABLE Products USING INDEX idx_category_price (Category=? AND Price>?)
```

This indicates that the query is using the index `idx_category_price` to speed up the search.

If no index is used, it might say something like `SCAN TABLE Products`.

**How to interpret:**
- **Using Index**: This is good because it means the query is using the index to avoid a full scan.
- **Full Table Scan**: This indicates the query is checking every row in the table, which can be slow on large datasets.

---

### 2. **Measuring Query Execution Time with `sqlite3` Command Line**
In SQLite’s command-line tool, you can use the `.timer` command to measure the time it takes for a query to execute. This is very useful for comparing the performance of different queries or with and without indexes.

#### Example:

1. **Enable Timing**: First, enable the timer by running:
   
   ```bash
   .timer on
   ```

2. **Run Your Query**: Then, run your query as usual:

   ```sql
   SELECT * FROM Products WHERE Category = 'Electronics' AND Price > 100;
   ```

3. **Check the Output**: SQLite will output the execution time for the query.

   ```bash
   0.002345 sec
   ```

This tells you how long the query took to execute.

---

### 3. **Using `PRAGMA profile` for Detailed Query Timing**
The `PRAGMA profile` command in SQLite gives you a more detailed view of what SQLite is doing during query execution. It shows you each individual step SQLite takes, including the time taken for each operation.

#### Example:

```sql
PRAGMA profile=1;

SELECT * FROM Products WHERE Category = 'Electronics' AND Price > 100;
```

You will see an output with detailed execution steps like:

```
0|SELECT|0|SEARCH TABLE Products USING INDEX idx_category_price (Category=? AND Price>?)
0|0|0|SCAN TABLE Products
```

Each operation will be logged along with the time it took, which allows you to see where the performance bottlenecks are.

---

### 4. **Measuring Before and After Index Creation**
One of the best ways to understand the impact of an index is to compare query performance **before** and **after** creating an index. You can measure the execution time of the query before adding the index, create the index, and then measure the time again.

#### Steps:

1. **Run Query Before Index**: 

   ```sql
   .timer on
   SELECT * FROM Products WHERE Category = 'Electronics' AND Price > 100;
   ```

2. **Create Index**:

   ```sql
   CREATE INDEX idx_category_price ON Products(Category, Price);
   ```

3. **Run Query After Index**: 

   ```sql
   .timer on
   SELECT * FROM Products WHERE Category = 'Electronics' AND Price > 100;
   ```

Compare the times to see if the index improved the performance.

---

### 5. **Using `SQLite` with External Profiling Tools**
If you need more advanced profiling (for example, over multiple queries or with large datasets), you can use external tools to track database performance. Some options include:

- **SQLite Performance Analyzer**: Some third-party tools help you analyze SQLite performance in-depth.
- **SQLite Logging**: You can log queries and their times in an external file and analyze the logs afterward.

---

### Summary of Methods:

- **`EXPLAIN QUERY PLAN`**: Check if your index is being used and understand the query plan.
- **`.timer` in SQLite CLI**: Measure query execution time directly.
- **`PRAGMA profile`**: Get detailed logs of each step in query execution.
- **Before and After Index Creation**: Compare performance with and without indexes.
- **External Profiling Tools**: Use advanced tools for more complex use cases.

---

### Example Exercise for Performance Measurement:

1. **Create a `Products` table** with columns `ProductID`, `Name`, `Category`, and `Price`.
2. **Insert 1,000 rows** with random data.
3. **Measure query time** before creating an index:

   ```sql
   .timer on
   SELECT * FROM Products WHERE Category = 'Electronics' AND Price > 100;
   ```

4. **Create an index** on `Category` and `Price`:

   ```sql
   CREATE INDEX idx_category_price ON Products(Category, Price);
   ```

5. **Measure the query time again**:

   ```sql
   .timer on
   SELECT * FROM Products WHERE Category = 'Electronics' AND Price > 100;
   ```

6. Compare the execution times. If the time is lower after creating the index, that means the index is improving query performance.

---

### References:

- [SQLite EXPLAIN QUERY PLAN](https://www.sqlite.org/cli.html#explain_query_plan)
- [SQLite PRAGMA PROFILE](https://www.sqlite.org/pragma.html#pragma_profile)
- [SQLite Timer Command](https://www.sqlite.org/cli.html#timer)

---

### Keywords:
- SQLite, Performance, Index, EXPLAIN QUERY PLAN, PRAGMA profile, Query Timing, Query Optimization, Execution Time, Profiling, Index Creation