---
published_at: 2025-04-27 16:00
slug: how-to-emulate-date-part-function-in-bigquery
type: misc
name: How to emulate date_part() function in BigQuery
title: How to emulate date_part() function in BigQuery
description: Learn how to extract parts of a date or timestamp in BigQuery using EXTRACT().
keywords: SQL, date functions, date_part, BigQuery
compatibility: false
see_also_pages:
  - name: date_part() function in SQL
    url: /mdn/date-part
  - name: extract() function in SQL
    url: /mdn/extract
  - name: How to emulate date_part() function in MySQL
    url: /mdn/how-to-emulate-date-part-function-in-mysql
---

In PostgreSQL, the `date_part('part', source)` function is a handy way to pull out pieces of a date or timestamp — like the year, month, day, hour, etc.

But what about BigQuery? BigQuery doesn’t support `date_part()` directly — instead, it uses the `EXTRACT()` function, which does almost the same thing in a slightly different style.

Let’s dive in!

## Syntax

To emulate `date_part()` in BigQuery, you use the `extract` function:

~~~pgsql
SELECT extract(part FROM date_column)
FROM your_table
~~~
{: .js-no-run-query-link}

The `extract()` function has two params:

* **`part`** is what you want to pull out (like YEAR, MONTH, DAY, HOUR, MINUTE, etc)
* **`date_column`** is your date or timestamp part.

:mag: Note that we're using a slighly strange syntax for these two params: `part FROM date_column`. Typically, we'd expect a function to have its arguments separated by comma, but here we have an exception.

:bulb: The reason for such syntax is that the SQL committee (a group of people who designed the SQL language back in the 90s) wanted to avoid confusion between the two arguguments — what's argument is the part and what's the date column.

## extract() function

The `extract()` function lets you grab a specific part of a date or timestamp.

:bulb: The [`extract()` function](/mdn/extract) also works in PostgreSQL, Redshift, MySQL and Snowflake. It's a very common function and only SQLite lacks the support of `extract()`.

Here's how we can extract the year:

~~~pgsql
SELECT extract(YEAR FROM DATE '2025-04-27')
~~~

Result:

| f0_ |
|-----|
| 2025 |

The month:

~~~pgsql
SELECT extract(MONTH FROM DATE '2025-04-27')
~~~

Result:

| f0_ |
|-----|
| 4 |

Or the day from a date:

~~~pgsql
SELECT extract(DAY FROM DATE '2025-04-27')
~~~

Result:

| f0_ |
|-----|
| 27 |

## Common parts you can extract

Here are some of the most common parts you might want:

| Part    | Meaning                        |
|---------|---------------------------------|
| YEAR    | Year number (like 2025)         |
| MONTH   | Month number (1–12)             |
| DAY     | Day of month (1–31)             |
| HOUR    | Hour of the day (0–23)          |
| MINUTE  | Minute of the hour (0–59)       |
| SECOND  | Second of the minute (0–59)     |
| QUARTER | Quarter of the year (1–4)       |
| WEEK    | ISO week number (1–53)          |
| DAYOFWEEK | Day of the week (1=Sunday)    |

## Example with a real table

Let's look at user signup timestamps in the `users` table:

~~~pgsql
SELECT created_at
FROM users
LIMIT 3
~~~

Example rows:

| created_at           |
|-----------------------|
| 2024-03-05 15:20:30   |
| 2024-06-18 08:14:52   |
| 2025-01-01 00:00:00   |

If you want to extract the year in PostgreSQL:

~~~pgsql
SELECT date_part('year', created_at) AS year_created
FROM users
~~~

To do the same thing in BigQuery:

~~~pgsql
SELECT extract(YEAR FROM created_at) AS year_created
FROM users
~~~

Similarly, to get the month and day:

~~~pgsql
SELECT
  extract(MONTH FROM created_at) AS month_created,
  extract(DAY FROM created_at) AS day_created
FROM users
~~~
{: .js-no-run-query-link}

## One small difference to keep in mind

In PostgreSQL, `date_part()` returns a `double precision` number.
In BigQuery, `EXTRACT()` usually returns an **integer** (except for some special cases like fractional seconds).

This usually doesn’t matter, but if you're comparing results from both databases, now you know why one looks like `2025` and the other like `2025.0`.

## Quick Recap

Even though BigQuery doesn't have a native `date_part()` function, it’s super easy to get the same result with `EXTRACT()`.

Whenever you need to pull the year, month, day, or any other part from a date or timestamp — just `EXTRACT()` it!

{{compatibility}}

{{see_also}}
