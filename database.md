



1. SELECT
2. FROM
3. WHERE
4. GROUP
5. HAVING
6. ORDER


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



<details> <summary>Inner Joins</summary>

- Inner joins only return rows that meet all the join conditions. 
- Inner joins are exclusive
- Used for selecting rows with a matching condition.
- Multiple can be chained together to match across many tables
- Can't output null values 
~~~
SELECT 
    table_a.foo,
    table_b.bar,
FROM table_a
INNER JOIN table_b
    ON table_a.key = table_b.key
WHERE table_a.foo = table_b.bar;
~~~

You can filter inner joins using the "AND" keyword:
~~~
SELECT 
    table_a.foo,
    table_b.bar,
FROM table_a
INNER JOIN table_b
    ON table_a.key = table_b.key
        AND table_a.foo = table_b.bar
        AND Table_a.foo > 2;
~~~


</summary> </details>




<details> <summary>Outer Joins</summary>

- Outer joins are inclusive
- Outer joins will output null values


</summary> </details>

