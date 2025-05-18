---
published_at: 2024-03-11 21:30
slug: except-all
types:
  - operator
name: EXCEPT ALL
title: EXCEPT ALL operator in SQL
description: The EXCEPT ALL operator in SQL is used to return all rows from the first query that are not present in the result set of the second query without deduplication.
keywords: SQL, operator, EXCEPT ALL, sets
compatibility: true
see_also_pages:
  - name: EXCEPT operator in SQL
    url: /mdn/except
  - name: UNION operator in SQL
    url: /mdn/union
  - name: UNION ALL operator in SQL
    url: /mdn/union-all
---

The `EXCEPT ALL` operator in SQL is used to return all records from the first query that are not found in the second query, including duplicates. Unlike the [`EXCEPT` operator](/mdn/except){:target="_blank"}, which removes duplicate rows, `EXCEPT ALL` preserves duplicate records in the results.

This operator is particularly useful when you need to analyze the exact differences between two datasets, even if some rows are repeated.

:bulb: If we look at it mathematically, the `EXCEPT ALL` operator is a difference between two sets of values. This and a couple of other operators ([`UNION`](/mdn/union){:target="_blank"}) come from a branch of math called ["set theory"](https://en.wikipedia.org/wiki/Set_(mathematics)#Basic_operations){:target="_blank"}.

## Syntax

The syntax for the `EXCEPT ALL` operator involves two `SELECT` statements. The first `SELECT` statement defines the primary dataset, and the second `SELECT` statement defines the dataset you want to exclude from the results.

Here's a simple query to demonstrate the `EXCEPT ALL` operator:

~~~pgsql
SELECT id AS user_id
FROM users
EXCEPT ALL
SELECT user_id
FROM profiles
~~~

:mag: It's important that each `SELECT` statement has the same number of columns and compatible data types to avoid errors.

This query gives us `user_id`-s of all library entries (every time a user starts reading a book a `books_users` record is created) for free users.

## Understanding how `EXCEPT ALL` works

Let's build some trivial data sets with [CTE-s](/mdn/with-as){:target="_blank"} and see how `EXCEPT ALL` works in details.

~~~pgsql
WITH table1 AS (
  SELECT 1 AS id
  UNION ALL
  SELECT 1
  UNION ALL
  SELECT 2
), table2 AS (
  SELECT 1 AS id
  UNION ALL
  SELECT 2
)

SELECT *
FROM table1
EXCEPT ALL
SELECT *
FROM table2
~~~

:mag: Note how we've used another set operator [`UNION ALL`](/mdn/union-all){:target="_blank"} to combine multiple constant rows into a temporary table. This is a perfect way sandbox approach to learn any SQL operation. :rocket:

As you can see, we got the following result set:

| id |
|---|
| 1 |
{: .table-with-header }

:mag: It shows us that `EXCEPT ALL` removes one :warning: record from the `table1` for every matching record from the `table2`. All other duplicated records will make it to the final result set.

## `EXCEPT ALL` vs `JOIN`-s

As you can see, the `EXCEPT ALL` operator is quite tricky. It's hard to use it for real analysis, because columns in both sets must match.

It's more intuitive to use [`INNER JOIN`](/mdn/inner-join){:target="_blank"} or [`LEFT JOIN`](/mdn/left-join){:target="_blank"} to implement subtraction between tables.

If we want to see all users without profiles, we can easily do this via a `LEFT JOIN` and pull any columns into the final result set:

~~~pgsql
SELECT
  u.id,
  u.email
FROM users u
LEFT JOIN profiles p
  ON u.id = p.user_id
WHERE
  p.id IS NULL
~~~

{{compatibility}}

{{see_also}}
