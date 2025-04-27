---
published_at: 2025-04-26 22:00
slug: date-part
type: function.timestamp
name: date_part
title: date_part() function in SQL
description: SQL date_part() function allows to extract a specific part (year, month, day, hour, etc.) from a timestamp or date.
keywords: SQL, date_part, timestamp, date
compatibility: true
see_also_pages:
  - name: date_trunc() function in SQL
    url: /mdn/date-trunc
  - name: How to emulate date_part() function in MySQL
    url: /mdn/how-to-emulate-date-part-function-in-mysql
  - name: How to emulate date_part() function in BigQuery
    url: /mdn/how-to-emulate-date-part-function-in-bigquery
  - name: How to emulate date_part() function in SQLite
    url: /mdn/how-to-emulate-date-part-function-in-sqlite
---

The `date_part()` function in SQL is used to extract a specific part (such as year, month, day, hour, etc.) from a date or timestamp value. It's a very handy function when you need to break down timestamps into smaller components for analysis or reporting.

## Syntax

The basic syntax of the `date_part()` function is:

~~~pgsql
SELECT date_part('part', source)
FROM table_name
~~~
{: .js-no-run-query-link }

- **part** is a string specifying the part of the date/time you want to extract. Common values are `year`, `month`, `day`, `hour`, `minute` and `second`.
- **source** is a column or a value of type `timestamp`, `date`, or `interval` from which we want to extract the part.

:mag: The `date_part()` function always returns a number. For example, `4` for any date in April if we want to extract a month, etc.

Here's a simple example:

~~~pgsql
SELECT
  signup_date,
  date_part('year', signup_date) AS signup_year
FROM users
LIMIT 10
~~~

This query extracts the **year** part from the `signup_date` column in the `users` table.

## Extracting month and day from timestamps

Suppose you want to find out in which month users have signed up:

~~~pgsql
SELECT
  date_part('month', signup_date) AS signup_month,
  COUNT(*)
FROM users
GROUP BY signup_month
ORDER BY signup_month
~~~

This query groups users by the month they signed up.

Or if you want to find the day of the month purchases were made:

~~~pgsql
SELECT
  date_part('day', created_at) AS purchase_day,
  COUNT(*)
FROM purchases
GROUP BY purchase_day
ORDER BY purchase_day
~~~

## Building more customized time-based analyses

Unlike [`date_trunc`](/mdn/date-trunc), which rounds down the timestamp to a certain granularity and returns that rounded timestamp, `date_part()` lets you simply *extract* a single part as a number. This makes it useful when you need to create custom reports, like calculating purchases by hour of the day:

~~~pgsql
SELECT
  date_part('hour', created_at) AS purchase_hour,
  COUNT(*)
FROM purchases
GROUP BY purchase_hour
ORDER BY purchase_hour
~~~

## Combining extracted parts

You can also combine multiple extracted parts to create custom labels. For instance, to show signups by year and month:

~~~pgsql
SELECT
  date_part('year', signup_date) || '-' || LPAD(date_part('month', signup_date)::int::text, 2, '0') AS year_month,
  COUNT(*)
FROM users
GROUP BY year_month
ORDER BY year_month
~~~

This concatenates the extracted year and month into a `YYYY-MM` format.

## Conclusion

The `date_part()` function is an essential tool when working with dates and times in SQL. Whether you want to group users by signup month, calculate peak purchase hours, or simply break down a timestamp into parts, `date_part()` gives you a simple and flexible way to do so.

Understanding how and when to use `date_part()` will significantly improve your ability to perform time-based analyses and create more detailed reports. :calendar:

{{compatibility}}

{{see_also}}
