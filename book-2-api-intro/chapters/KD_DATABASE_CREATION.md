# Kneel Diamonds Database

## Setup

1. In your project directory, create a `kneeldiamonds.sqlite3` file to be your database.
2. In your project directory, create a `kneel.sql` file where you will store your SQL queries.

## Creating the Tables

Use the `CREATE TABLE` statement to define all of your tables. Here's your first one. You define the other 3 tables.

```sql
CREATE TABLE `Metals`
(
    `id` INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    `metal` NVARCHAR(160) NOT NULL,
    `price` NUMERIC(5,2) NOT NULL
);
```

Make sure you set up the foreign key constraints on the Orders table. You have to define the column, and separately define the foreign ke constraint.

```sql
`metal_id` INTEGER NOT NULL,
FOREIGN KEY(`metal_id`) REFERENCES `Metals`(`id`)
```

This is your first time using SQL to create a relational database. Working with your instruction team is a good idea if you're stuck on anything or need to talk about concepts.

Once you have all tables defined in SQL, run the statements and select `kneeldiamonds.sqlite3` from the list of options that appear. Then open the file and verify that all three tables got created.

Next: [Requirements chapter >](./KD_REQUIREMENTS.md)