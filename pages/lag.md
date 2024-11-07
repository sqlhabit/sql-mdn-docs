---
published_at: 2024-11-07 21:30
slug: lag
type: function.window
name: LAG
title: LAG() window function in SQL
description: The LAG() window function in SQL is used to access the value from a previous row in the same result set, based on a specific ordering.
keywords: SQL, window functions, LAG
compatibility: true
see_also_pages:
  - name: LEAD() window function in SQL
    url: /mdn/lead
---

The `LAG` window function in SQL is used to access the value from a previous row in the same result set, based on a specific ordering. It is commonly used for analyzing time series data, calculating changes between rows, or identifying trends.

## Syntax

The basic syntax of the `LAG` function includes the column to retrieve from the previous row, the offset (number of rows back to look), and a default value if the offset position does not exist.

~~~pgsql
SELECT LAG(column_name, *offset, *default) OVER (ORDER BY column_name)
FROM table_name
~~~
{: .js-no-run-query-link}

- **column_name**: The column from which the previous value will be accessed.
- **offset** (optional). Specifies the number of rows back to look. Defaults to 1 if not provided.
- **default_value** (optional). Provides a default value if the offset position does not exist (e.g., on the first row).

## Simple example

Imagine we have an app and we want to see how fast we're growing every day. Let's use a [CTE](/mdn/with-as){:target="_blank"} and the [`UNION`](/mdn/union){:target="_blank"} to generate a virtual table with daily numbers of signups:

~~~pgsql
WITH daily_users AS (
  SELECT '2024-11-08' AS date, 90 AS user_count
  UNION ALL
  SELECT '2024-11-09', 80
  UNION ALL
  SELECT '2024-11-10', 100
)

SELECT
  date,
  user_count,
  LAG(user_count) OVER (ORDER BY date ASC) AS previous_user_count
FROM daily_users
~~~

:mag: This query retrieves the previous `user_count` for every row. Since we have today's and yesterday's number of signup in one row now, it's easy to calculate the absolute or percentage difference between these numbers.

## Real example

Here's how this query would look like with a real `users` table:

~~~pgsql
WITH daily_users AS (
  SELECT
    created_at::date AS date,
    COUNT(*) AS user_count
  FROM users
  GROUP BY 1
)

SELECT
  date,
  user_count,
  LAG(user_count) OVER (ORDER BY date ASC) AS previous_user_count
FROM daily_users
~~~

:mag: Note that we had to aggregate and [count](/mdn/count){:target="_blank"} user records to get the same table as in our trivial example.

## Applications of the `LAG` window function

- **Time series analysis**. Compare consecutive numbers in time series and calculate absolute/percentage changes over time.
- **User analytics**. Detect changes in user behavior, such as device or location switches, by comparing consecutive entries.
- **Financial analysis**: Analyze stock prices, account balances, or sales by calculating the difference between consecutive values.

:bulb: The most typical use case for the `LAG` function is to look back one row, but sometime we must look more than one row. For example, 12 rows if we want to compare a number for a month with last year's number for the same month.

{{compatibility}}

{{see_also}}
