## Table of Contents
- [SQL Course 3: SQL Installation](#sql-course-3-sql-installation)

- [SQL Course 4: SQL SELECT Query](#sql-course-4-sql-select-query)

- [SQL Course 6: SQL DML Commands](#sql-course-6-sql-dml-commands)

- [SQL Course 8: SQL Joins Basic](#sql-course-8-sql-joins-basic)

- [SQL Course 9: Advanced SQL JOINs](#sql-course-9-advanced-sql-joins)

- [SQL Course 10: Joining Multiple Tables in SQL](#sql-course-10-joining-multiple-tables-in-sql)

- [SQL Course 11: SQL SET Operators: UNION, UNION ALL, EXCEPT (MINUS), INTERSECT](#sql-course-11-sql-set-operators-union-union-all-except-minus-intersect)

- [SQL Course 12: SQL Functions Explained | In 5 Minutes](#sql-course-12-sql-functions-explained--in-5-minutes)

- [SQL Course 13: SQL String Functions | A Detailed Guide](#sql-course-13-sql-string-functions--a-detailed-guide)

- [SQL Course 26: Why You Need These 5 SQL Techniques in Your SQL Project | Architecture](#sql-course-26-why-you-need-these-5-sql-techniques-in-your-sql-project--architecture)

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

***

## SQL Course 11: SQL SET Operators: UNION, UNION ALL, EXCEPT (MINUS), INTERSECT

SQL Set Operators are powerful tools used to **combine the rows of multiple queries or tables into a single result set**. Unlike SQL JOINs, which combine columns side-by-side, set operators append rows underneath each other. They do not require a key column but have strict rules for combining data.

**Key Differences from SQL JOINs:**
*   **Purpose:** Set operators combine rows, while JOINs combine columns.
*   **Key Requirement:** JOINs typically require a key column for combining data, whereas set operators do not; they only require the same columns.

**Syntax:**
The basic syntax involves placing a set operator between two or more `SELECT` statements:
`SELECT ... FROM Query1`
`[SET_OPERATOR]`
`SELECT ... FROM Query2`

**Rules of SQL Set Operators:**
For queries to be combined using set operators, several rules must be followed:
*   **`ORDER BY` Clause:** Can only be used once, and only at the very end of the entire combined query. It cannot be used within individual `SELECT` statements.
*   **Number of Columns:** All `SELECT` statements being combined **must return the same number of columns**. An error will occur if the column counts differ.
*   **Data Types:** The data types of corresponding columns in each query **must be compatible or match**. The first query often dictates the expected data type for each position.
*   **Order of Columns:** The columns in each query **must be in the same order**. SQL maps columns positionally (first column of query 1 to first column of query 2, etc.), not by name.
*   **Column Aliases/Names:** The column names and aliases in the final output are **determined exclusively by the first query**. Names from subsequent queries are ignored. The first query also controls the data types of the output.
*   **Correct Information Mapping (User Responsibility):** Even if all SQL rules are met and no errors occur, the user is **solely responsible for ensuring that the *content* of the columns maps correctly**. SQL does not understand the meaning of the data; it only checks data types and order. Incorrect mapping can lead to inaccurate results (e.g., last names appearing in a first name column).

**Types of SQL Set Operators:**

1.  **UNION:**
    *   Returns **all distinct (unique) rows** from both queries.
    *   It removes duplicate rows from the combined result set.
    *   The order of queries generally doesn't affect the final result set, but the first query controls column naming.
    *   SQL processes it by taking columns from the first query, then adding distinct rows from both queries, carefully avoiding duplicates.

2.  **UNION ALL:**
    *   Returns **all rows from both queries, including all duplicates**.
    *   It is the **only set operator that does not remove duplicates**.
    *   **Performance:** Generally **faster than UNION** because it avoids the extra step of checking for and removing duplicates.
    *   **Use Cases:** Recommended when you know there are no duplicates in your data, or when you specifically want to see duplicates (e.g., for data quality checks).
    *   The order of queries does not affect the content of the result, but the first query dictates column naming.
    *   SQL simply appends all rows from the second query to all rows from the first query without any checks.

3.  **EXCEPT (also called MINUS in some databases):**
    *   Returns **distinct rows from the first query that are *not found* in the second query**.
    *   **Order of Queries Matters:** The order of the `SELECT` statements is **crucial** and directly affects the result. `Query1 EXCEPT Query2` will produce a different result than `Query2 EXCEPT Query1`.
    *   It removes duplicates from its result set.
    *   SQL uses the second query only as a lookup to check for exclusion; it does not add any rows from the second query to the output.

4.  **INTERSECT:**
    *   Returns **only the rows that are common to both queries**.
    *   Similar in concept to an `INNER JOIN` in terms of finding commonalities, but it operates on rows rather than combining columns.
    *   It removes duplicates from its result set.
    *   The **order of queries does not matter** for the final result.
    *   SQL identifies and returns only those rows that exist in both query results.

**Important Use Cases for Set Operators:**

*   **Combining Similar Tables for Data Analysis/Reporting:**
    *   Aggregating data from multiple similar tables (e.g., `employees`, `customers`, `suppliers`, `students` into a single `persons` table).
    *   Combining data from tables split for performance (e.g., `orders_2022`, `orders_2023` into a single `orders` table).
    *   This approach simplifies subsequent analytical queries, as you only need to query one combined table instead of multiple.

*   **Finding the Delta (New Data) between Data Batches (Data Engineering):**
    *   Using **EXCEPT** to identify new records generated in a source system that need to be loaded into a data warehouse or data lake (e.g., comparing current day's data with previous load).

*   **Data Completeness Checks (Data Migrations/Quality):**
    *   Using **EXCEPT** to verify if all records have successfully migrated from a source database to a target database.
    *   This involves performing two `EXCEPT` checks: `SourceTable EXCEPT TargetTable` (to find missing records in target) and `TargetTable EXCEPT SourceTable` (to find extra/unexpected records in target). An empty result from both indicates identical tables.

**Best Practices when Combining Data:**
*   **Explicitly list columns** instead of using `SELECT *`. This makes the query more robust to schema changes (e.g., column reordering, additions) in the underlying tables over time, preventing silent data mismatches.
*   Consider **adding a "Source Table" column** (a static string) to your combined result set to identify which original table each record came from. This can be very useful for analysis and auditing.

***

## SQL Course 12: SQL Functions Explained | In 5 Minutes
*   **What is an SQL Function?**
    *   An SQL function is a **built-in code block** that accepts an input value, processes it, and then returns a result (an output value).
    *   They are used to perform various operations on data within tables, such as data manipulation, aggregation, analysis, data cleansing, and data transformations, to solve specific SQL tasks.

*   **Categories of SQL Functions:**
    *   **Single-row functions**: These functions take a **single input value** and return a **single output value**. An example is the `LEFT` function, which extracts a specified number of characters from the left of a string. Subcategories include functions for string, numeric, date and time values, and handling NULLs.
    *   **Multi-row functions** (also known as Aggregate functions): These functions accept **multiple input values** (multiple rows) and return **one single aggregated output value**. An example is the `SUM` function, which calculates the sum of all input values. Subgroups include simple aggregate functions and advanced window/analytical functions.

*   **Nesting Functions:**
    *   You can **nest functions** by using multiple functions together, where the **output of one function becomes the input for another function**.
    *   This process is likened to a factory where material is processed at multiple stations, and the output of one station becomes the input for the next.
    *   When functions are nested, the **order of execution always starts from the innermost function** and proceeds outwards. For example, in `LENGTH(LOWER(LEFT('Maria', 2)))`, `LEFT` is executed first, then `LOWER`, and finally `LENGTH`.

*   **Roles in Data Professions:**
    *   **Single-row functions** are primarily used by **Data Engineers** to clean up, transform, and manipulate data, preparing it for analysis.
    *   **Multi-row functions** (especially aggregate functions) are mostly used by **Data Analysts** for almost every analysis task.

*   **Importance**: Understanding these functions is crucial because they allow you to perform extensive manipulations and analyses on your data.
***

## SQL Course 13: SQL String Functions | A Detailed Guide

SQL functions are **built-in code blocks** that take an input, process it, and return an output. They are used for various operations like data manipulation, aggregation, analysis, cleansing, and transformation. This lecture focuses specifically on **string functions** used to transform string values.

String functions are categorized based on their purpose:
1.  **Data Manipulation Functions**: Modify string values (e.g., concatenation, case conversion, cleaning spaces, replacing characters).
2.  **Calculation Functions**: Perform calculations on string values (e.g., counting characters).
3.  **Extraction Functions**: Extract parts of a string value (e.g., from the beginning, end, or a specific position).

#### 1. Data Manipulation Functions

*   **CONCAT (Concatenation)**
    *   **Purpose**: Combines **multiple string values into one value**. This is useful for merging information from different columns, such as a first name and last name into a full name, or a first name and country into a single display column.
    *   **Syntax**: `CONCAT(value1, value2, ...)`.
    *   **Example**: To combine `first_name` and `country` from a `customers` table into a new column called `name_country`:
        ```sql
        SELECT CONCAT(first_name, country) AS name_country FROM customers;
        ```
    *   **Adding Separators**: You can include spaces or other characters (e.g., dashes, underscores) as arguments to improve readability.
        ```sql
        SELECT CONCAT(first_name, ' ', country) AS name_country FROM customers;
        ```
        This creates a nice separation between the first name and country.

*   **UPPER and LOWER**
    *   **Purpose**:
        *   **UPPER**: Converts all characters of a string to **uppercase**.
        *   **LOWER**: Converts all characters of a string to **lowercase**.
    *   **Behavior**: If the string is already in the target case (e.g., applying `UPPER` to an already uppercase string), nothing changes in the output.
    *   **Example**: To convert the `first_name` column to lowercase:
        ```sql
        SELECT LOWER(first_name) AS low_name FROM customers;
        ```
    *   **Example**: To convert the `first_name` column to uppercase:
        ```sql
        SELECT UPPER(first_name) AS up_name FROM customers;
        ```

*   **TRIM**
    *   **Purpose**: Removes **leading and trailing spaces** (empty or white spaces) from a string value. It cleans up empty spaces at the beginning and end of a string.
    *   **Scenarios**: `TRIM` handles various cases: no spaces, only leading spaces, only trailing spaces, or both leading and trailing spaces. It can also remove multiple spaces at the start or end.
    *   **Data Cleansing**: Spaces are considered "evil" in data, and `TRIM` is essential for data cleansing.
    *   **Detecting Spaces**:
        *   **Method 1 (Comparing with `TRIM`ed value)**: Compare the original string with its `TRIM`med version. If they are not equal, it means there were spaces.
            ```sql
            SELECT first_name
            FROM customers
            WHERE first_name <> TRIM(first_name);
            ```
        *   **Method 2 (Comparing Lengths)**: Compare the length of the original string with the length of its `TRIM`med version. If the lengths are different, there were spaces.
            ```sql
            SELECT first_name,
                   LENGTH(first_name) AS length_original,
                   LENGTH(TRIM(first_name)) AS length_trimmed,
                   LENGTH(first_name) - LENGTH(TRIM(first_name)) AS flag
            FROM customers
            WHERE LENGTH(first_name) <> LENGTH(TRIM(first_name));
            ```
            A `flag` value greater than zero indicates the presence of white spaces.

*   **REPLACE**
    *   **Purpose**: Replaces a **specific "old" character or string with a "new" character or string** within a given value.
    *   **Syntax**: `REPLACE(value, old_value, new_value)`.
    *   **Use Cases**:
        *   **Replacing Characters**: E.g., changing dashes in a phone number to slashes.
            ```sql
            SELECT REPLACE('123-456-7890', '-', '/') AS formatted_phone;
            ```
        *   **Removing Characters**: By specifying an **empty string (`''`)** as the `new_value`, the `REPLACE` function effectively removes all occurrences of the `old_value`.
            ```sql
            SELECT REPLACE('123-456-7890', '-', '') AS clean_phone;
            ```
        *   **Changing File Extensions**: E.g., changing `.txt` to `.csv` in a file name.
            ```sql
            SELECT REPLACE('reports.txt', '.txt', '.csv') AS new_file_name;
            ```

#### 2. Calculation Functions

*   **LENGTH**
    *   **Purpose**: Counts the **number of characters** in a given value. It calculates the length of a value.
    *   **Behavior**: Works for strings, numbers (counts digits), and even date values (counts each character/digit, including separators). The output is always a number.
    *   **Example**: To calculate the length of each customer's first name:
        ```sql
        SELECT first_name, LENGTH(first_name) AS link_name FROM customers;
        ```

#### 3. Extraction Functions

*   **LEFT**
    *   **Purpose**: Extracts a **specific number of characters from the start (left side)** of a string value.
    *   **Syntax**: `LEFT(value, number_of_characters)`.
    *   **Example**: To retrieve the first two characters of each `first_name`:
        ```sql
        SELECT LEFT(first_name, 2) AS first_two_character FROM customers;
        ```
    *   **Combining with TRIM**: To handle leading spaces before extraction, you can nest `TRIM` inside `LEFT`:
        ```sql
        SELECT LEFT(TRIM(first_name), 2) AS first_two_character FROM customers;
        ```

*   **RIGHT**
    *   **Purpose**: Extracts a **specific number of characters from the end (right side)** of a string value.
    *   **Syntax**: `RIGHT(value, number_of_characters)`.
    *   **Example**: To retrieve the last two characters of each `first_name`:
        ```sql
        SELECT RIGHT(first_name, 2) AS last_two_character FROM customers;
        ```
    *   **Note**: If trailing spaces might be present, it's good practice to use `TRIM` before `RIGHT`.

*   **SUBSTRING**
    *   **Purpose**: Extracts a part of a string from a **specified starting position**. This is used when you need to extract characters from the "middle" of a string, not just the beginning or end.
    *   **Syntax**: `SUBSTRING(value, starting_position, length)`.
        *   `starting_position`: The character position where SQL should begin extracting (counting starts from 1).
        *   `length`: How many characters to extract from the `starting_position`.
    *   **Example**: To extract two characters after the second character from 'Maria' (i.e., 'ri'):
        *   'M' is position 1, 'a' is position 2. "After the second character" means starting from position 3 ('r').
        *   We want 2 characters: 'r' and 'i'.
        ```sql
        SELECT SUBSTRING('Maria', 3, 2); -- Returns 'ri'
        ```
    *   **Dynamic Length (Extracting "Everything After")**: If you want to extract all characters from a specified `starting_position` until the end of the string, you can use the `LENGTH` function for the `length` argument. This ensures you always extract enough characters, regardless of the string's actual length, without error.
        *   **Example**: To remove the first character of each `first_name` (i.e., extract everything from the second character onwards):
            ```sql
            SELECT SUBSTRING(first_name, 2, LENGTH(first_name)) AS subname FROM customers;
            ```
            *   `starting_position` is 2 (after the first character).
            *   `LENGTH(first_name)` ensures the `length` argument is dynamic and sufficient for any name.
    *   **Nesting Functions for Complex Tasks**: SQL allows **nesting multiple functions** together, where the output of one function becomes the input for another [Dựa trên ghi chú trước đó, không trực tiếp từ nguồn mới]. For example, `TRIM`, `LENGTH`, and `SUBSTRING` can be combined to clean leading/trailing spaces before extracting a substring with a dynamic length.
        ```sql
        SELECT SUBSTRING(TRIM(first_name), 2, LENGTH(TRIM(first_name))) AS subname FROM customers;
        ```
        The **order of execution** when nesting is always from the **innermost function outwards**

**Conclusion**: Understanding and utilizing these string functions provides powerful tools for manipulating and transforming string values in your data.
***

## SQL Course 14: SQL Number Functions | ROUND & ABS
This video introduces two simple but important SQL functions for transforming numeric values: **ROUND** and **ABS (Absolute)**.

### 1. **ROUND Function**
*   **Purpose**: To round numeric values to a specified number of decimal places or to the nearest integer.
*   **How it Works**:
    *   It takes a number and an optional argument for the number of decimal places you want to keep.
    *   **Rounding Rule**: SQL checks the digit immediately after the last desired decimal place.
        *   If this digit is **5 or higher**, the number is **rounded up**.
        *   If this digit is **less than 5**, the number is **not rounded up**; it stays as is.
    *   **Digits after the rounding point** will be reset to zero.
*   **Examples with `3.516`**:
    *   `ROUND(3.516, 2)`: Rounds to two decimal places. The third digit (6) is higher than 5, so 51 is rounded up to 52, resulting in **`3.52`**.
    *   `ROUND(3.516, 1)`: Rounds to one decimal place. The second digit (1) is less than 5, so 5 is not rounded up, resulting in **`3.5`**.
    *   `ROUND(3.516, 0)`: Rounds to zero decimal places (an integer). The first digit after the decimal (5) is 5, so the number 3 is rounded up to 4, resulting in **`4`**.
*   **Application**: Can be used with static values for practice or applied to data within a database.

### 2. **ABS (Absolute) Function**
*   **Purpose**: To convert any negative number into its positive equivalent. It returns the absolute value of a number.
*   **How it Works**:
    *   If you have a **negative number** (e.g., `-10`), `ABS(-10)` will return **`10`**.
    *   If the number is **already positive** (e.g., `10`), `ABS(10)` will return **`10`**; nothing changes.
*   **Practical Importance**:
    *   It's a "really nice and cool function" that is important for transforming numbers.
    *   Useful for **data correction**, especially when dealing with illogical negative values in a database, such as negative sales figures, which "make no sense". `ABS` can convert these negative figures to positive ones.
***







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


