---
published_at: 2024-04-08 19:30
slug: having
type: clause
name: HAVING
title: HAVING clause in SQL
description: The HAVING clause in SQL is used together with the GROUP BY clause to filter groups based on aggregation results.
keywords: SQL, HAVING, GROUP BY
see_also_pages:
  - name: GROUP BY clause in SQL
    url: /mdn/group-by
  - name: AND operator in SQL
    url: /mdn/and
  - name: OR operator in SQL
    url: /mdn/or
---

The `HAVING` clause in SQL is used together with the `GROUP BY` clause to filter groups based on a specified condition. Unlike the `WHERE` clause, which filters rows before the aggregation (using data already present in tables), the `HAVING` clause filters the results after the aggregation (using aggregated values).

One can survive without ever using the `HAVING` clause. The great benefit of using the `HAVING` clause is that it makes queries more concise and readable.

## Syntax

The `HAVING` clause comes right after the `GROUP BY` clause in a query and can use aggregate functions for conditions (unlike the `WHERE` clause).

Here is a basic example of using `HAVING` to filter groups:

~~~pgsql
SELECT
  country,
  COUNT(*)
FROM users
GROUP BY country
HAVING
  COUNT(*) > 100
~~~

The `HAVING` clause is executed last by the database engine. That allows us to aplly an additional filter to the final result set using an aggregated value (in that case, `COUNT(*) > 100`).

## HAVING vs CTE

Let's rewrite our example query :point_up: without the `HAVING` clause. To do that we'd have to rely on a [CTE](/mdn/with-as):

~~~pgsql
WITH country_users AS (
  SELECT
    country,
    COUNT(*) AS user_count
  FROM users
  GROUP BY country
)

SELECT *
FROM country_users
WHERE
  user_count > 100
~~~

It is exactly the same query, but it's a bit more bulky. The CTE approach always requires 2 steps – a subquery definition and then the main query with filters, etc. The `HAVING` clause allows us to save a CTE and do aggregate filtering right away.

## HAVING with multiple conditions

You can combine multiple conditions in the `HAVING` clause using the [`AND`](/mdn/and) and [`OR`](/mdn/or) logical operators. To find countries with more than 100 users but fewer than 1000 users:

~~~pgsql
SELECT
  country,
  COUNT(*)
FROM users
GROUP BY country
HAVING
  COUNT(*) > 100
  AND COUNT(*) < 1000
~~~

## HAVING vs WHERE

It's important to understand the difference between `HAVING` and `WHERE`:

`WHERE` filters rows before the grouping. The `WHERE` clause filtering happens before we get the result set, we're basically skipping records from the tables we're querying.

`HAVING` filters the result set after the grouping. You can think about it in 2 steps – first, the query without the `HAVING` clause is executed and we get a result set. Then the `HAVING` clause is applied to this intermediate result set.

In short, `HAVING` is applied to result set groups, not individual rows.

{{compatibility}}

{{see_also}}
