
# Python Objects and Classes 

- [python](python.md) </br>
- [index](index.md) </br>


<details> <summary>Classes</summary>

- Constructor with "__init__"
- Must pass in "self" to use the object's variables
- Delete an object with "del" keyword
```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def greeting(self)
        print("Hi, my name is " + self.name + " and I am " + self.age + " years old."))


p1 = Person("Bill", 36)
p1.age = 100
p1.greeting()
del p1
```
Output:
> Hi, my name is Bill and I am 100 years old.

</summary> </details>


<details> <summary>Inheritance</summary>

In this example:
- Wizard is a subclass of the Person class found above
- The greeting method overrides it's parent's greeting 
- No written constructor, because sub/super instance variables identical 
```python
class Wizard(person):
    def greeting(self):
        print("I am a " + super.age +" year old wizard.")

w1 = Wizard("bob", 36)
w1.greeting()
```
output:
> I am a 36 year old wizard
</br>
#### Constructor override
- If a child has a constructor, it will override it's parent
- To get around this explicitly call the superclass constructor

```python
class Wizard(Person):
    def __init__(self, name, age, hasWand) 
        super().__init__(self, name, age)
        self.hasWand = hasWand
```

</summary> </details>

