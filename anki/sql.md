---
title: "SQL"
date: "2021-06-16T14:26:34"
description: "Anki deck for SQL cards."
draft: true
# image: /path/to/image
css: custom-styles.css
---

# SQL

## What case should you use when naming database objects?

Lowercase

## How do you separate words in database object names?

With underscores

## Do you use singular or plural when naming tables in sql?

singular

## How do you test for null in sql?

Using `IS NULL` or `IS NOT NULL`. The equal operator will not work.

## How do you write a CASE statement in sql?

```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN conditionN THEN resultN
    ELSE result
END;
```

## What type of quotes do you use for a string in sql?

Single quotes

## What type of quotes do you use for a database identifier in sql?

Double quotes, these are useful when referring to identifiers that have special characters or spaces.

## What does "%" do in a SQL LIKE clause?

Matches any string

## What does "_" do in a SQL LIKE clause?

Matches any single character

## What is the argument to the IN operator in SQL?

A table with a single column or a list.

Example table with a single column

`IN (SELECT column FROM table)`

Example list

`IN (1, 2, 3)`

## How can you specify a date in sql?

As a string with `yyyy-mm-dd hh:mm:ss` format.

## What is the default order for ORDER BY in SQL?

Ascending

## How does UNION work in SQL?

Merges the results of two sql queries into a single table.

The results of both queries must have the same number of columns and compatible data types.

## What is the difference between UNION and UNION ALL in SQL?

UNION remove duplicate rows.

UNION ALL does not remove duplicates.

## How can you get the maximum value of a column in SQL?

Use the `MAX` function. `MAX(column)`

## How can you put an aggregate value in a WHERE clause in SQL?

Use a subquery.

```sql
SELECT firstname, surname, joindate
FROM cd.members
WHERE joindate = (
    SELECT MAX(joindate)
    FROM cd.members
);
```

## What is a scalar table in SQL?

A table with a single column and a single row.

## How do you concatenate strings in SQL?

With double bars

```sql
SELECT 'hello' || ' ' || 'world' FROM dual;
-- 'hello world'
```

## Can you join a table with itself in SQL?

Yes

## What does a left join do in SQL?

Perform a join of a left and right table where the left row is returned even if no row in the right table matches the join condition.

<div markdown="block" data-question>
Can you use a derived column in a WHERE clause in SQL?

For example

```sql
SELECT a, b, a*b AS c
FROM t
WHERE c = 2
```
</div>

No you must specify the derived column in the WHERE clause.

```sql
SELECT a, b, a*b AS c
FROM t
WHERE a*b = 2
```

## What is the key thing which makes a subquery a correlated subquery in SQL?

The subquery utilizes information from the out query in a way that it has to be run for each row in the result set.

## Can you put a `SELECT` statement in a `SELECT` clause in SQL?

Yes a nested select statement can be used to calculate aggregates and is known as a subquery.

## What workaround can you use to reference a derived column in a WHERE clause in SQL?

Select the derived column in a subquery then reference the derived column in the outer where clause.

```sql
SELECT derived_column
FROM (...subquery)
WHERE derived_column ...
```

<div markdown="block" data-question>
Given a sql table with a nullable varchar column address complete the logic in the following statemnets.

- `COUNT(*)` {{c1::simply returns the number of rows}}
- `COUNT(address)` {{c2::counts the number of non-null addresses in the result set}}
- `COUNT(DISTINCT address)` {{c3::counts the number of different addresses in the facilities table}}
</div>

<div markdown="block" data-question>
What is wrong with the following sql query? How do we fix it?

```sql
SELECT facid, COUNT(*) 
FROM cd.facilities
```
</div>

The `COUNT(*)` tries to return a single value but there are multiple `facid` so the database does not know what `COUNT(*)` to associate with each `facid`.

We can return the total count with a subquery. The database knows to perform this query for each row.

```sql
SELECT facid, (SELECT COUNT(*) FROM cd.facilities)
FROM cd.facilities
```

## How does the `EXTRACT` function work in SQL?

`extract` lets you extract a component from a date or timestamp.

`EXTRACT(<field> from <expression>)`

For example

`EXTRACT(YEAR FROM some_date)`

<div markdown="block" data-question>
## What is wrong with the following SQL query? How can we fix it?

```sql
SELECT facid, SUM(slots) as "Total Slots"
        FROM cd.bookings
        WHERE SUM(slots) > 1000
        GROUP BY facid
        ORDER BY facid
```
</div>

You cannot put an aggregate function in a `WHERE` clause.

Instead you need to put the aggregate function in a `HAVING` clause

```sql
SELECT facid, SUM(slots) as "Total Slots"
        FROM cd.bookings
        GROUP BY facid
        HAVING SUM(slots) > 1000
        ORDER BY facid
```

## What is the difference between a `HAVING` clause and a `WHERE` clause in sql?

The `HAVING` clause filters data that has been passed through an aggregate function while the `WHERE` clause filters data before it has been passed to an aggregate function.

## Can you put derived columns in a `HAVING` clause in sql?

Yes in most cases but not in Postgres. In postgres you can use a subquery.

## How do you write a Common Table Expression in SQL?

An expression of the form `WITH CTEName as (SQL-Expression), CTEName2 as (SQL-Expression)...`

It can be written before a query and the `CTEName` parts can be accessed as table view from within the query.

## What is a Common Table Expression in SQL?

Think of a CTE as a named query or a runtime table.

In this example we are creating a runtime table called `sum` which we can use anywhere else we would use a table such as in a `FROM` statement.

```sql
WITH sum AS (SELECT facid, SUM(slots) as totalslots
	FROM cd.bookings
	GROUP BY facid
)
SELECT facid, totalslots 
	FROM sum
	WHERE totalslots = (SELECT MAX(totalslots) from sum);
```

## What is the syntax for a window function in SQL?

```sql
SELECT <query> OVER(PARTITION BY <query> ORDER BY <query>)
```

The contents of `OVER` and the `ORDER BY` are optional.

These are all valid


```sql
-- empty over
SELECT <query> OVER()
```

```sql
-- no order by
SELECT <query> OVER(PARTITION BY <query>)
```

```sql
-- no partition
SELECT <query> OVER(ORDER BY <query>)
```

## What does `ORDER BY` do in a window function in SQL?

Limits the window to the rows up to and including the current row.

## How do you write a comment in SQL?

Two hyphens

```sql
-- this is a comment
```

## How do you cast a value to a given type in SQL?

With `value::type` or `CAST(value, type)`

```sql
-- option 1
SELECT '2012-08-31 01:00:00'::TIMESTAMP;

-- option 2
SELECT CAST('2012-08-31 01:00:00', TIMESTAMP);
```

## How do you write a recursive common table expression in SQL?

```sql
WITH RECURSIVE <NAME>(columns) as (
	<initial statement>
	UNION ALL
	<recursive statement>
)
```

## How does a recursive common table expression work in SQL?

- The initial statement runs and populates initial data.
- then the recursive statement runs but each time the recursive statement runs it only sees data from the previous iteration
- the recursive statement runs until no more data is produced

```sql
WITH RECURSIVE <NAME>(columns) as (
	<initial statement>
	UNION ALL
	<recursive statement>
)
```

Example

```sql
with recursive increment(num) as (
	select 1
	union all
	select increment.num + 1 from increment where increment.num < 5
)
select * from increment;
```
