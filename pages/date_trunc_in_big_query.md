---
published_at: 2024-04-02 21:50
slug: date-trunc-in-bigquery
type: misc
name: How to use date_trunc() function in BigQuery
title: How to use date_trunc() function in BigQuery
description: In this article, you'll learn how to use date_trunc() SQL function in BigQuery and truncate dates and timestamp to a specific precision.
keywords: SQL, date_trunc, function, BigQuery, PostgreSQL
compatibility: true
see_also_pages:
  - name: date_trunc() function in SQL
    url: /mdn/date-trunc
---

BigQuery, Google Cloud's enterprise data warehouse, supports SQL for querying data, though BigQuery SQL syntax differs from traditional SQL databases like PostgreSQL.

BigQuery has the `date_trunc()` function, but the syntax differs a little bit from PostgreSQL.

## Syntax

In PostgreSQL, `date_trunc()` allows truncation of a date or timestamp to a specified precision, such as year, month, day, hour, minute, etc. Here's an example in PostgreSQL:

~~~pgsql
SELECT date_trunc('month', timestamp '2024-04-15 14:42:51')
~~~

In BigQuery, you can achieve similar results using the `date_trunc()` function for dates, and `timestamp_trunc()` for timestamps.

## Truncate to year using timestamp_trunc() and date_trunc()

To truncate a date to the first day of its year in BigQuery:

~~~pgsql
SELECT
  date_trunc(created_at, YEAR) AS signup_year,
  *
FROM users
~~~
{: .js-no-run-query-link }

This query returns the first day of the year for the `created_at` timestamps and nullified hours, minutes and seconds like this: `2018-01-01T00:00:00.000Z`.

If we pass a date column as the first argument of the `date_trunc()` function, we'll get the date back as well:

~~~pgsql
SELECT
  date_trunc(signup_date, YEAR) AS signup_year,
  *
FROM users
~~~
{: .js-no-run-query-link }

This query will return the `signup_year` column as date, like `2018-01-01`.

The `timestamp_trunc()` will behave the same for our use case, but regardless of date or timestamp input, it'll always return a timestamp `signup_year` result like `2018-01-01T00:00:00.000Z`:

~~~pgsql
SELECT
  timestamp_trunc(signup_date, YEAR) AS signup_year,
  *
FROM users
~~~
{: .js-no-run-query-link }

:bulb: The rule of thumb is simple – use `date_trunc()` for truncating date columns and `timestamp_trunc()` for timestamps.

## Truncate to month

To truncate a timestamp to the month (it'll round the timestamp to the first day of the month) in BigQuery, we simply need to use the `MONTH` precision in `timestamp_trunc()`:

~~~pgsql
SELECT
  timestamp_trunc(created_at, MONTH) AS signup_month,
  *
FROM users
~~~
{: .js-no-run-query-link }

The same applies for the `date_trunc()` function:

~~~pgsql
SELECT
  date_trunc(signup_date, MONTH) AS signup_month,
  *
FROM users
~~~
{: .js-no-run-query-link }

We're using the `timestamp_trunc()` function for the `created_at` timestamp column and get a rounded timestamp as a return, like `2018-04-01T00:00:00.000Z`.

In the second example, the `date_trunc()` function is used for the date `signup_date` column and we get dates as `2018-04-01` in the result set.

While BigQuery's syntax and functions may differ from PostgreSQL, the underlying principles of SQL remain the same – truncating/rounding functions typically receive 2 arguments (value and precision). Mastery of the date and time functions in BigQuery (and in other analytical DBs) is essential for your data analysis game and reporting, allowing you to derive more insightful conclusions from the temporal data.

{{compatibility}}

{{see_also}}
