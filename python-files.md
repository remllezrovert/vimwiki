
# Python file handling

- [python](python.md) </br>
- [index](index.md) </br>

<hr>

- Use the "r" character to read
- Use the "a" character to append
- Use the "w" character to overwrite
- Ues the "x" character to create new file
<details> <summary>Reading</summary>

- This loop reads out every line in the file
- Remember to close files after use
```python
f = open("/home/remllez/exampleFile.txt", "r")
for x in f:
    print(x)
f.close()
```

- Read 5 characters from the file
- Leave the read() method empty to read entire file
- No path needed if files in the same dir
```python
f = open("exampleFile.txt", "r")
print(f.read(5)) 
f.close()
```

- Open a file on the device with it's path 
- Read the first two lines of the file
```python
f = open("/home/remllez/exampleFile.txt", "r")
print(f.readline()) #Reads the first line
print(f.readline()) #Reads the second line
f.close()

```
</summary> </details>


#### Appending
- Append onto the end of the file
```python
f = open("exampleFile.txt", "a")
f.write("Now the file has more content!")
f.close()
```
#### Writing
- Wipes the file and starts from scratch
```
f = open("/home/remllez/exampleFile.txt", "w")
f.write("Woops! I have deleted the content!")
f.close()
```
#### Deleting
- Use 'os.remove()' to delete files
- Use 'os.rmdir()'  to delete directories 
```python
import os
if os.path.exists("exampleFile.txt"):
  os.remove("exampleFile.txt")
else:
  print("The file does not exist") 
```





