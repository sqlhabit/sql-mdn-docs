---
published_at: 2024-03-19 20:30
slug: with-as
compatibility_key: with-as
type: clause
name: WITH .. AS
title: SQL WITH ... AS clause
description: SQL WITH .. AS clause or Common Table Expression is used to define temporary queries (subqueries).
keywords: SQL, WITH AS
see_also_pages:
  - name: Common Table Expressions (CTEs) in MySQL
    url: /mdn/common-table-expressions-in-mysql
---

# WITH AS clause in SQL

The `WITH..AS` clause in SQL, often referred to as the Common Table Expression (CTE), is a temporary result set which you can reference within a `SELECT` statement.

CTEs can make your queries more readable and modular, allowing for better readability, easier debugging or performance optimization.

## Syntax

The `WITH..AS` clause allows you to define a CTE as follows:

~~~pgsql
WITH cte_name AS (
  SELECT column1, column2
  FROM existing_table
  WHERE
    filters
)
SELECT *
FROM cte_name
~~~
{: .js-no-run-query-link }

:mag: You can read it as:

* Step 1. We define a virtual `cte_name` table.
* Step 2. We're querying the virtual `cte_name` table as if it was a real table in our database.

## Simplifying Complex Queries

CTEs can be particularly useful in simplifying complex SQL queries by breaking them down into smaller, more manageable pieces.

For instance, if you're working with nested `SELECT` statements, using a CTE can make your query more readable.

### :red_circle: BAD

Look how heavy and unreadable a nested query looks like:

~~~pgsql
SELECT
  email, age
FROM (
  SELECT *
  FROM users
  WHERE
    status = 'customer'
) AS customers
~~~

### :green_circle: GOOD

A CTE, on the other hand, allows us to read the same query top-to-bottom and follow the author's idea of data analysis:

~~~pgsql
WITH customers AS (
  SELECT *
  FROM users
  WHERE
    status = 'customer'
)

SELECT
  email, age
FROM customers
~~~

## Using `WITH..AS` for Data Preparation

The `WITH..AS` clause is a perfect tool for data preparation.

Such preparation steps might include:

* **Data Cleaning**. I bet you've already heard a phrase ":hankey: IN – :hankey: OUT". If we have duplicated, incomplete or broken records before our data analysis, chances are they might ruin the result.
* **Transformations**. For example, we might not be interested in specific user ages, but in age groups – 16-21, 22-30, 31-40, etc. We can use CTE to add a new `age_group` column to the existing `users` table.

:mortar_board: Try adding a CTE to the following query to calculate age groups:

~~~pgsql
SELECT age
FROM users
~~~

Here'e a free SQL Habit lesson that might help: [If/else logic via CASE statement](/content/lessons/if-else-logic-via-case-statement).

{{compatibility}}

{{see_also}}
