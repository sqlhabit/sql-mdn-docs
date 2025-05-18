---
published_at: 2024-03-23 10:00
slug: or
types:
  - operator
name: OR
title: OR operator in SQL
description: OR is a logical operator in SQL that is used to combine multiple conditions, typically used inside a WHERE clause.
keywords: SQL, OR, boolean, condition
see_also_pages:
  - name: AND operator in SQL
    url: /mdn/and
  - name: CASE operator in SQL
    url: /mdn/case
---

The `OR` operator in SQL is used to combine multiple conditions in a `WHERE` clause, but unlike [the `AND` operator](/mdn/and), it only requires one of the conditions to be true for a row to be included in the result set. This makes the `OR` operator particularly useful for filtering data based on alternative criteria, allowing for more flexible and inclusive queries.

The `OR` operator comes from a math area called [Boolean algebra](https://en.wikipedia.org/wiki/Boolean_algebra), that operates with `TRUE` or `FALSE` values. Think of `OR` as making a choice between two things: if either one is true, or both are, then the whole thing is true. It's really useful in SQL because it helps you build more flexible conditions for filtering data.

## OR application in SQL

The truth table (a tool used in boolean algebra to show operotor's output for all possible inputs) for the `OR` operator looks like this:

| A     | B     | A OR B  |
|-------|-------|---------|
| TRUE  | TRUE  | TRUE    |
| TRUE  | FALSE | TRUE    |
| FALSE | TRUE  | TRUE    |
| FALSE | FALSE | FALSE   |
{: .table-with-header }

This table shows that the `OR` operator returns true when any value of A or B is true, mirroring its use in SQL where a row must satisfy at least one condition connected by the `OR` operator to be included in the result set.

Thus, the `OR` operator in SQL is a direct application of mathematical principles from boolean algebra, enabling flexible filtering of data based on multiple criteria.

:bulb: When using the `OR` operator, at least one condition must be true for the rows to be included in the result set. It helps greatly with filtering data based on multiple criteria.

## OR in WHERE clause

The `WHERE` clause is where the `OR` operator is most commonly used, enabling the selection of rows that match any one of the provided conditions. For instance, here's a query that lists all users that are 21-65 years old:

~~~pgsql
SELECT *
FROM books
WHERE
  genre = 'Thriller'
  OR genre = 'Horror'
~~~

## Using OR in SELECT clause

Although the `OR` operator is predominantly used within `WHERE` clauses to filter selected data based on conditions, its principle of inclusivity can indirectly influence how `SELECT` statements are constructed.

Here's an example of such a query:

~~~pgsql
SELECT
  genre = 'Thriller' OR genre = 'Horror' AS is_scary_book,
  *
FROM books
~~~

## Tips for using OR in SQL

* Remember that if any condition connected by `OR` for a row is true, this row will be included in the result set
* Use parentheses `()` to group conditions and control the precedence of evaluation, especially when combining `AND` with `OR` operators.

{{compatibility}}

{{see_also}}
