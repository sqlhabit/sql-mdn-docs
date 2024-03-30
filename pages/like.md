---
published_at: 2024-03-30 11:45
slug: like
type: operator
name: LIKE
title: LIKE operator in SQL
description: LIKE operator in SQL is used to filter data based on specific text patterns.
keywords: SQL, LIKE, ILIKE
see_also_pages:
  - name: IS operator in SQL
    url: /mdn/is
---

`LIKE` is a powerful SQL operator used to filter text data based on a specific pattern.

Unlike the `=` operator, which looks for exact matches, `LIKE` allows you to use wildcards for more flexible searches.

## Syntax

Typeically, the `LIKE` operator is used in a `WHERE` clause to search for a specified pattern in a column.

There are two wildcards often used in conjunction with the `LIKE` operator:

- `%` represents zero, one, or multiple characters
- `_` represents a single character

### % wildcard

~~~pgsql
SELECT *
FROM users
WHERE email LIKE '%@gmail.com'
~~~

This query selects all users whose email ends with `@gmail.com`.

To find users whose name starts with 'J', you could use:

~~~pgsql
SELECT *
FROM users
WHERE
  first_name LIKE 'J%'
~~~

### _ wildcard

If you're looking for users with a specific email provider, but from different countries, here's a query with the `_` wildcard that does exactly that:

~~~pgsql
SELECT email
FROM users
WHERE
  email LIKE '%@boogle.__'
~~~

## Using LIKE for pattern matching

The `LIKE` operator is invaluable for when you're not exactly sure what you're looking for but know a pattern or part of the data. It's widely used for text search.

For instance, to find any book whose name contains 'World', regardless of where in the name 'World' appears, you would use:

~~~pgsql
SELECT *
FROM books
WHERE
  name LIKE '%World%'
~~~

:warning: Note that this query is case sensitive, meaning that it will filter out all books with a lower case "world" in their names.

{{compatibility}}

{{see_also}}
