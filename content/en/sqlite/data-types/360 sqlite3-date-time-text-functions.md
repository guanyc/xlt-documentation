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

title: "Sqlite3 Date Time Text Functions"
date: "2025-01-09 11:17:59+08:00"
lastmod: "2025-01-09 11:17:59+08:00"
draft: false

keywords: [SQLite date and time functions,  SQLite datetime() example  ,Handling timezones in SQLite,  SQLite strftime() tutorial  ,SQLite date calculations  ,Format modifiers in SQLite , SQLite STRFTIME examples  ,SQLite DATE vs DATETIME  ,SQLite Julian Day calculations]

tags: [sqlite3]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

weight: 360
type: docs

featured_image:


---
### Speech: **Date and Time Functions in SQLite**

---

**Scene:** XiaoMing and James are sitting in a cozy café with their laptops open. James seems a bit frustrated as he stares at his screen.

---

**James:**  
Ugh, XiaoMing, I’m trying to build this feature that tracks when users log in and calculates how long they’ve been active. But this whole date and time thing is messing with my brain. SQLite isn’t exactly... intuitive here.

**XiaoMing:**  
(Laughs) Welcome to the world of date and time handling, James! It can be tricky at first, but SQLite actually has a pretty robust set of date and time functions. Wanna dive in?

**James:**  
Absolutely. I feel like once I crack this, my app will be unstoppable.

**XiaoMing:**  
Alright, so first, remember that SQLite doesn’t have a dedicated `DATE` or `TIME` data type. Instead, it stores date and time values as **text**, **real**, or **integer**. It all depends on how you want to represent the data.

**James:**  
Wait, so I can choose? That sounds... liberating but also terrifying.

**XiaoMing:**  
(Laughs) It’s not that bad. Let me break it down for you:

1. **TEXT** format stores date and time as ISO8601 strings, like `"2025-01-01 14:30:00"`.
2. **REAL** format stores the date as a Julian day number (used mainly in astronomical calculations).
3. **INTEGER** format stores the number of seconds since the Unix epoch (`1970-01-01 00:00:00 UTC`).

**James:**  
Cool, but when do I use which?

**XiaoMing:**  
It depends on your needs. If you want human-readable data, go for **TEXT**. If you’re doing math with dates or need precision, **REAL** or **INTEGER** might be better.

---

### **Common Date and Time Functions**

**XiaoMing:**  
Now let’s talk about SQLite’s built-in functions. Here are some of the most useful ones:

1. **`date()`**: Returns the date in the format `"YYYY-MM-DD"`.  
   Example:  
   ```sql
   SELECT date(); -- Returns today's date
   SELECT date('now'); -- Returns today's date
   ```

2. **`time()`**: Returns the current time in the format `"HH:MM:SS"`.  
   Example:  
   ```sql
   SELECT time('now'); -- Returns the current time
   ```

3. **`datetime()`**: Combines date and time in the format `"YYYY-MM-DD HH:MM:SS"`.  
   Example:  
   ```sql
   SELECT datetime('now'); -- Returns the current date and time
   ```

4. **`strftime()`**: Allows custom formatting for date and time values.  
   Example:  
   ```sql
   SELECT strftime('%Y-%m-%d %H:%M', 'now'); -- Custom format
   ```

5. **`julianday()`**: Returns the Julian day number.  
   Example:  
   ```sql
   SELECT julianday('now'); -- Julian day for the current time
   ```

6. **`unixepoch()`**: Converts a Unix timestamp to human-readable format.  
   Example:  
   ```sql
   SELECT datetime(1672531200, 'unixepoch'); -- Converts a Unix timestamp
   ```

7. **Add/Subtract Dates**: Use modifiers like `'+'` or `'-'` for adding/subtracting time.  
   Example:  
   ```sql
   SELECT date('now', '+7 days'); -- Date 7 days from now
   SELECT datetime('now', '-1 month'); -- Datetime one month ago
   ```

