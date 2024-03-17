# SQL Mastery, Discovery, Nuances (MDN) docs

## Page types

* statement (SELECT, INSERT, etc)
* clause (FROM, WHERE, etc)
* operator (AND, OR, NOT, =, >, <, etc)
* function (split_part, etc)
* keyword (AS, DISTINCT, THEN, END, etc)

## Data types

Atm all SQL functions are grouped via the following generic types (not the actual specific database types because there're too many):

* numeric (we're mixing together actual `integer`, `float`, `numeric`, `bigint`, etc type)
* text
* date
* timestamp
* boolean
* array
* json
* null

## Page updated_at date

Run `bin/generate-update-dates` to generate update dates for each page.

## How to create a new page

### Step 1: clone the repo

```bash
git clone https://github.com/sqlhabit/sql-mdn-docs.git
```

### Step 2: run a CLI command to create page and compatibility files

This step assumes you have [Ruby installed](https://www.ruby-lang.org/en/documentation/installation/).

Let's say, we want to add a new page for the PostgreSQL `date_trunc` function. Here's the CLI command that creates the necessary files for your new page:

```bash
bin/new-page date_trunc
```

### Step 3: add page content

The CLI `bin/new-page` command adds a new file: `pages/date_trunc.md`.

Fill the YAML section (the top section between `---` symbols).

### Step 4: add compatibility entry

The CLI `bin/new-page` command also adds a compatibility file: `compatibiltiy/date_trunc.yml`.

This is a [YAML](https://en.wikipedia.org/wiki/YAML) file that powers the "Database compatibility" section.

Add correct versions for each database.

## Page features

### Example queries

When creating a new page, make sure to provide an example (otherwise it's not really MDN – Mastery, Discovery & Nuances). When a new page is published, all its queries are runnable by default inside [the Bindle database](https://sqlhabit.github.io/sql_schema_visualizer/).

In the next paragraphs you'll learn how to specify a different dataset or disable the "Run" button for a query.

### Specify query dataset

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

### Disable "Run" link for a query

SQL Habit allows only `SELECT` queries (otherwise people will modify datasets), so we have to disable non-SELECT queries. You can do it by adding the `.js-no-run-query-link` class to a query in Markdown:

```markdown
~~~pgsql
UPDATE users
SET country = 'au'
~~~
{: .js-no-run-query-link}
```
