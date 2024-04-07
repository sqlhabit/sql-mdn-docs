---
published_at: 2024-04-07 10:45
slug: min
type: function.aggregate
name: MIN
title: Aggregate function MIN() in SQL
description: The `MIN()` function in SQL is an aggregate function that returns the smallest value in a selected column.
keywords: SQL, MIN, aggregate function
see_also_pages:
  - name: Aggregate function MAX() in SQL
    url: /mdn/max
  - name: Aggregate function SUM() in SQL
    url: /mdn/sum
  - name: Aggregate function COUNT() in SQL
    url: /mdn/count
  - name: Aggregate function AVG() in SQL
    url: /mdn/avg
  - name: GROUP BY clause in SQL
    url: /mdn/group-by
---

The `MIN()` function in SQL is an aggregate function that returns the smallest value in a selected column. It is incredibly useful for data analysis, allowing you to quickly identify the minimum value in a dataset, which can be crucial for financial analysis, performance metrics, incident detection, etc.

## Syntax

To use the `MIN()` function, you simply need to include it in your `SELECT` statement, specifying the column you want to analyze.

~~~pgsql
SELECT MIN(column_name)
FROM table_name
~~~
{: .js-no-run-query-link }

For instance, to find the lowest price from a products table, your query would look like this:

~~~pgsql
SELECT MIN(price)
FROM products
~~~

:mag: In this query, `MIN()` looks like any scalar function (think pure math function that accepts a bunch of arguments and returns a value as a result), but it's actually acting on an aggregation – the entire table is our group.

## Using MIN() in complex queries

Most of the time, you'll use the `MIN()` function with the `GROUP BY` statement to find the minimum values within each group.

~~~pgsql
SELECT
  country,
  MIN(age)
FROM users
GROUP BY country
~~~

This query returns the lowest age for each user country. The same way we can aggregate revenue of marketing campaigns, revenue of countries, usage per app feature, etc.

## Finding the oldest record

Another great application of the `MIN()` function is looking up the oldest value in a table. That helps when we're exploring a new database and want to make sense of our data.

Here's a query that finds the signup timestamp of the very first user:

~~~pgsql
SELECT MIN(created_at)
FROM users
~~~

The `MIN()` function is a straightforward yet powerful tool in SQL, it's simply a must-have in your Data Analysis repertoire.

{{compatibility}}

{{see_also}}
