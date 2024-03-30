---
published_at: 2024-03-30 11:30
slug: insert
type: statement
name: INSERT
title: INSERT statement in SQL
description: INSERT statement in SQL is used to add new rows to a table.
keywords: SQL, INSERT, statement
see_also_pages:
  - name: SELECT statement in SQL
    url: /mdn/select
  - name: DELETE statement in SQL
    url: /mdn/delete
  - name: UPDATE statement in SQL
    url: /mdn/update
---

`INSERT` is a crucial SQL command used to add new rows to a table.

It's fundamental for populating a database with data, whether you're adding a single record or multiple records at once. Understanding how to use the `INSERT` statement is essential for managing the data within your database effectively.

These days, one would rarely run an `INSERT` statement manually. Typically one inserts data to a database via a bulk import from CSV, JSON, custom API integrations, an ETL pipeline, etc. It's simply more convinient that way.

Nevertheselss, it's important to understand how the `INSERT` statement works, because any data import boils down to an `INSERT` statement internally.

## Syntax

The `INSERT` statement can be used in several ways, but at its core, it requires specifying the table to insert into and the values to insert.

To insert a single row into a table, you specify the column names and the corresponding values:

~~~pgsql
INSERT INTO users (id, email, country, age)
VALUES (1, 'foo@bar.com', 'de', 34)
~~~
{: .js-no-run-query-link }

You can also insert multiple rows in a single statement by providing multiple sets of values:

~~~pgsql
INSERT INTO users (id, email, country, age)
VALUES
  (2, 'foo@gmail.com', 'us', 25),
  (3, 'bar@example.com', 'de', 28)
~~~
{: .js-no-run-query-link }

## Using INSERT to populate your database

Populating your database with `INSERT` statements is not just about adding data; it's also a great way to learn about data integrity and relationships between tables. For example, when inserting data into a table that has a foreign key, you'll learn how to ensure that your data maintains referential integrity.

A simple `INSERT` can look like this:

~~~pgsql
INSERT INTO users (email, country)
VALUES ('foo@bar.com', 'us')
~~~
{: .js-no-run-query-link }

:bulb: This will add a new user to your `users` table, assuming that `id` is auto-incremented primary key and `age` is either nullable or has a default value.

Regardless whether you're a Product Manager, Data Analyst or an Engineer, mastering the `INSERT` command will make your more proficient at working with any sort of data.

{{compatibility}}

{{see_also}}
