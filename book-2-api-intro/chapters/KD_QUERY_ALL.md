# Support GET For Orders

## Inserting Some Orders

Before writing Python code, practice your SQL by by authoring some `INSERT INTO` SQL statements in your SQL file.

1. Create as many records in the Metals, Styles, and Sizes tables that you need.
1. Create several records in the Orders tables.

## Handling GET Requests for Orders

### All Orders

1. Implement the required code, starting with the `do_GET()` function to get all records from the **Orders** table.
2. Restart your debugger.
3. GET http://localhost:8088/orders
4. Verify that you get the correct JSON representation of all of your orders.

### Single Orders

1. Implement the required code to get a single record from the **Orders** table.
2. Restart your debugger.
3. GET http://localhost:8088/orders/2
4. Verify that you get the correct JSON representation of your order.

