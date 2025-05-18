---
published_at: 2024-04-02 21:00
slug: date-trunc-in-sqlite
types:
  - misc
name: How to emulate date_trunc() function in SQLite
title: How to emulate date_trunc() function in SQLite
description: In this article, you'll learn how to emulate date_trunc() SQL function in SQLite and round up dates and timestamp to a specific precision.
keywords: SQL, date_trunc, function, SQLite, PostgreSQL
compatibility: false
see_also_pages:
  - name: date_trunc() function in SQL
    url: /mdn/date-trunc
---

SQLite, [unlike PostgreSQL](/mdn/date-trunc), does not have a built-in `date_trunc()` function. This function is used in PostgreSQL to truncate a date or timestamp to the specified precision (e.g., year, month, day, hour, etc). However, you can emulate this functionality in SQLite using its `date()` and `strftime()` functions.

## Understanding date_trunc() in PostgreSQL

In PostgreSQL, `date_trunc()` is used to truncate a date or timestamp to a specific component, such as 'year', 'month', 'day', 'hour', etc. This is particularly useful for aggregating data over different time periods.

~~~pgsql
SELECT date_trunc('month', timestamp '2024-04-15 14:42:51')
~~~

This query truncates the date to the first day of the month, returning `2024-04-01 00:00:00`. Now we can use this rounded timestamp for aggregating records and building a monthly timeline.

## Emulating date_trunc() in SQLite

Since SQLite does not support `date_trunc()` directly, we can use the SQLite's `date()` function to achieve similar results. For example, to truncate a date to the start of the month, you can use:

~~~pgsql
SELECT date(column_name, 'start of month')
FROM table_name
~~~
{: .js-no-run-query-link }

This returns the date of the first day of the month as a string (like `2018-05-01`) for each date in the `column_name`.

### Truncating to the start of the year

Similarly, to get the start of the year in SQLite, you can do:

~~~pgsql
SELECT date(column_name, 'start of year')
FROM table_name
~~~
{: .js-no-run-query-link }

As in the previous example, we'll get a string like `2018-01-01` that points to the Jan, 1st of every year from the `column_name`.

### Truncating to the start of the day

Truncating to the start of the day is straightforward in SQLite, as the `date()` function without time part does this by default:

~~~pgsql
SELECT date(your_date_column)
FROM table_name
~~~
{: .js-no-run-query-link }

This query is simply the shorter version of this one:

~~~pgsql
SELECT date(your_date_column, 'start of day')
FROM table_name
~~~
{: .js-no-run-query-link }

It returns the string that follows the `%Y-%m-%d` format, like `2018-12-28`.

### Truncating to hour/minute/second with strftime()

To truncate a timestamp value to the hour in SQLite, you can use the `strftime(format, timestamp)` function.

This function formats a date according to the specified format. Here's the available placeholders for the format: `%Y-%m-%d %H:%M:%S`. By nullifying or removing some of them, you can effectively truncate your timestamp to a specific precision like we did with the `date()` function previously.

Here's an example of truncating a timestamp to the hour:

~~~pgsql
SELECT strftime('%Y-%m-%d %H:00:00', created_at)
FROM users
~~~
{: .js-no-run-query-link }

To truncate to minutes, we'll have to nullify only the seconds part:

~~~pgsql
SELECT strftime('%Y-%m-%d %H:%M:00', created_at)
FROM users
~~~
{: .js-no-run-query-link }

## Conclusion

Even though SQLite does not have a `date_trunc()` function like PostgreSQL, you can still perform similar date truncations using SQLite's date and time functions. This allows for flexible data analysis and reporting directly within SQLite.

{{compatibility}}

{{see_also}}
