<div align="center">

# SQL Mastery, Discovery, Nuances (MDN) docs

[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC_BY--NC--SA_4.0-47A3F3.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

This repo hosts all the content behind https://www.sqlhabit.com/mdn.

[:microscope: How it works](?tab=readme-ov-file#how-it-works) | [:mag: How to add a page](?tab=readme-ov-file#how-to-create-a-new-page) |  [:handshake: Contributing](?tab=readme-ov-file#contributing)

</div>

SQL MDN Docs is here to document all flavors of SQL: MySQL, PostgreSQL, SQLite, Redshift, Google Cloud and Snowflake.

SQL MDN Docs was created to help people who already know or study one SQL flavor (say PostgreSQL) to transition to analytical databases used at companeis they work for – most likely Snowflake, Redshift or Google Cloud.

Finally, let's simply build the best SQL documentation in the world a-la [MDN Web Docs for JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript).

## How it works

This repo is basically a content database for the [SQL MDN Docs website](https://www.sqlhabit.com/mdn).

The main entry point is the [pages folder](https://github.com/sqlhabit/sql-mdn-docs/tree/main/pages). Behind the scenes, SQL Habit website pull all published Markdown pages from this folder and converts them to HTML pages shown at https://www.sqlhabit.com/mdn.

A page file consists of 2 parts: [YAML](https://en.wikipedia.org/wiki/YAML) config on top of the file

```
---
published_at: 2024-03-23 09:00
slug: and
type: operator
name: AND
title: AND operator in SQL
description: AND is a logical operator in SQL that is used to combine multiple conditions, typically used inside a WHERE clause.
keywords: SQL, AND, boolean, condition
compatibility: true
see_also_pages:
  - name: OR operator in SQL
    url: /mdn/or
  - name: CASE operator in SQL
    url: /mdn/case
---
```

followed by the [Markdown](https://en.wikipedia.org/wiki/Markdown) content of a page.

:mag: To be precise, we're using the [Kramdown](https://kramdown.gettalong.org/) flavor of Markdown. Kramdown adds a couple of useful features on top of the regular Markdown syntax.

In every page file you'll see these 2 sections:

```
{{compatibility}}

{{see_also}}
```

They're replaced with a proper HTML components during the Markdown compilation step:

<img src="https://github.com/sqlhabit/sql-mdn-docs/blob/main/.README/db_compat_and_see_also.png?raw=true" alt="" DB Compatibility and See also sections width="600" />

The "Database compatibility" section gets its content from a separate YAML file in the [compatibility](https://github.com/sqlhabit/sql-mdn-docs/tree/main/compatibility) folder.

The "See also pages" section is configured via the YAML page config:

```yaml
see_also_pages:
  - name: OR operator in SQL
    url: /mdn/or
  - name: CASE operator in SQL
    url: /mdn/case
```

Finally, there's the [updated_at](https://github.com/sqlhabit/sql-mdn-docs/tree/main/updated_at) folder where page update dates are stored. This allows us to show a line like `This page was last modified on March 23, 2024.` on each page. Good news – these dates are auto-generated via [the post-commit hook](https://github.com/sqlhabit/sql-mdn-docs/blob/main/.overcommit.yml).

## How to create a new page

### Step 1: clone the repo

```bash
git clone https://github.com/sqlhabit/sql-mdn-docs.git
```

### Step 2: run a CLI command to create page files

This step assumes you have [Ruby installed](https://www.ruby-lang.org/en/documentation/installation/).

Let's say, we want to add a new page for the PostgreSQL `date_trunc` function. Here's the CLI command that creates the necessary files (page, compatibility and updated_at files) for your new page:

```bash
bin/new-page date_trunc
```

### Step 3: configure your page

Go over all config keys and assign them a value.

#### Configure page type

Set a page type depending whether you're documenting an actual keyword (statement/clause/etc) or writing an explainer on how to use a keyword in another database (misc):

* **statement** (SELECT, INSERT, etc)
* **clause** (FROM, WHERE, etc)
* **operator** (AND, OR, NOT, =, >, <, etc)
* **function.DATA_TYPE** (split_part, etc)
* **keyword** (AS, DISTINCT, THEN, END, etc)
* **misc** (articles on how to bridge gaps betweens databases, etc)

If you're writing a page for an SQL function, further specify the function data type:

* **function.numeric**
* **function.text**
* **function.date**
* **function.timestamp**
* **function.boolean**
* **function.array**
* **function.json**
* **function.null**

#### Set SEO meta tags

`title`, `description` and `keywords` are used to fill the correspondent meta tags on the page.

The `title` will also be used as a page headline (h1 tag).

#### How to hide compatibility table

If you're adding a how-to page, make sure to disable the DB compatibility table by setting:

```yaml
compatibility: false
```

### Step 4: add page content

Add the Markdown page content below the config section.

### Step 5: add compatibility entry

The CLI `bin/new-page` command also adds a compatibility file: `compatibiltiy/date_trunc.yml`.

Add correct versions for each database by setting the `min_version` and `min_version_released_at` keys ([example](https://github.com/sqlhabit/sql-mdn-docs/blob/main/compatibility/with_as.yml#L2)).

If necessary, link related pages ([example](https://github.com/sqlhabit/sql-mdn-docs/blob/main/compatibility/with_as.yml)).

## Markdown content features

### Runnable queries

When creating a new page, make sure to provide an example (otherwise it's not really MDN – Mastery, Discovery & Nuances). When a new page is published, all its queries are runnable by default inside [the Bindle database](https://sqlhabit.github.io/sql_schema_visualizer/).

In the next paragraphs you'll learn how to specify a different dataset or disable the "Run" button for a query.

### How to specify query dataset

SQL Habit allows running `SELECT` queries in the following datasets:

| Dataset | ID | Description |
| --- | --- | --- |
| Bindle dataset | 1 | This data warehouse belongs to a fictional startup named Bindle. Bindle is a web and mobile app for reading books, it has subscription business model. The SQL Habit Course is based on Bindle’s story. 📖 Bindle’s data warehouse contains everything needed to run a modern Internet company – web and mobile analytics, marketing data, AB-test data, etc. |
| E-commerce dataset | 2 | This data warehouse is inspired by an E-commerce website like Amazon. 🛒 Our E-commerce website allows vendors to sell items in multiple categories. Users can add as many items as they want to a cart and then purchase a cart with/without a discount code. Users also can return items and leave reviews. |
| Finance dataset | 3 | This data warehouse simply contains all company’s financial transactions. 💵 If the company paid for something – there’s a debit transaction with negative amount. If someone paid the company – it’s a credit transaction with positive amount. 💰 |
| Live dataset | 4 | The Live dataset contains data of a meditation mobile app with subscription business model. 📱 The data is updated daily. You can run queries to calculate metrics for the past 24h, week, month, etc. and build dashboards as if you were actually working for that company. 📊 |
| NBA dataset | 5 | The NBA dataset contains stats of NBA games since 1949. It is regularly updated. The dataset contains aggregated game stats (team_game_stats table) and individual player stats per quarter or overtime period (player_period_stats). Have a ball! 🏀 |

Check out all dataset tables, columns and their descriptions on the [SQL Schema Visualizer website](https://sqlhabit.github.io/sql_schema_visualizer/).

By default, all queries are meant for the Bindle dataset, since it's the main dataset behind SQL Habit course. You can assign a different dataset (in that case Finance) like so:

```markdown
~~~pgsql
SELECT *
FROM transactions
~~~
{: data-dataset-id="3"}
```

### How to disable "Run query" link

SQL Habit allows only `SELECT` queries (otherwise people will modify datasets), so we have to disable non-SELECT queries. You can do it by adding the `.js-no-run-query-link` class to a query in Markdown:

```markdown
~~~pgsql
UPDATE users
SET country = 'au'
~~~
{: .js-no-run-query-link}
```

### How to add a table

If you're adding a table, please add the `table-with-header` class. CSS class helps to avoid CSS collisions with other tables on the page (DB compatibility table, etc):

```markdown
| A     | B     | A OR B  |
|-------|-------|---------|
| TRUE  | TRUE  | TRUE    |
| TRUE  | FALSE | TRUE    |
| FALSE | TRUE  | TRUE    |
| FALSE | FALSE | FALSE   |
{: .table-with-header }
```

## Contributing

Contribute a new page to SQL MDN Docs, there's so much to cover!

Just make sure to check out the [contribution guidelines](https://github.com/sqlhabit/sql-mdn-docs/blob/main/CONTRIBUTING.md). :pray:

## License

SQL MDN Docs are licensed under [CC BY-NC-SA 4.0 license](https://github.com/sqlhabit/sql-mdn-docs/blob/main/LICENSE.md)
