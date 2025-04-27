---
published_at: 2025-04-27 14:30
slug: extract
type: function.timestamp
name: extract
title: extract() function in SQL
description: SQL extract() function allows to retrieve specific parts (like year, month, day, etc.) from date or timestamp values.
keywords: SQL, extract, timestamp, date function
compatibility: true
see_also_pages:
  - name: date_part() function in SQL
    url: /mdn/date-part
  - name: date_trunc() function in SQL
    url: /mdn/date-trunc
---

The `extract()` function in SQL is used to retrieve specific parts of a date or timestamp value, such as the year, month, day, hour, minute, second, and more. It is an essential tool when you need to perform detailed analysis on time-based data, such as creating time series reports or filtering datasets by particular components of a date.

## Syntax

~~~pgsql
extract(part FROM source)
~~~
{: .js-no-run-query-link }

- **`part`**: The part of the date or time you want to extract. Common fields are `year`, `month`, `day`, `hour`, `minute`, `second`, `dow` (day of week), `doy` (day of year), `week`, `quarter`, etc.
- **`source`**: The date, time, or timestamp value from which you want to extract the part.

The function returns a numeric value (integer or decimal, depending on the part).

## Simple Example

You don't always need a table to use `extract()`. Here's a very basic example where we extract the month from a hardcoded date:

~~~pgsql
SELECT extract(month FROM DATE '2025-04-27')
~~~

This will simply return `4`, since April is the fourth month of the year. Simple uses like this are great for quick tests or when working with constant values.

## Extracting parts of user signup dates

Suppose we want to know the year and month when users signed up. We can use `extract()` on the `signup_date` part from the `users` table:

~~~pgsql
SELECT
  id,
  signup_date,
  extract(year FROM signup_date) AS signup_year,
  extract(month FROM signup_date) AS signup_month
FROM users
LIMIT 5
~~~

This query adds two new columns showing the signup year and month separately for each user.

## Filtering purchases by year

Let's say we want to find all purchases made in 2018. We can filter using `extract()`:

~~~pgsql
SELECT *
FROM purchases
WHERE
  extract(year FROM created_at) = 2018
~~~

This is particularly useful when the `created_at` part contains both date and time, and you only want to focus on the year part.

## Grouping events by weekday

You can also use `extract()` to group data by the day of the week. In PostgreSQL, Sunday is represented as 0, Monday as 1, and so on.

Here's how you could analyze which weekdays are the most popular for mobile events:

~~~pgsql
SELECT
  extract(dow FROM created_at) AS weekday,
  COUNT(*) AS events_count
FROM mobile_analytics.events
GROUP BY 1
ORDER BY 2 DESC
~~~

This will return the number of events per day of the week, helping you understand user activity patterns.

## Extracting hour from pageviews

Suppose you want to analyze traffic by hour to find peak usage times. You can extract the hour from the `created_at` timestamp in the `web_analytics.pageviews` table:

~~~pgsql
SELECT
  extract(hour FROM created_at) AS hour,
  COUNT(*) AS pageviews
FROM web_analytics.pageviews
GROUP BY 1
ORDER BY 1
~~~

This way, you can easily see at which hours your website is most active.

## Practical Use Cases

- **Trend Analysis**: Track user activity by year, quarter, or month.
- **Operational Reports**: Find peak operating hours or days.
- **Marketing Analysis**: Understand customer behavior across time segments.
- **Data Cleaning**: Quickly identify outliers or incorrect date entries.

The `extract()` function is extremely flexible and integrates smoothly into a wide range of queries where time-based slicing and analysis are needed.

{{compatibility}}

{{see_also}}
