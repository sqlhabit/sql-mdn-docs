---
published_at: 2024-04-10 22:30
slug: substring
type: function.text
name: substring
title: substring() function in SQL
description: The substring() function is used to extract a substring from a string.
keywords: SQL, substring, function
see_also_pages:
  - name: concat() function in SQL
    url: /mdn/concat
---

The `substring()` function in SQL is used to extract a substring from a string. It allows you to specify the starting point and the length of the substring you want to extract. This function is incredibly useful for manipulating and analyzing string data stored in a database.

## Syntax

The basic syntax of the `substring()` function is as follows:

~~~pgsql
SUBSTRING(input_string, start_index, finish_index)
~~~
{: .js-no-run-query-link }

- `string` is the string from which you want to extract a substring.
- `start` is the position where the extraction will begin. The count starts with 1.
- `length` is the number of characters to extract.

For example, if we want to extract "foo" from "foobar", we'd call it like so:

~~~pgsql
SUBSTRING('foobar', 1, 3)
~~~

## Using `substring()` to extract dates

`substring()` can be used in various data analysis tasks, such as extracting parts of strings that contain certain patterns, or when you need to truncate string data to fit into reports or analyses.

For example, if our marketing campaign names always start with date (campaign launch date), we can extract it like so:

~~~pgsql
SELECT
  utm_campaign,
  SUBSTRING(utm_campaign, 1, 8) AS launch_date
FROM users
WHERE
  utm_campaign IS NOT NULL
~~~

## Using `substring()` to extract countries

Same way, we can continue extracting insights from marketing campaign names. If know the position of a country code in a campaign name, we can extract it using the `substring()` function:

~~~pgsql
SELECT
  utm_campaign,
  SUBSTRING(utm_campaign, 10, 2) AS country_code
FROM users
WHERE
  utm_campaign IS NOT NULL
~~~

{{compatibility}}

{{see_also}}
