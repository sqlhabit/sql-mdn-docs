---
published_at: 2024-04-26 17:45
slug: how-to-emulate-split-part-function-in-bigquery
types:
  - misc
name: How to emulate split_part() function in BigQuery
title: How to emulate split_part() function in BigQuery
description: Learn how to split text in BigQuery using the SUBSTRING_INDEX() function.
keywords: SQL, function, split text
compatibility: false
see_also_pages:
  - name: split_part() function in SQL
    url: /mdn/split-part
  - name: How to emulate split_part() function in MySQL
    url: /mdn/how-to-emulate-split-part-function-in-mysql
  - name: How to emulate split_part() function in SQLite
    url: /mdn/how-to-emulate-split-part-function-in-sqlite
---

In PostgreSQL, the `split_part(string, delimiter, part)` function is a great tool to slice up a text value based on a separator. It takes three arguments: the full string, the separator character (or a string), and which part you want (1 for the first, 2 for the second, and so on).

Unfortunately, in BigQuery, there’s no direct `split_part()` function — but don’t worry! We can easily recreate its magic using the `SPLIT()` function and the `SAFE_OFFSET()` operator.

Let’s dive into it.

## Syntax

In BigQuery, to emulate `split_part()`, we use:

~~~pgsql
SELECT SPLIT(column_name, delimiter)[SAFE_OFFSET(index)]
FROM your_table
~~~
{: .js-no-run-query-link}

Here’s how it works:

- `SPLIT(text, delimiter)` is a function that breaks a string into an **array** based on the separator.
- `[SAFE_OFFSET(index)]` is an array operator that picks an element from that array safely (without throwing an error if the index doesn’t exist).

:warning: Keep in mind that BigQuery uses **zero-based indexing**! That means the first item is at position 0, the second is at position 1, etc. In other databases like PostgreSQL indexing starts from 1.

Let’s see each part in more detail.

## SPLIT() function

The `SPLIT()` function chops up a string into an array of parts:

~~~pgsql
SELECT SPLIT('apple,banana,cherry', ',')
~~~
{: .js-no-run-query-link}

Here's a result of this query:

| f0_                         |
|------------------------------|
| ["apple", "banana", "cherry"] |

Now all we have to do is to choose an element.

## SAFE_OFFSET() accessor

When you split a string into an array, you can grab elements with `SAFE_OFFSET(index)`. If you ask for an index that doesn’t exist, it will quietly return `NULL` instead of blowing up like the `OFFSET(index)` operator.

Example:

~~~pgsql
SELECT SPLIT('apple,banana,cherry', ',')[SAFE_OFFSET(1)]
~~~
{: .js-no-run-query-link}

Here's the final result:

| f0_    |
|--------|
| banana |

:mag: Notice we used `SAFE_OFFSET(1)` to get the second item, because counting starts from 0.

## Emulating split_part()

Suppose we have this table in PostgreSQL:

~~~pgsql
SELECT screen_resolution
FROM mobile_analytics.events
LIMIT 3
~~~

Here's some sample data:

| screen_resolution |
|--------------------|
| 1080x1920          |
| 750x1334           |
| 1440x2560          |

If we want to extract the width (the part before the "x") in PostgreSQL, we would write:

~~~pgsql
SELECT
  split_part(screen_resolution, 'x', 1) AS width
FROM mobile_analytics.events
~~~

To do the same thing in BigQuery, the query becomes:

~~~pgsql
SELECT
  SPLIT(screen_resolution, 'x')[SAFE_OFFSET(0)] AS width,
  SPLIT(screen_resolution, 'x')[SAFE_OFFSET(1)] AS height
FROM mobile_analytics.events
~~~
{: .js-no-run-query-link}

Boom! We get the width part and even the height in a single query.

## One more thing

What if the part we're trying to select doesn't exist? For example, we're splitting emails via `@` sign and we're trying to select the 3rd part.

:mag: PostgreSQL returns an empty string `''` if the part doesn’t exist, but BigQuery returns `NULL` — something to be careful about!

Here's the PostgreSQL example:

~~~pgsql
SELECT split_part('foo@bar.com', '@', 3)
--- The result is an empty string ''
~~~

Here's the same query in BigQuery:

~~~pgsql
SELECT SPLIT('foo@bar.com', '@')[SAFE_OFFSET(2)]
--- The result is NULL
~~~
{: .js-no-run-query-link}

## Quick Recap

It's fascinating how SQL syntax differs between popular databases. Make sure to check out how the `split_part()` function could be implemented [in SQLite](/mdn/how-to-emulate-split-part-function-in-sqlite) and [in MySQL](how-to-emulate-split-part-function-in-mysql) — it'll blow your mind and you'll for sure learn smth new.

{{compatibility}}

{{see_also}}
