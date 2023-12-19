
[java](java.md) </br>



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


