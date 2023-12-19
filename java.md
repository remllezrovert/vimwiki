# Java Programming </br>
 
[index](index.md)

[java-theory](java-theory.md)


[java-classes](java-classes.md)

[java-interfaces](java-interfaces.md)

[java-math](java-math.md)

[java-logic](java-logic.md)

[java-arrays](java-arrays.md)

[java-loops](java-loops.md)


[java-strings](java-strings.md)







<details> <summary>Data types</summary>

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









<details> <summary>Documentation</summary>




</summary> </details>


