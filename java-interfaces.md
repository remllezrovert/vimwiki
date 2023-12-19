
[java](java.md)

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


