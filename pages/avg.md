---
published_at: 2024-04-07 11:15
slug: avg
type: function.aggregate
name: AVG
title: Aggregate function AVG() in SQL
description: The `AVG()` function in SQL is an aggregate function that returns the average value from a selected column.
keywords: SQL, MIN, aggregate function
see_also_pages:
  - name: Aggregate function COUNT() in SQL
    url: /mdn/count
  - name: Aggregate function MAX() in SQL
    url: /mdn/max
  - name: Aggregate function MIN() in SQL
    url: /mdn/min
  - name: Aggregate function SUM() in SQL
    url: /mdn/sum
  - name: GROUP BY clause in SQL
    url: /mdn/group-by
---

The `AVG()` function in SQL calculates the average value of a specified numeric column. It's an aggregate function that's incredibly useful for Data Analysis, helping to understand the central tendency of a data set, which can be critical in fields like user behaviour, finance, sales, and many others.

## Syntax

To start calculating averages, you use the `AVG()` function within a `SELECT` statement, targeting the column of interest.

~~~pgsql
SELECT AVG(column_name)
FROM table_name
~~~
{: .js-no-run-query-link }

For example, to find the average user age we'd run the following query:

~~~pgsql
SELECT AVG(age)
FROM users
~~~

## Using AVG() for detailed insights

In real life scenario, we'd further break down our average metric to groups, like average age per country. Here's an example of a `AVG()` query with the `GROUP BY` statement:

~~~pgsql
SELECT
  country,
  AVG(age)
FROM users
GROUP BY country
~~~

Usually, we wouldn't stop here and continue breaking down our groups with other dimensions (gender, occupation), etc.

## Importance of AVG() function

The `AVG()` function is a fantastic way to deepen your understanding of SQL and Data Analysis.

It allows you to not only measure the average of a data set but also to slice the data in various ways for nuanced insights. Practice using `AVG()` in different contexts:

* user demographics (average age per country, city, gender, signup source, etc)
* revenue analysis (average purchase amount, average purchase items count, etc)
* product analysis (average session duration, average page views, etc)

As you can see, the `AVG()` function is essential Data Analysis tool which you have to master.

{{compatibility}}

{{see_also}}
