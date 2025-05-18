---
published_at: 2024-03-28 21:10
slug: where
types:
  - clause
name: WHERE
title: WHERE clause in SQL
description: WHERE clause in SQL is used to specify conditions for filtering data.
keywords: SQL, WHERE
see_also_pages:
  - name: AND operator in SQL
    url: /mdn/and
  - name: OR operator in SQL
    url: /mdn/or
  - name: SELECT statement in SQL
    url: /mdn/select
  - name: FROM keyword in SQL
    url: /mdn/from
---

The `WHERE` clause in SQL is used for filtering records. It allows you to specify conditions that each row of the table must meet to make it to the result set (query result). This makes the `WHERE` clause essential for making any data analysis or data operation.

The `WHERE` clause can be used with any SQL statement: `SELECT`, `UPDATE`, `DELETE` or `INSERT`.

## Syntax

The basic syntax of a `WHERE` clause looks like this:

~~~pgsql
SELECT column1, column2
FROM table
WHERE condition
~~~
{: .js-no-run-query-link}

In such a query, SQL engine goes over every row inside the table and checks whether it satisfies the condition (when you hear "condition" it basically means a statement that returns either `TRUE` or `FALSE`).

The condition in the `WHERE` clause supports various operators such as `=`, `!=`, `<`, `>`, `LIKE`, `IN`, etc., to specify the criteria the data must meet.

We can also combine multiple filters using the [`AND`](/mdn/and) or [`OR`](/mdn/or) operators. Let's look at some examples.

## Filtering data with WHERE

### Using comparison operators

You can use comparison operators to filter data based on numeric comparison:

~~~pgsql
SELECT *
FROM transactions
WHERE
  amount_usd > 100
~~~
{: data-dataset-id="3"}

### String pattern matching with LIKE

The `LIKE` operator is used for pattern matching in string columns. You can use `%` as a wildcard character:

~~~pgsql
SELECT *
FROM users
WHERE
  email NOT LIKE '%@gmail.com'
~~~

### Filtering with multiple conditions

You can combine multiple conditions using `AND` and `OR` operators:

~~~pgsql
SELECT *
FROM users
WHERE
  country = 'us'
  AND age >= 21
~~~

Understanding and utilizing the `WHERE` clause effectively is a cornerstone of bulding an SQL habit – a state where we can type queries faster than English and answer any question with data.

Mastering the `WHERE` clause is essential for querying data, precise data analysis and manipulation.

{{compatibility}}

{{see_also}}
