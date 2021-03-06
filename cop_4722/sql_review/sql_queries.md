# SQL Queries

One of the purposes of the SQL language is to retrieve information stored in a database. This is commonly referred to as querying. Queries allow us to communicate with the database by asking questions and returning a result set with data relevant to the question.



## Where and Its Operators

### Select

`SELECT` is used every time you want to query data from a database and `*` means *all* columns.

Suppose we are only interested in two of the columns. We can select individual columns by their names (separated by a comma):

```sql
SELECT column1, column2
FROM table_name;
```

To make it easier to read, you can move `FROM` to another line. Line breaks don't mean anything specific in SQL. A query can be written entirely in one line   or multiple and it would run fine.

### As

Knowing how `SELECT` works, suppose we have the code below:

```sql
SELECT name AS 'Titles'
FROM movies;
```

`AS` is a keyword in SQL that allows you to *rename* a column or table using an alias. The new name can be anything you want as long as you put it inside of single quotes. Here we renamed the `name` column as `Titles`.

Some important things to note:

-   Although it's not always necessary, it's best practice to surround your aliases with single quotes.
-   When using `AS`, the columns are not being renamed in the table. The aliases only appear in the query result.

### Distinct

When we are examining data in a table, it can be helpful to know what *distinct* values exist in a particular column.

`DISTINCT` is used to return unique values in the output. It filters out all duplicate values in the specified column(s). 

For instance:

```sql
SELECT tools
FROM inventory;
```

| Tools  |
| :----: |
| Hammer |
| Nails  |
| Nails  |
| Nails  |

```sql
SELECT DISTINCT tools
FROM inventory;
```

| Tools  |
| :----: |
| Hammer |
| Nails  |

Filtering the results of a query is an important skill in SQL. it is easier to see the different possible `genres` in a `movie` table after the data has been filtered than to scan every row in the table.

### Where

We can restrict query results using the `WHERE` clause in order to obtain only the information we want.

Following this format, the statement below filters the result set to only included top rated movies (IMDb ratings greater than 8):

```sql
SELECT *
FROM movies
WHERE imdb_rating > 8;
```

1.  `WHERE` clause filters the result set to only include rows where the following *condition* is true.
2.  `imdb_rating > 8` is the condition. Here, only rows with a value greater than 9 in the `imdb_rating` will be returned.

The `>` is an *operator*.  Operators create a condition that can be evaluated as either *true* or *false*.

Comparison operators used with the `WHERE` clause are:

-   `=` equal to
-   `!=` not equal to
-   `>` greater than
-   `<` less than
-   `>=` greater than or equal to
-   `<=` less than or equal to

### Like 

`LIKE` can be a useful operator when you want to compare similar values.

The `movies` table contains two films with similar titles, 'Se7ven' and 'Seven'.

How could we select all movies that start with 'Se' and end with 'en' and have exactly one character in the 

middle?

```SQL
SELECT *
FROM movies
WHERE name LIKE 'Se_en';
```

1.  `LIKE` is a special operator used with the WHERE clause to search for a specific pattern in a column.
2.  `name LIKE 'Se_en'` is a condition evaluating the `name` column for a specific pattern.
3.  `Se_en` represents a pattern with a wildcard character.

The `_` means you can substitute any individual character here without breaking the pattern. The names `Seven` and `Se7en` both match this pattern.

The percentage sign `%` is another wildcard character that can be used with `LIKE`.

This statement below filters the result set to only include movies with names that begin with the letter 'A':

```sql
SELECT *
FROM movies
WHERE name LIKE 'A%';
```

`%` is a wildcard character that matches zero or more missing letters in the pattern.

-   `A%` matches all movies with names that begin with letter 'A'.
-   `%a` matches all movies that end with 'a'.

You can also use `%` both before and after a pattern:

```sql
SELECT *
FROM movies
WHERE name LIKE '%man%';
```

Here, any movie that *contains* the word 'man' in its name will be returned in the result.

`LIKE` is not case sensitive. 'Batman' and 'Man of Steel' will both appear in the result of the query above.

### Is NULL

More often than not, the data you encounter will have missing values.

Unknown values are indicated by `NULL`.

It is not possible to test for `NULL` values with comparison operators such as `=` and `!=`. Instead, we will have to use these operators:

-   `IS NULL`
-   `IS NOT NULL`

To filter for all movies *with* an IMDb rating:

```SQL
SELECT name
FROM movies
WHERE imdb_rating IS NOT NULL;
```

### Between

The `BETWEEN` operator is used in a `WHERE` clause to filter the result set within a certain *range*. It accepts two values that are either numbers, text, or dates.

For example, this statement filters the result set to only include movies with `year` from 1990 up to, *and including* 1999.

