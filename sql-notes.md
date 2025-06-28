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