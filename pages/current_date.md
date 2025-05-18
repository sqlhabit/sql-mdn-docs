---
published_at: 2024-11-01 15:30
slug: current-date
types:
  - function.date
name: current_date
title: current_date function in SQL
description: SQL current_date function allows to get today's date.
keywords: SQL, now, date, function
compatibility: true
see_also_pages:
  - name: now() function in SQL
    url: /mdn/now
  - name: current_timestamp function in SQL
    url: /mdn/current-timestamp
---

The `current_date` function in SQL returns the current date based on the system’s local date and is typically represented in `YYYY-MM-DD` format. The `current_date` function is commonly used in reports, data validations, and time-based calculations, providing an easy way to work with today’s date in queries.

## Syntax

The basic syntax of the `current_date` function does not require any parameters, as it simply returns the current date:

~~~pgsql
SELECT current_date
~~~

:mag: Note how we skipped the `FROM` clause – we're not querying a table, so we can skip it. This is a great way to test other scalar function (that return a single value).

:mag: Note that we haven't used parentheses in the function call: `current_date`. :warning: This is because `current_date` is a SQL standard-defined keyword representing a **constant** function.

The value of `current_date` will be calculated by the database server at the beginning of running a query and all references of the `current_date` in a query will have the same value. That's why `currnet_date` doesn't require parentheses: it behaves more like a variable or a constant and not a function.

## Using `current_date` for filtering

One of the common uses for `current_date` is filtering data to retrieve records created on, before, or after the current date. For instance, to find all users who signed up we can run the following query:

~~~pgsql
SELECT *
FROM mobile_analytics.events
WHERE
  created_at::date = current_date
~~~
{: data-dataset-id="4"}

:mag: Note that we have to extract the date part from the `created_at` timestamp for comparison with `created_at::date`.

## Calculating date differences

Once we have today's date, we can calculate all sorts of values. For example, how many days have passed since a specific date. Let's count user who created accounts within the past 30 days:

~~~pgsql
SELECT
  COUNT(*)
FROM users
WHERE
  created_at::date >= current_date - '30 days'::interval
~~~
{: data-dataset-id="4"}

## Using `current_date` in date ranges

Finally, we can zoom into specific date ranges by combining `current_date` function and [`BETWEEN`](/mdn/between){:target="_blank"} operator. For example, let's see all purchases made within the previous week (more like 7 day period):

~~~pgsql
SELECT *
FROM purchases
WHERE
  created_at::date BETWEEN current_date - INTERVAL '14 days' AND current_date - INTERVAL '7 days'
~~~
{: data-dataset-id="4"}

The `current_date` function is a simple yet essential tool in SQL, widely used for creating dynamic date-based queries that do not require constant manual adjustments to the date. Queries with `current_date` and [`current_timestamp`](/mdn/current-timestamp){:target="_blank"} will power all your real-time dashboards. :bar_chart:

{{compatibility}}

{{see_also}}
