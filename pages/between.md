---
published_at: 2024-04-07 12:00
slug: between
type: operator
name: BETWEEN
title: BETWEEN operator in SQL
description: The BETWEEN operator in SQL is used to filter data within a specific range.
keywords: SQL, operator, BETWEEN
see_also_pages:
  - name: IN operator in SQL
    url: /mdn/in
  - name: IS operator in SQL
    url: /mdn/is
  - name: AND operator in SQL
    url: /mdn/and
  - name: OR operator in SQL
    url: /mdn/or
---

The `BETWEEN .. AND` operator in SQL is used to filter the data within a specific range.

This operator can be used with numbers, text (to filter within alphabetical ranges), and dates, making it versatile for various types of Data Analysis.

## Syntax

The syntax for `BETWEEN .. AND` is straightforward. You specify the column name followed by the `BETWEEN` keyword, the start of the range, the `AND` keyword, and then the end of the range.

~~~pgsql
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2
~~~
{: .js-no-run-query-link }

For example, to select users with age between 21 and 65:

~~~pgsql
SELECT
  age,
  *
FROM users
WHERE
  age BETWEEN 21 AND 65
~~~

:mag: The `BETWEEN` operator is **inclusive**, meaning it includes the values specified by the `BETWEEN` and `AND` keywords to the result (`value1` and `value2` in our case).

In practice, it means that in this query's result set you'll find users with age 21 and 65.

## Selecting dates within a range

The `BETWEEN .. AND` operator is particularly useful for performing range queries, such as finding records within a specific date range. Here's a query that finds users who signed up within a specific date range:

~~~pgsql
SELECT *
FROM users
WHERE
  signup_date BETWEEN '2018-01-01' AND '2018-01-31'
~~~

### Analyzing specific numerical ranges

To filter purchases within a specific amount range:

~~~pgsql
SELECT *
FROM purchases
WHERE
  amount BETWEEN 10 AND 20
~~~

This query is equivalent to the following:

~~~pgsql
SELECT *
FROM purchases
WHERE
  amount >= 10
  AND amount <= 20
~~~

As you can see, the `BETWEEN..AND` version is more concise and readable.

Understanding and using the `BETWEEN .. AND` operator is crucial for efficiently querying subsets of data based on specific criteria.

:warning: The only trick to remember is that the `BETWEEN` operator is **inclusive**.

{{compatibility}}

{{see_also}}
