---
published_at: 2024-03-30 12:10
slug: in
types:
  - operator
name: IN
title: IN operator in SQL
description: IN operator in SQL
keywords: SQL, IN, operator
see_also_pages:
  - name: IS operator in SQL
    url: /mdn/is
  - name: AND operator in SQL
    url: /mdn/and
  - name: OR operator in SQL
    url: /mdn/or
---

`IN` is an SQL operator that is perfect for filtering for multiple values in a `WHERE` clause. If you want to match something in a list of possible values, the `IN` operator is the way to go.

You can achieve the same functionality by combining multiple [`OR`](/mdn/or) operators, but the `IN` operator syntax is way more concise.

## Syntax

The `IN` operator allows you to specify a list of values to compare with a column's value. If the column's value matches any one of the values in the list, the row is included in the result set.

Here's a basic example of its usage:

~~~pgsql
SELECT *
FROM users
WHERE
  country IN ('us', 'ca', 'au')
~~~

This query selects all users who are from the United States, Canada, or Australia.

## IN operator vs OR operator

The `IN` operator simplifies queries and makes them more readable, especially when filtering records by a column that can have multiple values. It's a cleaner approach than chaining many `OR` conditions together, which can make the SQL statement difficult to read and maintain.

For instance, instead of writing:

~~~pgsql
SELECT *
FROM books
WHERE
  category = 'Classic'
  OR category = 'Detective'
  OR category = 'Biography'
~~~

You can write:

~~~pgsql
SELECT *
FROM books
WHERE
  category IN ('Classic', 'Detective', 'Biography')
~~~

This makes your query more compact and easier to understand at a glance.

`IN` is a must-have tool in your Data Analysis SQL toolkit for writing simple, elegant queries.

{{compatibility}}

{{see_also}}
