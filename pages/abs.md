---
published_at: 2024-03-22 19:45
slug: abs
type: function
name: abs
title: abs() function in SQL
description: The abs() function returns the absolute value of a given number.
keywords: SQL, function, abs()
---

# abs() function in SQL

The `abs()` function in SQL is used to return the absolute value of a given number. The absolute value of a number is the value of the number without considering its sign. Therefore, `abs(-10)` is `10`, and similarly, `abs(10)` is `10`. This function is particularly useful in data analysis for normalizing values and ensuring consistency in the data's magnitude, regardless of its direction.

You can try out the `abs()` function even without a table:

~~~pgsql
SELECT abs(-10)
~~~

## Syntax

The syntax for using the `abs()` function is as follows:

~~~pgsql
SELECT abs(amount_usd)
FROM transactions
~~~
{: data-dataset-id="3"}

In this syntax, `amount_usd` is the column name from which you want to get the absolute value.

## Using abs() as a filter

The `abs()` function can also be useful in filtering records based on the absolute value of a column. For instance, to find all transactions where the absolute value of the balance change exceeds 100:

~~~pgsql
SELECT *
FROM transactions
WHERE
  abs(amount_usd) > 100
~~~
{: data-dataset-id="3"}

## Applications of the abs() function in SQL

The `abs()` function is instrumental in normalizing data, especially in scenarios where the direction of a number is irrelevant, and only its magnitude matters.

{{compatibility}}

{{see_also}}
