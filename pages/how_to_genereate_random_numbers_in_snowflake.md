---
published_at: 2024-11-01 12:00
slug: how-to-genereate-random-numbers-in-snowflake
type: misc
name: How to generate random numbers in Snowflake
title: How to generate random numbers in Snowflake
description: Learn how to generate random numbers and work with randomness in Snowflake.
keywords: SQL, Snowflake, random
compatibility: false
see_also_pages:
  - name: random() function in SQL
    url: /mdn/random
---

Great news: Snowflake database supports the `random()` function. Other news: it generates a random 64-bit integer instead of a float number between 0 and 1 (like in other databases).

That's why we need to learn a couple of tricks in Snowflake to generate float numbers between 0 and 1, random number from a given range, etc.

## Syntax

The syntax for the `random()` in Snowflake is simple and requires no arguments:

~~~pgsql
SELECT random()
~~~
{: .js-no-run-query-link}

This will return a random 64-bit integer (a number between between -9223372036854775808 and +9223372036854775807).

## Generating a float random number between 0 and 1

To generate a random floating-point number between 0 and 1, we have to use a different function: [`uniform()`](https://docs.snowflake.com/en/sql-reference/functions/uniform). This function is used to generate random numbers in ranges:

~~~pgsql
SELECT uniform(0::float, 1::float, random())
~~~
{: .js-no-run-query-link}

As you can see, the `uniform(min, max, gen)` function has 3 arguments. `min` and `max` are simply the lowest and the highest values for our range (both are inclusive :warning:). The `gen` (short for *generator*) argument is a randomness function that is used to generate a raw value than is mapped to our range. Typically, it is the `random()` function (for the uniform distribution).

## Generating random values in ranges

There're no `uniform()` function in other databases, so we have to use a formula to map 0-1 float distribution to a desired range (see the page for the [`random()`](/mdn/random){:target="_blank"}).

Here's a Snowflake query that generates random integer numbers between 1 and 10:

~~~pgsql
SELECT uniform(1, 10, random())
~~~
{: .js-no-run-query-link}

## Shuffling and sampling records with random()

When inspecting tables, we often want to see a couple of random records. This is a perfect usecase for the `random()` function:

~~~pgsql
SELECT *
FROM users
ORDER BY random()
LIMIT 10
~~~
{: .js-no-run-query-link}

:mag: `ORDER BY random()` shuffles (sorts in random order) records and `LIMIT 10` captures the first 10 (our sample).

{{compatibility}}

{{see_also}}
