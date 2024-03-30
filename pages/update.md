---
published_at: 2024-03-30 09:45
slug: update
type: statement
name: UPDATE
title: UPDATE statement in SQL
description: UPDATE statement in SQL is used to modify records in a table.
keywords: SQL, UPDATE
see_also_pages:
  - name: SELECT statement in SQL
    url: /mdn/select
---

`UPDATE` is a SQL command used to modify existing records in a table. It allows you to change the data of one or multiple rows based on specific criteria.

Typically, one would very rarely run `UPDATE` statements manually, because in contemporary data stacks there's a whole tech (ETL pipelines, etc) that cleans, transforms and maintains the quality of the data.

It's still important to know how to run the `UPDATE` statements. It'll come handy when prototyping tables, working in isolated sandboxes or hacking things together.

## Syntax

The basic syntax of an `UPDATE` statement includes specifying the table name, the column(s) you wish to change, and the new value(s) for those columns. You can also use a `WHERE` clause to narrow down the rows that will be updated.

~~~pgsql
UPDATE table_name
SET
  column1 = value1,
  column2 = value2
WHERE
  conditions
~~~
{: .js-no-run-query-link }

## Updating multiple columns

You can update more than one column in a single `UPDATE` statement. To do this, separate each column-value pairs with a comma:

~~~pgsql
UPDATE purchases
SET
  refunded = TRUE,
  updated_at = now()
WHERE
  id = 3084
~~~
{: .js-no-run-query-link }

This query updates a specific purchase, indicating that the purchase was refunded.

## Using UPDATE with conditions

The `WHERE` clause in an `UPDATE` statement specifies which rows should be updated. Without a `WHERE` clause, all rows in the table will be updated, which is rarely what you want. :bomb:

Note that you can update a single row (like in a previous query) or update a group of rows like in this example:

~~~pgsql
UPDATE products
SET
  price = price * 1.2
WHERE
  name ILIKE '%yearly subscription%'
~~~
{: .js-no-run-query-link }

This query increases the price of all yearly subscription products.

## Tips for using UPDATE

- Always back up your data before running bulk `UPDATE` operations :bulb:
- Test your `UPDATE` statements on a small subset of the data first to ensure they work as expected

`UPDATE` statement is a powerful tool for modifying your data. With great power comes great responsibility, so use it wisely to keep your database accurate and up-to-date.

{{compatibility}}

{{see_also}}
