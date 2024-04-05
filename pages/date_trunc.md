---
published_at: 2024-03-31 22:00
slug: date-trunc
type: function.timestamp
name: date_trunc
title: date_trunc() function in SQL
description: SQL date_trunc() function allows to extract a specific part of a timestamp (year, month, day, hour, etc).
keywords: SQL, date_trunc, timestamp
---

The `date_trunc()` function in SQL is used to truncate a date or time to the specified precision, such as year, month, day, etc. It's used very often for grouping and analyzing data over specific time periods.

## Syntax

The basic syntax of the `date_trunc` function is as follows:

~~~pgsql
SELECT date_trunc('precision', timestamp)
FROM table_name
~~~
{: .js-no-run-query-link }

Where "precision" can be year, month, day, hour, minute, etc., and `timestamp` is the column or value you want to truncate.

:mag: Note that the function accepts a date or a timestamp and returns a date or a timestamp. Basically, `date_trunc` rounds down the input timestamp to a specific component, such as year, month, day, etc.

Let's look at a simple example:

~~~pgsql
SELECT date_trunc('day', signup_date)
FROM users
LIMIT 1
~~~

## Using `date_trunc` to build timeline reports

Typically, `date_trunc` is used to build time series. For example, you can use it to group purchases by month to see monthly sales trends:

~~~pgsql
SELECT
  date_trunc('month', created_at) AS month,
  COUNT(*)
FROM purchases
GROUP BY 1
ORDER BY 1 DESC
~~~

Here's another example with daily signup trends:

~~~pgsql
SELECT
  date_trunc('day', created_at) AS day,
  COUNT(*)
FROM users
GROUP BY 1
ORDER BY 1 DESC
~~~

Sometimes you might even need a finer precision, so here's an example with an hourly pageviews trend:

~~~pgsql
SELECT
  date_trunc('hour', created_at) AS hour,
  COUNT(*)
FROM web_analytics.pageviews
GROUP BY 1
ORDER BY 1 DESC
~~~

The `date_trunc` function is not only a useful tool for data analysis but also a great feature to practice and understand how SQL handles dates and times. Experiment with different date/time precisions and datasets to learn how to manipulate and interpret time series effectively. :bar_chart:

{{compatibility}}

{{see_also}}
