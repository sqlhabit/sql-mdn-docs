---
published_at: 2024-04-11 21:45
slug: reverse
type: function.text
name: reverse
title: reverse() function in SQL
description: The reverse() function in SQL is used to reverse a string or a text value.
keywords: SQL, reverse, function
see_also_pages:
  - name: lower() function in SQL
    url: /mdn/lower
    - name: upper() function in SQL
    url: /mdn/upper
  - name: length() function in SQL
    url: /mdn/length
---

The `reverse()` function in SQL flips the order of characters in a string, producing a mirror image of the original text. This function can be used for data manipulation tasks, such as creating unique identifiers or processing text in creative ways for analysis or display.

## Syntax

The syntax for the `reverse()` function is straightforward:

~~~pgsql
SELECT reverse(column_name)
FROM table_name
~~~
{: .js-no-run-query-link }

It requires a single argument: the column or string you wish to reverse.

Here's a basic example without table data:

~~~pgsql
SELECT reverse('abc')
~~~

## Using `reverse()` to find palindromes

A [palindrome](https://en.wikipedia.org/wiki/Palindrome) is a word that reads the same backwards.

For example, if you're running a lotery and you want to select lottery tickets with palindrome codes, here's a query that will do that:

~~~pgsql
SELECT *
FROM lottery_tickets
WHERE
  code = reverse(code)
~~~
{: .js-no-run-query-link }

## Combining `reverse()` with other functions

Let's level up our previous example and search for users with palindrome names. Since user names could contain lowercase and uppercase letters, let's normalize the names with the [`lower()`](/mdn/lower) function first:

~~~pgsql
SELECT *
FROM users
WHERE
  lower(first_name) = reverse(lower(first_name))
~~~

Exploring the `reverse()` function is a fun way to get more familiar with SQL's string functions. You can test and see the immediate results of reversing strings:

~~~pgsql
SELECT reverse('SQL is fun!')
~~~

The `reverse()` function might seem less common then other functions, but it definitely adds a unique capability to your Data Analysis toolkit, allowing for creative data manipulation and offering a different perspective on string analysis.

{{compatibility}}

{{see_also}}
