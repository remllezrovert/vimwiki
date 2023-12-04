[sql-ddl](sql-ddl.md)
[database](database.md)



<details> <summary>basics</summary>


1. SELECT - Chooses the fields and expressions in the result relation.
2. FROM  - Assembles the tables where source data is located. 
3. WHERE - Defines the search criteria for result rows.
4. GROUP - Chooses the fields for agregating rows
5. HAVING - Defines the search criteria for result grouped rows.
6. ORDER - Defines the fields for sorting results.




</summary> </details>



<details> <summary>Subquearies</summary>

1. A nested queary is a subqueary that can function independently without it's surrounding super queary.

2. Subquaries for column expressions. This is subquearies in the SELECT statement of their superqueary
3. A scalar subqueary is used to get a single value which is used in the super-queary for comparison.
- These are frequently used for grouping
4. A nexted list subqueary uses the IN keyword
- An outer join can be replaced with `WHERE NOT IN` to make it easier to understand.
- Use the `ANY` keyword to compare a subqueary and return all values that match the comparison criteria.

```SQL
WHERE fanQuantity > ANY (
SELECT fanQuantity FROM Bands WHERE bandName LIKE '%forest%'
);

```


- Use the `ALL` keyword to return superqueary values if every value in the subqueary meets the critera.
- The queary below would return all bands that are more popular than every single slam metal band.
```SQL
WHERE fanQuantity > ALL (
SELECT fanQuantity FROM Band WHERE genrename LIKE 'Slam Metal'
);
```

5. Table subqearies
```
SELECT bandName
FROM Band AS B
INNER JOIN (
    SELECT bandId, albumName
    FROM Album
    INNER JOIN BandAlbum
    USING(bandId)
    WHERE albumName != 'untitled'
) AS A
ON A.bandId = B.bandId;
```



6. Common Table Expressions (CTE) are temporary tables created on the fly to solve problems
- They are sort of like functions in python/java. They can be called repeatedly.
```
WITH <cte_name> AS (
<select queary>
)
SELECT * FROM <cte_name>;
```

7. Correlated SubQuearies
- Retrieve subqueary information specific to individual values in the super queary
- Use when the outer queary affects or depends upon the inner queary
- Subqueary runs after SuperQueary because it's dependent
- Use for aggregate value lookups
    - Show all students and the number of clases they are taking.
    - List all customers and the date of the most recent ordr they placed.
- Use for filtering on aggregate values
    - Which bowler has the highest score on each team
- Simply complex inner and outer joins
    - Show al customers who have not ordered a bike.
    - Which students have withdrawn from at least one class.

8. Correlated List SubQuearies
- Solve the outer queary first
- `EXISTS`
- `NOT EXISTS`


```SQL
SELECT
FROM
WHERE EXISTS (
<queary>
)
```










</summary> </details>




<details> <summary>Set operations (UNION)</summary>


- UNION is used to lump together rows from different tables so that they are in the same output
- UNION eliminates duplicates where they exist
- The rows being united must have the same number of fields and type of fields
- The union is sandwitched between two SELECT statements
- UNION ALL does not eliminate duplicates


- INTERSECT only shows values that are in both tables
- The number of fields and type of fields must match
- EXCEPTION works like subtraction. Only shows the rows unique to the left table.


</summary> </details>





<details> <summary>WHERE</summary>


The WHERE clause searches for rows in a table that meet a given condition. </br>

_ _ _
The statement below allows you to search rows that match multiple keywords in one column </br>
`SELECT * FROM IceCream WHERE Brand IN ('Breyers', 'Haagen-Dazs');` </br>


_ _ _
Filther by pattern: `SELECT * FROM IceCream WHERE Flavor LIKE '%Chocolate%';` </br>

pattern        | matches
---------------|----------------
'X%'           | Any String starting with x
'%X'           | Any string ending with x
'%X%'          | Any string containing X
'X_'           | X followed by a one character

</summary> </details>

<details> <summary>Outer Joins</summary>

- Outer joins are inclusive
- Outer joins will output null values


</summary> </details>






<details> <summary>Inner Joins</summary>

- Inner joins only return rows that meet all the join conditions. 
- Inner joins are exclusive
- Used for selecting rows with a matching condition.
- Multiple can be chained together to match across many tables
- Can't output null values 
```sql
SELECT 
    table_a.foo,
    table_b.bar,
FROM table_a
INNER JOIN table_b
    ON table_a.key = table_b.key
WHERE table_a.foo = table_b.bar;
```

