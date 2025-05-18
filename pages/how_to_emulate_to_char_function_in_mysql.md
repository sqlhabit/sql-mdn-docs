---
published_at: 2025-05-18 14:00
slug: how-to-emulate-to-char-function-in-mysql
type: misc
name: How to emulate to_char() function in MySQL
title: How to emulate to_char() function in MySQL
description: Learn how to emulate the to_char() formatting function from in MySQL using DATE_FORMAT() and FORMAT().
keywords: SQL, to_char, format, date, number, MySQL
compatibility: false
see_also_pages:
  - name: to_char() function in SQL
    url: /mdn/to-char
---

The [`to_char()` function](/mdn/to-char) is super flexible: it lets you format both **dates** and **numbers** into human-friendly strings. It looks something like this:

~~~pgsql
SELECT to_char(created_at, 'YYYY-MM-DD HH24:MI:SS')
FROM users
~~~

or:

~~~pgsql
SELECT to_char(price, 'FM999,999,999.00')
FROM products
~~~

Unfortunately, MySQL doesn’t support the `to_char()` function. But don’t worry — we can get pretty close using two different functions:

* `DATE_FORMAT()` for dates
* `FORMAT()` for numbers

Let’s break them down!

## Emulating to_char() for dates

In MySQL, you can use the `DATE_FORMAT()` function to format dates and timestamps into a string using specific format specifiers.

### Syntax

Here's how it works:

~~~pgsql
SELECT DATE_FORMAT(date_value, 'format_string')
FROM your_table
~~~
{: .js-no-run-query-link}

### Standard example

Let’s take a query that uses `to_char()` function:

~~~pgsql
SELECT to_char(created_at, 'YYYY-MM-DD HH24:MI:SS')
FROM users
~~~

To do the same thing in MySQL, we write:

~~~pgsql
SELECT DATE_FORMAT(created_at, '%Y-%m-%d %H:%i:%s')
FROM users
~~~
{: .js-no-run-query-link}

Here’s a quick list of the most common MySQL format tokens:

| to_char() tokens   | MySQL date_format() tokens    | Meaning               |
|-------------|-----------|------------------------|
| `YYYY`      | `%Y`      | 4-digit year           |
| `YY`        | `%y`      | 2-digit year           |
| `MM`        | `%m`      | 2-digit month          |
| `MON`       | `%b`      | Abbreviated month name |
| `MONTH`     | `%M`      | Full month name        |
| `DD`        | `%d`      | 2-digit day            |
| `DY`        | `%a`      | Abbreviated day name   |
| `DAY`       | `%W`      | Full day name          |
| `HH24`      | `%H`      | Hour (24-hour)         |
| `HH12`      | `%h`      | Hour (12-hour)         |
| `HH`        | `%h`      | Hour (12-hour)         |
| `AM/PM`     | `%p`      | AM or PM indicator     |
| `MI`        | `%i`      | Minutes                |
| `SS`        | `%s`      | Seconds                |
| `US`        | `%f`      | Microseconds           |
| `WW`        | `%u`      | Week of year           |
| `D`         | `%w`      | Day of week (0-6)      |
| `Q`         | `%q`      | Quarter of year        |
| `DDD`       | `%j`      | Day of year            |

## Emulating to_char() for numbers

When formatting numbers, `to_char()` can add thousands separators, control decimal places, add currency symbols, etc.

~~~pgsql
SELECT to_char(price, 'FM999,999,999.00')
FROM products
~~~

Sadly, in MySQL there's no single function that would allow you that level of control. Although you can achieve similar formatting using the `FORMAT()` function.

The `FORMAT()` function prints a number using this format `9,999,999.00` and you can control the number of decimal places:

~~~pgsql
SELECT FORMAT(number_column, decimal_places)
~~~
{: .js-no-run-query-link}

### Example

Let's look at the `to_char()` example that formats a number in a similar way:

~~~pgsql
SELECT
  to_char(price, 'FM999,999,999.00')
FROM products
~~~

In MySQL we'd simply do:

~~~pgsql
SELECT
  FORMAT(price, 2)
FROM products
~~~
{: .js-no-run-query-link}

:warning: Note that `FORMAT()` always uses a comma `,` as a thousands separator and a dot `.` for decimals — unless your database locale settings change that.

## Summary

Unfortunately, MySQL doesn’t have the mighty `to_char()` function. You can somewhat similar functionality using:

* `DATE_FORMAT()` for formatting dates
* `FORMAT()` for formatting numbers

{{compatibility}}

{{see_also}}
