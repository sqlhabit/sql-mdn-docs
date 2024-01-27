---
slug: distinct
compatibility_key: distinct
title: SQL DISTINCT statement
keywords: SQL, DISTINCT
description: SQL DISTINCT - DISTINCT tells SQL engine to present only unique records in the result set.
type: statement
see_also_pages:
  - https://www.sqlhabit.com/mdn/foo
  - https://www.sqlhabit.com/mdn/bar
---

# SQL DISTINCT

## Syntax

~~~pgsql
SELECT DISTINCT(country)
FROM users
~~~

## Description

TODO

## Try it

### With brackets

~~~pgsql
SELECT DISTINCT(country)
FROM users
~~~

### Without brackets

~~~pgsql
SELECT DISTINCT country
FROM users
~~~

## Database compatibility

{{compatibility}}

## See also

{{see_also}}
