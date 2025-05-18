---
published_at: 2025-05-18 13:30
slug: to-char
type: function.timestamp
name: to_char
title: to_char() function in SQL
description: The to_char() function in SQL is used to convert a number or date to a string in a specified format.
keywords: SQL, to_char, function, text function, date formatting
compatibility: true
see_also_pages:
---

The `to_char()` function in SQL is a versatile tool used to convert a number or a timestamp into a string based on a specified format. This function is exceptionally useful for presenting data in a more readable or expected format, facilitating easier interpretation and reporting.

## Syntax

The basic syntax of the `to_char()` function is as follows:

~~~pgsql
to_char(value, format)
~~~
{: .js-no-run-query-link }

- **`value`**: This is the number or date that you want to convert.
- **`format`**: A text string that defines the output format. The format varies depending on whether you're formatting a timestamp or a number.

## Formatting Dates

When used with dates, the `to_char()` function allows you to specify the exact way you want the date to be represented.

### Example: Formatting user's signup date

Suppose you want to display the `signup_date` from the `users` table in a more friendly format (e.g., "January 15, 2023"):

~~~pgsql
SELECT
  id,
  to_char(signup_date, 'Month DD, YYYY') AS formatted_signup_date
FROM users
LIMIT 5
~~~

Here, the format string `Month DD, YYYY` specifies that you want the full name of the month followed by the day and the year.

## Formatting Numbers

The `to_char()` function can also format numeric values, turning them into strings with specified patterns, such as adding leading zeroes, commas, or fixed decimal places.

### Example: Formatting product prices

Suppose you want to format the `price` in the `products` table to include two decimal places and commas for thousands:

~~~pgsql
SELECT
  id,
  name,
  to_char(price, 'FM$9,999,999.00') AS formatted_price
FROM products
~~~

In this format string, `FM` is used to suppress leading spaces, `$` adds a dollar sign, and commas are used for thousands while `.00` ensures two decimal places.

## Practical Use Cases

- **Report Generation**: Use `to_char()` to generate readable dates or numeric values for reports.
- **User Interfaces**: Present values in a web or app interface in a user-friendly manner.
- **Data Exporting**: Ensure that dates and numbers are presented in a consistent format when exporting data to CSV, Excel, etc.

## More on Date and Number Formatting

Here's a list of all formatting tokens available to you for formatting dates and timestamps:

### Date Formatting Tokens

| Format | Description | Example |
|--------|-------------|---------|
| `YYYY` | Full year (4 digits) | 2023 |
| `YY` | Last 2 digits of year | 23 |
| `MM` | Month as a two-digit number | 01-12 |
| `MON` | Abbreviated month name (uppercase) | JAN, FEB |
| `Mon` | Abbreviated month name (capitalized) | Jan, Feb |
| `mon` | Abbreviated month name (lowercase) | jan, feb |
| `MONTH` | Full month name (uppercase) | JANUARY |
| `Month` | Full month name (capitalized) | January |
| `month` | Full month name (lowercase) | january |
| `DD` | Day of the month (01-31) | 01-31 |
| `D` | Day of the week (1-7, Sunday=1) | 1-7 |
| `DY` | Abbreviated day name (uppercase) | MON, TUE |
| `Dy` | Abbreviated day name (capitalized) | Mon, Tue |
| `dy` | Abbreviated day name (lowercase) | mon, tue |
| `DAY` | Full day name (uppercase) | MONDAY |
| `Day` | Full day name (capitalized) | Monday |
| `day` | Full day name (lowercase) | monday |
| `W` | Week of month (1-5) | 1-5 |
| `WW` | Week of year (1-53) | 1-53 |
| `IW` | ISO week of year (1-53) | 1-53 |
| `HH24` | Hour of day (00-23) | 00-23 |
| `HH` or `HH12` | Hour of day (01-12) | 01-12 |
| `MI` | Minute (00-59) | 00-59 |
| `SS` | Second (00-59) | 00-59 |
| `MS` | Millisecond (000-999) | 000-999 |
| `AM` or `PM` | Meridian indicator (uppercase) | AM, PM |
| `am` or `pm` | Meridian indicator (lowercase) | am, pm |
| `TZ` | Timezone abbreviation | PST, EST |

