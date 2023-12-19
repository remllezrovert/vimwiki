

[java](java.md) </br>

<details> <summary>Lingo</summary>

Modular development - Devide a program into modules or microservices. Test and develop each separately.
Incremental development - test as you develop. Test constantly.
Method stub - empty or "abstract" method that does nothing YET. Will eventually do something



</summary> </details>



<details> <summary>The heap and the stack</summary>

- Methods live in the stack. Newest at the top
- The stack stores frames
- Local varaibles live on the stack
- The stack is part of the JVM's memory
- Reference variables point to the heap
- Completed methods pop out of the stack



- Objects live on the heap
- Instace variables live on the heap
- Unreferenced stuff in the heap goes to the garbage collector

</summary> </details>


<details> <summary>garbage collection</summary>

- if an object isn't being pointed to by a reference like `new exampleObject()` it will be deleted.

- if one object reference is set equal to another they will read from the same spot in ram.

- if a reference is reassigned and the previous object has no reference, it will be deleted.


</summary> </details>


