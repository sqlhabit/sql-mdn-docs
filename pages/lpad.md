---
published_at: 2024-04-13 08:20
slug: lpad
type: function.text
name: lpad
title: lpad() function in SQL
description: The lpad() function in SQL is used to pad a string with another string to a specified total length from the left side.
keywords: SQL, lpad, function
see_also_pages:
  - name: rpad() function in SQL
    url: /mdn/rpad
  - name: repeat() function in SQL
    url: /mdn/repeat
  - name: WITH..AS clause in SQL
    url: /mdn/with-as
---

The `lpad()` function in SQL (short for "left pad") is used to pad a string with another string to a specified total length from the left side. This function is helpful for formatting output, aligning data within reports, or preparing data for applications that require fixed-width text fields.

## Syntax

The syntax for the `lpad()` function involves three arguments:

~~~pgsql
SELECT lpad(string, length, pad_string)
~~~
{: .js-no-run-query-link }

- **string** is the original string to pad.
- **length** is the desired total length of the output string after padding.
- **pad_string** is the string used to pad the original string to the desired length.

Here's a basic example:

~~~pgsql
SELECT lpad('bar', 6, 'f')
~~~

:mag: Note that the **pad_string** could also be a multicharacter string:

~~~pgsql
SELECT lpad('bar', 10, 'foo')
~~~

In that case, the SQL engine will try to fit as many **pad_string**-s as possible from left to right (the last **pad_string** might be cut to achieve the desired **length**).

## Using `lpad()` in practice

Imagine you need to format credit cards data so that all numbers appear real 16 character card numbers. You can use the `lpad()` function to add leading symbols to 4-digit numbers from the table:

~~~pgsql
WITH credit_cards AS (
  SELECT '1248' AS last_four_digits
  UNION
  SELECT '5914'
)

SELECT lpad(last_four_digits, 16, '0000')
FROM credit_cards
~~~

:mag: Note how we used a [CTE](/mdn/with-as) to emulate a `credit_cards` table for this example.

`lpad()` is a versatile SQL function that is indispensable for data formatting, allowing for the creation of visually consistent and professionally formatted text outputs.

{{compatibility}}

{{see_also}}
