---
published_at: 2024-04-13 07:40
slug: left
type: function.text
name: left
title: left() function in SQL
description: The left() function in SQL is used to extract a specified number of characters from the beginning of a string.
keywords: SQL, left, function
see_also_pages:
  - name: right() function in SQL
    url: /mdn/right
  - name: substring() function in SQL
    url: /mdn/substring
  - name: lower() function in SQL
    url: /mdn/lower
---

The `left()` function in SQL is used to extract a specified number of characters from the beginning of a string. This function is particularly useful for data cleaning, substring extraction, and when working with standardized formats where the significance of characters is position-dependent.

## Syntax

The syntax for the `left()` function is simple:

~~~pgsql
SELECT left(string, number)
~~~
{: .js-no-run-query-link }

This function takes two arguments: the string from which to extract characters, and the number of characters to extract from the left.

Here's a basic example without any table data:

~~~pgsql
SELECT left('foobar', 3)
~~~

## Using `left()` in practice

Suppose you have a table with full names of individuals, but you only need to retrieve the first three letters of each name for an initial-based identification system. You could use the `left()` function as follows:

~~~pgsql
SELECT left(first_name, 3) AS initials
FROM users
~~~

This query extracts the first three characters from the `full_name` column and labels the result as `initials`.

## Combining `left()` with other functions

`left()` can be effectively combined with other SQL functions to perform more complex string manipulations. For example, if we want to make sure that the initials from the previous example are always in the lowercase, we can use combine `left()` with the [`lower()`](/mdn/lower) function:

~~~pgsql
SELECT lower(left(first_name, 3)) AS initials
FROM users
~~~

## Extracting prefix with `left()`

Sometimes, a single text column might contain multiple strings concatenated together and we need to split them for analysis.

For example, if we know that our marketing campaign names always start with a launch date (8 digits), we can extract it like so using `left()`:

~~~pgsql
SELECT left(utm_campaign, 8)
FROM marketing_spends
~~~

The `left()` function is an essential tool for text processing in SQL, enabling efficient substring extraction and playing a critical role in preparing and formatting string data.

{{compatibility}}

{{see_also}}
