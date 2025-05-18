---
published_at: 2024-04-07 20:45
slug: coalesce
types:
  - function.conditional
name: COALESCE
title: COALESCE() function in SQL
description: The COALESCE() function in SQL is conditional function that allows you to return the first non-NULL value in a list of arguments.
keywords: SQL, COALESCE
see_also_pages:
  - name: CASE operator in SQL
    url: /mdn/case
---

The `COALESCE` function in SQL is a conditional function that allows you to return the first non-`NULL` value in a list of arguments. It's particularly handy in Data Analysis for dealing with missing data, default values, and data transformation tasks.

## Syntax

The basic syntax of the `COALESCE()` function is straightforward: you pass it a list of values, and it scans from left to right, returning the first value that is not `NULL`.

~~~pgsql
SELECT COALESCE(column1, column2, ..., 'default value')
~~~
{: .js-no-run-query-link}

## Using COALESCE() with text values

One common scenario where `COALESCE()` comes in handy is in handling user data that might be incomplete. For instance, consider a situation where you want to display a user's avatar, but some users might not have provided their avatar images.

Here's a query that returns either a specified user avatar or a default avatar as a fallback:

~~~pgsql
SELECT
  COALESCE(avatar_url, 'https://bit.ly/default-avatar') AS avatar_url
FROM profiles
~~~

## Using COALESCE() with numerical values

Another typical use case is in financial reporting or analysis, where missing values might be interpreted as zeros.

Imagine we've joined the `purchases` tables to `users` table via [`LEFT JOIN`](/mdn/left-join). We'll have a lot of `NULL` values for users without purchases.

If it's relevant for our analysis, we can prettify revenue data and report paid amount as 0 instead of `NULL`, maintaining the consistency and accuracy of your financial reports:

~~~pgsql
SELECT
  u.email,
  COALESCE(p.amount, 0) AS paid_amount
FROM users u
LEFT JOIN purchases p
  ON u.id = p.user_id
~~~

By using `COALESCE`, you can ensure that your query results remain meaningful and informative, even when dealing with incomplete data relationships.

The `COALESCE()` function does not belong to a group of pure text or mathematical functions, because it accepts arbitrary types of arguments. It's a pure spreadsheet/SQL function. Often it's referred to as a **conditional expression** and it's an absolute must-have in your Data Analysis and SQL toolbox.

{{compatibility}}

{{see_also}}
