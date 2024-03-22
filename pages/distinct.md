---
published_at: 2024-03-19 19:50
slug: distinct
compatibility_key: distinct
type: keyword
name: DISTINCT
title: SQL DISTINCT keyword
description: SQL DISTINCT - DISTINCT tells SQL engine to return only unique records in the result set.
keywords: SQL, DISTINCT
---

# DISTINCT keyword in SQL

The `DISTINCT` keyword in SQL is a powerful tool used to eliminate duplicate rows from a result set.

The `DISTINCT` command is particularly useful when dealing with large datasets where there may be numerous instances of the same data. These duplicates could be specific values in columns (like user countries) or entire duplicated records (when using `LEFT JOIN`, for example).

Understanding how to use `DISTINCT` effectively can help you maintain the integrity of your data analysis and ensure accurate results.

## Syntax

When you use the `DISTINCT` keyword in a `SELECT` statement, SQL engine filters out all duplicate rows based on the columns you've specified and returns only unique rows.

Here's an example with one column:

~~~pgsql
SELECT DISTINCT country
FROM users
~~~

This query retrieves a list of unique countries from the `users` table.

:bulb: Note that you can also use the `DISTINCT` command with brackets like so:

~~~pgsql
SELECT DISTINCT(country)
FROM users
~~~

## `DISTINCT` on multiple columns

You can also use `DISTINCT` with multiple columns to get unique combinations of values across the specified columns.

~~~pgsql
SELECT DISTINCT country, age
FROM users
~~~

This query returns unique combinations of `country` and `age` from the `users` table.

:mag: If there are two users from the same country but with different ages, both rows will appear in the result set.

## Using `DISTINCT` in Data Analysis

`DISTINCT` can be particularly useful in data analysis in many scenarios:

* **Identifying Unique Values**. When you need to know the different variations of a particular attribute in your data.
* **Data Cleaning**. Helps in identifying and removing duplicates, which is crucial for accurate analysis (think business revenue reporting).
* **Aggregate Functions**: Combine `DISTINCT` with functions like `COUNT` to understand the size of a particular subset of data.

For instance, to count the number of unique countries in the `users` table:

~~~pgsql
SELECT COUNT(DISTINCT country)
FROM users
~~~

{{compatibility}}

{{see_also}}
