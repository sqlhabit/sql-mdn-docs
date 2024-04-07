---
published_at: 2024-04-07 15:40
slug: inner-join
type: clause
name: INNER JOIN
title: INNER JOIN in SQL
description: INNER JOIN clause in SQL is used to combine rows from two or more tables, based on a relation between them.
keywords: SQL, INNER JOIN
see_also_pages:
  - name: LEFT JOIN in SQL
    url: /mdn/left-join
---

The `INNER JOIN` clause in SQL is a powerful tool used to combine rows from two or more tables, based on a related column between them. It is one of the most common types of joins used in SQL for querying relational databases, enabling the retrieval of related data stored across different tables.

## Syntax

The syntax for `INNER JOIN` involves specifying the tables to join and the condition upon which the join is based.

~~~pgsql
SELECT
  table1.*,
  table2.*
FROM table1
INNER JOIN table2
  ON table1.common_column = table2.common_column
~~~
{: .js-no-run-query-link }

You can shorted the `JOIN` clause by utilizing table aliases:

~~~pgsql
SELECT
  t1.*,
  t2.*
FROM table1 t1
INNER JOIN table2 t2
  ON t1.common_column = t2.common_column
~~~
{: .js-no-run-query-link }

For example, here's a query that joins the `users` table and the `purchases` table:

~~~pgsql
SELECT *
FROM users u
INNER JOIN purchases p
  ON u.id = p.user_id
~~~

:mag: The `INNER JOIN` is called **inner** because it'll return only the intersection between the two table, i.e. all records from both table where the **join condition** (`ON u.id = p.user_id`) is truthy (`TRUE`).

Here's a diagram that visualizes the `INNER JOIN` clause:

![INNER JOIN in SQL](https://github.com/sqlhabit/sql-mdn-docs/blob/main/images/inner_join.png?raw=true)

## One-to-one join using INNER JOIN

It's often the case that we have two tables with equal number of records. For example, users and profiles (there's only one profile for each user).

If we ever need to analyze something where we need data from both tables, we can use the `INNER JOIN` to create a result set containing records from both tables:

~~~pgsql
SELECT
  email,
  postal_code
FROM users u
INNER JOIN profiles p
  ON u.id = p.user_id
~~~

:mag: Note that the `email` column comes from the `users` table and the `postal_code` column comes from the `profiles` table. We don't need to specify table prefixes for unique column names.

## One-to-many join using INNER JOIN

Here's a query that joins users and their web pageviews:

~~~pgsql
SELECT *
FROM users u
INNER JOIN web_analytics.pageviews p
  ON u.id = p.user_id
~~~

## Joining with complex conditions

For every pair of rows, the join condition (`ON ...`) is evaluted into a single `TRUE` (records will make it to the `INNER JOIN` result set) or `FALSE` (this pair is skipped).

It means we can use other logical operators (that return `TRUE` or `FALSE`) to write more complex `JOIN` statements. Here's an example where we join non-refunded purchases to users:

~~~pgsql
SELECT *
FROM users u
INNER JOIN purchases p
  ON u.id = p.user_id
    AND p.refunded = FALSE
~~~

## Joining multiple tables

We can join multiple tables using the `INNER JOIN` clause for our research. For example, when analyzing user behaviour we might join users, profiles (to get postal codes) and purchases:

~~~pgsql
SELECT
  email,
  postal_code,
  pu.*
FROM users u
INNER JOIN profiles pr
  ON u.id = pr.user_id
INNER JOIN purchases pu
  ON u.id = pu.user_id
~~~

`INNER JOIN` clause is why relational databases are called **relational** – because we can join together related records from different tables.

Mastering the `INNER JOIN` clause is essential for anyone looking to perform comprehensive data analysis with SQL.

{{compatibility}}

{{see_also}}
