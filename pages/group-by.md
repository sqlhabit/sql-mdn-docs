---
published_at: 2024-03-29 09:15
slug: group-by
type: clause
name: GROUP BY
title: GROUP BY clause in SQL
description: GROUP BY clause in SQL is used for grouping records and calculating aggregate values for these groups (COUNT, SUM, etc).
keywords: SQL, GROUP BY, aggregation
see_also_pages:
  - name: SELECT statement in SQL
    url: /mdn/select
  - name: FROM keyword in SQL
    url: /mdn/from
  - name: WHERE clause in SQL
    url: /mdn/where
  - name: LIMIT clause in SQL
    url: /mdn/limit
  - name: ORDER BY clause in SQL
    url: /mdn/order-by
---

The `GROUP BY` clause in SQL is critical for organizing data into groups based on one or more columns. It's always accompanied by aggregate functions like `COUNT()`, `SUM()`, `AVG()`, `MAX()`, and `MIN()`, allowing for detailed analysis of subsets within a dataset. For example, counting a number of users per country, average check per cart in an E-commerce store, etc.

## Syntax

There're two parts to `GROUP BY` syntax: grouping and aggregating.

Grouping comes first – we need to specify into which groups we're breaking our data. To do that, we're using the `GROUP BY` clause after the `FROM` clause and any `WHERE` conditions:

~~~pgsql
SELECT column1, aggregate_function(column2)
FROM table_name
GROUP BY column1
~~~
{: .js-no-run-query-link }

The second step is the aggregate function. Imagine the `GROUP BY` clause splits the data into groups. Then the `aggregate_function` calculates a value for each group (COUNT, SUM, etc).

As you can see, inside the `SELECT` clause we have both the aggregation column and aggregate function. It means that in the result set for every unique value of the aggregation column (read: each group) there will be a result of the aggregate function.

## Grouping data with GROUP BY

### Single column grouping

Grouping by a single column is straightforward. Here's how you might count the number of users in each unique country of the `country` column:

~~~pgsql
SELECT
  country,
  COUNT(*) AS user_count
FROM users
GROUP BY country
~~~

### Multiple column grouping

To group by more than one column, simply list the columns in the `GROUP BY` clause. This is useful for more granular analysis:

~~~pgsql
SELECT
  country,
  age,
  COUNT(*) AS user_count
FROM users
GROUP BY country, age
~~~

You can visualize grouping by multiple columns as splitting the dataset by the first column, then splitting each group further by the second column, etc.

## Practical applications of GROUP BY

Understanding and effectively utilizing the `GROUP BY` clause can significantly enhance data analysis capabilities. It enables data analysts to summarize data, identify trends, visualize timelines and make data-informed decisions. Whether you're preparing a report, conducting a comprehensive data analysis, or building dashboards, `GROUP BY` can help organize and present data in a more insightful and actionable manner.

{{compatibility}}

{{see_also}}
