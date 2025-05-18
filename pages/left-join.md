---
published_at: 2024-04-07 16:00
slug: left-join
types:
  - clause
name: LEFT JOIN
title: LEFT JOIN in SQL
description: LEFT JOIN clause in SQL is used to combine rows from two or more tables, based on a relation between them.
keywords: SQL, LEFT JOIN
see_also_pages:
  - name: INNER JOIN in SQL
    url: /mdn/inner-join
---

The `LEFT JOIN` clause in SQL, also known as `LEFT OUTER JOIN`, is used to combine rows from two or more tables. Unlike an `INNER JOIN`, a `LEFT JOIN` will return **all rows from the left table**, and the matched rows from the right table. If there is no match, the result is NULL on the side of the right table.

Here's a diagram you'll typically see on the Internet:

![LEFT JOIN in SQL](https://github.com/sqlhabit/sql-mdn-docs/blob/main/images/left_join.png?raw=true)

## Syntax

The syntax for `LEFT JOIN` includes specifying **the primary table** (left table) and the table to be joined (right table), along with the join condition:

~~~pgsql
SELECT
  t1.*,
  t2.*
FROM table1 t1
LEFT JOIN table2 t2
  ON t1.common_column = t2.common_column
~~~
{: .js-no-run-query-link }

:mag: Note that we specified `t1` and `t2` table aliases to avoid writing full table names in the join condition like `table1.common_column`.

Here's an example where we join `purchases` to all `users`:

~~~pgsql
SELECT *
FROM users u
LEFT JOIN purchases p
  ON u.id = p.user_id
~~~

In this example, all records from the left table (`users`) will be present in the result set (hence filled left circle in the diagram). All purchases that satisfy the join condition (i.e. that belong to a user) will also be in the result set. For users without purchases (no correspondent `purchases` records) the purchases rows will contain `NULL` values in all columns from the `purchases` table.

:bulb: Simply run the example query :point_up: and browse the result set.

## Joining multiple tables

We can use multiple `JOIN` clauses within one query, that's the whole idea behind relational databases – to join related data. Here's an example where we join users, their pageviews and purchases (for example, to calculate purchase rate later):

~~~pgsql
SELECT *
FROM users u
LEFT JOIN purchases p
  ON u.id = p.user_id
LEFT JOIN web_analytics.pageviews pv
  ON u.id = pv.user_id
~~~

## Complex join conditions

For `LEFT JOIN`, a record from the right table will be joined to the left record only when the join condition (`ON ...`) is evaluated to `TRUE`.

In the previous examples, we've used a very simple join condition like `ON u.id = pv.user_id`. As you can see, it could be `TRUE` (when id-s match) or `FALSE`.

We can use more complex conditions and enhance them with other logical operators like [`AND`](/mdn/and), [`OR`](/mdn/or), etc.

Here's an example where we join non-refunded purchases to all users:

~~~pgsql
SELECT *
FROM users u
LEFT JOIN purchases p
  ON u.id = p.user_id
    AND p.refunded = FALSE
~~~

Understanding and using `LEFT JOIN` effectively allows for more versatile and comprehensive data analysis. The `LEFT JOIN` comes very handy in scenarios where maintaining a complete list from one table is crucial (calculating per-user metrics, for example).

The `LEFT JOIN` clause is invaluable for detailed reporting and ensuring no data is overlooked simply because it does not have a corresponding match in another table.

[`INNER JOIN`](/mdn/inner-join) and `LEFT JOIN` are a must-have for anyone who works with relational data.

{{compatibility}}

{{see_also}}
