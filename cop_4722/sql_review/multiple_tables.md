# Multiple Tables

In order to efficiently store data, we often spread related information across multiple tables.

For instance, a magazine company has users with different types of subscriptions to different products. Different subscriptions might have many different properties. Each customer would also have lots of associated information.

We could have one table with all of the sample information:

-   `order_id`
-   `customer_id`
-   `customer_name`
-   `customer_address`
-   `subscription_id`
-   `subscription_description`
-   `subscription_monthly_price`
-   `subscription_length`
-   `purchase_date`

However, a lot of information would be repeated. If the same customer has multiple subscriptions, that `customer_name` and `customer_address` will be reported multiple times. If the same subscription type is ordered by multiple customers, then the `subscription_price` and `subscription_description`. This would make the table big and unmanageable.

So instead, you split your data into three tables:

-   `orders` would contain just the information necessary to describe what was ordered:
    -   `order_id`, `customer_id`, `subscription_id`, `purchase_date`
-   `subscriptions` would contain the information to describe each type of subscription:
    -   `subscription_id`,`description`, `price_per_month`, `subscription_length`
-   `customers` would contain the information for each customer:
    -   `customer_id`, `customer_name`, `address`

## Combining Tables

If we just look at the `orders` table, we can't really tell what's happened in each order. However, if we refer to the other tables, we can get a complete picture.

To find out the customer name attached to an order, we need to look at the `customers` table and cross reference the `customer_id` found in both tables. This kind of matching is called **joining** two table.

Combining tables manually is time-consuming. Luckily, SQL gives us an easy sequence for this: it's called a `JOIN`.

If you want to combine `orders` and `customers`, you would type:

```sql
SELECT *
FROM orders
JOIN customers
	ON orders.customer_id = customers.customer_id;
```

1.  The first line selects all columns from our combined table. If we only want to select certain columns, we can specify which ones we want.
2.  The second line specified the first table that we want to look in, `orders`.
3.  The third line uses `JOIN` to say that we want to combine information from `orders` with `customers`.
4.  The fourth line tells us how to combine the two tables. We want to match `orders` table's `customer_id` column with `customers` table's `customer_id` column.

Because column names are often repeated across multiple tables, we use the syntax `table_name.column_name` to be sure that our requests for columns are unambiguous. In this example, we use this syntax in the `ON` statement, but we will also use it in the `SELECT` or any other statement where we refer to column names.

For example: Instead of selecting *all* the columns using `*`. if we only wanted to select `orders` table's `order_id` column and `customers` table's `customer_name` column, we could use the following query:

```sql
SELECT orders.order_id,
	customers.customer_name
FROM orders
JOIN customers
	ON orders.customer_id = customers.customer_id;
```

## Inner Joins

Let's revisit how we joined `orders` and `customers`. For every possible value of `customer_id` in `orders`, there was a corresponding row of `customers` with the same `customer_id`.

However, that isn't necessarily true.

For instance, imagine that our `customers` table was out of date, and was missing any information on customer 11. If that customer had an order in `orders`, what would happen when we joined the tables?

When performing a simple `JOIN` (often called an *inner join*) the result only includes rows that match our `ON` condition.

Consider the following tables:

| C1   | C2   |
| ---- | ---- |
| A    | B    |
| Q    | W    |
| X    | Y    |

| C2   | C3   |
| ---- | ---- |
| B    | C    |
| E    | R    |
| Y    | Z    |

If we were to join these two tables using `table1.c2 = table2.c2` then the following table would be the result:

| C1   | C2   | C3   |
| ---- | ---- | ---- |
| A    | B    | C    |
| X    | Y    | Z    |

The first and last rows have matching values of `c2`. The middle rows do not match. The final result has all values from the first and last rows but does not include the non-matching middle row.

## Left Joins

What if we want to combine two tables and keep some of the unmatched rows?

SQL lets us do this through a command called `LEFT JOIN`. A *left join* will keep all rows from the first table, regardless of whether there is a matching row in the second table.

Consider the following tables:

| C1   | C2   |
| ---- | ---- |
| A    | B    |
| Q    | W    |
| X    | Y    |

| C2   | C3   |
| ---- | ---- |
| B    | C    |
| E    | E    |
| Y    | Z    |

If we were to join these two tables using `LEFT JOIN` we would be  left with:

| C1   | C2   | C3   |
| ---- | ---- | ---- |
| A    | B    | C    |
| Q    | W    |      |
| X    | Y    | Z    |

The first and last rows have matching values of `c2`. The middle rows do not match. The final result will keep all rows of the first table but will omit the un-matched row from the second table.

The final table represents an operation produced by the following command:

```sql
SELECT *
FROM table1
LEFT JOIN table2
	ON table1.c2 = table2.c2
```

1.  The first line selects all columns from both tables.
2.  The second line selects `table` (the *left* table).
3.  The third line performs a `LEFT JOIN` on `table2` (the *right* table).
4.  The fourth line tells SQL how to perform the join (by looking for matching values in column `c2`).

## Primary Key vs. Foreign Key

Let's return to our example of the magazine subscriptions. Recall that we had three tables: `orders`, `subscriptions`, and `customers`.

