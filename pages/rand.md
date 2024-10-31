---
published_at: 2024-10-31 11:30
slug: rand
type: function.numeric
name: rand
title: rand() function in SQL
description: The rand() function in SQL is used to generate a random floating-point number between 0 and 1.
keywords: SQL, math, function, random
compatibility: true
---

The `rand()` function in SQL is used to generate a random floating-point number between 0 (inclusive) and 1 (exclusive).

The `rand()` function is a "good" example of how database designers went different ways: in half of the modern databases this function is named `rand()` and in the other half [`random()`](/mdn/random){:target="_blank"}. Talking about engineers being lazy saving 2 characters from a function name. :smile:

## Syntax

The syntax for the `rand()` function is straightforward, as it doesn’t require any arguments:

~~~pgsql
SELECT rand()
~~~
{: .js-no-run-query-link}

:bulb: We skipped the `FROM` keyword since we don't need a table to call a simple scalar function. This is a great way to test other scalar functions (that return a single value).

## Generating random values

In practical use, `rand()` is often combined with columns in a table to generate random values for each row. For example, to assign a random value to each user in the `users` table:

~~~pgsql
SELECT
  id,
  email,
  rand() AS random_value
FROM users
~~~
{: .js-no-run-query-link}

## Generating random values in ranges

If an integer within a specific range is needed, we can use the `rand()` function in combination with a range formula:

{:.js-mathjax}
  $\Large{RandomValue = floor(low + rand() * (high - low + 1))}$

* [`floor()`](/mdn/floor){:target="_blank"} is a function that rounds down a number to the closest integer
* **high** is the highest number in your distribution (inclusive)
* **low** is the lowest number in your distribution (inclusive)

For example, here's a query that generates a random age for the `users` table:

~~~pgsql
SELECT
  id,
  email,
  floor(18 + rand() * (100 - 18 + 1)) AS random_age
FROM users
~~~
{: .js-no-run-query-link}

## Shuffling rows with rand()

The most common use case for the `rand()` function is to shuffle records. For that we need to use the `rand()` function as a sorting value:

~~~pgsql
SELECT *
FROM users
ORDER BY rand()
~~~
{: .js-no-run-query-link}

## Sampling rows with rand()

Now that we have shuffled records, we can retrieve a random subset of users from the `users` table with a `LIMIT` clause:

~~~pgsql
SELECT *
FROM users
ORDER BY rand()
LIMIT 10
~~~
{: .js-no-run-query-link}

{{compatibility}}

{{see_also}}
