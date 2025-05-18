---
published_at: 2024-04-11 21:35
slug: length
types:
  - function.text
name: length
title: length() function in SQL
description: The length() function in SQL is used to measure the number of characters in a string.
keywords: SQL, length, function
see_also_pages:
  - name: lower() function in SQL
    url: /mdn/lower
  - name: upper() function in SQL
    url: /mdn/upper
  - name: reverse() function in SQL
    url: /mdn/reverse
---

The `length()` function in SQL is used to obtain the length of a string, measured in the number of characters.

## Syntax

The syntax for the `length()` function is simple:

~~~pgsql
SELECT length(column_name)
FROM table_name
~~~
{: .js-no-run-query-link }

This function takes a text column or a string value whose length you want to measure.

Here's a trivial example with a hardcoded string value:

~~~pgsql
SELECT length('foobar@gmail.com')
~~~

## Using `length()` in practice

A typical example of the `length()` function is to measure the user input. For example, you're looking for users to interview. You want to interview a specific cohort based on user interests.

To select such a cohort, you want to filter out users who haven't provided enough information about their interests:

~~~pgsql
SELECT *
FROM profiles
WHERE
  length(interests) > 50
~~~

This query selects only profiles where the `interests` text column contains at least 50 characters.

## Combining `length()` with other functions

The `length()` function can be combined with other SQL functions to perform more nuanced data manipulation and analysis.

For instance, if we want to check whether user country codes are valid (a valid country code contains only 2 characters) we can combine the `length()` function with the [`CASE`](/mdn/case) operator:

~~~pgsql
SELECT
  CASE WHEN length(country) = 2 THEN 'valid' ELSE 'invalid' END AS is_country_valid,
  *
FROM users
~~~

This combination is particularly useful for cleansing data and preparing it for analysis.

Practicing with the `length()` function can help you understand how SQL handles string data, including spaces and special characters. You can experiment with this function by running simple queries like this one:

~~~pgsql
SELECT length(' Hello world! ')
~~~

This will return the length of the string, including leading, trailing spaces, and punctuation, giving you a concrete example of how `length()` calculates string length.

The `length()` function is a fundamental SQL tool for working with text data, allowing analysts and developers to measure and validate string data efficiently.

{{compatibility}}

{{see_also}}
