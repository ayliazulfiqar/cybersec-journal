# Day 10 - UNION Attacks

## Review

What confused me from yesterday's lab?

It was actually the syntax; otherwise, everything was fine. I also got a bit confused about the intercept-on/off situation.

## What is a UNION attack?

A UNION-based SQL injection attack occurs when an attacker exploits unsafe SQL query construction to combine the application's expected results with results from another query.

### The two UNION requirements

   Column count: Both SELECT queries must return the same number of columns.

  Compatible data types: Corresponding columns must have compatible types.

### How can the column count be identified?

  ORDER BY: Test column positions and observe when the query fails or the response changes.

  UNION SELECT NULL: Compare queries with different numbers of NULL expressions.

## PortSwigger labs completed

**Lab 1 — Determining the number of columns returned by the query**

Status: Completed

What I learned:

Why the number of columns matters in a UNION attack.

How to test column counts using ORDER BY and UNION SELECT NULL.

How database errors or changes in the HTTP response can help identify the correct column count.

_Key takeaway: Both queries must return the same number of columns for UNION to work._

**Lab 2 — Finding a column containing text**

Status: Completed

What I learned:

Why identifying text-compatible columns is important.

How to test different column positions using a text marker.

How to observe application responses to identify a column that can display text.

_Key takeaway: Knowing the column count is not enough; I also need to identify which columns can hold the data types I want to retrieve._

**Lab 3 — Retrieving data from other tables**

Status: Completed

What I learned:

How UNION attacks can expose information from tables other than the one the application normally displays.

Why understanding table names and column names matters.

How the column count and data-type compatibility requirements apply when retrieving data from another table.

_Key takeaway: If an application is vulnerable and query results are reflected in its response, UNION can expose data the application was not intended to display._

**Lab 4 — Retrieving multiple values in a single column**

Status: Completed

What I learned:

How multiple values can be combined into one output column using string concatenation.

Why a separator can make combined values easier to distinguish.

How database-specific concatenation syntax can differ.

_Key takeaway: When only one suitable output column is available, concatenation can combine multiple values into a single string._

### What developers should do

**Parameterised queries**

Use prepared statements and parameterised queries so user input is treated as data rather than executable SQL code.

**Input validation**

Validate user input against expected formats and application rules. Input validation is an additional safeguard, not a replacement for parameterised queries.

**Least-privilege database permissions**

Give the application's database account only the permissions it needs. Restricting access limits the potential impact if an injection vulnerability is discovered.

**Safe error handling**

Avoid exposing detailed database errors to users. Log diagnostic information securely and return appropriate, generic error messages.

## How does a UNION attack work?

A UNION attack happens when a hacker tricks a website’s database into merging secrets with normal webpage data.
When you search for something on a site (like a product), the site asks its database for that info and shows it on your screen. A hacker injects the SQL word UNION into the search bar to glue a second, hidden question onto the site's original request. If the site isn't protected, the database runs both requests and displays the stolen data—like admin passwords or credit card numbers—right on the public webpage.

## My First 10 Days: Weekly Review

**Things I Understand Well**

Linux is my strongest area so far. I already had a solid foundation in Linux commands and was comfortable with the interface and operating system, which made it easy to pick up new Linux concepts quickly.

**Things I Need to Practice More**

Networking is the area where I need the most practice. While reviewing my progress, I noticed that I’m still not as confident in it as I’d like to be, and I plan to spend more time working through it.

**My Biggest Confusion**

Networking remains my biggest point of confusion. I haven’t yet built a clear understanding of how its core concepts fit together.
