---
published_at: 2024-11-07 21:30
slug: lead
types:
  - function.window
name: LEAD
title: LEAD() window function in SQL
description: The LEAD() window function in SQL is used to access the value from the following row in the same result set, based on a specific ordering.
keywords: SQL, window functions, LEAD
compatibility: true
see_also_pages:
  - name: LAG() window function in SQL
    url: /mdn/lag
---

The `LEAD` window function in SQL is used to access data from the following row within a result set, based on a specified order. It's particularly useful for calculating differences or observing changes between consecutive rows, such as tracking the next event for a user or comparing values across time periods.

## Syntax

The basic syntax for the `LEAD` function involves specifying the column to access from the next row and, optionally, an offset (number of rows to look ahead) and a default value to use if there are no more rows.

~~~pgsql
SELECT LEAD(column_name, *offset, *default) OVER (ORDER BY column_name)
FROM table_name
~~~
{: .js-no-run-query-link }

- **column_name**: The column from which the previous value will be accessed.
- **offset** (optional). Specifies the number of rows forward to look. Defaults to 1 if not provided.
- **default_value** (optional). Provides a default value if the offset position does not exist (e.g., on the last row).

## Example: Time between purchases

Suppose we want to look at user purchasing behaviour and calculate the time gap between each purchase. The `LEAD()` function allows us to pull the next purchase timestamp for every purchase and calculate the time difference:

~~~pgsql
SELECT
  user_id,
  created_at AS purchased_at,
  LEAD(created_at) OVER (PARTITION BY user_id ORDER BY created_at) AS next_purchased_at
FROM purchases
~~~

:mag: Note that we have to provide the `ORDER BY created_at` command to ensure the `LEAD()` function can deterministically produce the same value. Many databases will throw an exception if you miss the `ORDER BY` clause.

:mag: In this particular example, we had to partition purchases with the `PARTITION BY user_id` command to ensure we're looking only at each user's individual purchases.

## Applications of the `LEAD` window function

- **Time series analysis**. Compare consecutive numbers in time series and calculate absolute/percentage changes over time.
- **User analytics**. Detect changes in user behavior, such as device or location switches, by comparing consecutive entries.
- **Seasonality analysis.**. When working with weekly or monthly metrics, we may want to look multiple rows forward (like 12 months ahead) for comparison.

{{compatibility}}

{{see_also}}
