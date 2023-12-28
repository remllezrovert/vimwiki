
[java](java.md) </br>



<details> <summary>if/else</summary>

- If else statements have a shorthand
- The two expressions below are the same

```java
if (x > 20) {y = 3;} else {y = x;}
y = (x > 20) ? 3 : x; //this is shorthand for the expression above

if (!(z > 20 && z < 30)) z += 99; //No need for parenthesis if there is only one expression

```

</summary> </details>

<details> <summary>Switch case </summary>

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


