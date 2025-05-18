---
published_at: 2024-04-06 16:20
slug: floor
types:
  - function.numeric
name: floor
title: floor() function in SQL
description: The floor() function rounds a number to the closest lower integer.
keywords: SQL, function, floor()
see_also_pages:
  - name: round() function in SQL
    url: /mdn/round
  - name: ceil() function in SQL
    url: /mdn/ceil
---

The `floor()` function in SQL is used to return the largest integer less than or equal to a specified number.

In essence, it rounds down the given value to the nearest integer. Here's a comparison table between `floor()` and `round()` functions:

| number | floor(number) | round(number) |
| ----- | ----- | ----- |
| 1.49 | 1 | 1 |
| 1.51 | 1 | 2 |
| -1.49 | -2 | -1 |
| -1.51 | -2 | -2 |

This function finds its utility in various scenarios where rounding down is necessary, such as discount calculations, or when dealing with time slots in scheduling applications.

## Syntax

The basic syntax of the `floor()` function is as follows:

~~~pgsql
SELECT FLOOR(number)
FROM table_name
~~~
{: .js-no-run-query-link }

The `number` argument is the numeric field that you wish to round down or a result of a math expression.

## Using floor() in discount calculations

Here's a scenario where we apply a 30% discount and we want to round the final price to a nice integer number:

~~~pgsql
SELECT
  floor(price * 0.7) AS final_price
FROM products
~~~

Note that we can't round the final price to the higher number (using the [`ceil() function`](/mdn/ceil)), because we'll overcharge users in that case.

## Practice with floor()

Exploring the `floor()` function is a great way for SQL beginners to get comfortable with numeric data manipulation. You don't even need a database table to start playing with the `floor()` function:

~~~pgsql
SELECT
  floor(7.95) AS floor_high_number,
  floor(7.25) AS floor_low_number,
  floor(-7.95) AS floor_negative_high_number,
  floor(-7.25) AS floor_negative_low_number
~~~

This query showcases the `floor()` function's application to both positive and negative numbers.

:bulb: Try visualizing these input numbers on a line (like on the X-axis of a chart) and see to which integer numbers the `floor()` function would round them. It'll help deeply understanding the `floor()` function and remember it forever.

{{compatibility}}

{{see_also}}
