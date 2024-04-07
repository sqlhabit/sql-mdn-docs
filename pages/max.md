---
published_at: 2024-04-07 11:00
slug: max
type: function.aggregate
name: MAX
title: Aggregate function MAX() in SQL
description: The `MAX()` function in SQL is an aggregate function that returns the largest value in a selected column.
keywords: SQL, MIN, aggregate function
see_also_pages:
  - name: Aggregate function MIN() in SQL
    url: /mdn/min
  - name: Aggregate function SUM() in SQL
    url: /mdn/sum
  - name: GROUP BY clause in SQL
    url: /mdn/group-by
---

The `MAX()` function in SQL is an aggregate function that finds the maximum value in a column. This function is essential for Data Analysis, as it helps in identifying the highest value across a dataset, whether that's the highest sale in a day, the top performing marketing campaign, etc.

## Syntax

The syntax for the `MAX()` function is straightforward. You specify the function and the column you wish to find the maximum value for.

~~~pgsql
SELECT MAX(column_name)
FROM table_name
~~~
{: .js-no-run-query-link }

For example, to find the highest priced product, your query would be:

~~~pgsql
SELECT MAX(price)
FROM products
~~~

## Using MAX() in detailed analysis

Typically, the  `MAX()` function is utilized alongside `GROUP BY` statement. It allows us to identify maximum values within specific groups.

~~~pgsql
SELECT
  country,
  MAX(age)
FROM users
GROUP BY country
~~~

This query reports the highest age in each user country.

## The most recent record

The `MAX()` function comes in very handy for dataset exploration. To find the latest activity date in a dataset, `MAX()` can be applied to a timestamp column.

For example, here's a query that reports the timestamp of the latest purchase:

~~~pgsql
SELECT MAX(created_at)
FROM purchases
~~~

The `MAX()` aggregate function is critical in many scenarios: highlight top performers, peak sales, and other maximum values critical to business and research.

{{compatibility}}

{{see_also}}
