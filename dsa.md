# Datastructures

- [dsa-trees](dsa-trees.md)
- [dsa-hash](dsa-hash.md)



<details> <summary>Stacks</summary>

- Last in first out
- 

 Op    | Time Complexity | Function
-------|-----------------|-----------
push() | O (1) | add to the top
pop() | O(1) | delete & retreive the top
peek() | O(1) | retreive the top
size() | O(1) | find the size


</summary> </details>


<details> <summary>Queues</summary>

- First in first out


 Op    | Time Complexity | Function
-------|-----------------|-----------
queue() | O(1) | add to the back
dequeue() | O(1) | delete & retreive front
peek() | O(1) | retreive the front
size() | O(1) | find the size
getNodeAt(int index) | O(n) | get a node mid queue
deleteAfter(int index) | O(n) | delete after a particular node
insertAfter(int index) | O(n) | delete after a particular node


</summary> </details>


<details> <summary>lists</summary>



#### Linked lists ####

Action | Time 
-------|-------------------
Accessing elements | O(n)
Insert/Remove first |O(1)
Insert/Remove last | O(n)
Insert/Remove middle |O(n)

each memory address stores the address of the next address. </br>

deleteAfter()



#### Doubly linked lists  ####
each memory address stores the address of the next AND previous address


</summary> </details>



<details> <summary>Arrays</summary>


Action | Time 
-------|-------------------
Insert/Remove first |O(1)
Insert/Remove last | O(n)
Insert/Remove middle |O(n)
Searching | O(N)
Accessing elements | O(1)


#### Dynamic Arrays ####
- Indexes shift after a delete
    - example {4,3,5,7,9,2,1}
    - remove(1)
    - result {4,5,7,9,2,1}
    - get(1) == 5
- Automatically assign more memory when array hits max capacity


</summary> </details>


# Algorythms



<details> <summary>Big O</summary>


O(1) - Constant time </br>
- random access of an element in an array
- inserting at the beginning of a linked list

O(log n) - Logarithmic time
- Binary search

O(n) - Linear time
- looping through n elements in an array
- searching through a linked list

O(n log n) = QuasiLinear Time
- quicksort
- mergesort
- heapsort

$O(n^2)$ = Quadratic time
- Insertion sort
- Selection sort
- bubble sort

$O(n!)$ = Factorial time
- Traveling Salesman Problem





</summary> </details>


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







<details> <summary>Selection sort</summary>

Cons:
- Very Inefficient for large datasets

Pros: 
- Simple


- go through each index in the array one by one
- compare the current element (i) to every element afer it (j)
- if i > j then they swap places

```java
    for (int i = 0; i < array.length - 1; i++){
        int min = i;
        for (int j - i + 1; j < array.length; j++){
            if (array[min] > array [j] ){
             min = j;
            
            }

    }

int temp = array[i]; //these three lines swap min with 
array[i] = array[min];
array[min] = temp;

}
```
</summary> </details>



<details> <summary>Insertion sort</summary>


- Bad for large datasets, decent for small ones
- Runs in Ouadratic time $O(n^2)$
- Best case is O(n) which is fater than selection sort's best case

- Start at index 1
- compare current element (i) to everything to the left of it (j)
    - store i in memory as temp
- compare i to each element (j) to the left of it
- if i < j then shift j to the right by one
    - Repeat this. Stop when j > i
    - if j > i 
        - then array[j + 1] = temp
        - move to the next i





```java

private static void insertionSort(int[] array){

for (int i = 1; i < array.length; i++) //start at one so that we can compare to zero
    {
    int temp = array[i];
    int j = i - 1;
    while(j >= 0 && array[j] > temp){
        array[j + 1] = array[j]; //shift element to the right
        j--;
    }
    array[j + 1]  = temp;
}
}


```



</summary> </details>


<details> <summary>Merge sort</summary>



$O(n \cdot \log_2{n})$

$\Omega(n \cdot \log_2{n})$

$\Theta (n \cdot \log_2{n})$



- Recursive "divide and conquer" algorythm
- Split array into sub arrays until each array is size 1
- starting at the size 1 arrays
    - put both of the children back into their parent in sorted order
    - repeat this until the origional array is sorted


#### Comparison ####
- Fast, comparable to quick sort and heap sort
- Uses more space than bubble, insert, and selection sort.

</summary> </details>






<details> <summary>Algorithms</summary>



- Actions
- Order
- Sequence structure
- Selection structure 
- Iteration structure

</summary> </details>






