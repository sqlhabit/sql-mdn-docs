---
published_at: 2024-03-23 12:00
slug: case
type: operator
name: CASE
title: CASE operator in SQL
description: CASE operator in SQL is used for a if-then-else control flow.
keywords: SQL, CASE, operator, if/else, conditions
compatibility: true
see_also_pages:
  - name: AND operator in SQL
    url: /mdn/and
  - name: OR operator in SQL
    url: /mdn/or
---

The `CASE` operator in SQL is a versatile control flow tool that allows you to perform if-then-else type logic directly within your SQL queries.

This functionality enables the dynamic transformation of data based on specific conditions, making it incredibly useful for creating calculated fields, custom sorting, or implementing conditional logic in data retrieval.

## Syntax

The `CASE` operator can be used in any statement that accepts a valid boolean expression (`TRUE`/`FALSE`), such as `SELECT`, `WHERE`, `ORDER BY`, and so on. Here's the basic `CASE` operator syntax:

~~~pgsql
SELECT
  CASE
    WHEN condition_1 THEN result_1
    WHEN condition_2 THEN result_2
    ...
    ELSE default_result -- Optional clause
  END AS alias_name
FROM table_name
~~~
{: .js-no-run-query-link}

## Applications of CASE

### Multi-line syntax

One of the most common uses of the `CASE` operator is within `SELECT` clauses, where it can dynamically calculate new columns in the result set based on certain conditions.

Here's an example query that calculates user language based on their account country:

~~~pgsql
SELECT
  id,
  email,
  CASE
    WHEN country = 'us' THEN 'english'
    WHEN country = 'de' THEN 'german'
    ELSE 'other'
  END AS user_language
FROM users
~~~

### One-line syntax

The `CASE` operator often comes handy when we need to derive a new status column from existing columns.

Here's an example from a subscription product where we calculate user access tier based on their subscription status column:

~~~pgsql
SELECT
  CASE WHEN status = 'customer' OR status = 'trial' THEN 'premium' ELSE 'free' END access_tier,
  *
FROM users
~~~

### Skipping the default value

The `ELSE` part (the default value when no conditions are matching) of the `CASE` operator is optional. We can rewrite the last query without it:

~~~pgsql
SELECT
  CASE WHEN status = 'customer' OR status = 'trial' THEN 'premium' END access_tier,
  *
FROM users
~~~

The default value of the `CASE` statement in this query will be `NULL`. Essentially, it's a shorter version of the following query:

~~~pgsql
SELECT
  CASE WHEN status = 'customer' OR status = 'trial' THEN 'premium' ELSE NULL END access_tier,
  *
FROM users
~~~

:bulb: Every `WHEN` clause is eventually evaluated into a single `TRUE` or `FALSE`, so we can use any combination of `AND`, `OR` or boolean functions.

{{compatibility}}

{{see_also}}
