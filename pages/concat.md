---
published_at: 2024-04-07 11:30
slug: concat
types:
  - function.text
name: concat
title: concat() function in SQL
description: The concat() function concatenates multiple text values into one.
keywords: SQL, function, concat()
---

The `concat()` function in SQL is used to combine two or more strings into a single string. It's a straightforward and frequently used function for data manipulation and preparation, especially useful in generating formatted output, combining data from different columns, or creating unique identifiers.

## Syntax

The basic syntax of the `concat()` function involves specifying the strings or column names to be concatenated.

~~~pgsql
SELECT concat(string1, string2, ..., stringN)
FROM table_name
~~~
{: .js-no-run-query-link }

For example, to concatenate the first name and last name of a user into a full name:

~~~pgsql
SELECT concat(first_name, ' ', last_name) AS full_name
FROM users
~~~

## Using concat() for data preparation

`concat()` can be particularly useful in preparing data for reports, where you might need to merge various pieces of information into a single column for better readability.

~~~pgsql
SELECT concat(first_name, ' ', last_name, '; ', email)
FROM users
~~~

This query combines user first and names into a full name, and then adds their email. This query emulates CSV output format, so we can later use this data for other purposes (sending an email campaign or doing a further analysis).

### Creating unique identifiers

To create a unique identifier by combining a book's name with its genre:

~~~pgsql
SELECT concat(name, '--', genre) AS unique_id
FROM books
~~~

The `concat()` function is a simple yet powerful tool in SQL, offering a variety of ways to manipulate and prepare text data.

It exemplifies how SQL functions can transform raw data into a more useful and readable format. Experimenting with `concat()` can help you become more proficient in SQL, enabling you to handle a wide range of data preparation and analysis tasks.

{{compatibility}}

{{see_also}}
