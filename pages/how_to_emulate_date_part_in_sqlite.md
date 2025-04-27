---
published_at: 2025-04-27 18:00
slug: how-to-emulate-date-part-function-in-sqlite
type: misc
name: How to emulate date_part() function in SQLite
title: How to emulate date_part() function in SQLite
description: Learn how to extract parts of a date like year, month, or day in SQLite, similar to the date_part() function in PostgreSQL.
keywords: SQL, date_part, function, SQLite, PostgreSQL
compatibility: false
see_also_pages:
  - name: date_part() function in SQL
    url: /mdn/date-part
  - name: How to emulate date_trunc() function in BigQuery
    url: /mdn/how-to-emulate-date-part-function-in-bigquery
  - name: How to emulate date_trunc() function in MySQL
    url: /mdn/how-to-emulate-date-part-function-in-mysql
---

In PostgreSQL, the `date_part(field, source)` function lets you easily extract specific parts of a date or timestamp, like the year, month, day, hour, minute, and so on.

Example:

~~~pgsql
SELECT date_part('year', created_at) AS year
FROM users
~~~

But in SQLite, there is no `date_part()` function.
No worries! We can recreate this magic using the `strftime()` function available in SQLite.

Let’s dive into it.

## strftime() syntax

In SQLite, you can emulate `date_part()` like this:

~~~pgsql
SELECT strftime(format_string, date_column)
FROM your_table
~~~
{: .js-no-run-query-link}

Here’s the idea:

* **`format_string`** is a string that describes the formatting of the date/timestamp. You can use values like **`%Y`** (for year) or **`%m`** (for month).
* **date_column** is a date/timestamp column name or a value of type date/timestamp

Let's learn about `strftime()` first.

## strftime() in action

Let's see how the `strftime()` function works with a constant value. In that case, we don't even need a table to write a query:

~~~pgsql
SELECT strftime('%Y', '2024-04-27')
~~~
{: .js-no-run-query-link}

Result:

| strftime('%Y', '2024-04-27') |
|------------------------------|
| 2024                         |

Here are some useful format codes:

| Format Code | Description |
|-------------|-------------|
| **`%Y`** | year (like 2025) |
| **`%m`** | month (01 to 12) |
| **`%d`** | day of the month (01 to 31) |
| **`%H`** | hour (00 to 23) |
| **`%M`** | minute (00 to 59) |
| **`%S`** | second (00 to 59) |

Here's a more comple example that prints out date and time of a timestamp:

~~~pgsql
SELECT
  strftime('%Y-%m-%d %H:%M', created_at)
FROM users
LIMIT 3
~~~
{: .js-no-run-query-link}

## Emulating date_part()

As you can see, the `strftime()` function offers way more functionality that `date_part()`. Emulating `date_part()` boils down to formatting a specific part of the timestamp. Let's look at some examples.

:mag: One thing to keep in mind — `date_part()` function returns a numeric value, but the `strftime()` always returns a string.

### Extracting year

PostgreSQL:

~~~pgsql
SELECT date_part('year', created_at) AS year
FROM users
~~~

SQLite:

~~~pgsql
SELECT strftime('%Y', created_at) AS year
FROM users
~~~
{: .js-no-run-query-link}

### Extracting month

PostgreSQL:

~~~pgsql
SELECT date_part('month', created_at) AS month
FROM purchases
~~~

SQLite:

~~~pgsql
SELECT strftime('%m', created_at) AS month
FROM purchases
~~~
{: .js-no-run-query-link}

### Extracting day

PostgreSQL:

~~~pgsql
SELECT date_part('day', signup_date) AS day
FROM users
~~~

SQLite:

~~~pgsql
SELECT strftime('%d', signup_date) AS day
FROM users
~~~
{: .js-no-run-query-link}

### Extracting hour

PostgreSQL:

~~~pgsql
SELECT date_part('hour', created_at) AS hour
FROM web_analytics.pageviews
~~~

SQLite:

~~~pgsql
SELECT strftime('%H', created_at) AS hour
FROM web_analytics.pageviews
~~~
{: .js-no-run-query-link}

### Extracting minute

PostgreSQL:

~~~pgsql
SELECT date_part('minute', created_at) AS minute
FROM mobile_analytics.events
~~~

SQLite:

~~~pgsql
SELECT strftime('%M', created_at) AS minute
FROM mobile_analytics.events
~~~
{: .js-no-run-query-link}

## Quick Recap

Even though SQLite doesn’t have `date_part()` built-in like PostgreSQL, you can easily mimic it with `strftime()` and the right format codes.

Pretty cool, right? ✨

You might also want to check out how to emulate [date_trunc()](/mdn/date-trunc-in-sqlite) in SQLite for rounding timestamps instead of extracting parts.

{{compatibility}}

{{see_also}}
