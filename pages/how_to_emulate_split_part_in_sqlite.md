---
published_at: 2024-04-25 21:30
slug: how-to-emulate-split-part-function-in-sqlite
type: misc
name: How to emulate split_part() function in SQLite
title: How to emulate split_part() function in SQLite
description: Learn how to split text in SQLite using a recursive CTE.
keywords: SQL, function, split text
compatibility: false
see_also_pages:
  - name: split_part() function in SQL
    url: /mdn/split-part
  - name: How to emulate split_part() function in BigQuery
    url: /mdn/how-to-emulate-split-part-function-in-bigquery
  - name: How to emulate split_part() function in MySQL
    url: /mdn/how-to-emulate-split-part-function-in-mysql
---

In PostgreSQL, the `split_part()` function is a super handy way to split a string into parts based on a separator and pick the part you need. Unfortunately, SQLite doesn’t have a built-in `split_part()` function. :disappointed:

But good news: we can still get the same result! :tada: We just have to get a bit creative by using a **recursive CTE** ([Common Table Expression](/mdn/with-as)) along with some SQLite **string functions** like `substr()` and `instr()`.

Let’s walk through it together!

## "Simple" example: split a list of words

Before we start working with an actual table with records let's practice on a plain text `'red,blue,green,yellow'` and separator `,`.

If we want to select the third color (`green`), here's a query with `split_part()`:

~~~pgsql
SELECT split_part('red,blue,green,yellow', ',', 3)
~~~

Just one line, wow! Here's it's analogue in SQLite:

~~~pgsql
WITH RECURSIVE split AS (
  SELECT
    1 AS i,
    SUBSTR('red,blue,green,yellow', 1, INSTR('red,blue,green,yellow', ',') - 1) AS part,
    SUBSTR('red,blue,green,yellow', INSTR('red,blue,green,yellow', ',') + 1) AS remainder
  UNION ALL
  SELECT
    i + 1 AS i,
    CASE
      WHEN INSTR(remainder, ',') > 0 THEN SUBSTR(remainder, 1, INSTR(remainder, ',') - 1)
      ELSE remainder
    END,
    CASE
      WHEN INSTR(remainder, ',') > 0 THEN SUBSTR(remainder, INSTR(remainder, ',') + 1)
      ELSE ''
    END AS remainder
  FROM
    split
  WHERE
    remainder != ''
)

SELECT
  i,
  part
FROM
  split
WHERE
  i = 3
~~~
{: .js-no-run-query-link}

Pretty crazy, right? :sweat_smile:

:mag: Note that to select a specific part of the splitted text we're using a filter `i = 3`. Unlike other databases, in SQLite there's no easy way to emulate `split_part()` with another function. We're splitting our input text into multiple numbered rows, that's why our selection happens in the `WHERE` clause with a filter.

## Real-life example: split an email by "@"

Before we dive into how this approach works, let's look at a real example — splitting user emails to username and email domain:

~~~pgsql
WITH RECURSIVE split AS (
  SELECT
    id,
    email,
    1 AS i,
    SUBSTR(email, 1, INSTR(email, '@') - 1) AS part,
    SUBSTR(email, INSTR(email, '@') + 1) AS remainder
  FROM users
  UNION ALL
  SELECT
    id,
    email,
    i + 1 AS i,
    CASE
      WHEN INSTR(remainder, '@') > 0 THEN SUBSTR(remainder, 1, INSTR(remainder, '@') - 1)
      ELSE remainder
    END,
    CASE
      WHEN INSTR(remainder, '@') > 0 THEN SUBSTR(remainder, INSTR(remainder, '@') + 1)
      ELSE ''
    END AS remainder
  FROM split
  WHERE
    remainder != ''
)

SELECT
  id AS user_id,
  i,
  email,
  part AS username
FROM
  split
ORDER BY id ASC
~~~
{: .js-no-run-query-link}

## How it works

### 1. `WITH RECURSIVE`

