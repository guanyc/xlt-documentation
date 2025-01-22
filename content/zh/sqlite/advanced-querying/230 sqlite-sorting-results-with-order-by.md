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

title: "Sorting Results with ORDER BY in SQLite"
date: "2024-12-22 19:49:35+08:00"
lastmod: "2024-12-22 19:49:35+08:00"
draft: false

keywords:
  - SQLite ORDER BY Tutorial
  - Sorting Results in SQLite
  - SQLite Query Optimization
  - SQL ORDER BY Examples
  - Learn SQLite Sorting
  - Sorting with Multiple Columns SQLite
  - SQL Sorting Techniques
  - SQLite DESC and ASC Usage
  - SQLite Exercises for Beginners
  - SQL Query Best Practices
tags:
  - sqlite3

categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

featured_image: images/sqlite/sqlite-order-by.png

weight: 230
type: docs

---

## **Sorting Results with ORDER BY**


**James**: David, my query is returning results, but they’re all over the place! Is there a way to make them more organized?

**David**: Absolutely, James! Welcome to the world of `ORDER BY`. It’s like asking SQLite to “tidy up” your results.

**James**: Sounds neat. How does it work?

---

### **Basics of `ORDER BY`**

**David**: The `ORDER BY` clause is how you sort your query results. By default, it organizes them in ascending order.

Example: Let’s use our `students` table:

```sql
CREATE TABLE students (
    id INTEGER PRIMARY KEY,
    name TEXT,
    age INTEGER,
    grade TEXT
);

INSERT INTO students (id, name, age, grade) VALUES
(1, 'Alice', 15, 'A'),
(2, 'Bob', 16, 'B'),
(3, 'Charlie', 15, 'C'),
(4, 'Diana', 17, 'A');
```

To sort students by age:

```sql
SELECT name, age
FROM students
ORDER BY age;
```

**James**: That’s easy! Can I sort in reverse?

**David**: Of course. Add `DESC` for descending order:

```sql
SELECT name, age
FROM students
ORDER BY age DESC;
```

**James**: What about sorting by multiple columns?

---

### **Sorting by Multiple Columns**

**David**: You can chain columns in `ORDER BY`. For example, sort by grade first, then by age:

```sql
SELECT name, age, grade
FROM students
ORDER BY grade, age;
```

**James**: So if two students have the same grade, it falls back to age?

**David**: Exactly! That’s called secondary sorting.

---

### **Sorting by Multiple Columns using both ASC and DESC**

**David**: You can futher using both asc and desc in `ORDER BY`.
For example, first sort by grade `DESC`, then by age `ASC`:

```sql
SELECT name, age, grade
FROM students
ORDER BY grade DESC, age ASC;
```

**James**:  first compared by garde descendingly, then by age ascendingly?

**David**: Exactly! You can combine `ASC` and `DESC` conditions futhermore.

---

### **Speech: SQLite ORDER BY with Column Position**


**James:** David, I’ve been using column names with `ORDER BY`, but I heard you can also use column positions. What’s that about?

**David:** Oh, yes! In SQLite, instead of specifying column names in the `ORDER BY` clause, you can use the column's position in the `SELECT` statement, starting from 1 for the first column. It’s a quick way to sort, but it has some drawbacks.

**James:** Hmm, I see. Can you show me an example?

**David:** Sure! Let’s work with this `employees` table:

```sql
CREATE TABLE employees (
    id INTEGER PRIMARY KEY,
    name TEXT,
    department TEXT,
    salary REAL
);

INSERT INTO employees (name, department, salary) VALUES
('Alice', 'Engineering', 75000),
('Bob', 'Engineering', 60000),
('Charlie', 'Sales', 50000),
('Diana', 'Sales', 70000),
('Eve', 'HR', 45000);
```

Now, imagine you want to sort employees by their department and then by their salary, but in different orders. Here's how you can use **column positions**:

```sql
SELECT name, department, salary
FROM employees
ORDER BY 2 ASC, 3 DESC;
```

**James:** Let me guess—`2 ASC` means sort by the second column (`department`) in ascending order, and `3 DESC` sorts by the third column (`salary`) in descending order?

**David:** You got it! Here’s the result:

```
name      | department  | salary
--------------------------------
Eve       | HR          | 45000
Bob       | Engineering | 60000
Alice     | Engineering | 75000
Diana     | Sales       | 70000
Charlie   | Sales       | 50000
```

**James:** That’s pretty cool! But I’m guessing there’s a catch, right?

**David:** Exactly. While it’s convenient, using column positions makes your query less readable. If the table schema changes, or someone else looks at your query, they might have a hard time figuring out what column `2` or `3` refers to. It’s usually better to use explicit column names for clarity.

**James:** I think I’ll stick to column names, but it’s good to know the shortcut! Thanks for explaining this so clearly.

**David:** Anytime, James. Let me know when you want to dive into more advanced query tricks!

---


### **Sorting by Expressions**

**David**: Did you know you can sort by expressions too?

Example: If you want to sort by years left until adulthood (18):

```sql
SELECT name, 18 - age AS years_to_adulthood
FROM students
ORDER BY years_to_adulthood;
```

---

### **Highlights**

1. Use `ORDER BY column_name` to sort results in ascending order by default.
2. Add `DESC` for descending order.
3. Sort by multiple columns by separating them with commas.
4. You can sort using expressions, calculated values, or aliases.
5. Column positions in `ORDER BY` start from 1, based on the columns in the `SELECT` list.
6. Using Column positions is a quick way to sort but can lead to less maintainable code.

---

### **Common Pitfalls**

1. **Default Sorting Confusion**: Forgetting that `ORDER BY` sorts in ascending order unless you specify `DESC`.
2. **Ambiguous Column Names**: If multiple tables are involved, qualify the column names to avoid errors.
3. **Null Values**: Remember that `NULL` values appear first in ascending order and last in descending order.(SQLite 3.30.0 added the NULLS FIRST and NULLS LAST options to the ORDER BY clause. The NULLS FIRST option specifies that the NULLs will appear at the beginning of the result set while the NULLS LAST option places NULLs at the end of the result set.)

---

### **Exercises for James**

1. Sort the `students` table by name in descending order.
2. Write a query to sort students by grade, then by age in ascending order.
3. Create a calculated column for the difference between `17` and the student’s age, and sort by this value in descending order.
4. Identify the impact of `NULL` values in sorting. Test it by adding a record with `NULL` for age and observing the result.


---

**James**: This makes my results so much clearer. Sorting by multiple columns is a game-changer!

**David**: Once you get the hang of `ORDER BY`, it’s hard to imagine working without it. Sorting is essential for clarity and precision.

**James**: Thanks, David! Time to tackle those exercises.

---

### **References**

1. **[SQLite SELECT Query Documentation](https://www.sqlite.org/lang_select.html)**
2. **[SQL ORDER BY Tutorial - W3Schools](https://www.w3schools.com/sql/sql_orderby.asp)**
3. **[SQLite Sorting Techniques](https://www.sqlitetutorial.net/sqlite-order-by/)**
4. **[Version-of-sqlite-used-in-android](https://stackoverflow.com/questions/2421189/version-of-sqlite-used-in-android)**
5. **[android.database.sqlite in android reference doc](https://developer.android.com/reference/android/database/sqlite/package-summary)**
