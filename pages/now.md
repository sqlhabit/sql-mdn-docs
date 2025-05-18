---
published_at: 2024-10-30 17:00
slug: now
types:
  - function.timestamp
name: now
title: now() function in SQL
description: SQL now() function allows to get the current time.
keywords: SQL, now, timestamp, time, function
compatibility: true
see_also_pages:
  - name: current_timestamp function in SQL
    url: /mdn/current-timestamp
---

The `now()` function in SQL is used to retrieve the current timestamp (date + time). It's particularly useful for calculating durations or querying records relative to the present moment (for example, counting the number of new users in the past 7 days).

## Syntax

`now()` is a scalar (returns a single result) function that doesn't take any arguments. It returns the current date and time in the format of a `timestamp`:

~~~pgsql
SELECT now()
~~~

:bulb: Note how we don't need a `FROM` keyword to call a function. This is a useful pattern to test any scalar function.

## Using `now()` to count recent records

Let's write a query for the example we started with – count users who signed up during the past 7 days:

~~~pgsql
SELECT
  COUNT(*)
FROM users
WHERE
  created_at > now() - '7 days'::interval
~~~
{: data-dataset-id="4"}

## Using `now()` to calculate time difference

Another useful application of the `now()` function is to calculate the duration between the current time and a timestamp in the database.

Here's a query that calculate the `age` (popular term for time time difference between a timestamp and now) of each signup:

~~~pgsql
SELECT
  id,
  email,
  now() - created_at AS signup_age
FROM users
LIMIT 5
~~~
{: data-dataset-id="4"}

{{compatibility}}

{{see_also}}
