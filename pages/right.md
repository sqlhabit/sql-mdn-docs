---
published_at: 2024-04-13 08:05
slug: right
type: function.text
name: right
title: right() function in SQL
description: The right() function in SQL is used to extract a specified number of characters from the end of a string.
keywords: SQL, right, function
see_also_pages:
  - name: left() function in SQL
    url: /mdn/left
  - name: substring() function in SQL
    url: /mdn/substring
  - name: upper() function in SQL
    url: /mdn/upper
---

The `right()` function in SQL is used to extract a specified number of characters from the end of a string. This function is crucial for operations that involve data extraction based on character position from the end of strings, such as analyzing file extensions, processing right-aligned data, or handling formatted text fields.

## Syntax

The syntax for the `right()` function is straightforward:

~~~pgsql
SELECT right(string, number)
~~~
{: .js-no-run-query-link }

This function takes two arguments: the string from which to extract characters, and the number of characters to extract from the right.

Here's a trivial example:

~~~pgsql
SELECT right('foobar', 3)
~~~

## Using `right()` in practice

If you have a table with credit card details and you want to extract only the last 4 digits for your report, here's a query that can do that with the `right()` function:

~~~pgsql
WITH credit_cards AS (
  SELECT '1111222233334444' AS card_number
  UNION
  SELECT '5555666677778888'
)

SELECT right(card_number, 4)
FROM credit_cards
~~~

:mag: Note how we used a [CTE](/mdn/with-as) to emulate a `credit_cards` table for this example.

## Extracting suffix with `right()`

For example, if you have a `subscriptions` table where an identifier contains a country code suffix, we can use the `right()` function to extract it:

~~~pgsql
WITH products AS (
  SELECT 'monthly-US' AS slug
  UNION
  SELECT 'yearly-de'
)

SELECT lower(right(slug, 2)) AS country
FROM subscriptions
~~~

:bulb: Note that we can reliably do it, since country codes are always 2 characters.

## Combining `right()` with other functions

`right()` can be combined with other SQL functions to handle more complex scenarios.

In the previous example, you see that country codes could be in lowercase or uppercase. Let's use the [`upper()`](/mdn/upper) function to normalize extracted country codes:

~~~pgsql
WITH products AS (
  SELECT 'monthly-US' AS slug
  UNION
  SELECT 'yearly-de'
)

SELECT upper(right(slug, 2)) AS country
FROM subscriptions
~~~

The `right()` function is a vital tool in SQL for text processing, particularly useful in scenarios where the end part of a string carries significant information or needs special handling.

{{compatibility}}

{{see_also}}
