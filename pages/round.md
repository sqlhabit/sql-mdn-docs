---
published_at: 2024-04-06 16:00
slug: round
type: function.numeric
name: round
title: round() function in SQL
description: The round() function rounds a number to the closest higher integer.
keywords: SQL, function, round()
---

The `round()` function in SQL is used to round a numeric field to the nearest value with a specified precision. It's particularly useful in financial calculations, data reporting, or anytime you need to standardize the number of decimal places in your data output.

## Syntax

The basic syntax of the `round()` function is as follows:

~~~pgsql
SELECT round(number, precision)
FROM table_name
~~~
{: .js-no-run-query-link }

- `number` is a numeric value you wish to round (column name or a result of a math expression)
- `precision` specifies the number of decimal places to which the value should be rounded (0 or better). If this parameter is omitted, the function rounds to the nearest integer number (..., -2, -1, 0, 1, 2, ...)

## Using round() in financial calculations

When dealing with financial data, it's often necessary to round values to two decimal places. Here's how you can use the `round()` function to achieve this:

~~~pgsql
SELECT round(amount_usd, 2)
FROM transactions
~~~
{: data-dataset-id="3"}

This query will return the values from the `amount_usd` column rounded to two decimal places for each record in the `transactions` table.

## Rounding without a specified precision

If you omit the `precision` argument, the `round()` function will round the number to the nearest whole number:

~~~pgsql
SELECT round(amount_usd)
FROM transactions
~~~
{: data-dataset-id="3"}

This can be particularly useful when you need to simplify data for summary reports or high-level analysis.

## Using ROUND for data analysis

Rounding numbers can be crucial for making datasets more understandable and for ensuring consistency in data analysis. For example, if you're analyzing a dataset with a wide range of values and you want to group these values into categories, rounding can help by simplifying the numbers to a consistent format.

Here's how you might round off sales data to the nearest hundred:

~~~pgsql
SELECT round(amount_usd, -2)
FROM transactions
~~~
{: data-dataset-id="3"}

This query demonstrates a negative precision value in the `round()` function, which rounds the number to the left of the decimal point, simplifying the data for analysis or reporting purposes.

## Practice with round()

The `round()` function is a great example where you can run a query without specifying a table name. We can simply call the `round()` function with arbitrary numbers:

~~~pgsql
SELECT
  ROUND(123.4567, 2) AS rounded_two_decimal,
  ROUND(123.4567, 0) AS rounded_whole_number,
  ROUND(123.4567, -2) AS rounded_hundreds
~~~

This query rounds the same number three different ways: to two decimal places, to the nearest whole number, and to the nearest hundred, demonstrating the flexibility and utility of the `round()` function in SQL.

{{compatibility}}

{{see_also}}
