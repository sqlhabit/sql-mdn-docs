---
published_at: 2024-10-31 11:30
slug: random
type: function.numeric
name: random
title: random() function in SQL
description: The random() function in SQL is used to generate a random floating-point number between 0 and 1.
keywords: SQL, math, function, random
compatibility: true
---

The `random()` function in SQL is used to generate a random floating-point number between 0 (inclusive) and 1 (exclusive). This function is highly useful in scenarios where randomness is required, such as sampling rows from a table, shuffling records aka random sorting, testing with dummy data, or creating randomized unique values.

## Syntax

The syntax for the `random()` function is straightforward, as it doesn’t require any arguments:

~~~pgsql
SELECT random()
~~~

:bulb: We skipped the `FROM` keyword since we don't need a table to call a simple scalar function. This is a great way to test other scalar functions (that return a single value).

## Generating random values

In practical use, `random()` is often combined with columns in a table to generate random values for each row. For example, to assign a random value to each user in the `users` table:

~~~pgsql
SELECT
  id,
  email,
  random() AS random_value
FROM users
~~~

## Generating random values in ranges

If an integer within a specific range is needed, we can use the `random()` function in combination with a range formula:

{:.js-mathjax}
  $\Large{RandomValue = floor(low + random() * (high - low + 1))}$

* [`floor()`](/mdn/floor){:target="_blank"} is a function that rounds down a number to the closest integer
* **high** is the highest number in your distribution (inclusive)
* **low** is the lowest number in your distribution (inclusive)

For example, here's a query that generates a random age for the `users` table:

~~~pgsql
SELECT
  id,
  email,
  floor(18 + random() * (100 - 18 + 1)) AS random_age
FROM users
~~~

## Shuffling rows with random()

The most common use case for the `random()` function is to shuffle records. For that we need to use the `random()` function as a sorting value:

~~~pgsql
SELECT *
FROM users
ORDER BY random()
~~~

## Sampling rows with random()

Now that we have shuffled records, we can retrieve a random subset of users from the `users` table with a `LIMIT` clause:

~~~pgsql
SELECT *
FROM users
ORDER BY random()
LIMIT 10
~~~

The `random()` function is an essential tool in SQL, providing flexibility in data sampling, testing, and generating random values for analysis.

{{compatibility}}

{{see_also}}
