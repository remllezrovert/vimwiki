 Java Programming
[index](index.md)

<details> <summary>Lingo</summary>

Modular development - Devide a program into modules or microservices. Test and develop each separately.
Incremental development - test as you develop. Test constantly.
Method stub - empty or "abstract" method that does nothing YET. Will eventually do something



</summary> </details>



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


<details> <summary>Constructors</summary>

- This calls the Duck constructor: `Duck d = new Duck();`
- If the class has no manually written constructor, it will automatically run anyway
- Manually construct on object by creating a method with it's class's name (example below)

```
public class Duck {
    public Duck(){
        System.out.println("Quack");
    }
}

```
- Parameters can be passed into a constructor to immeditly give the object values

```
public class Duck {
    public Duck(int duckSize){
        int size = duckSize;
        System.out.println("Quack");
    }
}

```
- Constructors can be 'overloaded' just like normal methods
- If the duck is created and an int is passed int the top 
```
public class Duck {
    public Duck(int duckSize){
        int size = duckSize;
        System.out.println("Quack");
    }
    public Duck(String duckName){
        String name = duckName;
    }
}

```



</summary> </details>



<details> <summary>Inheritance</summary>

- Subclasses cannot access private methods of their superclass without getters. 
- Use 'protected' instead of 'private' to allow subclasses access to variables.
- Inheritance chains one inside another. Use interfaces for a more flexable option.

- Method overriding: A subclass's method has the same name as a method in it's parent
- Method overloading: A class has multiple methods with the same name and different param

```java
class Vehicle {
    public void move(){}
}
class Car extends Vehicle {  //create a subclass
    super.move();           //call a method from the superclass
    private int numberOfCylinders;

    public int getNumberOfCylinders(){
        return numberOfCylinders;
    }

    public void setNumberOfCylinders(int numberOfCylanders) {
        this.numberOfCylinders = numberOfCylinders;
    }


}
```


</summary> </details>



<details> <summary>Abstraction and interfaces</summary>


- An interface is an abstract class used to group related methods with empty bodies
- Classes can 'impliment' interfaces and use their methods using the 'impliment' keyword
- A class can impliment multiple interfaces, just separate them with a comma
```java
interface Animal{
    public void animalSound();
    public void run();
    public void sleep();
}

class Pig implements Animal {
  public void animalSound() {
    System.out.println("The pig says: wee wee");
  }
  public void sleep() {
    System.out.println("Zzz");
  }
}



```

</summary> </details>


<details> <summary>Enums</summary>

- Enums store values that are unlikely to change, like months or days of the week
- This can be used for 'multiple choice' type fields

```java
public enum Cars {

    bugatti(200, "blue", "jeff"),
    honda(300, "red", "Trevor"),
    shitBox(25, "green", "bill")

    private int speed;
    private final String color;
    private final String owner;

    //This is called the constructor
    Cars (int speed, String color, String owner){
    this.speed = speed;
    this.color = color;
    this.owner = owner;
    }
    //getter method for the enum
    public int getSpeed(){
        return speed
    }
}
// Main method to test this enum
public static void main(String[] args){
    Cars car = Cars.shitBox; 

    System.out.println(car.getSpeed()); //this would print the speed of shitbox

    for (Cars myCar: Car.values()){
        System.out.println(myCar.getSpeed()); // This for loop prints the speed of every car
    }                                       
}

```
</summary> </details>



<details> <summary>packages</summary>

- Indicate how class is packaged `package java111.project5;`
- Normally source code is kept in a source folder 'src'
- Normally compiled classes are kept in a folder 'classes'
- Indicate where to place compiled classes `javac -d classes`
- The compiler will mirror the directory heirarchy of 'src'
- compile with `javac -classpath classes -d classes src/java111/project/*.java`

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

```java
public class ExampleClass{

    private int exampleInt = 2;

    public int void exampleGet(){
        return exampleInt;
    }
    public void exampleSet(int externalInt){
        exampleInt = externalInt;
    }
}
```

</summary> </details>


<details> <summary>String Manipulation and Formatting</summary>


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
</br>
String Comparison
- The final character in a string has an index one less than it's length. 
> finalCharacterIndex = exampleString.length() - 1;  </br>


``` Java
if (stringOne.compareTo(stringTwo) > 0) {System.out.println("stringOne is greater than stringTwo");}
if (stringOne.compareToIgnoreCase(stringTwo) > 0) {System.out.println("stringOne is greater than stringTwo");}
stringThree.replace("Goodbye", "hello");
String.indexOf("i", 3) //Find index of third instance of the letter
stringFour.subSequence(

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



<details> <summary>Statements</summary>

- If else statements have a shorthand
- The two expressions below are the same
```java
if (x > 20) {y = 3;} else {y = x;}
y = (x > 20) ? 3 : x; //this is shorthand for the expression above

if (!(z > 20 && z < 30)) z += 99; //No need for parenthesis if there is only one expression
```


```java
switch (n) {
    case 0:
        System.out.println("n is 0");
        break;
    case 100:
        system.out.println("n is 100");
        break;
    default:
        system.out.println("n is none of the above");
    case -3:
        System.out.println("n is -3");
        break;
}
```
output: </br>
> n is none of the above </br>
> n is -3
- The switch keyword checks for equality
- Each case is a check for equality
- The default case triggers if none of the above are true
- A break statement must end each case, or the proceeding case will be triggeres even if it's false.


</summary> </details>


<details> <summary>Documentation</summary>




</summary> </details>


