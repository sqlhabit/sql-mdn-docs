---
published_at: 2024-04-13 08:35
slug: rpad
types:
  - function.text
name: rpad
title: rpad() function in SQL
description: The rpad() function in SQL is used to pad a string with another string to a specified total length from the right side.
keywords: SQL, rpad, function
see_also_pages:
  - name: lpad() function in SQL
    url: /mdn/lpad
  - name: WITH..AS clause in SQL
    url: /mdn/with-as
  - name: repeat() function in SQL
    url: /mdn/repeat
---

The `rpad()` function in SQL (short for "right pad") is used to pad a string with another string to a specified total length from the right side. This function is essential for ensuring consistent formatting across textual data, aligning text in reports, or setting up data for systems that require fixed-width fields.

## Syntax

The syntax for the `rpad()` function involves three arguments:

~~~pgsql
SELECT rpad(string, length, pad_string)
~~~
{: .js-no-run-query-link }

- **string** is the original string to pad.
- **length** is the desired total length of the output string after padding.
- **pad_string** is the string used to pad the original string to the desired length.

Here's a basic example:

~~~pgsql
SELECT rpad('foo', 6, 'b')
~~~

:mag: Note that the **pad_string** could also be a multicharacter string:

~~~pgsql
SELECT rpad('foo', 10, 'bar')
~~~

In that case, the SQL engine will try to fit as many **pad_string**-s as possible from left to right (the last **pad_string** might be cut to achieve the desired **length**).

## Using `rpad()` in practice

Imagine we're buildling a table of contents for book catalog. We need to list all books and make sure each line has a length of 50 characters: a book title padded with dashes. Here's a query that does exactly that:

~~~pgsql
SELECT rpad(name, 50, '-') AS padded_name
FROM books
~~~

{{compatibility}}

{{see_also}}
