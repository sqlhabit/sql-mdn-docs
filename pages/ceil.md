---
published_at: 2024-04-06 16:35
slug: ceil
types:
  - function.numeric
name: ceil
title: ceil() function in SQL
description: The ceil() function rounds a number to the closest higher integer.
keywords: SQL, function, ceil()
see_also_pages:
  - name: round() function in SQL
    url: /mdn/round
  - name: floor() function in SQL
    url: /mdn/floor
---

The `ceil()` (short from ceiling) function in SQL is used to return the smallest integer value that is greater than or equal to a specified number. Essentially, it rounds up the given value to the nearest integer. This function is particularly useful in scenarios where you need to ensure that values are rounded up, such as in inventory management (when you can't have 7.8 of a physical item).

Here's a table that compares the behaviour of `ceil()` function to the `round()` function:

| number | ceil(number) | round(number) |
| ----- | ----- | ----- |
| 1.49 | 2 | 1 |
| 1.51 | 2 | 2 |
| -1.49 | -1 | -1 |
| -1.51 | -1 | -2 |

## Syntax

The basic syntax of the `CEIL` function is as follows:

~~~pgsql
SELECT CEIL(number)
FROM table_name
~~~
{: .js-no-run-query-link }

Here, the `number` argument is a numeric column name or a result of a math expression.

## Using ceil()

Sometimes we're not interested in the decimal part of a number, especially when dealing with large numbers. Here's an example where we calculate a total amount of financial transactions:

~~~pgsql
SELECT CEIL(SUM(amount_usd))
FROM transactions
~~~
{: data-dataset-id="3"}

Here the decimal part of the final sum isn't of any interest. We're using `ceil()` to remove decimal digits without a risk of under-reporting the final amount.

## Practice with ceil()

A great thing about using simple math functions like `ceil()` is that you can easily practice them without a querying the actual data. You can simply call the `ceil()` function with a bunch of arbitrary numbers:

~~~pgsql
SELECT
  ceil(1.51) AS ceil_high_number,
  ceil(1.49) AS ceil_low_number,
  ceil(-1.51) AS ceil_negative_high_number,
  ceil(-1.49) AS ceil_negative_low_number
~~~

This query demonstrates the `ceil()` function's behavior with positive and negative numbers.

:bulb: To memorize how this function works, it's better to imagine a table like in the example above :point_up: or, even better, imagine a horizontal line when numbers on it and see to which nearest integers the `ceil()` function rounds them. It will help to deeply understant the `ceil()` function and retain it in memory forever.

{{compatibility}}

{{see_also}}
