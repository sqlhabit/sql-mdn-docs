---
published_at: 2024-02-11 11:30
slug: union-all
type: operator
name: UNION ALL
title: UNION ALL operator in SQL
description: The UNION ALL operator in SQL is used to combine the result sets of two or more queries into a single result set.
keywords: SQL, operator, UNION ALL
compatibility: true
see_also_pages:
  - name: UNION operator in SQL
    url: /mdn/union
---

The `UNION ALL` operator in SQL is used to combine the result sets of two or more `SELECT` queries into a single result set. Unlike the [`UNION`](/mdn/union){:target="_blank"} operator, which removes duplicate rows, `UNION ALL` includes all rows, even if they are duplicates.

The `UNION ALL` operator is useful when you want to combine multiple tables or result sets without affecting the records. The only thing to keep in mind is that each `SELECT` statement within a `UNION ALL` query must have the same number of columns, and corresponding columns must have compatible data types.

:bulb: The `UNION` and other set operators come from the branch of math called ["set theory"](https://en.wikipedia.org/wiki/Set_(mathematics)#Basic_operations){:target="_blank"}.

## Syntax

The syntax for the `UNION ALL` operator involves specifying two or more `SELECT` statements that should be combined:

~~~pgsql
SELECT 1 AS id, 'foo@gmail.com' AS email
UNION ALL
SELECT 2, 'bar@gmail.com'
UNION ALL
SELECT 1, 'foo@gmail.com'
~~~

:bulb: Note how we skipped the `FROM` clause here and joined multiple rows. Combined with a [CTE](/mdn/with-as), we can easily generate temporary tables for testing:

~~~pgsql
WITH temp_users AS (
  SELECT 1 AS id, 'foo@gmail.com' AS email
  UNION ALL
  SELECT 2, 'bar@gmail.com'
  UNION ALL
  SELECT 1, 'foo@gmail.com'
)

SELECT *
FROM temp_users
~~~

## Merging data across systems

Suppose we want to merge analytics data from two versions of our app: mobile and web. Each platfrom collects its analytics data in the correspondent table: `mobile_analytics.events` or `web_analytics.events`.

Both platforms follow the same event notation a-la Google Analytics with **category** and **action** parameters (for example, an event could belong to a "AudioPlayer" category with "Play" and "Pause" actions).

Here's a query to combine both events into a single table for analysis:

~~~pgsql
SELECT category, action, created_at, 'mobile' AS platform
FROM mobile_analytics.events
UNION ALL
SELECT category, action, created_at, 'web' AS platform
FROM web_analytics.events
~~~

In this query, we get a list of all user events from both systems, without removing any duplicates. Now we can query this meta-table and compare platforms in a single query.

{{compatibility}}

{{see_also}}
