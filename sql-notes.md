## SQL Course 3: SQL Installation
- There are 2 ways to create a database: the 1st way is executing the script, and the 2nd way is place the script in the SQL DBMS and restore database. (review video SQL Course 3 to recheck)
## SQL Course 4: SQL SELECT Query
- Bad practice - `DISTINCT` keyword can slow down the query, so just use when really need it
- `SELECT TOP 3` 
- Coding Order
```
SELECT DISTINCT TOP 3
	Col1,
	SUM(Col2)
FROM Table
WHERE Col = 10
GROUP BY Col1
HAVING SUM(Col2) > 30
ORDER BY Col1 ASC
```
- Execute Order
```
1. FROM
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT DISTINCT
6. ORDER BY
7. TOP
```
## SQL Course 6: SQL DML Commands
- Insert into a tale from `SELECT` query: 
```
INSERT INTO table_name (column_list)
SELECT ...
FROM ...
```
- Delete all data from a table
1st way: `DELETE FROM table_name`
2nd way: `TRUNCATE TABLE table_name` => reset the table, faster than the 1st way
## SQL Course 8: SQL Joins Basic 
There are 2 ways to combine tables:
- Combine rows: SET Operators - Same columns
	+ `UNION`
	+ `UNION ALL`
	+ `EXCEPT (MINUS)`
	+ `INTERSECT`
- Combine columns: JOINs - Key column
	- `INNER JOIN`
	- `FULL JOIN`
	- `LEFT JOIN`
	- `RIGHT JOIN`
When to use `JOINs`: 3 use cases
1. Recombine Data - Big Picture: Inner Join, Left Join, Full Join
2. Data Enrichment - Extra Info: Left Join
3. Check Existence - Filtering: Inner Join, Left Join + WHERE (Left Anti Join), Full Join + WHERE (Full Anti Join)
Basic Types of `JOIN`:
- NO Join
- Inner Join
- Left Join
- Right Join
- Full Join
## SQL Course 9: Advanced SQL JOINs
Advanced Types of `JOIN`:
- Left Anti Join: Return Row from Left that has NO MATCH in Right
```
-- Get all customers who haven't place any order.
SELECT *
FROM customers AS c
LEFT JOIN orders AS o
ON c.id = o.customer_id
WHERE o.customer_id IS NULL
```
- Right Anti Join: Return Row from Right that has NO MATCH in Left
```
-- Get all orders without matching customers.
SELECT *
FROM customers AS c
RIGHT JOIN orders AS o
ON c.id = o.customer_id
WHERE c.id IS NULL
```
- Full Anti Join: Return Only Rows that DON'T MATCH in either Tables
```
-- Find customers without orders and orders without customers.
SELECT *
FROM customers AS c
FULL JOIN orders AS o
ON c.id = o.customer_id
WHERE c.id IS NULL
AND o.customer_id IS NULL
```
- Cross Join: Combine Every Row from Left with Every Row from Right 
=> All possible combinations --*Cartesian Join*--
=> No condition is needed
## SQL Course 10: Joining Multiple Tables in SQL

**Decision Tree for Joins**:

- **Inner Join**: Use when you need to see **only the matching data between tables**.
- **Left Join**: Use when you want to see **all data from one main/master table** and the matching data from another table. This is the instructor's **favorite and most frequently used join** for data analysis.
- **Full Join**: Use when you want to see **all data from all tables**, with no single table being more important than others.
- **Left Anti Join**: Use to see **only the unmatching data from one side** (the main table), using the other table for checks.
- **Full Anti Join**: Use to see **unmatching data from both tables** when both are equally important.
- **Right Join**: The instructor **does not use Right Join** in his decision tree.

**Preferred Approach for Joining Multiple Tables (Data Analysis)**:

- Always **start with a "main table" or "master table"** (e.g., the primary entity being analyzed).
- **Use `LEFT JOIN` for all other tables**. This is because data in the master table is often insufficient, and other tables provide additional, related information.
- **Control the final result (e.g., showing matching or unmatching data) using the `WHERE` clause**. This provides flexibility, similar to achieving a Left Anti Join effect.
- Visualized, this means a "master table" (Circle A) is Left Joined with other tables (Circle B, Circle C), always pulling matching data from B and C.
- An alternative, if **all tables are equally important and you only need the overlapping (matching) data from all of them, is to use `INNER JOIN`** for all tables.

**Practical Example: Joining `orders`, `customers`, `products`, `employees`**:

1. **Connect to `sales DB`**.
2. **Identify `orders` as the main table** because the task specifies retrieving "all orders" along with related details.
3. **Start the query from the main table**: `SELECT O.order_ID, O.sales` from `sales.orders` (alias `O`).
4. **Explore other tables or use an Entity Relationship (ER) model** to find necessary columns and common join keys (e.g., `customer_ID` between `orders` and `customers`). ER models are crucial for understanding table relationships in large projects.
5. **Sequentially `LEFT JOIN` other tables with the main `orders` table**:
    - `customers` on `O.customer_ID = C.customer_ID`.
    - `products` on `O.product_ID = P.product_ID`. **Crucially, always join back to the main `orders` table, not between the other joined tables** (e.g., not `customers` with `products`).
    - `employees` on `O.salesperson_ID = E.employee_ID`. The ER diagram helps confirm `salesperson_ID` in `orders` links to `employee_ID` in `employees`.

