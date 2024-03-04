
# Python Arrays (LSDT)
[index](index.md) </br>
[python](python.md) </br>
[python-loops](python-loops.md)
#### There's four types of arrays in python. See [math sets](sets.md)
<details> <summary>1. Lists</summary>

`thisList = ["apple", "banana", "banana", "cherry"]`
- Lists are ordered with indexes starting at zero
- Lists CAN contain duplicate values just like tuples

</summary> </details>


<details> <summary>2. Sets</summary>

`thisSet = {"apple","banana","cherry"}`
- Set items MUST BE UNIQUE
- Sets are UNORDERED, and may appear in a different order when used
- Individual set items are UNCHANGEABLE
- Create and Delete but cannot change set items


</summary> </details>

<details> <summary>3. Dictionaries</summary>

- Store key/value pairs
- Ordered as of python 3.7 
- Must be UNIQUE

```pyton
    thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
```

</summary> </details>

<details> <summary>4. Tuples</summary>

`thisTuple = ("apple", "banana", "banana", "cherry")`
- Ordered with indexes starting at zero just like lists
- Tuples CAN contain duplicate values just like lists
- Individual items are UNCHANGEABLE just like sets
- Items can be created and destroyed but not edited

</summary> </details>

#### Methods for collections of data

<details> <summary>Methods</summary>


<hr>

#### Lists
- type() # Displays the datatype (would return 'list')
- copy() # Return a copy of this list
- add() # Add to the list
- pop() # Delete from the list
- len() # Get the length of the list

<hr>

#### Sets
- type()
- copy()
- add()
- pop()
- union()
- intersection()

<hr>

#### Dictionaries
- type()
- copy()
- update() # If an item does not exist, update will created it.
- pop()
- popitem() # Deletes the last key/value pair that was inserted.
- get() # Returns value of specified key.
- keys() # returns a list of keys.
- values() # returns a list of values.
- items() # returns list of tuples displaying every key/value pair in the dict.
- clear() # deletes every key/value pair in the dict.
- len()

#### Tuples
- index() # get the index of a value in the tuple
- count() # returns the number of times a value occurs in a tuple.
- len()



</summary> </details>



