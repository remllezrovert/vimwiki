



<details> <summary>Array</summary>

- Fixed size (use linked lists for variable size)
- Indexable contiguous chunk of memory
- Think python lists or java arrays



</summary> </details>


<details> <summary>Linked lists</summary>

Hold two things
1. data
2. a pointer (memory address) to the next element

- The last element in the list points to null
- Can't access access elements by index in constant time (use array for this)

</summary> </details>






<details> <summary>Trees</summary>

Each node can hold:
1. from zero to multiple pointers
2. data


#### Binary Search Trees
- A node with no children is called a leaf node
- The parent node can be reffered to as the 'root' node 
- As the computer decends down the tree it compares the target value to each parent node </br>
if the target value is greater than the parent's key value it points to right child node 
- Left's key value $\leq$ parent's key value < right's key value
- Time complexity o(H) where H is the height of the tree
- Height is on average o(Log N).

bianary search trees can:
1. search
2. insert
3. delete

Self balencing bianary search trees
- red/black trees
- turn linked lists into search trees

</summary> </details>


<details> <summary>Heap</summary>

- Also known as priority queue
- Abstract data type where elements have priority
- higher priority elements served first
- most of the heap is only semi sorted
- searching through the heap is O(N) time complexity
- inserting takes O(log n) time

## min heaps 
- the smallest element will always be at the top

Adding nodes:
- new nodes attempt to attach to the first available parent (top to bottom left to right)
- once attached the node compares itself to it's parent. If smaller it will "bubble up", </br>
swapping places with it's parent until it's either at the top, or it's parent is smaller.

![dsa-minHeapUp](dsa-minHeapUp.gif)

Removing nodes:
- if the top node is removed, the newest leaf node will be placed on top. Then it (former newest leaf) will bubble </br>
down the tree, comparing itself to both children until both children are smaller


![dsa-minHeapDown](dsa-minHeapDown.gif)

</summary> </details>


