
[java](java.md) </br>


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


