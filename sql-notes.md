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

- [SQL Course 14: SQL Number Functions | ROUND & ABS](#sql-course-14-sql-number-functions--round--abs)

- [SQL Course 15: SQL Date & Time Functions | Datepart, Datename, Datetrunc, Eomonth](#sql-course-15-sql-date--time-functions--datepart-datename-datetrunc-eomonth)

- [SQL Course 16: SQL Date & Time Functions | Format, Convert, Cast](#sql-course-16-sql-date--time-functions--format-convert-cast)

- [SQL Course 17: SQL Date & Time Functions | Dateadd, Datediff, Isdate](#sql-course-17-sql-date--time-functions--dateadd-datediff-isdate)

- [SQL Course 18: SQL NULL Functions | COALESCE, ISNULL, NULLIF, IS (NOT) NULL](#sql-course-18-sql-null-functions--coalesce-isnull-nullif-is-not-null)

- [SQL Course 19: SQL NULL vs Empty String vs Blank Space Explained](#sql-course-19-sql-null-vs-empty-string-vs-blank-space-explained)

- [SQL Course 20: SQL Case When Statement | Use Cases](#sql-course-20-sql-case-when-statement--use-cases)

- [SQL Course 21: SQL Aggregate Functions | COUNT, SUM, AVG, MAX, MIN](#sql-course-21-sql-aggregate-functions--count-sum-avg-max-min)

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

## SQL Course 15: SQL Date & Time Functions | Datepart, Datename, Datetrunc, Eomonth

This lecture covers the fundamentals of date and time in SQL, explores 13 different date and time functions, and explains their syntax, functionality, and use cases.

**1. Understanding Date and Time in SQL**
*   **Date**: Represents a specific day, composed of:
    *   **Year**: Four-digit number (e.g., 2025).
    *   **Month**: Number between 1 and 12 (e.g., 8 for August).
    *   **Day**: Number between 1 and 31.
    *   Example: August 20th, 2025.
*   **Time**: Refers to a specific point within a day, composed of:
    *   **Hours**: Number between 0 and 23 (e.g., 18).
    *   **Minutes**: Number between 0 and 59 (e.g., 55).
    *   **Seconds**: Number between 0 and 59 (e.g., 45).
    *   Example: 18:55:45.
*   **Timestamp / Datetime**: Combines both date and time information.
    *   Often called `timestamp` in databases like Oracle, PostgreSQL, and MySQL, but `datetime` in SQL Server.
    *   Has a hierarchy from highest to lowest: **Year, Month, Day, Hour, Minute, Seconds**.
    *   Example: 2025-08-20 18:55:45 (including fractions of seconds like milliseconds).

**2. Sources of Date and Time Information in SQL Queries**
There are three main ways to get date information into your SQL queries:
1.  **Stored in the Database**: Dates and times are stored as columns in tables (e.g., `order date`, `shipping date` with `date` data type; `creation time` with `datetime` data type).
2.  **Hardcoded Date String**: You can define a static date directly in your query as a string (e.g., `'2025-08-20'`). This value is not stored in the database.
3.  **`GETDATE()` Function**: Returns the **current date and time** at the moment the query is executed. It takes no parameters.

**3. Categories of Date and Time Manipulation Functions**
SQL offers 13 different functions, grouped into four categories:
1.  **Part Extraction**: Extracting different components of a date (e.g., year, month, day).
2.  **Format and Casting**: Changing the display format or data type of dates.
3.  **Calculations**: Adding or subtracting time units, or finding differences between dates.
4.  **Validation**: Testing if a date is valid (e.g., using `ISDATE()`).

**4. Part Extraction Functions (The Biggest Category)**

*   **`DAY()`, `MONTH()`, `YEAR()`**
    *   **Purpose**: Simple functions to extract the day, month, or year part from a date.
    *   **Syntax**: Each function accepts **one parameter: the date** (e.g., `DAY(date_column)`, `MONTH(date_column)`, `YEAR(date_column)`).
    *   **Output Data Type**: **Integer**.
    *   **Example**:
        *   `YEAR('2025-08-20')` returns `2025`.
        *   `MONTH('2025-08-20')` returns `8`.
        *   `DAY('2025-08-20')` returns `20`.

*   **`DATEPART()`**
    *   **Purpose**: Returns a **specific part of the date as a number**, offering more options than `DAY()`, `MONTH()`, `YEAR()` (e.g., week, quarter, hour, minute, second, weekday).
    *   **Syntax**: Accepts **two parameters**:
        1.  **Part**: The specific date part you want to extract (e.g., `year`, `month`, `day`, `week`, `quarter`, `hour`, `minute`, `second`, `weekday`). Abbreviations (e.g., `yy` for year, `mm` for month) can also be used but full names are recommended for clarity and standardization.
        2.  **Date**: The date value from which to extract the part.
        *   Example: `DATEPART(month, order_date)`.
    *   **Output Data Type**: **Integer**.
    *   **Key Insight**: `DATEPART()` can extract parts not directly visible in a date field, like the quarter or week number. It can extract the same parts as `YEAR()`, `MONTH()`, `DAY()` (e.g., `DATEPART(year, creation_time)` is identical to `YEAR(creation_time)`) but also provides other parts like `hour`, `minute`, `second`, `quarter`, `weekday`, `week`.

*   **`DATENAME()`**
    *   **Purpose**: Very similar to `DATEPART()`, but it **returns the *name* of the date part**.
    *   **Syntax**: Identical to `DATEPART()`: **two parameters** (part, date).
    *   **Output Data Type**: **String**.
    *   **Key Differences & Insights**:
        *   For `month` and `weekday` parts, it returns the full name (e.g., `August` instead of `8`, `Wednesday` instead of `20` or a number).
        *   For parts like `day` or `year`, it still returns numbers, but the **data type of the output is a string**, not an integer.
        *   **Core Use Case**: **To present easy-to-read, human-readable information to users in reports** (e.g., showing `January` instead of `1` for sales by month).

*   **Decision Process for Part Extraction Functions**
    *   **Do I need `day` or `month`?**
        *   If **YES, as an integer (number)**, use `DAY()` or `MONTH()` (they are quick).
        *   If **YES, as the full name (string)**, use `DATENAME()`.
    *   **Do I need `year`?**
        *   Always use `YEAR()` directly (no 'year name' concept).
    *   **Do I need other parts (e.g., `week`, `quarter`, `hour`, `minute`, `second`, `weekday`)?**
        *   Use `DATEPART()` if you need the **number**.
        *   Use `DATENAME()` if you need the **name** (especially for `weekday`).

**5. `DATETRUNC()` (Date Truncation)**
*   **Purpose**: **Truncates a date or datetime to a specific level of detail** by resetting all lower-hierarchy components to their minimum values (e.g., minutes/seconds to `00`, day to `01`). It doesn't extract a part, but rather changes the precision of the date/time.
*   **Syntax**: Identical to `DATEPART()` and `DATENAME()`: **two parameters** (part, date).
*   **Output Data Type**: Always a **`date` or `datetime`** (or `datetime2`).
*   **How it Works (Hierarchy Resets)**:
    *   `DATETRUNC(minute, datetime_value)`: Keeps year, month, day, hour, minute; resets seconds to `00`.
    *   `DATETRUNC(hour, datetime_value)`: Keeps year, month, day, hour; resets minutes and seconds to `00`.
    *   `DATETRUNC(day, datetime_value)`: Keeps year, month, day; resets all time components (hour, minute, second) to `00:00:00`.
    *   `DATETRUNC(month, datetime_value)`: Keeps year, month; resets day to `01` and all time components to `00:00:00`.
    *   `DATETRUNC(year, datetime_value)`: Keeps year; resets month to `01`, day to `01`, and all time components to `00:00:00`.
*   **Key Insight: Amazing for Data Analytics**
    *   Allows **quick aggregation of data at different granularities** (e.g., aggregating orders by month or year instead of by second).
    *   Helps in "zooming in and zooming out" on data for analysis.

**6. `EOMONTH()` (End of Month)**
*   **Purpose**: Returns the **last day of the month** for a given date.
*   **Syntax**: Accepts **one parameter: the date** (e.g., `EOMONTH(date_value)`).
*   **Output Data Type**: **Date**.
*   **Example**: `EOMONTH('2025-08-20')` returns `2025-08-31`. If the date is already the last day of the month, it returns the same date.

**7. Getting the First Day of the Month**
*   There's no dedicated `SOMONTH()` function.
*   **Trick**: Use `DATETRUNC()` to truncate the date to the `month` level, which automatically resets the day to `01` and time to `00:00:00`.
*   **To get a `date` data type (without time)**, `CAST` the result of `DATETRUNC()` to `DATE`.
    *   Example: `CAST(DATETRUNC(month, creation_time) AS DATE)`.

**8. Use Cases for Extracting Date Parts**

*   **Data Aggregations and Reporting**
    *   Allows aggregating data based on specific time units (e.g., sales by year, quarter, or month).
    *   Example: `SELECT YEAR(order_date), COUNT(*) AS number_of_orders FROM sales_orders GROUP BY YEAR(order_date)`.
    *   For human-readable reports (e.g., showing month names), use `DATENAME()` in `SELECT` and `GROUP BY` clauses.

*   **Filtering Data**
    *   Used in `WHERE` clauses to filter data based on specific parts of a date (e.g., `WHERE MONTH(order_date) = 2` to find orders placed in February).
    *   **Recommendation**: When filtering, **always use functions that return numbers** (like `DAY()`, `MONTH()`, `YEAR()`, `DATEPART()`) instead of `DATENAME()`. Searching and filtering with integers is generally **faster** than with strings.

**9. Data Type Recap of Function Results**
Understanding the output data type is crucial to avoid unexpected results:
*   `DAY()`, `MONTH()`, `YEAR()`, `DATEPART()`: **Integer**.
*   `DATENAME()`: **String**.
*   `DATETRUNC()`: **`datetime2`** (or `datetime` in some contexts, meaning both date and time information).
*   `EOMONTH()`: **Date**.
***

## SQL Course 16: SQL Date & Time Functions | Format, Convert, Cast

This lecture delves into manipulating dates and times in SQL, specifically focusing on the concepts of **formatting** and **casting**, along with the key functions used for these operations: `FORMAT()`, `CONVERT()`, and `CAST()`.

### 1. Understanding Date Format

*   **Definition**: A date format is a combination of numbers and characters that represent date and time information. For instance, `2025-08-20 18:55:45` combines numbers like `2025`, `08`, `20` with characters like `-` and `:`.
*   **Format Specifiers**: These are characters that represent specific date/time components and are **case-sensitive**.
    *   **Year**: `yyyy` (e.g., `2025`).
    *   **Month**: `MM` (two digits, e.g., `08`); `MMM` (abbreviated name, e.g., `Aug`); `MMMM` (full name, e.g., `August`). Note: `MM` is for month, while `mm` is for minutes.
    *   **Day**: `dd` (two digits, e.g., `20`); `ddd` (abbreviated day of week); `dddd` (full day of week).
    *   **Hour**: `HH` (24-hour system); `hh` (12-hour system, used with `AM/PM`).
    *   **Minute**: `mm` (two digits).
    *   **Second**: `ss` (two digits).
    *   **AM/PM**: `tt`.
*   **Different Formatting Standards**:
    *   **International Standard (ISO 6801)**: `yyyy-MM-dd` (e.g., `2025-08-20`). **SQL Server adheres to this format** for all dates within the database.
    *   **USA Standard**: `MM-dd-yyyy` (e.g., `08-20-2025`).
    *   **European Standard**: `dd-MM-yyyy` (e.g., `20-08-2025`).

### 2. Formatting vs. Casting

*   **Formatting**:
    *   **Purpose**: To **change the display** of a value from one format to another **without altering its underlying data type**.
    *   Example: Changing `2025-08-20` to `08/20/25`.
*   **Casting**:
    *   **Purpose**: To **change the data type** of a value from one type to another.
    *   Example: Converting the string `"123"` to an integer `123`, or a `DATE` value to a `STRING`.

### 3. The `FORMAT()` Function

*   **Purpose**: To **format** date, time, or number values, changing their appearance.
*   **Syntax**: `FORMAT(value, format, [culture])`.
    *   **`value`**: The date, time, or number to be formatted.
    *   **`format`**: The desired new format, using format specifiers (e.g., `'dd/MM/yyyy'`).
    *   **`culture` (optional)**: A culture code specifying the style of a country or region (e.g., `'en-US'`, `'ja-JP'`). If not specified, SQL uses the default culture `en-US`. This option is less commonly used in real projects.
*   **Output Data Type**: Always a **string (`VARCHAR`)**.
*   **Formatting Examples**:
    *   `FORMAT(order_date, 'dd/MM/yyyy')`.
    *   Creating USA (`MM-dd-yyyy`) or European (`dd-MM-yyyy`) standard formats.
    *   Constructing complex custom formats by combining static text and date parts, such as "Day [Abbreviated Day Name] [Abbreviated Month Name] [Quarter] [Year] [Time AM/PM]".
*   **Use Cases**:
    *   **Data Aggregation and Reporting**: Formatting dates for reports at various levels of detail (e.g., sales by month showing abbreviated month names and two-digit years). It allows for more display customization than `DATEPART()`.
    *   **Data Preparation and Cleaning**: Converting different date formats from multiple sources into one standard format for analysis.
*   **Limitation**: Cannot be used to change the data type.

### 4. The `CONVERT()` Function

*   **Purpose**: To convert a value to a different data type and, **simultaneously, it can format** the value using `style numbers`.
*   **Syntax**: `CONVERT(target_data_type, value, [style_number])`.
    *   **`target_data_type`**: The desired data type (e.g., `INT`, `VARCHAR`, `DATE`).
    *   **`value`**: The value to be converted.
    *   **`style_number` (optional)**: A numeric code to format the output. If not specified, the default value `0` is used.
*   **Output Data Type**: Determined by the `target_data_type`.
*   **Use Cases**:
    *   **Pure Casting**:
        *   String to Integer: `CONVERT(INT, '123')`.
        *   String to Date: `CONVERT(DATE, '2025-08-20')`.
        *   Datetime to Date (loses time information): `CONVERT(DATE, creation_time)`.
    *   **Casting AND Formatting**:
        *   Converting `DATETIME` to `VARCHAR` with a specific format style (e.g., USA standard style `32`, European standard style `34`).
*   **Capabilities**: Can convert any data type to any other type. Can format date/time values when converting to a string type.
*   **Limitation**: Cannot format numbers.

### 5. The `CAST()` Function

*   **Purpose**: To convert a value to a different data type. This function is **solely for casting and has no formatting capabilities**.
*   **Syntax**: `CAST(value AS target_data_type)`.
    *   **`value`**: The value to be converted.
    *   **`AS`**: The keyword separating the value and the target data type.
    *   **`target_data_type`**: The desired data type (e.g., `INT`, `VARCHAR`, `DATE`).
*   **Output Data Type**: Determined by the `target_data_type`.
*   **Use Cases**:
    *   String to Integer: `CAST('123' AS INT)`.
    *   Integer to String: `CAST(123 AS VARCHAR)`.
    *   String to Date: `CAST('2025-08-20' AS DATE)`.
    *   Datetime to Date (removes time information): `CAST(creation_time AS DATE)`.
*   **Capabilities**: Can convert any data type to any other type.
*   **Limitation**: **Cannot be used for formatting or styling**. When casting with `CAST()`, the output will always be in SQL's standard format for the target data type.

### 6. Comparison of `CAST()`, `CONVERT()`, and `FORMAT()`

The table below summarizes the key differences between the three functions:

| Feature           | `CAST()`                                 | `CONVERT()`                              | `FORMAT()`                                        |
| :---------------- | :--------------------------------------- | :--------------------------------------- | :------------------------------------------------ |
| **Data Type Casting** | Yes (any type to any other type)    | Yes (any type to any other type)    | Converts only to **string** (as its main purpose is formatting) |
| **Formatting/Styling** | **No**                              | Yes (date/time formatting using style numbers) | Yes (date/time **and number** formatting using format specifiers) |

Understanding the distinctions between these functions is crucial for selecting the appropriate tool for your data manipulation needs in SQL.
***

## SQL Course 17: SQL Date & Time Functions | Dateadd, Datediff, Isdate

This video covers three essential SQL date and time functions: `DATEADD`, `DATEDIFF`, and `ISDATE`, demonstrating their use cases for data manipulation, calculations, and validation.

### 1. `DATEADD` Function

*   **Purpose**: Allows you to **add or subtract a specific time interval to or from a date**. Despite its name, it can also subtract.
*   **Syntax**: `DATEADD(part, interval, date)`.
    *   **`part`**: Specifies the part of the date you want to manipulate, such as `year`, `month`, or `day`.
    *   **`interval`**: An integer representing the number of units to add or subtract. A positive value adds, while a negative value subtracts.
    *   **`date`**: The original date value that will be manipulated.
*   **Examples/Use Cases**:
    *   **Adding years**: To add 3 years to '2025 August 20th', the output would be '2028 August 20th'.
    *   **Subtracting months**: To subtract 2 months from '2025 August 20th', the output would be '2025 June 20th'.
    *   **Adding days**: To add 5 days to '2025 August 20th', the output would be '2025 August 25th'.
    *   **Manipulating a field**: You can use `DATEADD(year, 2, OrderDate)` to add two years to each `OrderDate` in a table, or `DATEADD(day, -10, OrderDate)` to subtract 10 days.

### 2. `DATEDIFF` Function

*   **Purpose**: `DATEDIFF` (Difference) is used to **find the difference between two dates**. It returns a number representing the specified time interval between the two dates.
*   **Syntax**: `DATEDIFF(part, start_date, end_date)`.
    *   **`part`**: The unit of difference you want to find, such as `year`, `month`, or `day`.
    *   **`start_date`**: The earlier or youngest date.
    *   **`end_date`**: The later or oldest date.
*   **Examples/Use Cases**:
    *   **Finding difference between two specific dates**: If `OrderDate` is '2025 August 20th' and `ShippingDate` is '2026 February 1st', `DATEDIFF(year, OrderDate, ShippingDate)` returns 1 year, `DATEDIFF(month, OrderDate, ShippingDate)` returns 6 months (Note: The source example states 3 months which seems like an error based on the dates provided).
    *   **Calculating Age**: Use `DATEDIFF(year, BirthDate, GETDATE())` to find the age of employees by calculating the years between their birth date and the current date (`GETDATE()`).
    *   **Calculating Shipping Duration**: Find the number of days between `OrderDate` and `ShipDate` using `DATEDIFF(day, OrderDate, ShipDate)`.
    *   **Finding Average Shipping Duration per Month**: You can combine `DATEDIFF` with `AVG()` and `GROUP BY` the month of the `OrderDate` to find the average shipping duration for each month. This is a simple aggregation task.
    *   **Time Gap Analysis (e.g., Days Between Orders)**: To find the number of days between each order and the *previous* order, you can use `DATEDIFF(day, LAG(OrderDate) OVER (ORDER BY OrderDate), OrderDate)`. The `LAG` window function retrieves the `OrderDate` from the previous record. This type of analysis is crucial for business insights.

### 3. `ISDATE` Function

*   **Purpose**: `ISDATE` is a validation function that **checks whether a given value is a valid date**.
*   **Returns**: It returns `1` (true) if the value is a valid date string or number, and `0` (false) if it is not.
*   **Syntax**: `ISDATE(value)`. It accepts string values and can also accept numbers (like a year, e.g., '2025', which it considers valid).
*   **Examples/Use Cases**:
    *   `ISDATE('123')` returns `0`.
    *   `ISDATE('2025 August 20')` returns `1`.
    *   `ISDATE('20-08-2025')` might return `0` if the format does not follow the standard database format.
    *   `ISDATE('2025')` returns `1` (SQL considers this a valid year, possibly defaulting to January 1st of that year).
    *   `ISDATE('August')` returns `0`.
    *   **Data Quality and Error Handling**: `ISDATE` is particularly useful for preparing data before analysis, especially when dealing with data quality issues (e.g., corrupt string values that are supposed to be dates).
        *   **Preventing Errors During Casting**: If you try to directly `CAST` a string column with invalid date values to a `DATE` data type, SQL will throw an error.
        *   **Conditional Casting with `CASE WHEN`**: You can use `ISDATE` within a `CASE WHEN` statement to cast values to `DATE` only if they pass the `ISDATE` check (i.e., `ISDATE(OrderDate) = 1`). For values that fail the check, you can set them to `NULL` or a dummy value, preventing casting errors and allowing you to identify problematic data.
        *   **Identifying Data Quality Issues**: By filtering for records where `ISDATE(column_name) = 0`, you can easily identify all invalid date entries in a large table, which is crucial for data cleanup.

These date functions are powerful tools for performing analytical tasks and reporting in SQL.
***

## SQL Course 18: SQL NULL Functions | COALESCE, ISNULL, NULLIF, IS (NOT) NULL

#### 1. Understanding Nulls
*   **Definition**: In SQL databases, a **NULL** means nothing, unknown, or a missing value.
*   **Characteristics**:
    *   It is **not equal to zero**, an empty string, or a blank space.
    *   It simply tells us there is no value.
    *   It's like saying "I don't know what this value is".
*   **Scenario**: When filling out a form, optional fields left unanswered will be stored as NULLs in database tables.

#### 2. Overview of Null Functions
SQL provides special functions to handle NULLs in data. These functions primarily fall into categories:
*   **Replacing NULLs with values**: `ISNULL`, `COALESCE`.
*   **Replacing values with NULLs**: `NULLIF`.
*   **Checking for NULLs**: `IS NULL`, `IS NOT NULL`.

#### 3. Detailed Functions and Use Cases

##### A. ISNULL
*   **Purpose**: Replaces a NULL value with a specified replacement value.
*   **Syntax**: `ISNULL(value, replacement_value)`.
    *   `value`: The column or expression to check for NULLs.
    *   `replacement_value`: The value to use if `value` is NULL. This can be a **static value** (e.g., 'Unknown', 'N/A') or **another column**.
*   **How it Works**:
    *   If the `value` is **not NULL**, `ISNULL` returns the `value` itself.
    *   If the `value` **is NULL**, `ISNULL` returns the `replacement_value`.
*   **Important Considerations**:
    *   **Static Replacement**: If a static value is used as a replacement, the output will never contain a NULL.
    *   **Column Replacement**: If another column is used as a replacement, the output might still contain NULLs if the replacement column itself contains NULLs.
*   **Limitation**: `ISNULL` is limited to **two arguments**.

##### B. COALESCE
*   **Purpose**: Returns the **first non-NULL value** from a list of values.
*   **Syntax**: `COALESCE(value1, value2, value3, ...)`.
    *   It accepts a list of multiple values.
*   **How it Works**:
    *   It checks values from **left to right**.
    *   It stops immediately and returns the first non-NULL value it encounters.
*   **Advantages over ISNULL**:
    *   **Multiple Values**: Can handle a list of many values, unlike `ISNULL` which is limited to two. This allows for more sophisticated fallback logic (e.g., check `shipping_address`, then `billing_address`, then a default 'Unknown').
    *   **Database Standard**: `COALESCE` is available in **all different databases**, making it more portable and standard compared to `ISNULL` which has different keywords across databases (e.g., `NVL` in Oracle, `IFNULL` in MySQL).
*   **Disadvantage**: `ISNULL` is **faster** than `COALESCE`.
*   **Advice**: Generally **prefer `COALESCE`** for its standardization and flexibility, unless performance is a critical issue that necessitates `ISNULL`.

##### C. NULLIF
*   **Purpose**: Compares two values and **returns NULL if they are equal**, otherwise returns the first value.
*   **Syntax**: `NULLIF(value1, value2)`.
    *   Accepts **only two values** (a column and a static value, or two columns).
*   **How it Works**:
    *   If `value1` **equals** `value2`, `NULLIF` returns `NULL`.
    *   If `value1` **does not equal** `value2`, `NULLIF` returns `value1`.
    *   The `value2` is always used only for checking; it is never returned as an output.
*   **Use Cases**:
    *   **Replacing specific values with NULL**: For example, replacing a negative price (-1) with NULL because it indicates a data quality issue.
    *   **Highlighting/Flagging special cases**: Using NULL as a flag when two values (e.g., original price and discount price) are unexpectedly equal.
    *   **Preventing divide-by-zero errors**: By replacing a divisor of zero with NULL, any division by this NULL will result in NULL instead of an error.

##### D. IS NULL and IS NOT NULL
*   **Purpose**: Checks whether a value is NULL or not NULL, returning a **Boolean (TRUE or FALSE)** result.
*   **Syntax**:
    *   `value IS NULL`.
    *   `value IS NOT NULL`.
*   **How it Works**:
    *   `value IS NULL`: Returns `TRUE` if `value` is NULL, `FALSE` otherwise.
    *   `value IS NOT NULL`: Returns `TRUE` if `value` is not NULL, `FALSE` otherwise.
    *   These functions never return the value itself or a NULL; they always return a Boolean flag.
*   **Use Cases**:
    *   **Searching for missing information**: Identifying records where a specific column (e.g., score) is NULL.
    *   **Searching for existing information**: Identifying records where a specific column (e.g., score) is not NULL.
    *   **Implementing Advanced Join Types**: Used in combination with `LEFT JOIN` or `RIGHT JOIN` to find unmatching rows (anti-joins).

#### 4. Critical Use Cases for Handling Nulls (using ISNULL or COALESCE primarily)

##### A. Handling Nulls Before Data Aggregations
*   **Problem**: Aggregate functions (e.g., `AVG`, `SUM`, `MIN`, `MAX`) **ignore NULL values** in their calculations. `COUNT(*)` is an exception, as it counts all rows regardless of NULLs.
*   **Impact**: If a business understands NULL as zero (e.g., missing sales count as zero sales), ignoring NULLs in aggregations leads to **inaccurate results**.
*   **Solution**: **Replace NULLs with zero** (or another appropriate value) using `ISNULL` or `COALESCE` *before* performing aggregations.
    *   Example: `AVG(COALESCE(score, 0))` will include NULL scores as zeros in the average calculation, providing a more accurate result if that's the business's interpretation.

##### B. Handling Nulls Before Mathematical Operations
*   **Problem**: Any mathematical operation (e.g., `+`, `-`) involving a **NULL will result in NULL**. This also applies to string concatenation (e.g., `NULL + 'B'` results in `NULL`).
*   **Impact**: Leads to **unexpected or incomplete results** in calculations or concatenated fields.
*   **Solution**: **Handle NULLs** by replacing them with an appropriate value (e.g., zero for numbers, an empty string for text) *before* performing operations.
    *   Example: `first_name + ' ' + COALESCE(last_name, '')` ensures the full name is displayed even if the last name is missing.
    *   Example: `COALESCE(score, 0) + 10` ensures bonus points are added even if the initial score is NULL.

##### C. Handling Nulls Before Joins
*   **Problem**: SQL's `EQUAL` operator (`=`) **cannot compare NULLs**. If join keys contain NULLs, those rows will **not match** and will be **missing** from the join result, leading to incomplete data.
*   **Impact**: **Loss of records** and inaccurate analysis.
*   **Solution**: **Handle NULLs within the join keys** by replacing them with a consistent, non-NULL default value (e.g., an empty string, a blank space, or any static value) using `ISNULL` or `COALESCE` in the `ON` clause of the join.
    *   Example: `ON ISNULL(Table1.Key, '') = ISNULL(Table2.Key, '')`.
    *   Note: Handling NULLs in the join clause does *not* change the original values displayed in the `SELECT` list; it only affects how rows are matched.

##### D. Handling Nulls Before Sorting Data
*   **Problem**: When sorting data, SQL places NULLs consistently:
    *   **Ascending order**: NULLs appear **at the beginning** of the list.
    *   **Descending order**: NULLs appear **at the end** of the list.
    *   This is not because NULL is the lowest or highest value, but how SQL handles them.
*   **Impact**: May not align with desired sorting logic, especially if NULLs are expected to appear last in ascending order.
*   **Solutions**:
    *   **"Lazy Way"**: Replace NULLs with a very large number (for ascending sort where NULLs should be last) or a very small number (for descending sort where NULLs should be first) using `COALESCE`. This is less professional as the static value might conflict with actual data values later.
    *   **"Professional Way" (using `CASE WHEN`)**: Create a flag (e.g., 0 for non-NULL, 1 for NULL) and sort by this flag first, then by the original column. This pushes NULLs to the desired position without using arbitrary static values.
        *   Example for NULLs appearing last in ascending order: `ORDER BY CASE WHEN score IS NULL THEN 1 ELSE 0 END ASC, score ASC`.

#### 5. Advanced Join Types (using IS NULL)
While SQL has standard `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, and `FULL JOIN`, two advanced types can be implemented using `IS NULL`:

##### A. Left Anti Join
*   **Purpose**: Returns all rows from the **left table that do NOT have a matching row** in the right table.
*   **Implementation**: Combine a `LEFT JOIN` with a `WHERE` clause that checks if the **right table's join key is NULL**.
    *   Example: `SELECT C.* FROM Customers C LEFT JOIN Orders O ON C.CustomerID = O.CustomerID WHERE O.CustomerID IS NULL`. This returns customers who have not placed any orders.

##### B. Right Anti Join
*   **Purpose**: Returns all rows from the **right table that do NOT have a matching row** in the left table.
*   **Implementation**: Combine a `RIGHT JOIN` with a `WHERE` clause that checks if the **left table's join key is NULL**.
***

## SQL Course 19: SQL NULL vs Empty String vs Blank Space Explained

A comprehensive explanation of the critical distinctions between **NULLs, empty strings, and blank spaces** in SQL, highlighting their meanings, practical implications, and strategies for managing them to ensure data quality.

### 1. Key Concepts and Distinctions

The three concepts often cause confusion for developers and data professionals:

*   **NULL**:
    *   **Meaning**: Represents an **unknown value** or "no value". It is a special marker in SQL.
    *   **Data Type**: It does **not have a data type**.
    *   **Storage & Performance**: NULLs are the **most efficient** in terms of storage consumption and query performance.
    *   **Representation in Table**: Appears as "null".
    *   **Comparison**: Not equal to zero, empty strings, or any blank spaces. To search for NULLs, you must use `IS NULL`.
    *   **Detection**: The `DATALENGTH` function will return `NULL` for a NULL value, as its length is unknown.

*   **Empty String ('')**:
    *   **Meaning**: Represents a **known value that is nothing**; it is an empty value.
    *   **Data Type**: It is a **string** data type.
    *   **Size**: Has a **size of zero** characters.
    *   **Storage & Performance**: Occupies storage and memory, and while fast, it's not as fast as NULLs.
    *   **Representation in Table**: Appears as two quotes with nothing between them (`''`).
    *   **Comparison**: To search for empty strings, you use the `=` operator.
    *   **Detection**: The `DATALENGTH` function will return **0** for an empty string.

*   **Blank Space (' ')**:
    *   **Meaning**: Represents a **known value where spaces are the actual value**. It's often "evil" in databases as users might accidentally enter it.
    *   **Data Type**: It is a **string** data type.
    *   **Size**: Has a size of **one or more characters** (depending on how many spaces are entered).
    *   **Storage & Performance**: Occupies storage and memory, and is the **worst option for performance**.
    *   **Representation in Table**: Appears as two quotes with one or many spaces between them (`' '`).
    *   **Comparison**: To search for blank spaces, you use the `=` operator.
    *   **Detection**: The `DATALENGTH` function will return a value **greater than 0** (e.g., 1 for one space, 2 for two spaces).

**It's crucial not to rely solely on visual inspection** when dealing with empty strings and blank spaces as they can look identical in query results; always use the `DATALENGTH` function for precise detection.

### 2. Importance of Data Quality and Preparation

Understanding these distinctions is vital because encountering all three scenarios (NULLs, empty strings, blank spaces) is common in real-world data, especially with "bad data quality" from various sources. Failing to clean up and standardize this data before analysis leads to **inaccurate reports and analyses, resulting in wrong decisions**. Data preparation, including handling these three scenarios and bringing standards to your data, is a very important step before any analysis.

### 3. Data Cleaning and Standardization Policies

The document outlines three main data policy options for standardizing data:

*   **Policy 1: Only use NULLs and Empty Strings (Avoid Blank Spaces)**.
    *   **Goal**: Eliminate all blank spaces.
    *   **Implementation**: Use the **`TRIM` function** in SQL. `TRIM` removes leading and trailing spaces from a string, effectively converting blank spaces into empty strings.
    *   **Recommendation**: The source suggests avoiding this policy because it can still lead to confusion due to the presence of empty strings.

*   **Policy 2: Only use NULLs (Avoid Both Empty Strings and Blank Spaces)**.
    *   **Goal**: Convert all empty strings and blank spaces into NULLs.
    *   **Implementation Steps**:
        1.  **First, `TRIM`** any blank spaces to convert them into empty strings (like in Policy 1).
        2.  **Then, use the `NULLIF` function** to convert these empty strings into NULLs.
    *   **Recommendation**: This policy is highly recommended for **data preparation before inserting data into a database** (e.g., during ETL processes) because it optimizes storage and improves query performance.

*   **Policy 3: Use a Default Value (e.g., 'Unknown') (Avoid NULLs, Empty Strings, and Blank Spaces)**.
    *   **Goal**: Replace all instances of NULLs, empty strings, and blank spaces with a single, predefined default value (e.g., 'Unknown').
    *   **Implementation Steps**:
        1.  **First, `TRIM`** any blank spaces.
        2.  **Second, use `NULLIF`** to convert empty strings to NULLs.
        3.  **Finally, use `ISNULL` or `COALESCE`** functions to replace all resulting NULLs with the chosen default value.
    *   **Recommendation**: This policy is recommended for **data preparation immediately before presenting data to users in reports** (e.g., in Tableau or Power BI). Displaying a word like "Unknown" is easier for users to understand than a blank NULL value in a report, even though storing actual text like 'Unknown' takes more space and impacts performance if stored directly in the database.

### 4. General NULL Handling in SQL

NULLs are special and require specific handling in SQL:

*   **Functions for NULLs**:
    *   **`COALESCE` or `ISNULL`**: To replace a `NULL` with a specified value.
    *   **`NULLIF`**: To replace a value with `NULL`.
    *   **`IS NULL` or `IS NOT NULL`**: To check for the presence or absence of `NULL` values.
*   **Special Considerations**: NULLs must be handled before performing:
    *   **Data aggregations** (e.g., `AVERAGE`, `SUM`, `MAX`, `MIN`).
    *   **Mathematical operations** (e.g., using the `+` operator for string concatenation).
    *   **Joins**: Including introducing new types like Left Anti-Join and Right Anti-Join that exclude matching rows using `IS NULL`.
    *   **Sorting** data.

In essence, data management in SQL is like managing a pantry. A **NULL** is like an empty jar with no label—you don't know what was supposed to be in it, or if anything ever was. An **empty string** is an empty jar that's clearly labeled as "empty"—you know it's meant to hold nothing. A **blank space** is a jar labeled "empty" but secretly has a tiny speck of dust inside—it looks empty but isn't truly, and can cause unexpected issues if not properly cleaned out. Just as you'd want to organize your pantry to easily see what you have and what's truly missing, understanding and standardizing these 'empty' data states in SQL is crucial for accurate data analysis and decision-making.

## SQL Course 20: SQL Case When Statement | Use Cases

The `CASE` statement in SQL allows you to build **conditional logic** within your queries. It evaluates a list of conditions one by one and returns a value when the first condition is met.

#### 1. Core Syntax and Execution
*   **Keywords**: A `CASE` statement begins with the `CASE` keyword and ends with `END`.
*   **Conditions**: Inside, conditions are defined using `WHEN` followed by the condition, and `THEN` followed by the result if that condition is true.
    *   Example: `WHEN condition THEN result`.
*   **Default Value**: `ELSE` introduces a default value that is returned if **none of the preceding `WHEN` conditions are met**.
    *   `ELSE` is **optional**. If omitted and no conditions are met, the output will be `NULL`.
*   **Order of Evaluation**: SQL processes conditions **from top to bottom**.
    *   **Crucially, once a condition is found to be true, SQL stops evaluating any further conditions** and returns the corresponding `THEN` value. This means the order of your conditions is very important.

#### 2. Key Rules
*   **Data Type Matching**: The data types of all results (values after `THEN` and `ELSE`) **must match**. If they don't, SQL will throw an error.
*   **Location**: `CASE` statements can be used **everywhere** in SQL queries, including `SELECT`, `JOIN`, `FROM`, `WHERE`, `GROUP BY`, and `ORDER BY` clauses.

#### 3. Main Purpose and Use Cases

The main purpose of the `CASE` statement is **data transformations**, especially for **generating new columns** and deriving new information from existing data without modifying the source database for analytical purposes.

Here are the most useful use cases:

*   **Categorizing Data**:
    *   **Purpose**: To group data into different categories based on specific conditions. This makes data easier to understand, track, and aggregate for analysis and reporting.
    *   **Example**: Classifying sales as "high" (sales > 50), "medium" (sales between 20 and 50), or "low" (sales ≤ 20).
    *   This often involves creating a new category column and then aggregating data by these new categories.

*   **Mapping Values**:
    *   **Purpose**: To transform data from one form to another, making it more readable and usable for analytics. This is common when database values are stored as codes or flags (e.g., 0/1 for inactive/active) for performance optimization.
    *   **Example**: Changing 'F' and 'M' in a gender column to 'Female' and 'Male'.
    *   **Two Syntax Forms**:
        *   **Full Form**: `CASE WHEN condition THEN result`. This is more flexible for complex logic and multiple columns/operators.
        *   **Quick Form**: `CASE column_name WHEN value THEN result`. This form is **only applicable for evaluating a single column with an equality (`=`) operator**. It's shorter for simple mappings but less flexible. It is recommended to use the **full form** for better adaptability to future logic changes.

*   **Handling Nulls**:
    *   **Purpose**: To replace `NULL` values with a specific value to ensure more accurate calculations and avoid incorrect results in aggregations.
    *   **Syntax**: `WHEN column_name IS NULL THEN replacement_value ELSE column_name`.
    *   **Example**: Treating `NULL` scores as 0 when calculating an average score.

*   **Conditional Aggregations**:
    *   **Purpose**: To apply an aggregate function (e.g., `SUM`, `AVG`, `COUNT`) only on a **subset of data that meets specific conditions**. This is powerful for deep-dive or targeted analyses.
    *   **Method**: Create a "flag" column using `CASE` (e.g., 1 if condition is true, 0 otherwise), then aggregate (e.g., `SUM` or `COUNT`) this flag column.
    *   **Example**: Counting how many times each customer made an order with sales greater than 30.

In essence, the `CASE` statement in SQL acts like a **smart traffic controller** for your data. It directs each piece of information down a specific path based on certain rules you define, ensuring that it arrives at the correct destination (a transformed value or category) or is counted/aggregated only when appropriate, much like a post office sorts mail into different bins based on their destination addresses.
***

## SQL Course 21: SQL Aggregate Functions | COUNT, SUM, AVG, MAX, MIN

This video introduces **aggregate functions in SQL**. These functions are highlighted as being "amazing" and "really useful for insights" for data analysts or data scientists because they help **uncover insights about data**.

**Key Characteristics of Aggregate Functions:**
*   **Input:** They accept **multiple rows or multiple values** as input.
*   **Output:** They always return **one single, aggregated value**.

The video covers the following basic aggregate functions in SQL:

1.  **`COUNT()`**
    *   **Purpose:** To **count the number of rows** in a table.
    *   **Example:** If there are four orders in the database, `COUNT(*)` would return `4` as the total number of orders. The function simply counts rows and does not consider the content or specific values within those rows.
    *   **Syntax Example:** `SELECT COUNT(*) AS total_number_of_orders FROM orders`.

2.  **`SUM()`**
    *   **Purpose:** To **calculate the total sum of values** within a specified column.
    *   **Example:** To find the total sales in the business, `SUM(sales)` would be used. If the sum of all sales values is `80`, the function returns `80`.
    *   **Syntax Example:** `SELECT SUM(sales) AS total_sales FROM orders`.

3.  **`AVG()`**
    *   **Purpose:** To **calculate the average value** of a column.
    *   **How it works:** It summarizes all the values in the column and then divides by the number of values (or orders in the example).
    *   **Example:** If total sales are `80` from `4` orders, `AVG(sales)` would return `20` (80/4).
    *   **Syntax Example:** `SELECT AVG(sales) AS average_sales FROM orders`.

4.  **`MAX()`**
    *   **Purpose:** To **find the highest (maximum) value** within a specified column.
    *   **Example:** To find the highest sales amount, `MAX(sales)` would be used. If the highest sales value is `35`, the function returns `35`.
    *   **Syntax Example:** `SELECT MAX(sales) AS highest_sales FROM orders`.

5.  **`MIN()`**
    *   **Purpose:** To **find the lowest (minimum) value** within a specified column.
    *   **Example:** To find the lowest sales amount, `MIN(sales)` would be used. If the lowest sales value is `10`, the function returns `10`.
    *   **Syntax Example:** `SELECT MIN(sales) AS lowest_sales FROM orders`.

**Significance and Advanced Usage:**
*   Aggregate functions are described as **"very simple but yet very powerful"**.
*   They are fundamental for **exploring business performance** and understanding key business metrics like total orders or total sales.
*   The true power of aggregate functions is unlocked when **combined with the `GROUP BY` clause**.
    *   `GROUP BY` allows you to **break down "big numbers" into "smaller, more detailed numbers"**.
    *   This means you can calculate aggregate values (like total sales, average sales, highest sales, lowest sales) **for specific categories or groups**, such as by customer ID, date, or country. This enables **drilling down into data for deeper insights** for each customer or category.
    *   For example, you can find the total number of orders, total sales, average sales, highest sales, or lowest sales *for each customer*.

In essence, SQL aggregate functions are like a **powerful calculator for your data**. While each function (COUNT, SUM, AVG, MAX, MIN) performs a specific mathematical operation to give you a single summary number for your entire dataset, combining them with `GROUP BY` is like adding a **segmentation tool**. It allows you to perform those same calculations, not just for the whole, but for each individual segment or category within your data, providing a much richer and more granular understanding.
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
***

