

[java](java.md) </br>


<details> <summary>2d Arrays</summary>

```java
int[][] arr = new int[10][20];                              //declare 2d array and it's size

for (int row = 0, < arr.length, row++ ){                    //loop through each row 
    for (int col = 0, col < arr[row].length, row++) {       //loop through each col
        //do something here
    }
}
```



```java
public static int[][]getInputGrades(int... item) //variable argument ... accepts one to many
{
}
```

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


<details> <summary>Arrays </summary>
- Get the length with a attriute not a method
    - exampleArray.length


</summary> </details>


<details> <summary>Array List methods</summary>

- These are linked lists

#### Methods
    exampleArrayList.remove(index)
    exampleArrayList.remove(Object)
    exampleArrayList.toArray()
    exampleArrayList.add(newElement)
    exampleArrayList.get(index)
    exampleArrayList.contains(itemToFind)
    exampleArrayList.foreach((i) -> System.out.println("did lambda thingy"));
    exampleArrayList.indexOf()
    Arrays.toList(exampleArray)              #Convert regular array to arrayList

[Official Documentation](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html) </br>




</summary> </details>


<details> <summary>Arrays class</summary>

```
Arrays.sort()
Arrays.binarySerach(intArray, 5)
Arrays.equals()
Arrays.fill()
int[] exampleArrayTwo = Arrays.copyOf(exampleIntArray, exampleIntArray.length)
```

</summary> </details>






