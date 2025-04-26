---
published_at: 2024-04-25 17:30
slug: how-to-emulate-split-part-function-in-mysql
type: misc
name: How to emulate split_part() function in MySQL
title: How to emulate split_part() function in MySQL
description: Learn how to split text in MySQL using the SUBSTRING_INDEX() function.
keywords: SQL, function, split text
compatibility: false
see_also_pages:
  - name: split_part() function in SQL
    url: /mdn/split-part
  - name: How to emulate split_part() function in BigQuery
    url: /mdn/how-to-emulate-split-part-function-in-bigquery
  - name: How to emulate split_part() function in SQLite
    url: /mdn/how-to-emulate-split-part-function-in-sqlite
---

In PostgreSQL, the `split_part()` function is a handy way to split a string on a delimiter and retrieve a specific part. Here's a simple example:

~~~pgsql
SELECT
  split_part(email, '@', 1) AS username,
  split_part(email, '@', 2) AS email_domain
FROM users
~~~

However, MySQL does not have a direct equivalent to `split_part()`. Instead, we can emulate its behavior using a combination of other string functions available in MySQL like `SUBSTRING_INDEX()`.

## Syntax

Here’s the basic idea:

* use `SUBSTRING_INDEX()` once to shorten the string up to the *nth* delimiter
* then use `SUBSTRING_INDEX()` again to retrieve the last part from the shortened string

Let's start by understanding the `SUBSTRING_INDEX()` function.

## What is SUBSTRING_INDEX()

Here's the basic syntax:

~~~pgsql
SELECT SUBSTRING_INDEX(string, delimiter, count)
~~~
{: .js-no-run-query-link}

The `SUBSTRING_INDEX()` function returns the substring from the string `str` before the `count` occurrence of the delimiter `delim`.

If `count` is positive, it returns everything to the left of the final delimiter (counting from the left).

If `count` is negative, it returns everything to the right of the final delimiter (counting from the right).

Here's a simple example:

~~~pgsql
SELECT SUBSTRING_INDEX('red,blue,green,yellow', ',', 2)
~~~
{: .js-no-run-query-link}

This returns `'red,blue'` — the first two parts before the second comma.

Another example:

~~~pgsql
SELECT SUBSTRING_INDEX('red,blue,green,yellow', ',', -1)
~~~
{: .js-no-run-query-link}

This returns `'yellow'` — the last part after the last comma.

## Emulating split_part()

Now, to emulate `split_part(string, delimiter, part_number)`, we can combine two calls to `SUBSTRING_INDEX()`.

General approach:

~~~pgsql
SELECT
  SUBSTRING_INDEX(
    SUBSTRING_INDEX(string_column, delimiter, part_number),
    delimiter,
    -1
  )
FROM table_name
~~~
{: .js-no-run-query-link}

Let's continue with our color example and extract the 2nd item from the list using the `split_part()` function:

~~~pgsql
SELECT split_part('red,blue,green,yellow', ',', 2)
--- blue
~~~

In MySQL, we emulate this:

~~~pgsql
SELECT
  SUBSTRING_INDEX(
    SUBSTRING_INDEX('red,blue,green,yellow', ',', 2),
    ',',
    -1
  )
~~~
{: .js-no-run-query-link}

The first call to `SUBSTRING_INDEX()` selects the first two parts `red,blue` and the second call with `-1` `count` argument selects the last part `blue`.

## Summary

* MySQL does not have a native `split_part()` function
* You can always emulate it using one or two calls to `SUBSTRING_INDEX()`

{{compatibility}}

{{see_also}}
