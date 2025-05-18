---
published_at: 2024-03-30 12:45
slug: sum
types:
  - function.aggregate
name: SUM
title: Aggregate function SUM() in SQL
description: SUM() is an aggregate function in SQL that calculates the total sum of a numeric column.
keywords: SQL, SUM, aggregate function
see_also_pages:
  - name: Aggregate function COUNT() in SQL
    url: /mdn/count
  - name: Aggregate function AVG() in SQL
    url: /mdn/avg
  - name: Aggregate function MAX() in SQL
    url: /mdn/max
  - name: Aggregate function MIN() in SQL
    url: /mdn/min
  - name: GROUP BY clause in SQL
    url: /mdn/group-by
---

`SUM()` is an aggregate function in SQL that calculates the total sum of a numeric column. The `SUM` aggregate function is a must for financial calculations, statistical analysis, and more.

## Syntax

The basic syntax for the `SUM()` function is as follows:

~~~pgsql
SELECT SUM(column_name)
FROM table_name
WHERE condition
~~~
{: .js-no-run-query-link }

This will return the sum of the specified column for all rows that meet the condition.

## Using SUM() in queries

Here's a simple example that calculates the total amount from all purchases.

~~~pgsql
SELECT SUM(amount)
FROM purchases
~~~

### SUM() with GROUP BY

The `SUM()` function becomes even more powerful when combined with the `GROUP BY` statement. This allows you to calculate sums for each distinct group in your data.

For example, to find the total sales per product:

~~~pgsql
SELECT
  product_id,
  SUM(amount)
FROM purchases
GROUP BY product_id
~~~

### Handling NULL values

It's important to note that `SUM()` ignores `NULL` values when calculating the total. However, if there are no rows to sum or all values are `NULL`, `SUM()` returns `NULL`.

## Practical applications

The `SUM()` function is widely used in various scenarios, such as:

- Calculating total sales or revenue
- Summing up quantities of items sold
- Aggregating data for financial reports

It is a key tool for data analysis, allowing analysts to quickly perform aggregate calculations on large datasets.

## Best practices

While `SUM()` is straightforward to use, it's important to be mindful of data types and ensure that the column you are summing contains numeric data. Attempting to sum non-numeric data types will result in an error.

:warning: Another typical error with the `SUM()` function is duplicated records. Imagine your query reports a double or triple of total company revenue – it might lead to a total disaster. :bomb:

The `SUM()` function is a fundamental part of SQL that provides immense value in data analysis and reporting. By understanding and utilizing `SUM()`, you can extract meaningful insights from your data with ease.

{{compatibility}}

{{see_also}}
