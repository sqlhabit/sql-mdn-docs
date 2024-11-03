---
published_at: 2024-03-11 21:30
slug: except
type: operator
name: EXCEPT
title: EXCEPT operator in SQL
description: The EXCEPT operator in SQL is used to return unique rows from the first query that are not present in the result set of the second query.
keywords: SQL, operator, EXCEPT, sets
compatibility: true
see_also_pages:
  - name: EXCEPT ALL operator in SQL
    url: /mdn/except-all
  - name: UNION operator in SQL
    url: /mdn/union
  - name: UNION ALL operator in SQL
    url: /mdn/union-all
---

The `EXCEPT` operator in SQL is used to return unique rows from the first query that are not present in the second query.

The `EXCEPT` and other similar operators ([`UNION`](/mdn/union){:target="_blank"}, etc) are called **set operators** because they come from a branch of math called ["set theory"](https://en.wikipedia.org/wiki/Set_(mathematics)#Basic_operations){:target="_blank"}.

In terms of set theory, the `EXCEPT` operator implements the **difference** operation.

This `EXCEPT` operator is useful in identifying differences between two datasets, comparing changes, etc.

## Syntax

Let's see the `EXCEPT` operator in action. We don't need any tables to do that:

~~~pgsql
SELECT 1
EXCEPT
SELECT 2
~~~

We're subtracting a set of one record (`2`) from another set (`1`). There're no matching records, so we get the first set untouched.

When subtracting real tables, you need to make sure that the number and order of columns in the [`SELECT`](/mdn/select){:target="_blank"} statements is identical :warning:. Additionally, the data types of the columns being compared should match (otherwise an SQL server won't know how to subtract numbers from strings, for example).

Let's look at a more realistic example.

## Difference between analytics systems

Suppose we have a mobile and a webapp for our business. Both teams measure user activity by tracking events. Both teams use the same category/action approach to name event (a **category** could be **Checkout Page** and actions **Chose Payment Type** or **Entered Credit Card Details**).

If we want to find out the different between mobile and web events, we can use the `EXCEPT` operator:

~~~pgsql
SELECT category, action, name
FROM mobile_analytics.events
EXCEPT
SELECT category, action, name
FROM web_analytics.events
~~~

This query returns all events from `mobile_analytics.events` that do not have matching entries in `web_analytics.events` based on `event_id`, `category`, `action`, and `name`.

:mag: Note that we get unique events, because `EXCEPT` operator filters out duplicates.

## Emulating EXCEPT with LEFT JOIN

The `EXCEPT` operator was missing in older versions of MySQL database (it was added only in 2022). We can emulate the `EXCEPT` operator behavior using the [`LEFT JOIN`](/mdn/left-join){:target="_blank"}.

Let's start with a simple query that gives us all users who haven't created a profile:

~~~pgsql
SELECT id AS user_id
FROM users
EXCEPT
SELECT user_id
FROM profiles
~~~

Here's the alternative query using the `LEFT JOIN`:

~~~pgsql
SELECT DISTINCT u.id AS user_id
FROM users u
LEFT JOIN profiles p
  ON u.id = p.user_id
WHERE
  p.id IS NULL
~~~

We need 2 things for the trick to work:

1. After we joined the `profiles` table, we can filter out all matching records via `p.id IS NULL`.

2. In case users can create multiple profiles, we use the `DISTINCT` keyword to get only unique `user_id`-s in the final result set.

## Summary

- **Uniqueness**. The `EXCEPT` operator automatically removes duplicates in the result set. To retain duplicates, use the [`EXCEPT ALL`](/mdn/except-all){:target="_blank"} operator.
- **Column Alignment**. The number and order of columns in both `SELECT` queries must be the same.
- **LEFT JOIN approach**. We can always use `LEFT JOIN` to emulate the `EXCEPT` behaviour.

{{compatibility}}

{{see_also}}
