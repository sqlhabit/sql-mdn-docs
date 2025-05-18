---
published_at: 2024-11-01 10:40
slug: sum-window-function
types:
  - function.window
name: SUM
title: SUM() window function in SQL
description: The SUM() window function in SQL is used to calculate cumulative totals over a set of rows.
keywords: SQL, window functions, SUM
compatibility: true
see_also_pages:
  - name: Aggregate function SUM() in SQL
    url: /mdn/sum
---

The `SUM()` window function in SQL calculates cumulative totals within a specified window of rows, making it different from the standard [`SUM()` aggregate function](/mdn/sum){:target="_blank"} that provides a total for an entire dataset.

By using `SUM()` as a window function, you can calculate running totals or partitioned totals. For example, track cumulative revenues over time, etc.

## Syntax

The basic syntax of the `SUM()` window function involves specifying the column to sum and applying an optional `PARTITION BY` or `ORDER BY` clause to define the scope or ordering of the window.

Here's the function definition:

~~~pgsql
SELECT SUM(column_name) OVER ([PARTITION BY column_name] [ORDER BY column_name])
FROM table_name
~~~
{: .js-no-run-query-link }

:mag: Note that if we skip `PARTITION BY` clause, the whole table becomes a "window". You'll see that this is a key to calculating percentages from total.

## Using `SUM()` to calculate percentage from total

One of the most common applications of the `SUM()` window function is to simplify percentage calculations. Imagine we want to count users per country, but also display percentages.

To achieve this, we can use 2 aggregate functions to count users per country and count total amount of users. Such query quickly becomes overcomplicated. Take a look at the window function approach:

~~~pgsql
WITH countries_stats AS (
  SELECT
    country,
    COUNT(*) AS user_count
  FROM users
  GROUP BY 1
)

SELECT
  *,
  100.0 * user_count / SUM(user_count) OVER () AS user_count_pct
FROM countries_stats
ORDER BY 3 DESC
LIMIT 5
~~~

:mag: By using a plain `OVER ()` clause, we effectively counting all users with `SUM(user_count)` over the entire `countries_stats`.

## Using `SUM()` with partitioning

By adding a `PARTITION BY` clause, we can calculate the sum within each specific partition. For example, we can calculate total sales per user for every purchase:

~~~pgsql
SELECT
  id AS purchase_id,
  user_id,
  amount,
  SUM(amount) OVER (PARTITION BY user_id) AS user_total_sales
FROM purchases
~~~

## Using `SUM()` with partitioning and ordering

Adding an `ORDER BY` clause within the window function allows for a cumulative total that resets with each partition but follows a specified order within each partition. This can be useful for calculating running totals:

~~~pgsql
SELECT
  id,
  user_id,
  amount,
  created_at,
  SUM(amount) OVER (PARTITION BY user_id ORDER BY created_at) AS running_total
FROM purchases
~~~

:mag: In this query :point_up:, each user’s purchases are summed in chronological order, creating a cumulative spending history.

{{compatibility}}

{{see_also}}
