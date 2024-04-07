---
published_at: 2024-03-29 09:45
slug: count
type: function.aggregate
name: COUNT
title: Aggregate function COUNT() in SQL
description: Aggregate function COUNT() in SQL is used to count records.
keywords: SQL, COUNT, aggregate function
see_also_pages:
  - name: GROUP BY clause in SQL
    url: /mdn/group-by
  - name: DISTINCT keyword in SQL
    url: /mdn/distinct
  -- name: Aggregate function MAX() in SQL
    url: /mdn/max
  - name: Aggregate function MIN() in SQL
    url: /mdn/min
  - name: Aggregate function SUM() in SQL
    url: /mdn/sum
  - name: Aggregate function AVG() in SQL
    url: /mdn/avg
---

The `COUNT()` function in SQL is an aggregate function that returns the number of rows that match a specified condition. It is one of the most frequently used functions for data analysis, as it helps in quantifying the number of entries in a database table or the number of entries that meet certain criteria.

## Syntax

The syntax for the `COUNT()` function is simple. It can be used to count all rows in a table or just those that satisfy a particular condition.

In this case, we're still aggregating and there's a group of records, but this group is literally the whole table.

~~~pgsql
SELECT COUNT(*)
FROM table_name
~~~
{: .js-no-run-query-link }

To count rows for groups of records (aka aggregate), we need to use the [`GROUP BY` clause](/mdn/group-by):

~~~pgsql
SELECT
  column_name,
  COUNT(*)
FROM table_name
GROUP BY column_name
~~~
{: .js-no-run-query-link }

## Using COUNT() for data analysis

### Counting all rows

To determine the total number of rows in a table, use the `COUNT(*)` syntax. This counts all rows, regardless of NULL values or duplicates:

~~~pgsql
SELECT COUNT(*)
FROM purchases
~~~

### Counting non-NULL values

`COUNT(column_name)` is used to count all non-NULL values in a specific column:

~~~pgsql
SELECT COUNT(avatar_url)
FROM profiles
~~~

This example counts all users who have uploaded their avatar.

### Counting distinct values

To count the number of unique values in a column, use `COUNT(DISTINCT column_name)`:

~~~pgsql
SELECT COUNT(DISTINCT country)
FROM users
~~~

This query counts the number of unique user countries.

### Counting with GROUP BY

The most frequent use case for the aggregate `COUNT()` function is to count records for groups (aka cohorts) of users. We can break our dataset into groups using the [`GROUP BY` clause](/mdn/group-by):

~~~pgsql
SELECT
  country,
  COUNT(*) AS user_count
FROM users
GROUP BY country
~~~

## Practical applications of COUNT()

The `COUNT()` function is essential for data analysis, offering insights into the volume of data, the completeness of datasets, and the distribution of data across categories (like country, age, marketing campaigns, etc).

Whether you're assessing user engagement, measuring inventory levels, or analyzing survey responses, `COUNT()` provides a foundational metric for quantitative analysis. Its versatility makes it a critical tool for generating reports, monitoring data quality, and conducting exploratory data analysis.

{{compatibility}}

{{see_also}}
