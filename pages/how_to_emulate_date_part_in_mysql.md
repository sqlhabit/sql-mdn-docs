---
published_at: 2025-04-26 19:15
slug: how-to-emulate-date-part-function-in-mysql
type: misc
name: How to emulate date_part() function in MySQL
title: How to emulate date_part() function in MySQL
description: Learn how to extract parts of dates in MySQL using the EXTRACT() function.
keywords: SQL, date_part, extract, MySQL
compatibility: false
see_also_pages:
  - name: date_part() function in SQL
    url: /mdn/date-part
  - name: date_trunc() function in SQL
    url: /mdn/date-trunc
  - name: How to emulate date_part() function in BigQuery
    url: /mdn/how-to-emulate-date-part-function-in-bigquery
---

In PostgreSQL, the `date_part(part, source)` function lets you pull out specific parts of a date or timestamp, like the year, month, day, or even hour.

Example in PostgreSQL:

~~~pgsql
SELECT date_part('year', created_at) AS year
FROM users
~~~

But MySQL doesn’t have a `date_part()` function. Instead, MySQL uses a different but very straightforward function called `EXTRACT()`.

Let’s dive in!

## Syntax

In MySQL, you use the `EXTRACT()` function like this:

~~~pgsql
SELECT EXTRACT(part FROM date_column)
FROM table_name
~~~
{: .js-no-run-query-link}

The idea is super simple:

* `part` is what you want to grab (like `YEAR`, `MONTH`, `DAY` , etc). :mag: Note that a `part` is not a string, but an SQL keyword — no quotes around it are necessary.
* `date_column` is your column or a timestamp value.

Let’s look closer at each aspect of the `EXTRACT()` function in MySQL.

## What is EXTRACT()

The `EXTRACT()` function does exactly what it says — it pulls out part of a date.

Here’s the basic syntax again:

~~~pgsql
SELECT EXTRACT(YEAR FROM '2025-04-26')
~~~
{: .js-no-run-query-link}

This would return:

| EXTRACT(YEAR FROM '2025-04-26') |
|---------------------------------|
| 2025                            |

Pretty neat, right?

Here’s another example — extracting the **month**:

~~~pgsql
SELECT EXTRACT(MONTH FROM '2025-04-26')
~~~
{: .js-no-run-query-link}

Result:

| EXTRACT(MONTH FROM '2025-04-26') |
|----------------------------------|
| 4                                |

:mag: Note another syntactic detail: both `part` and `date_column` aren't separated by comma. Instead, MySQL expects you to use `PART FROM SOURCE` syntax. Weird. :person_shrugging:

## Available parts you can extract

Here are some of the most common parts you can use with `EXTRACT()` in MySQL:

- `YEAR`
- `MONTH`
- `DAY`
- `HOUR`
- `MINUTE`
- `SECOND`
- `WEEK`
- `QUARTER`
- `DAYOFYEAR`
- `DAYOFWEEK`
- `MICROSECOND`

## Extracting parts from table columns

Suppose we have a table of user signups, and we want to find out the year and month of each signup.

Here’s our table:

~~~pgsql
SELECT signup_date
FROM users
LIMIT 3
~~~

Example data:

| signup_date |
|-------------|
| 2023-08-21  |
| 2024-01-15  |
| 2025-04-26  |

Now, to extract the **year** and **month** of each signup in MySQL:

~~~pgsql
SELECT
  EXTRACT(YEAR FROM signup_date) AS signup_year,
  EXTRACT(MONTH FROM signup_date) AS signup_month
FROM users
~~~
{: .js-no-run-query-link}

Result:

| signup_year | signup_month |
|-------------|--------------|
| 2023        | 8            |
| 2024        | 1            |
| 2025        | 4            |

Simple and clean! :boom:

## Extracting time parts

If you have a `timestamp` column like `created_at` in the `purchases` table, you can extract hour and minute like this:

~~~pgsql
SELECT
  EXTRACT(HOUR FROM created_at) AS hour,
  EXTRACT(MINUTE FROM created_at) AS minute
FROM purchases
~~~
{: .js-no-run-query-link}

This can be super helpful if you want to know at what time of day most purchases happen.

## One important thing :mag:

MySQL’s `EXTRACT()` always returns a **number**, not a string.

So if you need to do something like concatenating extracted parts into a text, you’ll need to cast or convert these numbers to text manually.

Example:

~~~pgsql
SELECT
  CONCAT(EXTRACT(YEAR FROM signup_date), '-', LPAD(EXTRACT(MONTH FROM signup_date), 2, '0'))
FROM users
~~~
{: .js-no-run-query-link}

This builds a nicely formatted `YYYY-MM` string from the signup date!

## Quick Recap

* In PostgreSQL, we use `date_part(part, source)`.
* In MySQL, we use `EXTRACT(part FROM source)`.
* It's almost the same idea, just a slightly different syntax.
* `EXTRACT()` in MySQL always returns a number.

{{compatibility}}

{{see_also}}
