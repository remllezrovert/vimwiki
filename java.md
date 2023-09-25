
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
- for loops use the format **for (start; stop; step) {}**
- The example below will iterate through every car in the car array lowest to highest and make it drive.

```java
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


<details> <summary>String Formatting</summary>


- By default printing a 'char' will output it's ascii id number
- specify that you want to output the char as a string: System.out.print("" + exampleChar);

Escape Sequence | Char
----------------|-----------
`\n` | newline
`\t` | tab
`\'` | single quote
`\'` | double quote
`//` | backslash


```java
public class example{
    double myDouble = 23.45
    public static void main(String[] args){
    System.out.println("say \"Hello\" using quotes inside a string with escape sequence");
    System.out.println("\tIndented by one tab");
    System.out.println("\\ this is a backslach inside a string");
    System.out.printf("%.2f\n", double ) //this prints a formated double with a newline after it
    }
}
```




</summary> </details>


<details> <summary>scnr</summary>

method  | purpose
--------|-----------
nextLine() | prints the entire line including any whitespace
next() | print the first word in the string exculding whitespace


</summary> </details>


<details> <summary>Math </summary>



Method | Behavior | Example
-------|----------|--------
sqrt(x) | Square root | Math.sqrt(9.0);
pow(x,y) | $x^y$ | Math.pow(2.3,3.4);
abs | $/mid x /mid$ | Math.abs(-99.3);


- The modulo operator '%' evaluates the remainder of a division problem Example: `58 % 10 = 8`


</summary> </details>


