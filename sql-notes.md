## SQL Course 3
- There are 2 ways to create a database: the 1st way is executing the script, and the 2nd way is place the script in the SQL DBMS and restore database. (review video SQL Course 3 to recheck)
## SQL Course 4
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
## SQL Course 6
- Insert into a tale from `SELECT` query: 
```
INSERT INTO table_name (column_list)
SELECT ...
FROM ...
```
- Delete all data from a table
1st way: `DELETE FROM table_name`
2nd way: `TRUNCATE TABLE table_name` => reset the table, faster than the 1st way
## SQL Course 8
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
## SQL Course 9
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



