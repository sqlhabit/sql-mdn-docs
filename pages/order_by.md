---
published_at: 2024-03-28 22:00
slug: order-by
types:
  - clause
name: ORDER BY
title: ORDER BY clause in SQL
description: ORDER BY clause in SQL defines the order of records in the result set.
keywords: SQL, ORDER BY, sorting
see_also_pages:
  - name: SELECT statement in SQL
    url: /mdn/select
  - name: FROM keyword in SQL
    url: /mdn/from
  - name: WHERE clause in SQL
    url: /mdn/where
  - name: LIMIT clause in SQL
    url: /mdn/limit
---

The `ORDER BY` clause in SQL is used to sort the result set of a query by one or more columns, either ascending (ASC) or descending (DESC). This is crucial when you need to organize data in a specific order for analysis or reporting.

## Syntax

The basic syntax of the `ORDER BY` clause involves specifying the column or columns you want to sort by, followed by the direction of the sort.

~~~pgsql
SELECT column1, column2
FROM table
ORDER BY column1 ASC, column2 DESC
~~~
{: .js-no-run-query-link }

## Sorting data with ORDER BY

### Single column sorting

To sort data by a single column, you can use the `ORDER BY` clause with the column name:

~~~pgsql
SELECT *
FROM users
ORDER BY age DESC
~~~

### Multiple column sorting

You can also sort by more than one column. The sorting is performed on the first column specified, then on the next column within the previous sort, and so on:

~~~pgsql
SELECT *
FROM users
ORDER BY country ASC, age DESC
~~~

:mag: Note that we sorted by the text column first (here the `ASC` order means from "a" to "z") and then by the numeric column.

Sorting data with the `ORDER BY` clause enhances readability and understandability of query results, which is particularly useful when presenting data to other people. :bar_chart:

It also plays a crucial role in preparing data for reporting and dashboards, ensuring that the data is in the expected format or order.

Additionally, during the exploratory phase of data analysis, sorting can help analysts quickly identify the highest or lowest values in a dataset, facilitating deeper investigations and insights.

{{compatibility}}

{{see_also}}
