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

title: "Sql Functions Introduction"
date: "2025-01-21 21:03:48+08:00"
lastmod: "2025-01-21 21:03:48+08:00"
draft: false

keywords: [sqlite3]
tags: [sqlite3]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

weight: 380
type: docs

featured_image:


---

### Conversation Between David and James: Exploring SQLite Functions

---

#### Scene:  
David and James are sitting in a coffee shop, chatting about their ongoing project. David is more experienced with SQL, while James is just starting to learn SQLite.

---

**David**:  
Hey James, have you used SQLite functions in your project yet?

**James**:  
I’ve been doing some basic queries, but I’m not really sure about the functions part. What are those exactly?

**David**:  
SQLite functions are like built-in shortcuts that help you perform operations on data directly in your queries. They make things like calculations, string manipulation, and data aggregation a lot easier.

**James**:  
Ah, I see! Can you give me some examples?

**David**:  
Sure! Let’s start with something simple: **aggregation functions**. You’ve probably heard of `COUNT()`, `SUM()`, `AVG()`, `MIN()`, and `MAX()`? These are used to aggregate data from multiple rows into one result.

**James**:  
Right, like finding the average age of users in a table?

**David**:  
Exactly! Here’s an example:

```sql
SELECT AVG(age) FROM users;
```

This would give you the average age of all users in the `users` table.

**James**:  
Cool! So what if I want to count how many users are there?

**David**:  
That’s where `COUNT()` comes in. It counts the number of rows that match your query.

```sql
SELECT COUNT(*) FROM users;
```

This gives you the total number of users in the table. If you wanted to count only users above 18 years old, you’d do something like:

```sql
SELECT COUNT(*) FROM users WHERE age > 18;
```

**James**:  
Got it. What about string manipulation? Are there functions for that too?

**David**:  
Definitely. SQLite has a bunch of string functions. For instance, `UPPER()` and `LOWER()` to change case, or `SUBSTR()` to extract parts of a string. Here's an example using `UPPER()`:

```sql
SELECT UPPER(name) FROM users;
```

This would return all names in uppercase.

**James**:  
Nice! How do I use `SUBSTR()`?

**David**:  
`SUBSTR()` lets you extract a substring from a string. You give it a string, a starting position, and optionally, the length of the substring. Here's an example:

```sql
SELECT SUBSTR(name, 1, 3) FROM users;
```

This returns the first 3 characters of each user’s name.

**James**:  
I see, that’s useful. But what about numbers? Any functions for that?

**David**:  
Oh yeah. You can use functions like `ROUND()` to round numbers, or `RANDOM()` to get random values.

```sql
SELECT ROUND(price, 2) FROM products;
```

This will round the `price` column to 2 decimal places.

And here's how you'd get a random number between 1 and 100:

```sql
SELECT RANDOM() % 100 + 1;
```

**James**:  
That’s pretty fun! But are there any common pitfalls I should watch out for?

**David**:  
Oh, for sure! One common mistake is **mixing data types**. SQLite is pretty flexible with types, but if you’re not careful, you can run into problems. For example, if you’re using `SUM()` on a column that has non-numeric data, it’ll return `NULL`.

Another thing to watch out for is **NULL values**. Functions like `AVG()` and `COUNT()` ignore `NULL` values, but others, like `MAX()` or `MIN()`, will return `NULL` if all values are `NULL`.

**James**:  
Good to know! Any exercises to help me practice?

**David**:  
Absolutely! Here are a few:

### Exercises:

1. **Count the number of users with a certain status**:
   - `SELECT COUNT(*) FROM users WHERE status = 'active';`

2. **Find the highest and lowest prices in a product table**:
   - `SELECT MAX(price), MIN(price) FROM products;`

3. **Extract the first three letters of each user’s name**:
   - `SELECT SUBSTR(name, 1, 3) FROM users;`

4. **Calculate the average price of products in each category**:
   - `SELECT category, AVG(price) FROM products GROUP BY category;`

5. **Get a random product**:
   - `SELECT * FROM products ORDER BY RANDOM() LIMIT 1;`

---

**James**:  
These are awesome! I’ll give them a try. Thanks, David!

**David**:  
No problem! Just remember to play around with different functions, and make sure you test your queries on sample data. And check out the [SQLite documentation](https://www.sqlite.org/lang_aggfunc.html) if you need a quick reference for more functions.

---

### Key Points to Remember:
1. **SQLite Functions** are built-in tools to perform operations on data in queries (aggregation, string manipulation, etc.).
2. Functions like `COUNT()`, `SUM()`, `AVG()`, `MIN()`, and `MAX()` help you summarize data.
3. String functions like `UPPER()`, `LOWER()`, and `SUBSTR()` allow for manipulating text.
4. Numeric functions like `ROUND()` and `RANDOM()` are useful for rounding numbers and generating random values.
5. Watch out for **NULL values** in functions like `MAX()`, `MIN()`, and `AVG()`.
6. SQLite is **flexible** with data types but can cause issues if you're not careful with mixing types.

### Keywords:
- **SQLite functions**
- **Aggregation functions**
- **String manipulation**
- **Numeric functions**
- **COUNT()**
- **AVG()**
- **SUBSTR()**
- **RANDOM()**
- **NULL values**

---

### Featured Image :


```mermaid
mindmap
  root((SQLite Functions Introduction))
    Aggregation Functions
      COUNT
      SUM
      AVG
      MIN
      MAX
    String Manipulation Functions
      UPPER
      LOWER
      SUBSTR
    Numeric Functions
      ROUND
      RANDOM
    Key Points to Remember
      SQLite Functions are built in tools for query operations
      Watch out for NULL values in functions
      Be careful with mixing data types
    Common Pitfalls
      Mixing data types can cause issues
      NULL values affect function results
      
```mermaid