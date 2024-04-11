---
published_at: 2024-04-11 08:00
slug: replace
type: function.text
name: replace
title: replace() function in SQL
description: The replace() function is used to replace a substring in a string.
keywords: SQL, replace, function
see_also_pages:
  - name: concat() function in SQL
    url: /mdn/concat
  - name: substring() function in SQL
    url: /mdn/substring
  - name: CASE operator in SQL
    url: /mdn/case
  - name: COALESCE() function in SQL
    url: /mdn/coalesce
---

The `replace()` function is an essential tool in SQL for altering string data. It searches for a specified substring in a string and replaces it with another substring. This functionality is incredibly useful for cleaning or modifying text data within a database.

## Syntax

The basic syntax for the `replace()` function is straightforward:

~~~pgsql
SELECT REPLACE(string, substring_to_replace, replacement_substring)
~~~
{: .js-no-run-query-link }

We can see the `replace()` function in action without a table:

~~~pgsql
SELECT REPLACE('foobar@gmail.com', '@gmail.com', '')
~~~

## Using `replace()` to clean data

Data often comes with inconsistencies, especially in text form. The `replace()` function can be used to standardize or clean this data. For instance, replacing abbreviations with their full form or correcting common misspellings.

For example, correcting a common misspelling in a URL slug:

~~~pgsql
SELECT
  REPLACE(genre, 'Clasic', 'Classic')
FROM books
~~~

This query searches the `genre` column for the misspelling 'Clasic' and replaces it with the correct spelling 'Classic'.

## Removing unwanted characters

Sometimes you might want to remove certain characters from a string, like removing dashes from phone numbers to standardize the format. You can do this by replacing the character with an empty string:

~~~pgsql
SELECT
  REPLACE(url, 'https://', '')
FROM web_analytics.pageviews
~~~

In this example we're removing the "https://" substring from all URLs in the pageviews table. This will simplify our web analytics reports and make them easier to digest, since the "https://" substring present in every single URL.

## Handling NULL values

Be cautious when using `replace()` with possible `NULL` values in your data. `replace()` will return NULL if any of its arguments is `NULL`. To handle this, you might need to use [`COALESCE`](/mdn/coalesce) or [conditional logic](/mdn/case) to ensure your queries execute as expected.

`replace()` is a versatile function for string manipulation, allowing for the cleaning, standardizing, and modifying of text data. Mastering its use can significantly improve the quality of data analysis and reporting by ensuring data consistency and accuracy.

{{compatibility}}

{{see_also}}
