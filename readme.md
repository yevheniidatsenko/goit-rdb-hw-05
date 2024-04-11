## SQL Homework

This file contains the instructions for the SQL homework tasks.

### Task 1

Write a SQL query that will display the `order_details` table and the `customer_id` field from the `orders` table for each record in the `order_details` table. This should be done using a nested query in the `SELECT` operator.

The following is the SQL query for Task 1:

```sql
SELECT
  order_details.*,
  orders.customer_id
FROM order_details
INNER JOIN orders ON order_details.order_id = orders.order_id;
```

### Task 2

Write a SQL query that will display the `order_details` table. Filter the results so that the corresponding record in the `orders` table satisfies the condition `shipper_id=3`. This should be done using a nested query in the `WHERE` operator.

The following is the SQL query for Task 2:

```sql
SELECT
  order_details.*
FROM order_details
INNER JOIN orders ON order_details.order_id = orders.order_id
WHERE orders.shipper_id = 3;
```

### Task 3

Write a SQL query that uses a nested query in the `FROM` operator to select rows from the `order_details` table where the `quantity` is greater than 10. For the resulting data, find the average value of the `quantity` field, grouped by `order_id`.

The following is the SQL query for Task 3:

```sql
SELECT
  order_id,
  AVG(quantity) AS average_quantity
FROM (
  SELECT
    order_details.*
  FROM order_details
  WHERE quantity > 10
) AS t
GROUP BY order_id;
```

### Task 4

Solve Task 3 using the `WITH` operator to create a temporary table `temp`. If your MySQL version is earlier than 8.0, create this query in the same way as it is done in the notes.

The following is the SQL query for Task 4:

```sql
WITH temp AS (
  SELECT
    order_details.*
  FROM order_details
  WHERE quantity > 10
)
SELECT
  order_id,
  AVG(quantity) AS average_quantity
FROM temp
GROUP BY order_id;
```

### Task 5

Create a function with two parameters that will divide the first parameter by the second. Both parameters and the returned value should be of type `FLOAT`. Use the `DROP FUNCTION IF EXISTS` construct. Apply the function to the `quantity` attribute of the `order_details` table.

The following is the SQL query for Task 5:

```sql
DROP FUNCTION IF EXISTS divide_floats;

CREATE FUNCTION divide_floats(
  a FLOAT,
  b FLOAT
) RETURNS FLOAT
BEGIN
  RETURN a / b;
END;

SELECT
  order_details.*,
  divide_floats(quantity, 2) AS divided_quantity
FROM order_details;
```
