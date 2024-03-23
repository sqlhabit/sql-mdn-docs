---
published_at: 2024-03-23 09:00
slug: and
compatibility_key: and
type: operator
name: AND
title: AND operator in SQL
description: AND is a logical operator in SQL that is used to combine multiple conditions, typically used inside a WHERE clause.
keywords: SQL, AND, boolean, condition
---

# AND Operator in SQL

The `AND` operator in SQL is a logical operator that allows you to combine two or more conditions.

The `AND` operator in SQL, as well as in many programming languages, originates from boolean algebra, a branch of mathematics concerned with operations on logical values. In boolean algebra, an `AND` operation takes two boolean inputs (true/false) and returns true only if both inputs are true. This concept is directly applicable in SQL where `AND` is used to test whether multiple conditions are true simultaneously.

## AND application in SQL

The truth table (a tool that shows any operotor's output for all possible input combinations) for the `AND` operation is as follows:

| A     | B     | A AND B |
|-------|-------|---------|
| TRUE  | TRUE  | TRUE    |
| TRUE  | FALSE | FALSE   |
| FALSE | TRUE  | FALSE   |
| FALSE | FALSE | FALSE   |

This table shows that the `AND` operation returns true only when both A and B are true, mirroring its use in SQL where a row must satisfy all conditions connected by `AND` to be included in the result set.

Thus, the `AND` operator in SQL is a direct application of mathematical principles from boolean algebra, enabling precise filtering of data based on multiple criteria.

When using the `AND` operator, all conditions must be true for the rows to be included in the result set. It is crucial for filtering data based on multiple criteria, making your queries more specific and targeted.

## AND in WHERE clause

Here's an example of the `AND` operator used in the `WHERE` clause to filter records based on more than one condition:

~~~pgsql
SELECT *
FROM users
WHERE
  country = 'us'
  AND status = 'customer'
~~~

## AND in SELECT clause

The `WHERE` clause is not the only place you can use `AND` in a query. In fact, you can use it anywhere you can use boolean values (TRUE/FALSE). Here's an example of a query that uses the `AND` operator to calculate a new boolean value:

~~~pgsql
SELECT
  status = 'customer' AND referrer_id IS NOT NULL AS is_invited_customer,
  *
FROM users
WHERE
  country = 'us'
  AND status = 'customer'
~~~

## AND in JOIN clause

Another common place for using the `AND` operator is inside `JOIN` clauses:

~~~pgsql
SELECT *
FROM users u
INNER JOIN purchases p
  ON u.id = p.user_id
    AND p.refunded = FALSE
~~~

## Tips for Using AND in SQL

* Remember that all conditions connected by `AND` must be true for a row to be included in the result set.
* Use parentheses `()` to group conditions and control the precedence of evaluation, especially when combining `AND` with `OR` operators.

{{compatibility}}

{{see_also}}
