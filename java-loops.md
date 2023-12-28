

[java](java.md) </br>

<details> <summary>for loops</summary>

- For loops are good for arrays or lists with predictable lengths
- Use a for loop when possible because they are more efficent


## Array length looping
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

## Loop directly through array
- Alternative format for loop
- Looping through arrays is easier with colon syntax
- Can loop through object arrays aswell
- Can loop through arrays containing objects with the same interface

```java
public class ExampleLoop{
    public static void main(String[] args){
        String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
        for (String i : cars) {
            System.out.println(i);
        }
}
```

</summary> </details>



<details> <summary>While Loops</summary>

- This loop runs while 1 < x <= 1000
- Only use while loops if the bounds of the loop are unknown

```java
while (x > 1) {
    x -= 1;
    if (x > 1000)
        break;
}
```

## Do While Loop
- useful if code should always run atleast once, possibly multiple times
- The 'do' part will excute before the while
```java
do {
    x -=1;
    
} while (x > 1);
```



</summary> </details>

