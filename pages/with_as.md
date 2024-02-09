---
slug: with-as
published_at:
navbar: WITH .. AS
title: SQL WITH ... AS clause
keywords: SQL, WITH, AS
description: SQL WITH ... AS - WITH .. AS clause or Common Table Expression is used to define temporary queries (subqueries).
type: clause
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
