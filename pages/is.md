---
published_at: 2024-03-29 09:30
slug: is
types:
  - operator
name: IS
title: IS operator in SQL
description: IS operator in SQL is a logical operator for comparison values with TRUE/FALSE or NULL.
keywords: SQL, IS, operator
see_also_pages:
  - name: AND operator in SQL
    url: /mdn/and
  - name: OR operator in SQL
    url: /mdn/or
---

The `IS` operator in SQL is a logical operator that is used to compare a value with a boolean value (`TRUE`, `FALSE`), or with `NULL` to check if a value is `NULL`.

This operator is particularly useful in SQL for conditions where standard comparison operators might not suffice, especially when dealing with `NULL` values.

## Syntax

The basic syntax of the `IS` operator involves a column name followed by the `IS` keyword and then the value (`NULL`, `TRUE`, or `FALSE`):

~~~pgsql
SELECT column1, column2
FROM table_name
WHERE
  column1 IS NULL
~~~
{: .js-no-run-query-link }

## Using IS to check for NULL values

### Checking for NULL

One of the most common uses of the `IS` operator is to check for `NULL` values within a column:

~~~pgsql
SELECT *
FROM profiles
WHERE
  interests IS NULL
~~~

This query selects all user profiles who have not filled their interests.

### Checking for boolean values

`IS` can also be used to check for boolean values in a column:

~~~pgsql
SELECT *
FROM purchases
WHERE
  refunded IS FALSE
~~~

## Combining IS with NOT

The `IS` operator can be combined with `NOT` to check for non-matching conditions. Let's get back to our previous example and select profiles with interests:

~~~pgsql
SELECT *
FROM profiles
WHERE
  interests IS NOT NULL
~~~

## Practical applications of IS

The `IS` operator is essential for data integrity checks and ensuring data quality in SQL queries. It allows for precise identification of `NULL` values, which represent missing or unknown data, and boolean checks.

Whether you're cleaning data, preparing datasets for analysis, or ensuring accurate query results, the `IS` operator provides the necessary functionality to handle special SQL conditions effectively.

{{compatibility}}

{{see_also}}
