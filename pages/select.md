---
slug: select
title: SQL SELECT statement
keywords: SQL, SELECT
description: SQL SELECT - SELECT Statement is used to fetch the data from a database table which returns this data in the form of a table.
type: statement
compatibility_key: select
see_also_pages:
  - https://www.sqlhabit.com/foo
  - https://www.sqlhabit.com/bar
---

# SELECT statement

## Syntax

~~~pgsql
SELECT *
FROM users
~~~

## Description

Blah

## Try it

### Selecting all rows

~~~pgsql
SELECT *
FROM users
~~~

### Selecting specific columns

~~~pgsql
SELECT
  id,
  email
FROM users
~~~

### Using aggregate functions

~~~pgsql
SELECT
  COUNT(*)
FROM users
~~~

### Using window functions

~~~pgsql
...
~~~

## Database compatibility

{{compatibility}}

## See also

{{see_also}}
