---
slug: extract
navbar_copy: extract()
title: SQL EXTRACT function
keywords: SQL, EXTRACT
description: SQL EXTRACT - EXTRACT function is used to extract a part of date (year, month, day, etc) from a timestamp.
type: function
compatibility_key: extract
see_also_pages:
  - https://www.sqlhabit.com/foo
  - https://www.sqlhabit.com/bar
---

# EXTRACT function

## Syntax

~~~mysql
SELECT *
FROM users
~~~

## Description

Blah

## Try it

### Selecting all rows

~~~mysql
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
