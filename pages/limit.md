---
published_at: 2024-03-28 21:30
slug: limit
type: clause
name: LIMIT
title: LIMIT clause in SQL
description: LIMIT clause in SQL specifies how many records should be in the result set.
keywords: SQL, LIMIT
see_also_pages:
  - name: SELECT statement in SQL
    url: /mdn/select
  - name: FROM keyword in SQL
    url: /mdn/from
  - name: WHERE clause in SQL
    url: /mdn/where
---

The `LIMIT` clause is an essential feature in SQL that allows you to specify the maximum number of records to return from a query (aka result set).

This is particularly useful when you're working with large datasets and you want to sample the data or avoid overwhelming your database engine with too much data to process (if you have a billion records in the database, a query without limit might scan all billion records :bomb:).

## Syntax

The basic syntax of the `LIMIT` clause is straightforward. It's the last clause of your SQL query: after your `SELECT` statement, `WHERE` conditions, `GROUP BY` and `HAVING` clauses, you add the `LIMIT` keyword followed by the number of records you want to return:

~~~pgsql
SELECT column1, column2
FROM table
LIMIT number_of_records
~~~
{: .js-no-run-query-link}

## Using LIMIT for data analysis

### Sampling data

Sampling is a common technique in data analysis for getting a sense of what the data looks like without querying the entire table.

You can often here that this technique is called "eye-balling the data":

~~~pgsql
SELECT *
FROM users
ORDER BY created_at DESC
LIMIT 10
~~~

This query returns the most recent 10 records from the `users` table, which can be useful for a quick data inspection.

### Paginating results

Pagination involves dividing a large dataset into smaller, more manageable pieces, or "pages". The `LIMIT` clause, often used in conjunction with the `OFFSET` clause, allows for effective pagination:

~~~pgsql
SELECT *
FROM users
ORDER BY created_at DESC
LIMIT 10 OFFSET 30
~~~

This query skips the first 30 records and returns the next 10, effectively displaying page 4 of the results if you consider each page to have 10 items.

You can visualize `LIMIT` and `OFFSET` like this: imagine all your records are sorted in a line. You can see only a small amount of records at a time, like through a moving window (the size is controlled by the `LIMIT` value, say `LIMIT 10`). By default, you'll see only the first 10 records, but you can move that window forward by specifying the value of the `OFFSET`.

## LIMIT for performance optimization

Limiting the number of records returned by a query can significantly improve performance, especially when dealing with large tables.

By fetching only a subset of records, you reduce the load on the database and network, leading to faster querying times.

The worst case scenario is that you have a large dataset (like a couple of billion records) and you started a query that will end up scanning through the whole table. Such a query might easily run for 30 minutes, slowing down queries of other poeple. :bomb:

In conclusion, the `LIMIT` clause is a powerful tool for controlling the size of your query results, enhancing both the usability of your SQL queries and the performance of your database interactions.

{{compatibility}}

{{see_also}}
