

<details><summary>Create and Delete</summary>





Create a schema:
- A schema or 'database' is a place where tables go. 
```
CREATE SCHEMA IF NOT EXISTS ExampleDatabase; //creates a database idempotently
DROP SCHEMA IF EXISTS ExampleDatabase; //delete a database idempotently
```
Create a table:
```
//Create a table
CREATE TABLE IF NOT EXISTS ExampleTable (
ExampleColumn1 integer COMMENT 'useless number',       //comment for devs
ExampleColumn2 varchar(25) NOT NULL,                   //disallows the use of null columns
ExampleColumn3 date UNIQUE NULL,                       //allows a null column to exist
ExampleColumn4 float DEFAULT 3.14,                     //sets a default value
myKey1 integer AUTO_INCREMENT PRIMARY KEY              //sets the primary key
myKey2 PRIMARY KEY (ExampleColumn1, ExampleColumn2)    //creates a composite key
);


//Delete a table
DROP TABLE IF EXISTS ExampleTable;
```

</summary> </details>


<details> <summary>Data Types</summary>

Strings:
- TEXT values are unbounded potencially lengthy blobs
- VARCHAR(n) sets the upper bound to n. Use for columns containing strings with highly variable length.
- CHAR(n) use this for columns containing strings with relatively uniform length (phone number)

Integers:
- int has a range +-2 billion
- TINYINT is used for numbers from 0 to 255 signed without decimals

Floats:
- NUMERIC(m,n) numbers of values before and after decimal point
- FLOAT

Date:
- DATE
- TIME
- DATETIME


Which data type should I use?
- What type of value do you have
- What is the range
- Signed or unsighned numbers (allow negatives?)
- Computational efficiency 

</summary> </details>


<details> <summary>Table Indexes</summary>

- Indexes are a type of meta-data used to efficently queary on non-key fields
- Rows with similar primary key values are clustered together and paginated on a hard disk for efficency
- A table scan is used to find data without the primary key. INEFFICIENT
- A queary engine figures out how to most efficently read the pages it needs from disk
- The queary engine creates a queary plan to read from disk more efficently
- The queary plan indexes by traversing a tree-lilke structure using the primary key
- An index is a sort of alternate queary plan, using non key values, so that table scans can be avoided

```sql
CREATE INDEX ExampleIndex
ON ExampleTable
    (ExampleField1, ExampleField2); //index based on two fields, which don't have to be keys
```

</summary> </details>


<details> <summary>ALTER</summary>

```SQL
/* Add new column to table at specific location */
ALTER TABLE exampleTable ADD COLUMN EmailAddress varchar(50) NULL 
    AFTER LastName;

/* Modify the column's location and size*/
ALTER TABLE exampleTable MODIFY COLUMN EmailAddress varchar(40) NOT NULL
    BEFORE FirstName;
/* Renames are dangerous because it will update the database but not existing sql scripts*/
ALTER TABLE exampleTable RENAME COLUMN MiddleName TO MiddleInitial;
ALTER TABLE exampleTable DROP COLUMN MiddleInitial;

/* Select column as PK */
ALTER TABLE Customers
ADD PRIMARY KEY (CustomerId);

/* Delete index */
ALTER TABLE Customers
DROP INDEX CustomerNameIx;

/* Set PK to increment*/
ALTER TABLE Customers
AUTO_INCREMENT = 1;


```

</summary> </details>


<details> <summary>Contraints</summary>

- It is recommended to add constraints after making all the tables
To create constraints immediately:
```sql
CREATE TABLE CarOwner(
OwnerId integer PRIMARY KEY,                ##a primary key constraint
OwnerName varchar(50) NOT NULL,
VehicleId integer NOT NULl,
CONTRAINT FK_Car FOREIGN KEY (VehicleId)    ## a foreign key constraint using VehicleId
    REFERENCES Car(CardId)

);
```

To add constraints later (best technique):
```sql
ALTER TABLE CarOwner
ADD PRIMARY KEY (CustomerId);                   ## a primary key constraint
ADD CONTRAINT FK_Car FOREIGN KEY (VehicleId)    ## a foreign key constraint using VehicleId
    REFERENCES Car(CardId)


```

</summary> </details>

<details> <summary>INSERT</summary>

- Number of columns must match the number of expressions
- Don's specify AUTO_INCREMENT fields
- The type of each expresson must match the type of it's corrisponding column
```sql
INSERT INTO <table>
    (<column_name1>, <column_name2>, <column_nameN>)
VALUES (<expression_1>,<expression_2>,<expression_N>);
```

```sql
INSERT INTO <table>
(productNumber, productName, productDescription, retailPrice, quantityOnHand, categoryID)
VALUES 
    (12, "goat", "animal", null, 12, 3),
    (13, "sheep", "animal", 12822.2, 13, 4),
    (14, "duck", "animal", 56.5, 14, 5),
    (15, "cow", "animal", 22.3, 15, 6)


```

This example gets data from another table and inserts it. This is dynamic insertion
```sql
INSET INTO PRODUCTS
(productName, retailPrice, quantityOnHad, categoryID,)
SELECT 'studded Bike Tires', 24.99, 15, categoryID
FROM Categories
WHERE categoryDescription = 'tires';

```

This queary ignores errors while trying to insert. Useful for duplicate data with UNIQUE constraint.
```sql
INSERT IGNORE INTO Actor
(actorName)
SELECT Star1
FROM MovieStaging;
```

</summary> </details>


<details> <summary>UPDATE</summary>


```
UPDATE <table>

SET <column1> = <expression1>,
<column2> = <expression2>,
<column3> = <expression3>
WHERE <search criteria>;            #Which rows should update?
```

```
UPDATE <table>

SET
price  = price * 2,
color  = pink
WHERE color = red;            #Which rows should update?
```


</summary> </details>


<details> <summary>Subquearies</summary>

Update subqueary example
```
UPDATE Product_Ventors
SET price = price * 1.10
WHERE vendorID IN (
SELECT vendorID FROM vendors
WHERE vendName = 'Proformance');
```


</summary> </details>


        
