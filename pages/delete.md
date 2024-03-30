---
published_at: 2024-03-30 10:10
slug: delete
type: statement
name: DELETE
title: DELETE statement in SQL
description: DELETE statement in SQL is used to remove rows from a table based on a specific condition.
keywords: SQL, DELETE, statement
see_also_pages:
  - name: SELECT statement in SQL
    url: /mdn/select
  - name: UPDATE statement in SQL
    url: /mdn/update
  - name: INSERT statement in SQL
    url: /mdn/insert
---

`DELETE` is a SQL command used to remove rows from a table based on a specific condition.

The action of a `DELETE` query permanently removes records from a table, making it essential to use this command with caution.

Typically, one would very rarely run a `DELETE` query manually, since modern data stack (ETL pipelines, etc) rotate the data and clean up tables on an hourly/daily/weekly basis.

It's still important to know how to run `DELETE` queries. When you're prototyping something or working in an isolated sandbox, deleting a bunch of rows shouldn't be an issue. Plus, it's always useful to know how to hack things. Let's get started with the `DELETE` statement.

## Syntax

The basic syntax of a `DELETE` statement allows you to specify the table from which you want to delete rows, and optionally, a condition to select which rows to remove.

~~~pgsql
DELETE FROM users
WHERE email = 'foo@bar.com'
~~~
{: .js-no-run-query-link }

Without a `WHERE` clause, a `DELETE` statement will remove all rows from the table, which can be catastrophic if not intended :bomb:.

~~~pgsql
DELETE FROM users
~~~
{: .js-no-run-query-link }

Hence there's a simple rule: never run a `DELETE` statement in a production database or production data warehouse. If you have to – **triple check** everything.

## DELETE safety checks

Because `DELETE` operations are irreversible (outside of transaction controls), it's critical to always verify the `WHERE` clause to avoid accidental data loss.

For practice, you can use `DELETE` on a test table or ensure you have backups of your data before performing delete operations on important tables.

A safe practice is to perform a `SELECT` query before the `DELETE` to make sure you're targeting the right rows:

~~~pgsql
SELECT *
FROM users
WHERE
  country = '' OR country IS NULL
~~~

Following the selection, if you're confident in the rows you're about to delete:

~~~pgsql
DELETE FROM users
WHERE country = '' OR country IS NULL
~~~
{: .js-no-run-query-link }

{{compatibility}}

{{see_also}}
