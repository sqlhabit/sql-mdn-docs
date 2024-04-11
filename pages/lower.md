---
published_at: 2024-04-11 21:15
slug: lower
type: function.text
name: lower
title: lower() function in SQL
description: The lower() function in SQL is used to convert all letters in a specified string to lowercase.
keywords: SQL, lower, function
see_also_pages:
  - name: upper() function in SQL
    url: /mdn/upper
  - name: length() function in SQL
    url: /mdn/length
  - name: reverse() function in SQL
    url: /mdn/reverse
---

# `lower()` function in SQL

The `lower()` function is used to convert all letters in a specified string to lowercase. It is particularly useful when you need to perform case-insensitive comparisons or ensure data consistency across different text entries in your database.

## Syntax

The syntax for the `lower()` function is straightforward:

~~~pgsql
SELECT lower(column_name)
FROM table_name
~~~
{: .js-no-run-query-link }

This function takes a single argument, which is the text column you wish to convert to lowercase.

Here's a simple example that demonstrates how the `lower()` function works without table data:

~~~pgsql
SELECT lower('HELLO@gmail.COM')
~~~

## Using `lower()` in filters

Consider a scenario where you have a database of users, and you want to find all users whose name is "john". However, the names in the database are entered in a mix of uppercase and lowercase letters, like "John", "JOHN", or "jOhN". To reliably find all variations, you can use the `lower()` function:

~~~pgsql
SELECT *
FROM users
WHERE
  lower(first_name) = 'john'
~~~

This query converts all names to lowercase before comparing them to 'john', ensuring that the comparison is case-insensitive.

## Using `lower()` in SELECT statement

For a more generic name analysis we'd use the `lower()` function inside the [`SELECT`](/mdn/select) statement:

~~~pgsql
WITH modified_users AS (
  SELECT
    *,
    lower(first_name) AS lower_cased_first_name
  FROM users
)

SELECT
  lower_cased_first_name,
  COUNT(*)
FROM users
GROUP BY 1
ORDER BY 2 DESC
~~~

In this example we're counting user first names. Since inside the `users` table we don't know how the names are formatted, the `lower()` function helps us to unify the format before aggregation.

The `lower()` function is not only useful for practical querying but also a great way to practice SQL. Experimenting with different strings and functions can help you understand how SQL processes text data.

{{compatibility}}

{{see_also}}
