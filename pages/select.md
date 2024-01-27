---
slug: select
title: SQL SELECT statement
keywords: SQL, SELECT
description: SQL SELECT - SELECT Statement is used to fetch the data from a database table which returns this data in the form of a table.
type: statement
compatibility_key: select
see_also:
  - >
    [Foo](https://www.sqlhabit.com/mdn/foo)
  - >
    Also check out [Bar](https://www.sqlhabit.com/mdn/bar)
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