Each of these tables has a column that uniquely identifies each row of that table.

-   `order_id` for `orders`
-   `subscription_id` for `subscriptions`
-   `customer_id` for `customers`

These special columns are called **primary keys**.

Primary keys have a few requirements:

-   None of the values can be `NULL`.
-   Each value must be unique (you can't have two customers with the same `customer_id` in the `customers` table).
-   A table can not have more than one primary key column.

Lets examine a sample `orders` table.

| order_id | customer_id | subscription_id | purchase_date |
| -------- | ----------- | --------------- | ------------- |
| 1        | 2           | 3               | 2017-01-01    |
| 2        | 2           | 2               | 2017-01-01    |
| 3        | 3           | 1               | 2017-01-01    |

Note that `customer_id` (the primary key for `customers`) and `subscription_id` (the primary key for `subscriptions`) both appear in this.

When the primary key for one table appears in a different table, it is called a **foreign key**.

So `customer_id` is a primary key when it appears in `customers`, but a foreign key when it appears in `orders`.

In this example, our primary keys all had somewhat descriptive names. Generally, the primary key will just be called `id`. Foreign keys will have more descriptive names.

*Why is this important?* The most common types of joins will be joining a foreign key from one table with the primary key from another table. For instance, when we join `orders` and `customers`, we join on `customer_id`, which is a foreign key in `orders` and the primary key in `customers`.

## Cross Join

So far, we've focused on matching rows that have some information in common.

Sometimes, we just want to combine all rows of one table with all rows of another table.

For instance, if we had a table of `shirts` and a table of `pants`, we might want to know all the possible combinations to create different outfits.

Our code might look like this:

```sql
SELECT shirts.shirt_color,
	pants.pants_color
FROM shirts
CROSS JOIN pants;
```

-   The first two lines select the columns `shirt_color` and `pants_color`.
-   The third line pulls data from the table `shirts`.
-   The fourth line performs a `CROSS JOIN` with `pants`.

Notice that cross joins don't require an `ON` statement. You're not really joining on any columns.

If we have 3 different shirts (white, grey, olive) and 2 different pants (light denim, black), the results might look like this:

| shirt_color | pants_color |
| ----------- | ----------- |
| white       | light denim |
| white       | black       |
| grey        | light denim |
| grey        | black       |
| olive       | light denim |
| olive       | black       |

3 shirts * 2 pants = 6 combinations, checks out.

A more common use of `CROSS JOIN` is when you need to compare each row of a table to a list of values.

Let's return to the `newspaper` subscriptions example. This table contains two columns not previously mentioned.

-   `start_month`: the first month where the customer subscribed to the print newspaper (ex. 2 for February)
-   `end_month`: the final months where the customer subscribed to the print newspaper

Suppose we wanted to know how many users were subscribed during each month of the year. For each month (`1`,`2`,`3`) we would need to know if a user was subscribed. You can use `CROSS JOIN` to solve this problem.

```sql
SELECT month,
	COUNT(*)
FROM newspaper
CROSS JOIN months
WHERE start_month <= month
	AND end_month >= month
GROUP BY month;
```

## Union

Sometimes we just want to stack one dataset on top of the other. Well, the `UNION` operator allows us to do that.

Suppose we have two tables and they have the same columns.

 `table1`:

|  pokemon   | type  |
| :--------: | :---: |
| Bulbasaur  | Grass |
| Charmander | Fire  |
|  Squirtle  | Water |

`table2`:

| pokemon |  type  |
| :-----: | :----: |
| Snorlax | Normal |

If we combine these with `UNION` using:

```sql
SELECT *
FROM table1
UNION
SELECT *
FROM table2;
```

The result would be:

|  pokemon   |  type  |
| :--------: | :----: |
| Bulbasaur  | Grass  |
| Charmander |  Fire  |
|  Squirtle  | Water  |
|  Snorlax   | Normal |

SQL has strict rules for appending data:

-   Tables must have the same number of columns.
-   The columns must have the same dat type in the same order as the first table.

## With

Often times, we want to combine two tables, but one of the tables is the result of another calculation. Let's return to our magazine order example. our marketing department might want to know a bit more about our customers. For instance, they might want to know how many magazines each customer subscribes to. We can easily calculate this using our `orders` table.

```sql
SELECT customer_id
	COUNT(subscription_id) AS 'subscriptions'
FROM orders
GROUP BY customer_id;
```

This query is good. but a `customer_id` isn't terribly useful for our marketing department, they probably want to know the customer's name.

We want to be able to join the results of this query with out `customers` table, which will tell us the name of each customer. We can do this by using a `WITH` clause.

```sql
WITH previous_results AS (
	SELECT ...
	...
	...
)
SELECT *
FROM previous_results
JOIN customers
	ON ____ = ____;
```

-   The `WITH` statement allows for us to perform a separate query (such as aggregating customer's subscriptions).
-   `previous_results` is the alias that we will use to reference any columns from the query inside of the `WITH` clause.
-   We can then go on to do whatever we want with this temporary table (such as join the temporary table with another table).

Essentially, we are putting a whole first query inside the parenthesis `()` and giving it a name. After that, we can use this name as if it's a table and write a new query *using* the first query. 