


#Order of operations

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

