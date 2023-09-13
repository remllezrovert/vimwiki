
# Java Programming
[index](index.md)
[database](database.md)
[cisco](cisco.md)

<details> <summary>Primitive Types</summary>


Acronym | Value | Bytes
---------------|-------------|---|
| Be | Boolean | 1
| Careful | Char | 2
| Bears | Byte | 1
| Shouldn't | Short | 2
| Ingest | Int | 4
| Large | Long | 8
| Furry | Float | 4
| Dogs | Double | 8


</summary> </details>










<details> <summary>object arrays</summary>

- Array indexing starts at zero.
- Arrays are pointed with reference variables
- Arrays can contain reference-type variables, primative-type variables, null, or all of the above

```java
public class ExampleCars{
public Vehicle carArrayReference[];

    public static void main(String[] args){
        Vehicle car1 = new Vehicle();
        Vehicle car2 = new Vehicle();
        Vehicle car3 = new Vehicle();
        carArrayReference = new Vehicle[]{car1, car2, car3};
    }
}

```

</summary> </details>


<details> <summary>for loops</summary>


- Array indexing starts at zero.
- for loops use the format **for (start, stop, step) {}**
- The example below will iterate through every car in the car array lowest to highest and make it drive.
```jaava
public class ExampleLoop{
    public static void main(String[] args){
        for (int i = 0; i < carArrayReference.length; i++) {
            carArrayReference[i].drive();
        }
    }
}
```


</summary> </details>







<details> <summary>garbage collection</summary>

- if an object isn't being pointed to by a reference like `new exampleObject()` it will be deleted.

- if one object reference is set equal to another they will read from the same spot in ram.

- if a reference is reassigned and the previous object has no reference, it will be deleted.


</summary> </details>


<details> <summary>getters and setters</summary>

- A getter is a method that allows external classes to access private variables in a class.
- A setter is a method that allows external classes to set private variables in a class.

~~~java
public class ExampleClass{

    private int exampleInt = 2;

    public int void exampleGet(){
        return exampleInt;
    }
    public void exampleSet(int externalInt){
        exampleInt = externalInt;
    }
}
~~~

</summary> </details>