```SQL
SELECT *
FROM movies
WHERE year BETWEEN 1990 AND 1999;
```

When the values are text, `BETWEEN` filters the result set for within the alphabetical range.

In this statement, `BETWEEN` filters the result set to only include movies with `name` that begin with the letter 'A' up to, *but not including* ones with begin with 'J'.

```sql
SELECT *
FROM movies
WHERE name BETWEEN 'A' AND 'J';
```

However, if a movies has a name of simply 'J', it would actually match. This is because `BETWEEN` goes *up to* the second value — up to 'J'. So the movie named 'J' would be included in the result set but not 'Jaws'.

### And

Sometimes we want to *combine multiple conditions* in a `WHERE` clause to make the result set more specific and useful.

One way of doing this is to use the `AND` operator. Here, we use the `AND` operator to only return 90's romance movies.

```sql
SELECT *
FROM movies
WHERE year BETWEEN 1990 AND 1999
	AND genre = 'romance';
```

-   `year BETWEEN 1990 AND 1999` is the 1st condition.
-   `genre = 'romance'` is the 2nd condition.
-   `AND` combines the two conditions.

With `AND`, *both* conditions must be true for the row to be included in the result.

### Or

Similar to `AND`, the `OR` operator can also be used to combine multiple conditions in `WHERE`, but there is a fundamental difference:

-   The `AND` operator displays a row if *all* the conditions are true.
-   The `OR` operator displays a row if *any* condition is true.

Suppose we wanted to check out a new movie or something action-packed:

```sql
SELECT *
FROM movies
WHERE year > 2014
	OR genre = 'action';
```

-   `year > 2014` is the 1st condition.
-   `genre = 'action'` is the 2nd condition.
-   `OR` combines the two conditions.

With `OR`, if *any* of the conditions are true, then the row is added to the result.

That is it with `WHERE` and it's operators!

## Order By

It is often useful to list the data in our result set in a particular order.

We can *sort* the results using `ORDER BY`, either alphabetically or numerically. Sorting the results often makes the data more useful and easier to analyze. For example, if we want to sort everything by the movie's title from A through Z:

```sql
SELECT *
FROM movies
ORDER BY name;
```

-   `ORDER BY` is a clause that indicates you want to sort the result set by a particular column.
-   `name` is the specified column.

Sometimes we want to sort things in decreasing order. For example, if we want to select all of the well-received movies, sorted from highest to lowest by their year.

```sql
SELECT *
FROM movies
WHERE imdb_rating > 8
ORDER BY year DESC;
```

-   `DESC` is a keyword used in `ORDER BY` to sort the results in *descending* order (high to low or Z-A).
-   `ASC` is a keyword used in `ORDER BY` to sort the results in *ascending* order (low to high or A-Z).

The column that we `ORDER BY` doesn't even have to be one of the columns that we're displaying.

Note: `ORDER BY` always goes after `WHERE` (if `WHERE` is present).

## Limit

Lots of databases and SQL tables contain hundreds of thousands of records. In those situations, it becomes important to cap the number of rows in the result. For instance, imagine that we just wanted to see a few examples of records.

```sql
SELECT *
FROM movies
LIMIT 10;
```

`LIMIT` is a clause that lets you specify the maximum number of rows the result set will have. This saves space on our screen and makes our queries run faster. Here, we specify that the result set can't have more than 10 rows.

`LIMIT` always goes at the very end of the query. Also it is not supported in all SQL databases.

## Case

A `CASE` statement allows us to create different outputs (usually in the `SELECT`) statement. It is SQL's way of handling **if-then** logic.

Suppose we want to condense the ratings in movies to three levels:

-   If the rating is above 8, then it is *Fantastic*.
-   If the rating is above 6, then it is *Poorly Received*.
-   Else, *Avoid at All Costs*.

```sql
SELECT name,
CASE
	WHEN imdb_rating > 8 THEN 'Fantastic'
	WHEN imdb_rating > 6 THEN 'Poorly Received'
	ELSE 'Avoid at All Costs'
	END
FROM movies;
```

-   Each `WHEN` tests a condition and the following `THEN` gives us the string if the condition is true.
-   The `ELSE` gives us the string if *all* the above conditions are false.
-   The `CASE` statement must end with `END`.

In the result, you have to scroll right because the column name is very long. To shorten it, we can rename the column to "Review" using `AS`:

```sql
SELECT name,
CASE
	WHEN imdb_rating > 8 THEN 'Fantastic'
	WHEN imdb_rating > 6 THEN 'Poorly Received'
	ELSE 'Avoid at All Costs'
	END AS 'Review'
FROM movies;
```

