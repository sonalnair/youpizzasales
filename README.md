# youpizzasales
### Summary of the `youpizza.sql` Code

The provided `youpizza.sql` file is a MySQL database dump for a pizza sales database named `youpizza`. It defines the schema and data for a pizza restaurant's order management system, including tables for orders, order details, pizza types, and pizza pricing. I have worked on total number of order placed,revenue generation,most common pizza size and top 5 pizza ordered.
---

### Database Overview
- **Database Name**: `youpizza`
- **Purpose**: Tracks pizza orders, including details about pizzas, their types, sizes, prices, and order timestamps.
- **MySQL Version**: Compatible with MySQL 8.0.42.
- **Tables**: Four tables (`order_details`, `orders`, `pizza_types`, `pizzas`).

---

### Table Structure and Content

1. **Table: `orders`**
   - **Purpose**: ## Retrieve the total number of orders placed.
   - **Columns**:SELECT 
    COUNT(order_id) AS total_orders
   - **Key Insight**: Tracks total number of  pizzas are placed.
   - 
2. **Table: `order_details`**
   - **Purpose**: ### Calculate the total revenue generated from pizza sales.
   - **Columns**:SELECT 
    ROUND(SUM(order_details.quantity * pizzas.price),
            2) AS total_sales
FROM
    order_details
        JOIN
    pizzas ON pizzas.pizza_id = order_details.pizza_id
    - **Key Insight**: Provides temporal data for analyzing revenue genrated from pizza sales.

3. **Table: `pizza_types`**
   - **Purpose**: ##Identify the highest-priced pizza..
   - **Columns**:
     SELECT 
    pizza_types.name, pizzas.price
FROM
    pizza_types
        JOIN
    pizzas ON pizza_types.pizza_type_id = pizzas.pizza_type_id
ORDER BY pizzas.price DESC
LIMIT 1;
   - **Data**: 32 pizza types across four categories (e.g., `hawaiian`, `five_cheese`, `spicy_ital`).
   - **Key Insight**: Organizes pizzas by type and category for menu analysis.

4. **Table: `pizza size`**
   - **Purpose**: ##Identify the most common pizza size ordered.
  SELECT 
    pizzas.size,
    COUNT(order_details.order_details_id) AS order_count
FROM
    pizzas
        JOIN
    order_details ON pizzas.pizza_id = order_details.pizza_id
GROUP BY pizzas.size
ORDER BY order_count DESC
LIMIT 1;
   - **Data**: 91 records covering various sizes for each pizza type (e.g., `the_greek` has S, M, L, XL, XXL).
   

---


