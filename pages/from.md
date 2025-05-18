---
published_at: 2024-03-26 20:15
slug: from
types:
  - keyword
name: FROM
title: FROM keyword in SQL
description: FROM keyword in SQL is used to specify the source table(s) from which to retrieve data.
keywords: SQL, FROM keyword
compatibility: true
see_also_pages:
  - name: SELECT statement in SQL
    url: /mdn/select
  - name: WITH..AS clause in SQL
    url: /mdn/with-as
---

The `FROM` keyword in SQL is used to specify the source table (sometimes multiple tables) from which to retrieve data. It's an essential part of pretty much all queries, as it determines where the database system should look for the specified columns and records.

## Syntax

The basic syntax for the `FROM` clause is straightforward. You simply follow the `SELECT` keyword and the columns you wish to retrieve with the `FROM` keyword, and then specify the table name:

~~~pgsql
SELECT id, email, first_name
FROM users
~~~

## Joining Tables

One of the powerful features of SQL is the ability to join tables. The `FROM` clause can be used in conjunction with various types of joins (such as `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, and `FULL JOIN`) to combine rows from two or more tables based on a related column between them.

## Specifying Multiple Tables

You can also specify multiple tables in the `FROM` clause. This will create a [Cartesian product](https://en.wikipedia.org/wiki/Cartesian_product) of the tables specified (i.e., every combination of rows from the first table with every row of the second table).

~~~pgsql
SELECT *
FROM table1, table2
~~~
{: .js-no-run-query-link}

However, this approach is less common as it often produces a very large number of rows and is typically not what you want. Joins are a more efficient way to retrieve data from multiple tables.

Let's create a couple of small [CTE-s](/mdn/with-as) to demonstarte the effect of the `FROM` clause with multiple tables:

~~~pgsql
WITH letters AS (
  SELECT 'a' AS letter
  UNION
  SELECT 'b'
  UNION
  SELECT 'c'
), numbers AS (
  SELECT '1' AS number
  UNION
  SELECT '2'
  UNION
  SELECT '3'
)

SELECT *
FROM letters, numbers
~~~

## Using FROM with subqueries

The `FROM` clause can also include a subquery, effectively treating the result set of the subquery as a temporary table that can be selected from.

~~~pgsql
SELECT *
FROM (
  SELECT *
  FROM users
  WHERE
    status = 'customer'
) AS customers
~~~

Unless you're [using an old MySQL version](/mdn/common-table-expressions-in-mysql), the [Common Table Expressions (CTE-s)](/mdn/with-as) are a way superior way of strucutring such subqueies.

## Query without FROM

It's possible to write an entire query without a `FORM` clause. This is very handy when you want to play with SQL functions without using data from any table:

~~~pgsql
SELECT abs(-7.5)
~~~


{{compatibility}}

{{see_also}}
