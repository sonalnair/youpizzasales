# youpizzasales
### Summary of the `youpizza.sql` Code

The provided `youpizza.sql` file is a MySQL database dump for a pizza sales database named `youpizza`. It defines the schema and data for a pizza restaurant's order management system, including tables for orders, order details, pizza types, and pizza pricing. 
---

### Database Overview
- **Database Name**: `youpizza`
- **Purpose**: Tracks pizza orders, including details about pizzas, their types, sizes, prices, and order timestamps.
- **MySQL Version**: Compatible with MySQL 8.0.42.
- **Tables**: Four tables (`order_details`, `orders`, `pizza_types`, `pizzas`).

---

### Table Structure and Content

1. **Table: `order_details`**
   - **Purpose**: Stores individual items in each order.
   - **Columns**:
     - `order_details_id` (int, Primary Key): Unique identifier for each order item.
     - `order_id` (int): Links to the `orders` table.
     - `pizza_id` (text): Identifies the pizza (e.g., `hawaiian_m` for medium Hawaiian pizza).
     - `Quantity` (int): Number of pizzas ordered (all entries have `Quantity = 1` or `2` in the provided data).
   - **Data**: Contains 918+ records (partially shown), linking specific pizzas to orders (e.g., `order_details_id=1` links `order_id=1` to a `hawaiian_m` pizza).
   - **Key Insight**: Tracks which pizzas are ordered in each transaction.

2. **Table: `orders`**
   - **Purpose**: Records order metadata, including when orders were placed.
   - **Columns**:
     - `order_id` (int, Primary Key): Unique order identifier.
     - `order_date` (date): Date of the order (e.g., `2015-01-01` to `2015-12-31`).
     - `order_time` (time): Time of the order (e.g., `11:38:36`).
   - **Data**: Contains 21,350 orders from January 1, 2015, to December 31, 2015.
   - **Key Insight**: Provides temporal data for analyzing order patterns (e.g., peak hours or days).

3. **Table: `pizza_types`**
   - **Purpose**: Defines pizza types, their categories, and ingredients.
   - **Columns**:
     - `pizza_type_id` (text): Unique identifier (e.g., `bbq_ckn`).
     - `name` (text): Pizza name (e.g., `The Barbecue Chicken Pizza`).
     - `category` (text): Category (Chicken, Classic, Supreme, Veggie).
     - `ingredients` (text): List of ingredients (e.g., `Barbecued Chicken, Red Peppers, Green Peppers`).
   - **Data**: 32 pizza types across four categories (e.g., `hawaiian`, `five_cheese`, `spicy_ital`).
   - **Key Insight**: Organizes pizzas by type and category for menu analysis.

4. **Table: `pizzas`**
   - **Purpose**: Stores pizza sizes and prices for each pizza type.
   - **Columns**:
     - `pizza_id` (text): Unique pizza identifier (e.g., `bbq_ckn_s` for small Barbecue Chicken pizza).
     - `pizza_type_id` (text): Links to `pizza_types`.
     - `size` (text): Size (S, M, L, XL, XXL).
     - `price` (double): Price (e.g., $12.75 for `bbq_ckn_s`, $20.75 for `bbq_ckn_l`).
   - **Data**: 91 records covering various sizes for each pizza type (e.g., `the_greek` has S, M, L, XL, XXL).
   - **Key Insight**: Enables revenue calculations by linking pizza prices to orders.

---

### Key Relationships
- **Primary Keys**:
  - `order_details`: `order_details_id`
  - `orders`: `order_id`
- **Foreign Key Relationships** (implied, not explicitly defined in schema):
  - `order_details.order_id` references `orders.order_id`.
  - `order_details.pizza_id` references `pizzas.pizza_id`.
  - `pizzas.pizza_type_id` references `pizza_types.pizza_type_id`.
- **Structure**: The database uses a relational model to connect orders to specific pizzas, their types, and prices, allowing for detailed sales analysis.

---

### Potential Use Cases (for a Micro SQL Project)
This database is ideal for beginner SQL projects, as it supports:
- **Basic Queries**: Retrieve popular pizzas, total orders per day, or average order size.
  ```sql
  SELECT pt.name, COUNT(od.order_details_id) as order_count
  FROM order_details od
  JOIN pizzas p ON od.pizza_id = p.pizza_id
  JOIN pizza_types pt ON p.pizza_type_id = pt.pizza_type_id
  GROUP BY pt.name
  ORDER BY order_count DESC;
  ```
- **Joins**: Combine tables to analyze sales by category or size.
- **Aggregations**: Calculate total revenue or busiest hours.
  ```sql
  SELECT o.order_date, SUM(p.price * od.Quantity) as daily_revenue
  FROM orders o
  JOIN order_details od ON o.order_id = od.order_id
  JOIN pizzas p ON od.pizza_id = p.pizza_id
  GROUP BY o.order_date;
  ```
- **Filtering**: Find orders for specific pizzas or dates.


---