---

### **Examples in Action**

**James:**  
Alright, I think I’ve got it. Can we try some real examples?

**XiaoMing:**  
Sure thing! Here are a few:

1. **Getting the current date and time**  
   ```sql
   SELECT datetime('now');
   ```

2. **Calculating a user's subscription end date**  
   Let’s say the subscription is valid for 30 days:  
   ```sql
   SELECT date('now', '+30 days');
   ```

3. **Finding the day of the week for a specific date**  
   ```sql
   SELECT strftime('%w', '2025-01-01'); -- '0' for Sunday, '6' for Saturday
   ```

4. **Converting a Unix timestamp to a readable date**  
   ```sql
   SELECT datetime(1672531200, 'unixepoch');
   ```

5. **Time since a user’s last login**  
   ```sql
   SELECT datetime('now') - datetime('2025-01-01 12:00:00');
   ```


---

**Xiaoming**:  SQLite has a powerful date and time handling system, which uses text, integers, or real numbers to represent dates and times. But to manipulate and retrieve the data in different formats, you can use **format modifiers** with the built-in functions like `DATE()`, `TIME()`, `DATETIME()`, `JULIANDAY()`, and `STRFTIME()`.


### **More Examples,  Format Modifiers**  

Here’s how these functions work with examples, including the use of format modifiers:  


#### **1. Adding or Subtracting Time**  
You can add or subtract time intervals using keywords like `+` or `-` followed by the interval.  

```sql
SELECT DATE('2025-01-01', '+1 year'); -- Returns 2026-01-01
SELECT DATETIME('now', '-7 days');   -- Returns the date and time one week ago
SELECT TIME('12:00:00', '+3 hours'); -- Returns 15:00:00
```

**James**: So you can travel through time in SQLite?  

**Xiaoming**: (Laughs) Kind of. It’s handy for calculating deadlines or determining past and future dates.

---

#### **2. Start and End of the Month**  
SQLite can find the first or last day of a month.  

```sql
SELECT DATE('now', 'start of month'); -- Returns the first day of the current month
SELECT DATE('2025-02-15', 'start of month'); -- Returns 2025-02-01
SELECT DATE('2025-02-15', 'start of month', '+1 month', '-1 day'); -- Last day of the month
```

**James**: Cool! So with these modifiers, I can get the last day of any month?  

**Xiaoming**: Exactly! It’s great for billing cycles or recurring events.

---

#### **3. Day of the Week**  
You can adjust a date to a specific day of the week using `weekday`.  

```sql
SELECT DATE('2025-01-01', 'weekday 0'); -- Next Sunday after 2025-01-01
SELECT DATE('2025-01-01', 'weekday 1'); -- Next Monday
```

**James**: What if the date is already the target weekday?  

**Xiaoming**: Good question. SQLite skips to the *next* occurrence of that weekday.  

---

#### **4. Formatting Output with STRFTIME()**  
If you need to display dates or times in custom formats, `STRFTIME()` is your friend.  

```sql
SELECT STRFTIME('%Y-%m-%d', 'now'); -- Current date in YYYY-MM-DD format
SELECT STRFTIME('%H:%M:%S', 'now'); -- Current time in HH:MM:SS format
SELECT STRFTIME('%d-%b-%Y %H:%M:%S', 'now'); -- Custom format with abbreviated month
```

**James**: This is so helpful for making the data more readable!  

**Xiaoming**: Definitely. You can create any format you want by mixing the format specifiers.  

---

#### **5. Calculating Julian Days**  
Julian Day numbers are useful in astronomy and for certain calculations.  

```sql
SELECT JULIANDAY('2025-01-01'); -- Julian day for the given date
SELECT DATETIME(2451545.0, 'JULIAN'); -- Converts Julian day back to a readable date
```

**James**: Why would anyone use Julian days?  

**Xiaoming**: They’re great for calculating date differences or dealing with very old dates.  

