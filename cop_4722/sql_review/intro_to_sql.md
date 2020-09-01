# Introduction to SQL

## What is SQL?

**S**tructed **Q**uery **L**anguage is a programming language designed to manage data stored in relational databases.

SQL operates through simple, declarative statements. This keeps data accurate and secure, and helps maintain the integrity of databases, regardless of size.

The SQL language is widely used today across web frameworks and database applications. SQL gives you the freedom to explore your data, and the power to make better decisions. 

## Terminology

A `relational database`* is a database that organizes information into one or more tables. 

A `table` is a collection of data organized into rows and columns. Tables are sometimes referred to as `relations`. 

A `column` is a set of data values of a particular type. A `row` is a single record in a table.

All data stored in a relational database is of a certain data type. Some of the most common data types are:

-   `INTEGER`: a positive or negative whole number
-   `TEXT`: a text string
-   `DATE`: the date formatted as YYYY-MM-DD
-   `REAL`: a decimal value

## Statements and Clauses

A `statement` is text that the database recognizes as a valid command. Statements always end in a semicolon `;`.

A `clause` performs a specific task in SQL. By convention, clauses are written in capital letters. Clauses can also be referred to as commands.

The structure of SQL statements vary. The number of lines used does not matter. A statement can be written all on one line, or split up across multiple lines if it makes it easier to read. 

Example statement:

```sql
CREATE TABLE table_name (
	column_1 data_type
	column_2 data_type
	column_3 data_type
);
```

### Create

A `create` statement allows us to create a new table in the database. You can use the `create` statement anytime you want to create a new table from scratch. The statement below creates a new table named `celebs`.

```sql
CREATE TABLE celebs(
    id INTEGER,
    name TEXT,
    age INTEGER
);
```

1.  `CREATE TABLE` is a `clause` that tells SQL you want to create a new table.
2.  `celebs` is the name of the table.
3.  `(id INTEGER, name TEXT, age INTEGER)` is a list of parameters defining each `column`, or attribute in the table and its data type:
    1.  `id` is the first `column` in the table. It stores values of data type `INTERGER`.
    2.  `name` is the second `column` in the table. It stores values of data type `TEXT`.
    3.  `age` is the third `column` in the table. It stores values of data type `INTEGER`.

### Insert

The `INSERT` statement inserts a new row into a table. You can use the `INSERT` statement when you want to add new records. The statement below enters a record for a celebrity into the `celebs` table.

```sql
INSERT INTO celebs (id, name, age)
VALUES (1, 'Taylor Swift', 22)
```

1.  `INSERT INTO` is a `clause` that adds the specified row or rows.
2.  `celebs` is the name of the table the row is added to.
3.  `(id, name, age)` is a parameter identifying the columns that data will be inserted into.
4.  `VALUES` is a `clause` that indicates the data being inserted.
    1.  `(1, 'Taylor Swift', 22)` is a parameter identifying the values being inserted.
        1.  `1` is an integer that will be inserted into the `id` column.
        2.  `'Taylor Swift'` is text that will be inserted into the `name` column.
        3.  `22` is an integer that will be inserted into the `age` column.

### Select

A `SELECT` statement is used to fetch data from a database. In the statement below, `SELECT` returns all data in the `name` column of the `celebs` table.

```sql
SELECT name FROM celebs;
```

1.  `SELECT` is a clause that indicates that the statement is a query.
    -   You will use `SELECT every time you query data from a database.
2.  `name` specifies the column to query data from.
3.  `FROM celebs` specifies the name of the table to query data from. In this statement, data is queried from the celebs table.

You can also query data from all columns in a table using `SELECT`.

#### Wildcard

```sql
SELECT * FROM celebs;
```

`*` is a special wildcard character. It allows you to select every column in a table without having to name each one individually. Here, the result set contains every column in the `celebs` table.

`SELECT` statements always return a new table called the `result` set.

### Alter Table

The `ALTER TABLE` statement adds a new column to a table. You can use this command when you want to add columns to a table. The statement below adds a new column `twitter_handle` to the `celebs`table.

```sql
ALTER TABLE celebs
ADD COLUMN twitter_handle TEXT;
```

1.  `ALTER TABLE` is a clause that lets you make the specified changes.
2.  `celebs` is the name of the table that is being changed.
3.  `ADD COLUMN` is a clause that lets you add a new column to a table.
    1.  `twitter_handle` is the name of the new column being added.
    2.  `TEXT` is the data type for the new column.
4.  `NULL` is a special value in SQL that represents missing or unknown data. Here, the rows that existed before the column was added to have `NULL` values for `twitter_handle`.

### Update

The `UPDATE` statement edits a row in a table. You can use the `UPDATE` statement when you want to change existing records. The statement below updates the records with an `id` value of `1` to have the `twitter_handle` `@taylorswift13`

```sql
UPDATE celebs
SET twitter_handle = '@taylorswift13'
WHERE id = 1;
```

1.  `UPADTE` is a clause that edits a row in the table.
2.  `celebs` is the name of the table.
3.  `SET` is a clause that indicates the column to edit.
    1.  `twitter_handle` is the name of the column that is going to be updated.
    2.  `@taylorswift13` is the new value that is going to be inserted into the `twitter_handle` column.
4.  `WHERE` is a clause that indicates which row(s) to update with the new column value. Here the row with a `1` in the `id` column is the row that will have the `twitter_handle` updated to `@taylorswift13`.

### Delete

The `DELETE FROM` statement deletes one or more tows form a table. You can use the statement when you want to delete existing records. The statement below deletes all records in the `celeb` table with no `twitter_handle`.

```sql
DELETE FROM celebs
WHERE twitter_handle IS NULL
```

1.  `DELETE FROM` is a clause that lets you delete rows from a table.
2.  `celebs` is the name of the table we want to delete rows from.
3.  `WHERE` is a clause that lets you select which rows you want to delete. Here we want to delete all of the rows where the `twitter_handle` `IS NULL`.
4.  `IS NULL` is a condition in SQL that returns true when the value is `NULL` and false otherwise.

### Constraints

*Constraints* add information about how a column can be used and are invoked after specifying the data type for a column. They can be used to tell the database to reject inserted data that does not adhere to a certain restriction. The statement below sets *constraints* on the `celebs` table.

```sql
CREATE TABLE celebs(
	id INTERGER PRIMARY KEY,
	name TEXT UNIQUE,
	date_of_birth TEXT NOT NULL,
	date_of_death TEXT DEFAULT 'Not Applicable'
);
```

1.  `PRIMARY KEY` columns can be used to uniquely identify the row. Attempts to insert a row with an identical value to a row already in the table will result in a *constraint violation* which will not allow you to insert the new row.
2.  `UNIQUE` columns have a different value for every row. This is similar to `PRIMARY KEY` except a table can have many different `UNIQUE` columns.
3.  `NOT NULL` columns must have a value. Attempts to insert a row without a value for a `NOT NULL` column will result in a *constraint violation* and the new row will not be inserted.
4.  `DEFAULT` columns take an additional argument that will be the assumed value for an inserted row if the new row does not specify a value for that column.