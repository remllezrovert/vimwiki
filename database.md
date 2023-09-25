



1. SELECT
2. FROM (aliases live here)
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

<details> <summary>Outer Joins</summary>

- Outer joins are inclusive
- Outer joins will output null values


</summary> </details>






#### Inner Joins
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