**Important Considerations for Multi-Table Joins**:

- **Use aliases for columns**: When columns with the same name exist in different tables (e.g., `first_name` from both `customers` and `employees`), **rename them using aliases** (e.g., `customer_first_name`, `employee_first_name`) for clarity in results.
- **Always specify table or alias before column name**: This prevents ambiguity and errors, especially when column names are duplicated across tables (e.g., `O.order_ID`, `C.first_name`).
- **Double-check join keys**: **Ensure you use the correct columns for join conditions** (e.g., `O.customer_ID = C.customer_ID`), as incorrect keys will lead to meaningless results.
## SQL Course 26: Why You Need These 5 SQL Techniques in Your SQL Project | Architecture 

Five SQL techniques used to reduce and optimize the complexity of SQL queries, along with the reasons for their necessity and an overview of database architecture. The five techniques are:

- Subqueries
- Common Table Expressions (CTE)
- Views
- Temporary Tables
- `CREATE TABLE AS SELECT` (CTAS)

**1. Why These Techniques Are Needed**

In real-world projects, SQL queries become very complex due to multiple users with different roles (e.g., financial analysts, risk managers, data engineers, data scientists, data analysts) accessing the database and executing complex analytical or extraction queries. These complex scenarios introduce several challenges:

- **Redundant Logic:** Different users often write queries that contain **repeated logic and redundant code**, leading to duplicated effort and potential inconsistencies if not everyone implements the logic correctly.
- **Performance Issues:** Without optimization, complex queries can lead to **significant performance problems**. Queries might take hours or minutes to execute, affecting overall project efficiency.
- **Complexity for Users:** The underlying database often has a **complex data model** designed for specific applications, which includes many tables and relationships. Analysts and other users need to understand this model to write queries, leading to frequent questions for database experts and **stressing the database team with repetitive explanations**.
- **Database Stress:** Repeated execution of large, complex queries can cause **immense stress on the database**, potentially leading to its slowdown or even bringing it down.
- **Data Security:** Giving **direct access to physical database tables** to all users poses a security risk, as sensitive data might be exposed. It's crucial to protect tables, columns, and rows from unauthorized access.

The five SQL techniques mentioned (subqueries, CTE, views, temporary tables, CTAS) are presented as solutions to these common issues in data projects.

**2. Database Architecture (Simplified Overview)**

Understanding the database architecture is crucial to grasp how these techniques work behind the scenes. The architecture involves two main sides:

- **Client Side:** This is where the user writes and sends an SQL query.
- **Server Side:** This is where the database lives and processes queries. Key components on the server side include:
    - **Database Engine:** The **"brain" of the database**, responsible for handling operations like storing, retrieving, and managing data. It processes every query executed.
    - **Storage:** Databases utilize different types of storage:
        - **Disk Storage:** Acts as **long-term, permanent memory** where data is stored persistently, even when the system is off. It can store a lot of data but is **slow for reading and writing**.
        - **Cache:** Serves as **short-term, temporary memory** that holds frequently used data for quick access. It is **very fast** for data retrieval compared to disk but stores data only for a short period.
    - **Types of Storage Areas in Databases:** There are typically three main types:
        - **User Data Storage:** This holds the **main content and actual data** that users interact with and care about (e.g., tables like `customers`, `employees`, `orders`).
        - **System Catalog (Metadata):** This is the **internal storage for the database's own information**, acting as a blueprint that tracks everything about the database itself.
            - **Metadata** is defined as **"data about data"**. For example, for a `customers` table, its metadata would include table name, column names (`customer_ID`, `first_name`), data types (`int`, `varchar`), length, and nullability.
            - This information can be explored by users through a special hidden schema called `information_schema` in SQL Server, which contains built-in views (e.g., `information_schema.tables`, `information_schema.columns`). The system catalog helps the database quickly find the structure of tables and columns, and allows users to browse the database's catalog.
        - **Temporary Data Storage:** This is a **temporary space** used by the database for short-term tasks like processing queries or sorting data. Once these tasks are completed, this storage is cleaned up.
            - Temporary tables are found within a special system database called `tempdb`, which is typically only accessible to database administrators in real projects.

**3. Simple Query Execution Example:**

When a simple `SELECT` query is sent from the client to the server, the database engine first checks if the required data is in the **cache** for fast retrieval. If not, it retrieves the data from **disk storage**, executes the query, and sends the results back to the client.

The understanding of these challenges and the database architecture provides the foundation for appreciating the importance and function of the five SQL techniques that will be explored further.


