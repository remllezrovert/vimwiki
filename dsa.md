







[datastructures](datastructures.md)









<details> <summary>Binary search</summary>


- find element within sorted list
- cuts list in half repeatedly
- this example starts at zero

```python

def binary_search(arr, target):
    start = 0 
    end = len(arr) - 1                 #subtraction is done cause indexing starts at zero
    while start <= end:
        mid = (start + end) // 2       #Floor divison rounds quotient down to whole number
        if target == arr[mid]:
            return mid
        elif target < arr[mid]:
            end = mid - 1
        else:
            start = mid + 1
    return -1
    
```

</summary> </details>





## Sorting algorythms



