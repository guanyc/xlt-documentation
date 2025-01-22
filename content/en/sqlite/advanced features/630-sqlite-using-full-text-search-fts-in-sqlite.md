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

title: "Sqlite Using Full Text Search Fts in Sqlite"
date: "2025-01-21 13:46:14+08:00"
lastmod: "2025-01-21 13:46:14+08:00"
draft: false

keywords: [sqlite3]
tags: [sqlite3]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

weight: 630
type: docs

featured_image:


---
### **Full-Text Search in SQLite**

---

**David (Mentor):** Hey James, today let’s talk about **Full-Text Search (FTS)** in SQLite. It’s a powerful feature that helps you search text data more efficiently. Have you ever worked with it?

**James (Student):** I’ve heard of FTS, but I’m not sure how it works or when I would use it. It sounds useful though!

**David:** It definitely is! FTS allows you to create searchable indexes for text data, making it super fast to search through large amounts of text. You know how SQL’s `LIKE` clause can be slow for big data, right?

**James:** Yeah, the `LIKE` operator isn’t the best for large datasets. It takes forever to search through everything.

**David:** Exactly. FTS solves that problem. It creates an index for your text columns and allows for much faster searching using special queries. SQLite offers a couple of FTS modules: **FTS3**, **FTS4**, and **FTS5**. Each version offers different features and improvements, but they all let you do quick full-text searches.

---

### **Creating an FTS Table**

**James:** So, how do I set up FTS in SQLite?

**David:** It’s pretty simple. You use the `CREATE VIRTUAL TABLE` statement with the `USING fts4` or `fts5` module. Here’s a basic example using **FTS4**:

```sql
CREATE VIRTUAL TABLE documents USING fts4(title TEXT, body TEXT);
```

This creates a virtual table named `documents` with two columns: `title` and `body`. You can store your documents in it, and SQLite will automatically build a full-text index for those columns.

---

### **Inserting Data into an FTS Table**

**James:** Okay, I created the table. Now, how do I insert data?

**David:** Just like any other table! You can insert your text data like this:

```sql
INSERT INTO documents (title, body)
VALUES ('SQLite Introduction', 'SQLite is a serverless, self-contained, and zero-configuration database engine.');
```

SQLite will index the text in the `title` and `body` columns to make searching faster.

---

### **Performing Full-Text Searches**

**James:** Now comes the fun part—searching! How do I perform a full-text search?

**David:** Easy. You use the `MATCH` operator. For example, if you want to search for documents that contain the word "SQLite" in the `body` column, you’d do:

```sql
SELECT * FROM documents WHERE body MATCH 'SQLite';
```

This will return all rows where the `body` column contains the word "SQLite." You can even use more advanced features, like **phrase search** or **wildcards**.

---

### **Advanced FTS Features**

**James:** That’s pretty neat. Are there any advanced features in FTS?

**David:** Yes! Here are a few:

1. **Phrase Search**: If you want to find exact phrases, you can put the phrase in quotes:

   ```sql
   SELECT * FROM documents WHERE body MATCH '"self-contained"';
   ```

   This will search for the exact phrase "self-contained" in the `body` column.

2. **Wildcard Searches**: You can use wildcards for more flexible searches:

   ```sql
   SELECT * FROM documents WHERE body MATCH 'SQLite*';
   ```

   This will match any word that starts with "SQLite."

3. **Boolean Operators**: You can combine search terms with AND, OR, and NOT:

   ```sql
   SELECT * FROM documents WHERE body MATCH 'SQLite AND database';
   ```

   This finds rows where both "SQLite" and "database" appear in the `body`.

---

### **Pitfalls to Watch Out For**

**James:** This seems pretty powerful, but are there any things I should watch out for when using FTS?

**David:** Good question! Here are a few common pitfalls:

1. **Performance with Large Text**: While FTS is much faster than using `LIKE`, it’s still not as fast as querying indexed numeric data. So, if you’re dealing with huge volumes of text, it could still slow down.

2. **Not All Columns are Indexed**: FTS only indexes the columns you specify. If you try to search columns that weren’t indexed, the search won’t work as expected.

3. **Case Sensitivity**: By default, searches are **case-insensitive** in FTS, but if you need case-sensitive searches, you need to configure it properly.

4. **Complex Queries**: FTS works great for basic text searches, but if you need advanced text analysis (like stemming or exact language matches), you might need to look into more sophisticated tools like **Elasticsearch** or **Apache Solr**.

**James:** So, it’s fast, but like any tool, it has limitations—especially when you get into huge text data.

---

### **Highlights of Full-Text Search**

**David:** Exactly! Let’s summarize the key points:

- **Speed**: FTS dramatically improves text search performance compared to `LIKE`.
- **Full-Text Indexing**: It automatically creates an index for your text columns.
- **Advanced Search Features**: You can perform phrase searches, wildcard searches, and combine terms with Boolean operators.
- **Simplicity**: You can get started with basic text search without needing additional tools.

---

### **Exercises to Try**

1. **Exercise 1**: Create a virtual table `books` with columns `title`, `author`, and `summary`. Use FTS to index them and perform a search for books with a specific author or keyword.
   
2. **Exercise 2**: Implement a wildcard search on a blog posts table and search for all posts containing a specific phrase.

3. **Exercise 3**: Create a more advanced search for a `documents` table using both **AND** and **NOT** operators. For example, find documents that mention "SQLite" but not "database".

4. **Exercise 4**: Benchmark FTS performance by comparing search times on a regular table with `LIKE` vs an FTS table with large text data.

---

### **References**

- [SQLite Full-Text Search (FTS) Documentation](https://www.sqlite.org/fts3.html)
- [SQLite FTS5 Documentation](https://www.sqlite.org/fts5.html)

---

### **Keywords**

- SQLite full-text search
- FTS4 and FTS5
- `CREATE VIRTUAL TABLE`
- `MATCH` operator
- Phrase search
- Wildcard search
- Boolean search
- Performance of FTS
- SQLite indexing
