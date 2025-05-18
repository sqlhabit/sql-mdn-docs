---
published_at: 2024-04-11 08:30
slug: nullif
types:
  - function.conditional
name: NULLIF
title: NULLIF() function in SQL
description: The NULLIF function in SQL is a conditional expression that returns NULL if two expressions are equal.
keywords: SQL, nullif, function
see_also_pages:
  - name: CASE operator in SQL
    url: /mdn/case
  - name: COALESCE() function in SQL
    url: /mdn/coalesce
---

The `NULLIF()` function in SQL is a conditional expression that returns `NULL` if two expressions are equal. If they are not equal, it returns the value of the first expression.

This functionality is particularly useful for preventing division-by-zero errors and for handling cases where data normalization is required.

## Syntax

The syntax for the `NULLIF()` function is as follows:

~~~pgsql
NULLIF(value1, value2)
~~~
{: .js-no-run-query-link }

If `value1` equals `value2`, `NULLIF()` returns `NULL`:

~~~pgsql
NULLIF('foo', 'foo')
~~~

If values are not equal, the `NULLIF()` function returns `value1`:

~~~pgsql
NULLIF('foo', 'bar')
~~~

## Using `NULLIF()` to prevent errors

One of the most common uses of `NULLIF()` is to avoid division by zero errors in queries that perform division operations. By replacing a zero denominator with NULL, you prevent the error and can handle the result more gracefully.

First of all, let's examine the error:

~~~pgsql
SELECT 1 / 0
~~~

For example, to safely calculate the ratio of two columns:

~~~pgsql
SELECT
  numerator / NULLIF(denominator, 0)
FROM financials
~~~
{: .js-no-run-query-link }

This query divides `numerator` by `denominator`, but if `denominator` is 0, `NULLIF()` returns NULL, effectively avoiding a division-by-zero error.

Compare the result of this query with the error query about :point_up:

~~~pgsql
SELECT 1 / NULLIF(0, 0)
~~~

## Normalizing empty strings to NULL

Sometimes, empty strings in data are more meaningfully interpreted as NULL values. `NULLIF()` can be used to convert empty strings to NULL, allowing for more accurate data analysis.

To convert empty email fields to NULL:

~~~pgsql
SELECT
  NULLIF(postal_code, '') AS postal_code
FROM profiles
~~~

This converts any empty `postal_code` values to NULL, simplifying subsequent data processing steps.

The `NULLIF()` function is a simple yet powerful tool in SQL, offering the ability to handle potentially problematic data with elegance and efficiency. Its proper use can improve the robustness and accuracy of SQL queries, especially in Data Analysis and reporting contexts.

{{compatibility}}

{{see_also}}
