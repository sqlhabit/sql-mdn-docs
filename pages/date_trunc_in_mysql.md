---
published_at: 2024-04-02 21:30
slug: date-trunc-in-mysql
type: misc
name: How to emulate date_trunc() function in MySQL
title: How to emulate date_trunc() function in MySQL
description: In this article, you'll learn how to emulate date_trunc() SQL function in MySQL and truncate dates and timestamp to a specific precision.
keywords: SQL, date_trunc, function, MySQL, PostgreSQL
compatibility: false
see_also_pages:
  - name: date_trunc() function in SQL
    url: /mdn/date-trunc
---

In SQL, the ability to truncate dates to a specific component (year, month, day, hour, etc.) is essential for summarizing and analyzing time series data. While PostgreSQL and other popular databases offer the `date_trunc()` function for this purpose, MySQL does not have a direct equivalent.

However, we can achieve similar functionality in MySQL using various date and time functions. This chapter will guide you through emulating the `date_trunc()` behavior in MySQL.

## Syntax and examples

In PostgreSQL, `date_trunc(precision, timestamp)` allows you to truncate a timestamp to the precision specified by the first argument. For example:

~~~pgsql
SELECT date_trunc('month', now())
~~~

This will produce a timestamp with the first day of the month and no hour/minute/seconds, like `2024-04-01 00:00:00`. Such rounded timestamps are perfect for aggregating data and plotting time series.

To achieve similar functionality in MySQL, we have to use different approaches depending on the desired truncation precision.

### Truncate to year using DATE_FORMAT() function

Truncating to a year means we need to round a timestamp to the first of January of the timestamp's year. We'll use `DATE_FORMAT(timestamp, format)` function for that.

The `DATE_FORMAT(timestamp, format)` function accepts a `format` string argument where we can specify any combination of the following placeholders:

| Placeholder | Description
| --- | --- |
| %a | Abbreviated weekday name (Sun..Sat) |
| %b | Abbreviated month name (Jan..Dec) |
| %c | Month, numeric (0..12) |
| %D | Day of the month with English suffix (0th, 1st, 2nd, 3rd, …) |
| %d | Day of the month, numeric (00..31) |
| %e | Day of the month, numeric (0..31) |
| %f | Microseconds (000000..999999) |
| %H | Hour (00..23) |
| %h | Hour (01..12) |
| %I | Hour (01..12) |
| %i | Minutes, numeric (00..59) |
| %j | Day of year (001..366) |
| %k | Hour (0..23) |
| %l | Hour (1..12) |
| %M | Month name (January..December) |
| %m | Month, numeric (00..12) |
| %p | AM or PM |
| %r | Time, 12-hour (hh:mm:ss followed by AM or PM) |
| %S | Seconds (00..59) |
| %s | Seconds (00..59) |
| %T | Time, 24-hour (hh:mm:ss) |
| %U | Week (00..53), where Sunday is the first day of the week; WEEK() mode 0 |
| %u | Week (00..53), where Monday is the first day of the week; WEEK() mode 1 |
| %V | Week (01..53), where Sunday is the first day of the week; WEEK() mode 2; used with %X |
| %v | Week (01..53), where Monday is the first day of the week; WEEK() mode 3; used with %x |
| %W | Weekday name (Sunday..Saturday) |
| %w | Day of the week (0=Sunday..6=Saturday) |
| %X | Year for the week where Sunday is the first day of the week, numeric, four digits; used with %V |
| %x | Year for the week, where Monday is the first day of the week, numeric, four digits; used with %v |
| %Y | Year, numeric, four digits |
| %y | Year, numeric (two digits) |
| %% | A literal % character |
| %x | x, for any “x” not listed above |

Using the `%Y` placeholder, here's how can we round up a timestamp to the year:

~~~pgsql
SELECT DATE_FORMAT(timestamp_column_name, '%Y-01-01') FROM table_name
~~~
{: .js-no-run-query-link }

This returns the first day of the year for the given date, like `2024-01-01`.

### Truncate to month

To truncate a date to month we just need to set the day to the 1st of the month:

~~~pgsql
SELECT
  DATE_FORMAT(timestamp_column_name, '%Y-%m-01')
FROM table_name
~~~
{: .js-no-run-query-link }

This returns the first day of the month for the given date, like like `2024-04-01`.

### Truncate to hour/minute/second

Thanks to the giant list of placeholders, we can format timestamps in a multitude of ways. We can even truncate to a microsecond (never seen this in a business report). :smiley:

Let's get back to a more practical example and round up a timestamp to a minute:

~~~pgsql
SELECT
  DATE_FORMAT(timestamp_column_name, '%Y-%m-%d %H-%i-00')
FROM table_name
~~~
{: .js-no-run-query-link }

Emulating `date_trunc()` in MySQL requires a bit more effort than in PostgreSQL, but it's a valuable exercise in understanding the flexibility and power of SQL's date and time functions. By mastering these techniques, you can perform sophisticated time-based analyses and gain valuable insights from your data.

{{compatibility}}

{{see_also}}
