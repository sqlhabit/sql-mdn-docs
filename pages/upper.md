---
published_at: 2024-04-11 21:25
slug: upper
type: function.text
name: upper
title: upper() function in SQL
description: The upper() function in SQL is used to convert all letters in a specified string to uppercase.
keywords: SQL, upper, function
see_also_pages:
  - name: lower() function in SQL
    url: /mdn/lower
  - name: length() function in SQL
    url: /mdn/length
  - name: reverse() function in SQL
    url: /mdn/reverse
---

The `upper()` function is used to convert all the letters in a specified string to uppercase. This function is essential for formatting outputs, ensuring consistency in case-sensitive operations, and facilitating case-insensitive searches by standardizing text data to a uniform case.

## Syntax

The basic syntax for the `upper()` function is:

~~~pgsql
SELECT UPPER(column_name)
FROM table_name
~~~
{: .js-no-run-query-link }

It accepts a single text argument: the column or string expression you wish to convert to uppercase.

Here's a basic example that doesn't even require a table:

~~~pgsql
SELECT upper('foobar')
~~~

## Using `upper()` in practice

Imagine a database containing product information where the product names are stored in varying cases. To standardize the output for reporting or searching purposes, you can convert all product names to uppercase:

~~~pgsql
SELECT upper(name) AS product_name
FROM products
~~~

This query not only converts the names but also aliases the result column as `product_name` for better readability in the results.

## Combining `upper()` with other functions

`upper()` can be effectively combined with other SQL functions for more complex queries.

For example, if you are looking for all monthly product entries, regardless of case, you could use:

~~~pgsql
SELECT *
FROM products
WHERE
  upper(name) LIKE '%MONTHLY%'
~~~

This approach ensures that the search is case-insensitive by converting the column values to uppercase.

{{compatibility}}

{{see_also}}
