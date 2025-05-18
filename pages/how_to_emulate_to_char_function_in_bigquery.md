---
published_at: 2025-05-18 14:30
slug: how-to-emulate-to-char-function-in-bigquery
type: misc
name: How to emulate to_char() function in BigQuery
title: How to emulate to_char() function in BigQuery
description: Learn how to format dates and numbers in BigQuery just like PostgreSQL's to_char() function using FORMAT_TIMESTAMP(), FORMAT_DATE(), and FORMAT().
keywords: SQL, format, to_char, BigQuery, PostgreSQL
compatibility: false
see_also_pages:
  - name: to_char() function in SQL
    url: /mdn/to-char
  - name: How to emulate to_char() function in MySQL
    url: /mdn/how-to-emulate-to-char-function-in-mysql
---

The `to_char()` function is a super useful way to turn a **timestamp**, **date**, or **number** into a nicely formatted string. You can use it to extract specific date parts or prettify numeric values with leading zeroes, thousands separators, and more.

But what if you're working in BigQuery? There's no `to_char()` function — but you can get the same results using:

- `FORMAT_TIMESTAMP()` for timestamps
- `FORMAT_DATE()` for dates
- `FORMAT()` for numbers

Let's break it down and see how it works.

## Formatting timestamps with FORMAT_TIMESTAMP()

When using `to_char()` function for a standard timestamp formatting, you can write:

~~~pgsql
SELECT to_char(created_at, 'YYYY-MM-DD HH24:MI:SS')
FROM users
~~~

In BigQuery, we can emulate this using `FORMAT_TIMESTAMP()`:

~~~pgsql
SELECT FORMAT_TIMESTAMP('%Y-%m-%d %H:%M:%S', created_at)
FROM users
~~~
{: .js-no-run-query-link}

The two formats are almost identical, with just a few small differences in formatting tokens.

Here's a list of all formatting tokens for the `FORMAT_TIMESTAMP()` function in BigQuery:

| Format Token | Description | Example |
|--------------|-------------|---------|
| `%Y` | 4-digit year | 2024 |
| `%y` | 2-digit year | 24 |
| `%m` | 2-digit month (01-12) | 01, 12 |
| `%d` | 2-digit day (01-31) | 01, 31 |
| `%H` | 2-digit hour (00-23) | 00, 23 |
| `%I` | 2-digit hour (01-12) | 01, 12 |
| `%M` | 2-digit minute (00-59) | 00, 59 |
| `%S` | 2-digit second (00-59) | 00, 59 |
| `%p` | AM/PM indicator | AM, PM |
| `%A` | Full weekday name | Monday |
| `%a` | Abbreviated weekday name | Mon |
| `%B` | Full month name | January |
| `%b` | Abbreviated month name | Jan |
| `%j` | Day of year (001-366) | 001, 366 |
| `%u` | Day of week (1-7, Monday=1) | 1, 7 |
| `%V` | Week of year (01-53) | 01, 53 |
| `%z` | Timezone offset | +0000 |
| `%Z` | Timezone name | UTC |

Here's a nice example:

~~~pgsql
SELECT FORMAT_TIMESTAMP('%A, %B %d, %Y at %I:%M %p', TIMESTAMP '2024-12-25 18:45:00')
-- Returns: 'Wednesday, December 25, 2024 at 06:45 PM'
~~~
{: .js-no-run-query-link}

## Formatting dates with FORMAT_DATE()

If your column is a plain `DATE` instead of `TIMESTAMP`, you can use the `FORMAT_DATE()` function in BigQuery.

When using `to_char()` function:

~~~pgsql
SELECT to_char(signup_date, 'Month DD, YYYY')
FROM users
~~~

In BigQuery:

~~~pgsql
SELECT FORMAT_DATE('%B %d, %Y', signup_date)
FROM users
~~~
{: .js-no-run-query-link}

:mag: You can use all the same date formatting tokens with `FORMAT_DATE()` that you use with `FORMAT_TIMESTAMP()`. The only difference is that you can't use time-related tokens (like hours, minutes, or seconds) since we're working with dates only.

## Formatting numbers with FORMAT()

When using `to_char()` function we'd format a price number like so:

~~~pgsql
SELECT to_char(price, 'FM999,999.00')
FROM products
~~~

In BigQuery, we'd use the `FORMAT()` function for this purpose:

~~~pgsql
SELECT FORMAT('%,.2f', price)
FROM products
~~~
{: .js-no-run-query-link}

For example, `12345.6` becomes `'12,345.60'`.

The `FORMAT()` function has a lot of formatting tokens:

| Format Token | Description | Example |
|--------------|-------------|---------|
| `%d` | Decimal integer | 123 |
| `%i` | Decimal integer | 123 |
| `%u` | Unsigned decimal integer | 123 |
| `%o` | Octal integer | 173 |
| `%x` | Hexadecimal integer (lowercase) | 7b |
| `%X` | Hexadecimal integer (uppercase) | 7B |
| `%f` | Decimal floating point | 123.456000 |
| `%F` | Decimal floating point | 123.456000 |
| `%e` | Scientific notation (lowercase) | 1.234560e+02 |
| `%E` | Scientific notation (uppercase) | 1.234560E+02 |
| `%g` | Shorter of %e or %f | 123.456 |
| `%G` | Shorter of %E or %F | 123.456 |
| `%a` | Hexadecimal floating point (lowercase) | 0x1.edd2f1a9fbe77p+6 |
| `%A` | Hexadecimal floating point (uppercase) | 0X1.EDD2F1A9FBE77P+6 |
| `%c` | Character | A |
| `%s` | String | Hello |
| `%%` | Literal % | % |

Let's try a simple BigQuery-friendly version:

~~~pgsql
SELECT FORMAT('%.0f', price)
FROM products
~~~
{: .js-no-run-query-link}

This will round prices to a whole number without commas.

## Summary

| BigQuery equivalent of to_char()         | Used for        |
|-----------------------------|-----------------|
| `FORMAT_TIMESTAMP()`        | timestamps      |
| `FORMAT_DATE()`             | dates           |
| `FORMAT()`                  | numbers         |

BigQuery's functions might look different, but they give you the same flexibility when it comes to string formatting.

{{compatibility}}

{{see_also}}
