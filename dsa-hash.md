

[dsa](dsa.md)



- Use logic to turn values into memory addresses
- A collsion is when hashing produces the same memory address for multiple values
- Example
    - value % hashSet.size() = memoryAddress;






<details> <summary>Linear probing</summary>

- One value in each memory address
- If a memory address is already taken
    - Check the next available address (+1)
    - Keep adding 1 until you find it
    - If you hit the maximum value, wrap around to 0
- Deleted indexes replaced by tombstone
    - Cannot normally insert new values into tombstone.
    - Use 'lazy deletion' if you want to do this.


</summary> </details>


<details> <summary>Chaining</summary>

- Using hashing to put things into memory addresses
- Each memory address should store the head of a linked list
- If a collision occurs, add it as the next element on the linked list

</summary> </details>