* You can filter inner joins using the "AND" keyword:

* This queary uses the USING keyword to join tables, which is the same as  `on table_a.key = table_b.key`:
    ```sql
SELECT 
    table_a.foo,
    table_b.bar,
FROM table_a
INNER JOIN table_b
    USING key
        AND table_a.foo = table_b.bar
        AND Table_a.foo > 2;
```


* Self joins allow the selection of rows within the same table that have maching values
* Example: Show every posible combination of couples that could occor in north leeds
* The WHERE clause at the end exists so that 
    + People are not coupled with themselves in the output
    + It prevents "Bob and Jim" from being listed a second time as "Jim and Bob".
    ```sql
SELECT p1.FullName, p2.FullName, p1.Residence
FROM Population AS p1
INNER JOIN Population AS p2 ON p1.Residence = p2.Residence
WHERE p1.ID < p2.ID;
```

</summary> </details>


When to use GROUP BY
- When we want a single consolidated row for each group
- When the order of the rows in each group does not matter
- When the rows in each group are consolidated



<details> <summary>Aggregation</summary>

> ```sql
> SELECT Gender, AVG(Deadlift)
> FROM Lifts
> GROUP BY Gender
> HAVING LiftingStance = 'sumo';
> ```
> Gender | AVG(Deadlift)
> -------|------------
> Male | 500
> Female | 300
> Enby | 9000



- `SELECT COUNT(DISTINCT BowlerCity) FROM Bowlers;`
- Aggrigation is "collecting things"
- Gathering multiple rows of data
- Aggrigation occurs after the select statement 
- Thing "total, sum, max, or min".
- Must include all output fields in GROUP BY statement
- HAVING occurs after the groups have been created, WHERE occurs before
- Agrigate functions are not allowed in a WHERE clause, must using HAVING
- Only use HAVING for agrigate functions



function | what it does
---------|-------------
COUNT(<field>) | number of rows where <field> != null
COUNT(*) | Total number of rows
AVG(expression) | average value of the expression across
SUM(expression) | sum of the value of the expression across rows
MAX(expression) | the largest expression in all rows
MIN(expression) | the smallest expression in all rows
CONCAT(<field1>, ' ', <field2>) | combines many columns within the same row
GROUP_CONCAT(<field>) | comma-delimited list of one field in many rows





</summary> </details>

When to use windows
- Useful for ranking within categories, and displaying all categories
- When we want to see each individual group that meets the grouping critera
- does not cause rows to become grouped into a single output row
- windows functions performs a calculation across a set of related rows which are related to current row

<details> <summary>Window functions</summary>

- Grouping Fields - which rows (inside parenthesis) are related to our current row (outside parenthesis)
- Sorting Fields - how do I want to sort the related rows
- OVER - specifies what's inside the window
- You can create multiple windows by using "OVER" multiple times

```sql
SELECT <fields>, 
<aggregete or window function> ##How to summarise the rows##
    OVER (
    PARTITION BY <grouping fields> ##optional##
    ORDER BY <sorting fields> ##optional##
    )
FROM <table name>

```


### Ordering within windows
- Running total - calculate the category total, then add each category previous


Window Function | What it does
`ROW_NUMBER() OVER(ORDER BY Score)` | number the rows
`DENSE_RANK() OVER(ORDE BY SCORE)` | rank by score. Ties get indentical ranks. Normal ranking type
`RANK() OVER(ORDE BY SCORE)` | rank by score. Ties get identical ranks. Not normal ranking 
`FIRST_VALUE(expr)` | Show the value of expression for the first row in the frame
`LAST_VALUE(expr)` | Show the value of expression for the last row in the frame
`NTH_VALUE(exprn, num)` | Show the value of expression for the N'th row in the frame
`LEAD(expr, numRows)` | look at future rows for comparison
`LAG(expr, numRows)` | look at past rows for comparison
`NTILE(num)` | divides the partition in num groups by the value in an ORDER BY. Quartiles. Percents.
`PERCENT_RANK()`  |  show the percentage of partition values less than or equal to the value in current.
`CUME_DIST()` | 


</summary> </details>
    




<details> <summary>Operators</summary>



- Use CASE to create expressions whose value changes based on a condition
- example: change output based on a value in another column.
```SQL
SELECT ProductName, RetailPrice
(CASE
    WHEN RetailPrice > 100  THEN 'Luxury'
    WHEN RetailPrice < 50  THEN 'Mass Market'
    ELSE 'Economy'
END)

SELECT CAST(19550224 AS DATE);


```


</summary> </details>