---

#### **6. Combining Modifiers**  
You can chain multiple modifiers together to perform complex calculations.  

```sql
SELECT DATE('2025-01-01', '+1 year', '-9 months'); -- Correct way to add 1 year and subtract 9 months
SELECT DATETIME('now', '+1 day', 'start of month'); -- First day of next month
```

**James**: I like how you can stack these modifiers!  

---

### **Common Pitfalls**  

1. **Incorrect Format Strings**  
   If you use an invalid format string in `STRFTIME()`, SQLite won’t throw an error—it will simply return `NULL`. Always double-check your format strings.  

2. **Relying on `now` in Production**  
   The `now` keyword uses the local system’s time, which may lead to inconsistencies if the server’s time isn’t synchronized. For consistent results, store timestamps in UTC.  

3. **Adding Invalid Intervals**  
   Adding something like `'+15 months'` won’t work directly because SQLite doesn’t natively understand complex intervals. You’ll need to chain modifiers:  

   ```sql
   SELECT DATE('2025-01-01', '+1 year', '-9 months'); -- Correct way
   ```

---



### **Pitfalls to Watch Out For**

**XiaoMing:**  
Before you go all in, here are a few things to keep in mind:  

- **Timezones**: SQLite works with UTC by default. If you’re handling users in different time zones, you’ll need extra logic.  
- **Leap Years and Days**: Always double-check calculations that involve February 29th or daylight saving time changes.  
- **Human Readability**: If you’re storing dates as numbers, it might be confusing later when debugging.

1. **Incorrect Format Strings**:  
   If you use an invalid format string in `STRFTIME()`, SQLite won’t throw an error—it will simply return `NULL`. Always double-check your format strings.  

2. **Relying on `now` in Production**:  
   The `now` keyword uses the local system’s time, which may lead to inconsistencies if the server’s time isn’t synchronized. For consistent results, store timestamps in UTC.  

3. **Adding Invalid Intervals**:  
   Adding something like `'+15 months'` won’t work directly because SQLite doesn’t natively understand complex intervals. You’ll need to chain modifiers:  

   ```sql
   SELECT DATE('2025-01-01', '+1 year', '-9 months'); -- Correct way
   ```


---

### **Exercises**

**XiaoMing:**  
Okay, James, time to practice. Try these:

1. Get the date 90 days from today.  
2. Find the day of the week for `"2024-12-25"`.  
3. Convert the Unix timestamp `1700000000` into a readable date.  
4. Subtract 5 hours from the current time.  
5. Write a query to find how many days have passed since `"2025-01-01"`.
6. Display the last day of the current month using format modifiers.  
7. Format the current date as `YYYY/MM/DD`.  
8. Find the Julian Day for February 1, 2025.  
9. Write a query to calculate the next Friday after today’s date.  
---

### **Highlights**

- SQLite stores dates and times as `TEXT`, `REAL`, or `INTEGER`.  
- Use built-in functions like `date()`, `datetime()`, and `strftime()` for easy manipulation.  
- Be mindful of timezones, leap years, and data readability.

- Use `DATE()` for date-only calculations, `TIME()` for time-only, and `DATETIME()` for both.  
- `STRFTIME()` lets you format dates and times exactly how you want.  
- Format modifiers like `+`, `-`, and keywords like `weekday` or `start of month` make calculations powerful and concise.  
- Always store timestamps in UTC for consistency across systems.  

---

### **References**

1. [SQLite Date and Time Functions Documentation](https://www.sqlite.org/lang_datefunc.html)  
2. [ISO 8601 Date and Time Format](https://en.wikipedia.org/wiki/ISO_8601)  
3. [Working with Unix Timestamps](https://www.unixtimestamp.com/)  

---


**Featured Image**: Generating now!

The featured image above represents Xiaoming and James discussing SQLite date and time functions in a casual café setting, perfectly complementing the content. Let me know if you'd like further adjustments!