Let's try to use as many of them to illustrate how to format time values:

~~~pgsql
SELECT
  id,
  created_at,
  to_char(created_at, 'YYYY-MM-DD HH24:MI:SS') AS iso_format,
  to_char(created_at, 'Month DD, YYYY at HH12:MI:SS AM') AS readable_format,
  to_char(created_at, 'Dy, DD Mon YYYY (HH24:MI)') AS compact_format,
  to_char(created_at, 'YYYY"Q"Q W"W" HH24:MI:SS TZ') AS analytical_format
FROM users
LIMIT 5
~~~

This query demonstrates multiple formatting styles:

- Standard ISO format with 24-hour time
- Human-readable format with month name, 12-hour clock and AM/PM indicator
- Compact format with abbreviated day and month
- Analytical format showing year, quarter, week of year, and timezone

### Number Formatting Tokens

| Token | Description | Example |
| --- | --- | --- |
| `9` | Digit position (no leading zeros) | `9999` → `123` |
| `0` | Digit position (with leading zeros) | `0999` → `0123` |
| `.` | Decimal point | `9.99` → `1.23` |
| `,` | Thousands separator | `9,999` → `1,234` |
| `$` | Dollar sign | `$9999` → `$1234` |
| `L` | Currency symbol (locale-specific) | `L9999` → `£1234` |
| `D` | Decimal point (locale-specific) | `99D99` → `12,34` |
| `G` | Group separator (locale-specific) | `9G999` → `1.234` |
| `MI` | Minus sign (trailing) | `9999MI` → `1234-` |
| `S` | Sign (leading) | `S9999` → `+1234` |
| `PR` | Parentheses for negative numbers | `9999PR` → `<1234>` |
| `FM` | Fill mode (suppress padding, leading zeroes) | `FM9999` → `1234` |
| `TH` | Ordinal number suffix | `9TH` → `1ST` |
| `RN` | Roman numerals (uppercase) | `RN` → `IV` |
| `rn` | Roman numerals (lowercase) | `rn` → `iv` |

Let's see how to use these number formatting tokens:

~~~pgsql
SELECT
  id,
  price,
  to_char(price, '999,999.99') AS formatted_price,
  to_char(price, '$999,999.00') AS dollar_price,
  to_char(price, 'L999G999D99') AS locale_price,
  to_char(price, '999999MI') AS price_with_trailing_sign,
  to_char(price, 'S999999.99') AS price_with_leading_sign,
  to_char(price * -1, '999999PR') AS negative_price_parentheses,
  to_char(price, 'FM999999.99') AS price_without_padding,
  to_char(CAST(price AS integer), '999TH') AS ordinal_price
FROM products
LIMIT 5
~~~

For more complex formatting, we can combine multiple tokens:

~~~pgsql
SELECT
  id,
  amount_usd,
  to_char(amount_usd, 'FM$999,999,999.00') AS clean_currency,
  to_char(CAST(amount_usd AS integer), 'RN') AS roman_numeral,
  to_char(amount_usd, '"Total: $"FM999,999,999.00" (USD)"') AS report_format,
  CASE
    WHEN amount_usd < 0 THEN to_char(ABS(amount_usd), '$999,999.99PR')
    ELSE to_char(amount_usd, '$999,999.99')
  END AS accounting_format
FROM transactions
LIMIT 5
~~~
{: data-dataset-id="3"}

These examples demonstrate how to:

- Format prices with thousands separators and decimal places
- Add currency symbols (both fixed and locale-specific)
- Display negative numbers with trailing minus signs or parentheses
- Remove padding with the FM modifier
- Convert numbers to ordinal format or Roman numerals
- Create complex custom formats with text and numbers combined
- Format financial data in accounting style

As you can see, the `to_char()` function is a powerhouse! It can format both dates and numbers, ensuring that your SQL queries can produce output strings that are precise and human-friendly.

{{compatibility}}

{{see_also}}
