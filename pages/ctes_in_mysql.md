---
published_at: 2024-03-21 21:30
slug: common-table-expressions-in-mysql
compatibility_key: mysql-cte-workaround
type: misc
name: Common Table Expressions (CTEs) in MySQL
title: Common Table Expressions (CTEs) in MySQL
description: What to use instead of CTE-s in MySQL
keywords: SQL, MySQL, CTE, Common Table Expressions
compatibility: false
see_also_pages:
  - name: WITH..AS clause in SQL
    url: /mdn/with-as
---

# Common Table Expressions (CTEs) in MySQL

Common Table Expressions, or CTEs, have revolutionized the way we can query databases, offering a more readable and maintainable approach to constructing complex SQL queries.

[MySQL](https://en.wikipedia.org/wiki/MySQL) introduced support for CTEs starting from version 8.0, marking a significant enhancement in its SQL querying capabilities. Version 8.0 was released on September, 2016.

## What are CTEs?

CTEs allow the creation of temporary result sets (read: virtual table) that can be referred to in a `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statements. They can simplify complex queries by breaking them down into simpler, more readable components.

### Advantages of CTEs

* **Readability**: By separating parts of complex queries, CTEs make it easier to understand the query's logic.
* **Maintainability**: CTEs help in organizing the query better, making it simpler to modify and maintain.

## CTE Support in MySQL

MySQL began supporting CTEs in version 8.0. If you're working with MySQL 8.0 or later, you can leverage the power of CTEs to simplify your SQL queries.

### Basic CTE Syntax

~~~pgsql
WITH customers AS (
    SELECT id, email, country
    FROM users
    WHERE
      status = 'customer'
)
SELECT *
FROM customers
WHERE
  country = 'us'
~~~

This example illustrates a simple CTE that selects certain columns from a table and then uses them in the main query.

## Alternatives for Older Versions

For those using MySQL versions earlier than 8.0, similar functionality can be achieved through subqueries or temporary tables, although these might not be as efficient or easy to manage as CTEs.

Subquery Example:

~~~pgsql
SELECT *
FROM (
  SELECT id, email, country
  FROM users
  WHERE
    status = 'customer'
) AS customers
WHERE
  country = 'us'
~~~

While not as elegant or powerful as CTEs, subqueries offer a workaround for complex queries in older versions of MySQL.

In summary, CTEs provide a significant boost in writing complex queries in a more manageable way. For those on MySQL 8.0 or later, embracing CTEs can lead to cleaner, more understandable SQL code. If you're running MySQL older than 8.0 – time for an upgrade? :wink:

{{compatibility}}

{{see_also}}
