---
published_at: 2024-04-12 07:30
slug: repeat
type: function.text
name: repeat
title: repeat() function in SQL
description: The repeat() function is used to repeat a string a specified number of times.
keywords: SQL, repeat, function
see_also_pages:
  - name: substring() function in SQL
    url: /mdn/substring
---

The `repeat()` function in SQL is used to repeat a string a specified number of times. This function can be helpful for generating test data, formatting output, or creating visual effects in textual data presentations.

## Syntax

The syntax for the `repeat()` function is as follows:

~~~pgsql
SELECT repeat(string, number)
~~~
{: .js-no-run-query-link }

This function takes two arguments: the string to repeat and the number of times to repeat it.

Here's a basic example:

~~~pgsql
SELECT repeat('Hello', 3)
~~~

## repeat() for visual separator

Imagine you need to generate a visual separator in a report generated from SQL queries. You can use the `repeat()` function to create a line of dashes:

~~~pgsql
SELECT repeat('-', 20) AS separator
~~~

This query will produce a string of 20 dashes, which can be used as a divider between sections of a report.

## repeat() for credit card placeholder

The same way way we can generate a credit card placeholder instead of showing a real credit card number in our research:

~~~pgsql
SELECT repeat('X', 16) AS credit_card_number
~~~

The `repeat()` function isn't something you'd use every day for Data Analysis, but it's a versatile tool in SQL for enhancing the manipulation and presentation of string data, offering extensive possibilities for creative and practical applications.

{{compatibility}}

{{see_also}}
