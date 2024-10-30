---
published_at: 2024-10-30 18:30
slug: current-timestamp
type: function.timestamp
name: current_timestamp
title: current_timestamp function in SQL
description: SQL current_timestamp function allows to get the current time.
keywords: SQL, now, timestamp, time, function
compatibility: true
see_also_pages:
  - name: now() function in SQL
    url: /mdn/now
---

The `current_timestamp` function in SQL is used to retrieve the current date and time.

:mag: Note that we're calling this function without parentheses. This is because `current_timestamp` is a SQL standard-defined keyword representing a **constant** function.

Unlike typical functions that require parentheses (like [`now()`](/mdn/now)), certain functions in SQL, including `current_timestamp`, act as **special non-deterministic constants** that are evaluated once per query (when the SQL query begins execution). In other words, to improve readability SQL designers decided to omit parentheses to show that `current_timestamp` is a constant that could be referenced throughout a query.

## Syntax

The `current_timestamp` function is straightforward to use, requiring no arguments:

~~~pgsql
SELECT current_timestamp
~~~

:bulb: Since it's a scalar function (scalar == returns a single value), we can even skip the `FROM` keyword in our query.

## Using `current_timestamp` to count recent records

Let's write a query that counts purchases that happen during the past 7 days:

~~~pgsql
SELECT
  COUNT(*)
FROM purchases
WHERE
  created_at > current_timestamp - '7 days'::interval
~~~
{: data-dataset-id="4"}

## Using `current_timestamp` to calculate time gaps

Another typical application of the `current_timestamp` function is to answer questions like "How long ago something happened?" (we can translate it to SQL like "How old is this record?").

Here's an example query that calculates an "age" of each signup:

~~~pgsql
SELECT
  id,
  email,
  current_timestamp - created_at AS signup_age
FROM users
LIMIT 5
~~~
{: data-dataset-id="4"}

## Using `current_timestamp` throughout a query

To highlight why the `current_timestamp` is more like a variable and not a function, let's write a query that uses it in multiple places. This query shows recent purchases of users who signed up more than a month ago:

~~~pgsql
SELECT
  u.email,
  p.amount,
  current_timestamp - u.created_at AS signup_age,
  current_timestamp - p.created_at AS purchase_age
FROM users u
LEFT JOIN purchases p
  ON p.user_id = u.id
    AND p.created_at > current_timestamp - '7 days'::interval
WHERE
  u.created_at < current_timestamp - '1 month'::interval
~~~
{: data-dataset-id="4"}

{{compatibility}}

{{see_also}}
