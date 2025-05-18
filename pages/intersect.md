---
published_at: 2024-04-11 09:30
slug: intersect
types:
  - operator
name: INTERSECT
title: INTERSECT operator in SQL
description: The INTERSECT operator in SQL is used to return the common records from two or more SELECT queries.
keywords: SQL, operator, INTERSECT, sets
compatibility: true
see_also_pages:
  - name: EXCEPT ALL operator in SQL
    url: /mdn/except-all
  - name: EXCEPT operator in SQL
    url: /mdn/except
  - name: UNION operator in SQL
    url: /mdn/union
  - name: UNION ALL operator in SQL
    url: /mdn/union-all
---

The `INTERSECT` operator in SQL comes from a branch of math called ["set theory"](https://en.wikipedia.org/wiki/Set_(mathematics)#Basic_operations){:target="_blank"}.

There're 3 main set operations:

* union: a combination of all members of both sets ([`UNION operator`](/mdn/union){:target="_blank"})
* difference: members of set 1 that don't belong to set 2 ([`EXCEPT operator`](/mdn/except){:target="_blank"})
* intersection: a subset of members that are present in both set 1 and set 2.

The latter operation is called `INTERSECT` in SQL. It only returns unique :warning: rows that are present in both `SELECT` queries we're intersecting.

This operator is useful when you want to find shared data points between datasets.

## Syntax

Let's see the `INTERSECT` operator in action. We don't need any tables to do that:

~~~pgsql
SELECT 1
INTERSECT
SELECT 2
~~~

As you can see, our datasets are trivial and there's no overlap. You should see the empty result set when you run this :point_up: query.

Let's look at the deduplicating behaviour of the `INTERSECT` operator. Let's prepare more sophisticated datasets for intersection:

~~~pgsql
WITH table1 AS (
  SELECT 1 AS id
  UNION ALL
  SELECT 1
  UNION ALL
  SELECT 2
), table2 AS (
  SELECT 1 AS id
)

SELECT *
FROM table1
INTERSECT
SELECT *
FROM table2
~~~

:bulb: Note how userd [CTE](/mdn/with-as)-s and the [`UNION ALL operator`](/mdn/union-all){:target="_blank"} operator to prepare temporary datasets for experimenting. This is a best practice when it comes to exploring SQL features with simple data.

As you can see, this query :point_up: returned no duplicated `1` rows in the final result set:

| id |
|---|
| 1 |
{: .table-with-header }

Let's look at a more realistic example.

## Finding common users between platforms

Imagine we have a meditation mobile app and a web version of the same app. Both platforms measure user behaviour by tracking events using the category/action naming convention (category could be "Meditation" and action could be "Started", "Paused" or "Finished").

We can use the `INTERSECT` operator to see the common events between both platforms:

~~~pgsql
SELECT category, action
FROM mobile_analytics.events
INTERSECT
SELECT category, action
FROM web_analytics.events
~~~

## `INTERSECT` vs `JOIN`

I bet you won't often see the `INTERSECT` operator powering real analytical queries. The problem with `INTERSECT` is that columns of both queries must match, otherwise SQL engine won't know how to compare them.

It means if we want to pull more columns later, we'll have to probably JOIN them. We can do the same thing right away using the [`INNER JOIN`](/mdn/inner-join){:target="_blank"}:

~~~pgsql
SELECT *
FROM mobile_analytics.events m
INNER JOIN web_analytics.events w
  ON m.category = w.category
    AND m.action = w.action
~~~

:mag: Note that `INNER JOIN` won't filter out duplicates and we'd have to use the [`DISTINCT`](/mdn/distinct){:target="_blank"} keyword to do that.

Anyways, `INTERSECT` and other set operators are a must for anyone writing SQL. They're easy to understand and in ad hoc situations where we simply need to combine sets, subtract or intersect they're a perfect tool for the job.

{{compatibility}}

{{see_also}}
