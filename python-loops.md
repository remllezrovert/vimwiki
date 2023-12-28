
# Python-Loops
[python](python.md) </br>
[python-arrays](python-arrays.md)

<details> <summary>For Loops</summary>


## Looping through with ranges
```python
for x in range(start, stop, step):
    print(x)
```
- Example loop
- The 'else' keyword will trigger after the for loop is complete
```python
for x in range(4, 12, 2):
    print(x)
else:
    print("reached the max of the range")

```

## Looping Through Arrays
- Loop through the array using 'in' keyword
- Break with "break"
```python
fruits = ["apple", "banana", "cherry", "tomato", "grapes", "watermelon"]
for x in fruits:
  print(x)
  if x == "tomato":
    break
```

</summary> </details>


<details> <summary>While Loops</summary>

- While loops are most useful when the bounds of the loop are unknown or unpredictable
```python
i = 1
while i < 6:
  print(i)
  if i == 3:
    break
  i += 1 
```

## Continue keyword
- The continue keyword allows us to skip over part of the loop
- The example below will print every value between 1 and 6 except 3
```python
i = 0
while i < 6:
  i += 1
  if i == 3:
    continue
  print(i)
```

</summary> </details>

