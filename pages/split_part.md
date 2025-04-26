---
published_at: 2025-04-22 17:45
slug: split-part
type: function.text
name: split_part
title: split_part() function in SQL
description: The split_part() function is used to extract a specific part of a string that has been divided into segments based on a given delimiter.
keywords: SQL, split_part, function, text function
compatibility: true
see_also_pages:
  - name: How to emulate split_part() function in MySQL
    url: /mdn/how-to-emulate-split-part-function-in-mysql
  - name: How to emulate split_part() function in SQLite
    url: /mdn/how-to-emulate-split-part-function-in-sqlite
  - name: How to emulate split_part() function in BigQuery
    url: /mdn/how-to-emulate-split-part-function-in-bigquery
---

The `split_part()` function in SQL is used to extract a specific part of a string that has been divided into segments based on a given delimiter. It is especially useful when working with structured string data like URL-s or CSV-style data with a lot of delimiters.

## Syntax

~~~pgsql
split_part(string, delimiter, position)
~~~
{: .js-no-run-query-link }

- `string`: the source string to split.
- `delimiter`: the character or substring that separates parts of the string.****
- `position`: the index (starts with 1) of the part you want to extract.

## Example: Extracting domain from email

Suppose we want to extract the domain part of user emails in the `users` table:

~~~pgsql
SELECT
  id,
  email,
  split_part(email, '@', 2) AS email_domain
FROM users
~~~

This will return the email and the domain part (everything after the `@` symbol).

## Example: Parsing screen resolution

In the `mobile_analytics.events` table, there’s a `screen_resolution` column with values like `'1920x1080'`. We can use `split_part()` to extract width and height:

~~~pgsql
SELECT
  screen_resolution,
  split_part(screen_resolution, 'x', 1)::integer AS width,
  split_part(screen_resolution, 'x', 2)::integer AS height
FROM mobile_analytics.events
~~~

This query helps break down the resolution into separate columns and converts them to numbers for better analysis.

## Practical use cases

- **Email parsing**: Split user or domain from an email.
- **URL or ID parsing**: Since all URL-s have a predefined structure (parameters follow the key=value format, etc) we can extract useful data from URL-s.
- **Screen resolution breakdown**: We can extract screen width or height and split users into cohorts based on that data (wide or narrow screens, etc).

`split_part()` function is a must-have in your Data Analysis bag for any type of product or marketing analysis.

{{compatibility}}

{{see_also}}
