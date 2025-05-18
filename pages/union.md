---
published_at: 2024-02-11 11:30
slug: union
types:
  - operator
name: UNION
title: UNION operator in SQL
description: The UNION operator in SQL is used to combine the result sets of two or more queries into a single result set filtering out duplicates.
keywords: SQL, operator, UNION
compatibility: true
see_also_pages:
  - name: UNION ALL operator in SQL
    url: /mdn/union-all
---

The `UNION` operator in SQL is used to combine the result sets of two or more `SELECT` queries into a single result set. By default, `UNION` removes duplicate rows from the result.

:bulb: If you want to keep result sets intact, you need to use the [`UNION ALL`](/mdn/union-all){:target="_blank"} operator and it'll keep all duplicated rows.

The `UNION` operator is particularly useful when you need to merge similar data from different tables or queries. If `JOIN`-s combine tables "horizontally" (we're joining the right table to the left table), the `UNION` operator combines them "vertically" (the top result set and the bottom result set are stacked together).

:warning: To ensure compatibility of result sets, each `SELECT` statement within the `UNION` must have the same number of columns, and the data types of corresponding columns should be compatible.

:bulb: The `UNION` and other set operators come from the branch of math called ["set theory"](https://en.wikipedia.org/wiki/Set_(mathematics)#Basic_operations){:target="_blank"}.

## Syntax

The basic syntax of the `UNION` operator is as follows:

~~~pgsql
SELECT 1 AS id, 'foo@gmail.com' AS email
UNION
SELECT 2, 'bar@gmail.com'
~~~

:bulb: Note how we don't even need the `FROM` clause here and can join single constant rows. Combined with a [CTE](/mdn/with-as), we can easily generate temporary tables for testing:

~~~pgsql
WITH temp_users AS (
  SELECT 1 AS id, 'foo@gmail.com' AS email
  UNION
  SELECT 2, 'bar@gmail.com'
)

SELECT *
FROM temp_users
~~~

Let's see how the `UNION` operator removes duplicates:

~~~pgsql
SELECT 1 AS id, 'foo@gmail.com' AS email
UNION
SELECT 2, 'bar@gmail.com'
UNION
SELECT 1, 'foo@gmail.com'
~~~

The result set of this query :point_up: should contain only 2 unique rows.

:bulb: Go ahead and replace the `UNION` operator with the [`UNION ALL`](/mdn/union-all){:target="_blank"} and see the difference.

## Combining data from different sources

The `UNION` operator is helpful when you want to gather data from different sources that share common attributes.

For example, if you want a list of all actions taken by users from both the `mobile_analytics.events` and `web_analytics.events` tables, you could write:

~~~pgsql
SELECT action
FROM mobile_analytics.events
UNION
SELECT action
FROM web_analytics.events
~~~

We're relying on the deduplicating feature of the `UNION` operator to get a unique list of actions from both the mobile and web analytics tables.

{{compatibility}}

{{see_also}}
