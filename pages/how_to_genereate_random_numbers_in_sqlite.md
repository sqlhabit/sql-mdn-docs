---
published_at:
slug: how-to-genereate-random-numbers-in-sqlite
type: misc
name: How to generate random numbers in SQLite
title: How to generate random numbers in SQLite
description: Learn how to generate random numbers and work with randomness in SQLite.
keywords: SQL, SQLite, random
compatibility: false
see_also_pages:
  - name: random() function in SQL
    url: /mdn/random
---

In SQLite, the `random()` function is used to generate a random integer. Unlike MySQL or PostgreSQL, the `random()` function in SQLite returns a random 64-bit integer (a number ranging from -9223372036854775808 to 9223372036854775807) instead of a float number between 0 and 1.

## Syntax

The `random()` function can be used without any arguments:

~~~pgsql
SELECT random()
~~~
{: .js-no-run-query-link}

:mag: Great SQL trick: we can quickly test scalar (that return a single value) functions without specifying the `FROM` keyword.

## How to generate a float number between 0 and 1

Let's use SQLite's `random()` function to simulate the standard random behavior of other databases and generate a float number between 0 and 1:

~~~pgsql
SELECT (random() + 9223372036854775808) / 18446744073709551615.0
~~~
{: .js-no-run-query-link}

Let's understand the math behind this calculation. First, we're shifting our 64-bit distribution to the positive range only: from [-9223372036854775808, 9223372036854775807] to [0, 18446744073709551615].

Next, we're dividing a random positive integer by the max value of the range (18446744073709551615), mapping the final float random number to [0.0, 1.0].

## How to generate a random integer number within a range

If we want to generate an integer number within, we can use another math trick to map the original 64-bit distribution to a desired range.

First, let's map our distribution to only positive values by using the [`abs()`](/mdn/abs){:target="_blank"} function:

~~~pgsql
SELECT abs(random())
~~~
{: .js-no-run-query-link}

Then we can use the module `%` operator (returns the remainder of a division) to map the positive random value into a range (18 to 100, for example):

~~~pgsql
SELECT abs(random()) % (100 - 18 + 1) + 18
~~~
{: .js-no-run-query-link}

:mag: Note that we need the `+1` to achieve the inclusive range, otherwise we'll never get the highest value (100 in our case).

## Shuffling records

SQLite doesn’t have a specific shuffling function, but you can simulate shuffling by ordering the records randomly. This is achieved by using the `ORDER BY random()` clause in a query:

~~~pgsql
SELECT *
FROM users
ORDER BY random()
~~~
{: .js-no-run-query-link}

## Sampling records

Selecting a random sample of records to check the data and available columns is a common trick when working with new datasets. In SQLite, you can retrieve a random subset of records by using the `ORDER BY random()` clause in combination with `LIMIT`:

~~~pgsql
SELECT *
FROM users
ORDER BY random()
LIMIT 10
~~~
{: .js-no-run-query-link}

{{compatibility}}

{{see_also}}
