---
published_at: 2024-02-09 21:53
name: SELECT
type: statement
compatibility_key: select
slug: select
title: SQL SELECT statement
keywords: SQL, SELECT
description: SQL SELECT - SELECT statement is used to fetch the data from a database table. SELECT statement returns a table that's also called a result set.
---

# SELECT statement

`SELECT` is a fundamental SQL command that is used to retrieve data from one or more tables in a database. It is one of the most commonly used commands in SQL for querying a database to fetch data that matches specific criteria.

The result of a `SELECT` query is called a **result set** (basically a new table).

## Syntax

Inside a SELECT statement, you can specify which columns you want to have in your result set.

You can use a wildcard symbol `*` to select all available columns from a table.

~~~pgsql
SELECT *
FROM users
~~~

Sometimes it returns too many columns, so usually you want to specify the columns you want to get:

~~~pgsql
SELECT
  id,
  email,
  country,
  age
FROM users
~~~

## Using SELECT for learning SQL

`SELECT` is the most fundamental and most used keyword in SQL. You'll for sure use it a LOT to get data for creating reports, hunting for insights, etc.

You can also use `SELECT` statement to learn SQL and practice different expressions, operators, or functions.

For example, this is a valid SQL query, try running it:

~~~pgsql
SELECT 1
~~~

We're basically telling the database "Give me 1" and you'll get a result set with just a number.

In the same way, you can test a comparison operator `=`:

~~~pgsql
SELECT 1 = 2
~~~

My favorite trick is to use the `SELECT` statement for playing with SQL functions and see what they return and if I use them correctly. For example, if you want to check if the first element in the `split_part()` is indexed with 0 or 1 you can run a query like this:

~~~pgsql
SELECT split_part('Hello world', ' ', 1)
~~~

{{compatibility}}

{{see_also}}
