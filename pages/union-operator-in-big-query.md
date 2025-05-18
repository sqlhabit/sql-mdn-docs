---
published_at: 2024-02-11 11:30
slug: union-operator-in-big-query
types:
  - misc
name: UNION operator in BigQuery
title: UNION operator in BigQuery
description: Learn how to use combine result sets in BigQuery with UNION and UNION ALL operators.
keywords: SQL, operator, UNION, BigQuery
compatibility: false
---

The `UNION` operator in SQL comes from a branch of math called ["set theory"](https://en.wikipedia.org/wiki/Set_(mathematics)#Basic_operations){:target="_blank"}.

By default, the `UNION` operator in SQL is used to combine the result sets of two or more queries into a single result set. The main feature of the `UNION` operator is that it removes duplicates from all unioned sets.

Unfortunately, the Google BigQuery's implementation of the `UNION` operator differs slightly from other databases. The `UNION` operator in BigQuery always requires another keyword:

* `ALL` for combining all records with duplicates
* `DISTINCT` for combining only records

That's the only difference. If you try running a query with a lone `UNION` operator you'll get an exception like this: `Syntax error: Expected keyword ALL or keyword DISTINCT but got keyword SELECT`. :boom:

## Unioning records with duplicates

Here's a BigQuery's syntax for using `UNION` operator to combine records with duplicates:

~~~pgsql
SELECT 1 AS id, 'foo@gmail.com' AS email
UNION ALL
SELECT 2, 'bar@gmail.com'
UNION ALL
SELECT 1, 'foo@gmail.com'
~~~

As you can see, BigQuery supports the [`UNION ALL`](/mdn/union-all){:target="_blank"} operator as all other databases.

## Unioning records without duplicates

The previous :point_up: query contains a duplicate. Now let's union all records, but this time we'll use the `DISTINCT` keyword for combining only unique records:

~~~pgsql
SELECT 1 AS id, 'foo@gmail.com' AS email
UNION DISTINCT
SELECT 2, 'bar@gmail.com'
UNION DISTINCT
SELECT 1, 'foo@gmail.com'
~~~

This is a workaround we have to do to union unique records in BigQuery. Good news – almost all other databases (except SQLite) support the `UNION DISTINCT` syntax as well.

## A case for unioning unique records

I like to think about the `UNION` operator like it's a vertical join operation. Normally, any `JOIN` operation joins the right table to the left "horizontally" (or vice verse). The `UNION` operator combines them "vertically" and stacks one set of records on top of the other.

The typical application is when we have multiple versions of the same table, like mobile and web analytics. Here's a union query that combines all types of mobile and web events:

~~~pgsql
SELECT category, action
FROM mobile_analytics.events
UNION
SELECT category, action
FROM web_analytics.events
~~~
