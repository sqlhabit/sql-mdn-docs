# SQL Mastery, Discovery, Nuances (MDN) docs

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
