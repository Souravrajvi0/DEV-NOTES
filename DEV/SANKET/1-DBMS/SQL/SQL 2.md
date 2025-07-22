---
view-count: 6
---
## The MySQL BETWEEN Operator

The `BETWEEN` operator selects values within a given range. The values can be numbers, text, or dates.

The `BETWEEN` operator is inclusive: begin and end values are included.

![SQL 2-20250101101731542.webp](../../../Images/SQL%202-20250101101731542.webp)

![SQL 2-20250101101806596.webp](../../../Images/SQL%202-20250101101806596.webp)

![SQL 2-20250101101822708.webp](../../../Images/SQL%202-20250101101822708.webp)


![SQL 2-20250101101855097.webp](../../../Images/SQL%202-20250101101855097.webp)



![SQL 2-20250101101940786.webp](../../../Images/SQL%202-20250101101940786.webp)

![SQL 2-20250101102009084.webp](../../../Images/SQL%202-20250101102009084.webp)

![SQL 2-20250101102021063.webp](../../../Images/SQL%202-20250101102021063.webp)

## MySQL Aliases


Aliases are used to give a table, or a column in a table, a temporary name.

Aliases are often used to make column names more readable.

An alias only exists for the duration of that query.

An alias is created with the `AS` keyword.

![SQL 2-20250101102532369.webp](../../../Images/SQL%202-20250101102532369.webp)


![SQL 2-20250101102647116.webp](../../../Images/SQL%202-20250101102647116.webp)


![SQL 2-20250101102918238.webp](../../../Images/SQL%202-20250101102918238.webp)

Here We're Using Multiple Tables 




1. **What is a Table Alias?**
    
    - A table alias is a temporary name given to a table within a query. It allows you to reference the table using a shorter or more convenient name. In your query, `Customers` is aliased as `c` and `Orders` as `o`.
2. **Why Use Aliases?**
    
    - **Simplicity**: It makes the query shorter and easier to read, especially when dealing with multiple tables or long table names.
    - **Clarity**: It helps avoid ambiguity when two tables have columns with the same name. For example, both `Customers` and `Orders` might have a column named `CustomerID`.
3. **Using the Alias to Reference Columns**:
    
    - When you use an alias, you can reference the columns of the table using the alias followed by a dot (`.`) and the column name. For example:
        - `o.OrderID`: Refers to the `OrderID` column from the `Orders` table (aliased as `o`).
        - `c.CustomerName`: Refers to the `CustomerName` column from the `Customers` table (aliased as `c`).


- **`o.OrderID`**:
    - `o` is the alias for the `Orders` table.
    - `OrderID` is the column within that table.
    - This notation tells the SQL engine to look for the `OrderID` column specifically within the `Orders` table.

### Benefits of This Approach

- **Avoids Ambiguity**: If both tables had a column named `CustomerID`, using `c.CustomerID` and `o.CustomerID` makes it clear which table's column you are referring to.
- **Improves Readability**: Especially in complex queries with joins, using aliases can make the SQL statement cleaner and easier to understand.


## MySQL DESC TABLE 

`DESCRIBE table_name;`

![SQL 2-20250101105548330.webp](../../../Images/SQL%202-20250101105548330.webp)

## MySQL Joining Tables

A `JOIN` clause is used to combine rows from two or more tables, based on a related column between them.


![SQL 2-20250101114248529.webp](../../../Images/SQL%202-20250101114248529.webp)

- Now if we have to find the details of and order with the products in it! HOW CAN WE GET THE ACTUAL DATA???
- With the help of joins we can club or combine the data of multiple tables together based on their relational behavior 