`WITH RECURSIVE` lets us create a CTE that calls itself, perfect for peeling off one part of the string at a time. It consists of two parts:

1. **Initial (anchor) query** that sets the initial values.
2. **Recursive query** that repeatedly references the CTE itself until a specified condition is no longer true (stop condition).

Here's an example that prints numbers from 1 to 5:

~~~pgsql
WITH RECURSIVE counter(x) AS (
  SELECT 1
  UNION ALL
  SELECT x + 1
  FROM counter
  WHERE
    x < 5
)

SELECT x
FROM counter
~~~

#### Initial query

~~~pgsql
SELECT 1
~~~

The first step runs exactly once, starting our recursion with the value **1**.

At this point, the table `counter` looks like this:

| x |
|---|
| 1 |

#### Recursive Query

Next, the recursive query kicks in:

~~~pgsql
SELECT x + 1
FROM counter
WHERE
  x < 5
~~~

This step takes the previous rows generated and creates new ones. Specifically, it adds 1 to the value `x` for each row previously added, but only if the current value of `x` is less than 5.

Let’s expand this step-by-step:

**Iteration 1:**

- Previous row is `1`.
- Condition (`1 < 5`) is true.
- Adds `1 + 1 = 2`.

Now, `counter` has:

| x |
|---|
| 1 |
| 2 |

**Iteration 2:**

- Previous row is now `2`.
- Condition (`2 < 5`) is true.
- Adds `2 + 1 = 3`.

`counter` now contains:

| x |
|---|
| 1 |
| 2 |
| 3 |

A couple of iterations later:

**Iteration 5:**

- Previous row is `5`.
- Condition (`5 < 5`) is **false**. :warning:
- Recursion stops here. :boom:

#### Final Output

Finally, the recursive CTE returns all generated rows:

~~~pgsql
SELECT x
FROM counter
~~~

This query outputs:

| x |
|---|
| 1 |
| 2 |
| 3 |
| 4 |
| 5 |

### 2. `SUBSTR(str, start, length)`

`SUBSTR(string, start, length)` is a function that extracts a substring of a specific length from the start position in the original string.

If the `length` argument is omitted, the function will select the reminder of the string.

~~~pgsql
SELECT SUBSTR('Hello World', 1, 5);
~~~
{: .js-no-run-query-link}

This query result:

| Hello |

### 3. `INSTR(str, substring)`

`INSTR(string, substring)` function finds the position of the substring (which we'll use as the input for the `SUBSTR()` function).

**Example:**
~~~pgsql
SELECT INSTR('abc@xyz.com', '@');
~~~
{: .js-no-run-query-link}

This query result:

| 4 |

## Putting it all together

We'll use the `INSTR()` function to find the position of the first delimiter. Then we'll strip the first part using the `SUBSTR()` function and will continue doing these 2 steps until we iterate over the whole string. You can think about recursive CTE as a loop that allows us to iterate over each part of the string.

:mag: Probably the most complex part of the query is this `CASE` statement:

~~~pgsql
CASE
  WHEN INSTR(remainder, '@') > 0 THEN SUBSTR(remainder, INSTR(remainder, '@') + 1)
  ELSE ''
END AS remainder
~~~
{: .js-no-run-query-link}

We need a solid stop condition for our recursive CTE. Since SQLite's `SUBSTR()` function will return the whole string in case there's no delimiter in the string, we need an if/else logic to explicitely return an empty string for our stop condition `reminder != ''` to work:

~~~pgsql
SUBSTR('gmail.com', INSTR('gmail.com', '@') + 1)
~~~
{: .js-no-run-query-link}

Here's the result (but we want an empty string here):

| gmail.com |

## Final thoughts

Even though SQLite doesn’t have `split_part()` like PostgreSQL, by combining `WITH RECURSIVE`, `SUBSTR()`, and `INSTR()`, you can still split strings in a powerful (and super overcomplicated) way! I bet you won't use this approach in practice, but I hope it broaden your SQL horizon! 🚀

Voilá! 🎩✨

{{compatibility}}

{{see_also}}
