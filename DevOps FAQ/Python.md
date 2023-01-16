### 1. Write script to print statements in all possible ways that python allows?
```
print("Hello Python")
print('How r u')
print("Let's go for lunch")
print('He said,"I am busy today"')
print('He said,"Let\'s go for lunch"')
print("He said,\"Let's go for lunch\"")
```

### 2. How do you comment in python?
1. Single line comments start with #
2. Multiple line comments can start with '''  and end with ''' (or) start """ and end with """

### 3. How do you perform concatenation in python? 
```
print("Hello"+"Python")
print("Hi"+"5")
print("hi"+str(5))
print("8"+"5")
print("8"+str(5))
print(int("8")+5)
print("Hello","Python")
print("Hi",5)
```

### 4. How do you perform conditions in python? 
```
#if conditions
#Program to find the smallest of 3 numbers
a = 10
b = 20
c= 5
if a < b and a < c:
    print("a is the smallest ")
elif b < c:
    print("b is the smallest")
else:
    print("c is the smallest")
print("Program finished")
```

### 5. How do you perform loops in python? 
```
#Program to display the even numbers between 1-10
i = 2
while i <= 10:
    print(i)
    i = i + 2
```

### 6. How do you perform loops in python? 
1. while loop to display the 2 tables
```
i = 1
while i <= 10:
    print(2,"*",i,"=",2*i)
    i = i + 1
```
2. For Loops
```
a=[1,4,6,9,10]
for i in a:
    print(i)

tools=["Docker","Jenkins","Git","Ansible"]
for x in tools:
    print(x)
```
3. To display the sum of numbers in a list
```
numbers=[10,50,90,40,60]
sum = 0
for i in numbers:
    sum = sum + i
    
print("The total sum of numbers is: ",sum)
```
4. To find the max number in a list
```
numbers=[10,50,90,40,60]
max = 0
for i in numbers:
    if max < i:
        max = i

print("The maximum number in the list is :",max)
```
5. Program to find the number of even and odd
```
numbers=[1,2,3,4,5,6,7,8,9,10,11]
even = 0
odd = 0
for i in numbers:
    if i % 2 == 0:
        even = even + 1
        print("Even :",i)
    else:
        odd = odd + 1
        print("Odd :"i)

print("The even number count is :",even)
print("The odd number count is :",odd)
```

### 7. How do you perform read Write operations on Files?
1. To create a new file and write into it
```
text ="\nThis is a python session"
file=open("C:/Users/gandh/OneDrive/Desktop/file1.txt","w")
file.write(text)
```
2. To append we can open in append mode using 'a'
```
text ="\nThis is a python session"
file=open("C:/Users/gandh/OneDrive/Desktop/file1.txt","a")
file.write(text)
```
3. To read all the content of a file
```
file=open("C:/Users/gandh/OneDrive/Desktop/file1.txt","r")
text = file.read()
print(text)
```
4. To read the content line by line
```
file=open("C:/Users/gandh/OneDrive/Desktop/file1.txt","r")
text = file.readlines()
for x in text:
    print(x)
```
5. To copy all the content of a file into another file
```
file1=open("C:/Users/gandh/OneDrive/Desktop/file1.txt","r")
file2=open("C:/Users/gandh/OneDrive/Desktop/file2.txt","w")
text = file1.read()
file2.write(text)
```
6. To copy alternate lines of code from one file to another
```
file1=open("C:/Users/gandh/OneDrive/Desktop/file1.txt","r")
file3=open("C:/Users/gandh/OneDrive/Desktop/file3.txt","a")
text=file1.readlines()
i = 0
while i < len(text):
    file3.write(text[i])
    i = i + 2
```

### 8. What are Functions?
They are used for code resubality
```
def sum(a,b):
    print(a+b)
def sub(a,b):
    print(a-b)
def mul(a,b):
    print(a*b)
def div(a,b):
    print(a/b)

sum(10,20)
mul(4,5)
```

### 9. Create a predefined function to copy the content of a file into another 
```
def copy_file(srcfile,destfile):
    file1=open(srcfile,'r')
    file2=open(destfile,'w')
    text=file1.read()
    file2.write(text)

copy_file("path_file1","path_file2")
copy_file("path_file3","path_file4")
```

### 10. What are Classes and Objects?
Classes are logical entites which contian certain functionality while object is instance of class. The functions or attributes present in a class can be accessed only after an object is created.
```
class calculator:
    def add(self,a,b):
        print(a+b)
    def sub(self,a,b):
        print(a-b)
    def mul(self,a,b):
        print(a*b)
    def div(self,a,b):
        print(a/b)
    def exp(self,a,b):
        print(a**b)


c = calculator()
c.mul(10,10)
c.exp(2,4)
a = calculator()
a.add(10,5)
```

### 10. Write a script to import module in python?
```
import math
import calander
a=math.sqrt(16)
print(a)
a=math.factorial(4)
print(a)
print(calander.month(2020,10))
print(calander.isleap(2020)
```

### 11. Write an example custom module.
```
#Create a new pythin file "functions.py"
def area(length,breadth):
    area = length*breadth
    print("Area is : ",area)
def perimeter(length,breadth):
    print("Perimeter is : ",2*(length+breadth))

class myclass:
    def add(self,a,b):
        print(a+b)


#Create another python file and import the above "functions" module in it
import functions

functions.area(5,2)
functions.perimeter(5,2)

a=functions.myclass()
a.add(10,20)
```

### 12. Python Docker Automation
1. Python script to download docker images
```
import subprocess
image = input("Enter the image to be downloaded: ")

subprocess.call("docker pull %s"%image,shell=True)
```
2. Python script to create multiple containers from any docker image
```
import subprocess
image = input("Enter the docker image which has to be created as container: ")
count = input("Enter the number of containers that are to be created: ")
n = int(count)
i = 1
while  i <= n:
    subprocess.call("docker run --name container%d -d -P %s"%(i,image),shell=True)
    i = i + 1
```

### 13. What is the difference between list and tuples in Python?
1. Lists are mutable i.e they can be edited. Lists are slower than tuples.	
```
list_1 = [10, ‘Chelsea’, 20]
```
2. Tuples are immutable (tuples are lists which can’t be edited). Tuples are faster than list.
```
tup_1 = (10, ‘Chelsea’ , 20)
```

### 14 What are the key features of Python?
- Python is an interpreted language. That means that, unlike languages like C and its variants, Python does not need to be compiled before it is run. Other interpreted languages include PHP and Ruby.
- Python is dynamically typed, this means that you don’t need to state the types of variables when you declare them or anything like that. You can do things like x=111 and then x="I'm a string" without error
- Python is well suited to object orientated programming in that it allows the definition of classes along with composition and inheritance. Python does not have access specifiers (like C++’s public, private).
- In Python, functions are first-class objects. This means that they can be assigned to variables, returned from other functions and passed into functions. Classes are also first class objects
- Writing Python code is quick but running it is often slower than compiled languages. Fortunately，Python allows the inclusion of C-based extensions so bottlenecks can be optimized away and often are. The numpy package is a good example of this, it’s really quite quick because a lot of the number-crunching it does isn’t actually done by Python
- Python finds use in many spheres – web applications, automation, scientific modeling, big data applications and many more. It’s also often used as “glue” code to get other languages and components to play nice. Learn more about Big Data and its applications from the Data Engineering Training.

### 15. What type of language is python? Programming or scripting?
- Python is capable of scripting, but in general sense, it is considered as a general-purpose programming language. To know more about Scripting, you can refer to the Python Scripting Tutorial.

### 16. Python an interpreted language. Explain.
- An interpreted language is any programming language which is not in machine-level code before runtime. Therefore, Python is an interpreted language.

### 17. What is pep 8?
- PEP stands for Python Enhancement Proposal. It is a set of rules that specify how to format Python code for maximum readability.

### 18. What are the benefits of using Python?
The benefits of using python are:
-Easy to use– Python is a high-level programming language that is easy to use, read, write and learn.
Interpreted language– Since python is interpreted language, it executes the code line by line and stops if an error occurs in any line.
- Dynamically typed– the developer does not assign data types to variables at the time of coding. It automatically gets assigned during execution.
- Free and open-source– Python is free to use and distribute. It is open source.
Extensive support for libraries– Python has vast libraries that contain almost any function needed. It also further provides the facility to import other packages using Python Package Manager(pip).
- Portable– Python programs can run on any platform without requiring any change.
- The data structures used in python are user friendly.
- It provides more functionality with less coding.

### 19. What are Python namespaces?
A namespace in python refers to the name which is assigned to each object in python. The objects are variables and functions. As each object is created, its name along with space(the address of the outer function in which the object is), gets created. The namespaces are maintained in python like a dictionary where the key is the namespace and value is the address of the object. There 4 types of namespace in python-
- Built-in namespace– These namespaces contain all the built-in objects in python and are available whenever python is running.
- Global namespace– These are namespaces for all the objects created at the level of the main program.
- Enclosing namespaces– These namespaces are at the higher level or outer function.
- Local namespaces– These namespaces are at the local or inner function.

### 19. What are decorators in Python?
Decorators are used to add some design patterns to a function without changing its structure. Decorators generally are defined before the function they are enhancing. To apply a decorator we first define the decorator function. Then we write the function it is applied to and simply add the decorator function above the function it has to be applied to. For this, we use the @ symbol before the decorator.

### 20. What are Dict and List comprehensions?
Dictionary and list comprehensions are just another concise way to define dictionaries and lists.

1. Example of list comprehension is-
```
x=[i for i in range(5)]
# The above code creates a list as below-
#x= [0,1,2,3,4]
```
2. Example of dictionary comprehension is-
```
x=[i : i+2 for i in range(5)]
The above code creates a list as below-
x= [0: 2, 1: 3, 2: 4, 3: 5, 4: 6]
```

### 21. What are the common built-in data types in Python?
The common built-in data types in python are-
- Numbers– They include integers, floating-point numbers, and complex numbers. eg. 1, 7.9,3+4i
- List– An ordered sequence of items is called a list. The elements of a list may belong to different data types. Eg. [5,’market’,2.4]
- Tuple– It is also an ordered sequence of elements. Unlike lists , tuples are immutable, which means they can’t be changed. Eg. (3,’tool’,1)
- String– A sequence of characters is called a string. They are declared within single or double-quotes. Eg. “Sana”, ‘She is going to the market’, etc.
- Set– Sets are a collection of unique items that are not in order. Eg. {7,6,8}
- Dictionary– A dictionary stores values in key and value pairs where each value can be accessed through its key. The order of items is not important. Eg. {1:’apple’,2:’mango}
- Boolean– There are 2 boolean values- True and False.

### 22. What is the difference between .py and .pyc files?
The .py files are the python source code files. While the .pyc files contain the bytecode of the python files. .pyc files are created when the code is imported from some other source. The interpreter converts the source .py files to .pyc files which helps by saving time. You can get a better understanding with the Data Engineering Course in Washington.

### 23. What is slicing in Python?
 Slicing is used to access parts of sequences like lists, tuples, and strings. The syntax of slicing is-[start:end:step]. The step can be omitted as well. When we write [start:end] this returns all the elements of the sequence from the start (inclusive) till the end-1 element. If the start or end element is negative i, it means the ith element from the end. The step indicates the jump or how many elements have to be skipped. Eg. if there is a list- [1,2,3,4,5,6,7,8]. Then [-1:2:2] will return elements starting from the last element till the third element by printing every second element.i.e. [8,6,4].

### 24. What are Keywords in Python?
Keywords in python are reserved words that have special meaning.They are generally used to define type of variables. Keywords cannot be used for variable or function names. There are 33 keywords in python.

### 25. What are Literals in Python and explain about different Literals
A literal in python source code represents a fixed value for primitive data types. There are 5 types of literals in python-
- String literals– A string literal is created by assigning some text enclosed in single or double quotes to a variable. To create multiline literals, assign the multiline text enclosed in triple quotes. Eg.name=”Tanya”
- A character literal– It is created by assigning a single character enclosed in double quotes. Eg. a=’t’
- Numeric literals include numeric values that can be either integer, floating point value, or a complex number. Eg. a=50
- Boolean literals– These can be 2 values- either True or False.
- Literal Collections– These are of 4 types-
  - List collections-Eg. a=[1,2,3,’Amit’]
  - Tuple literals- Eg. a=(5,6,7,8)
  - Dictionary literals- Eg. dict={1: ’apple’, 2: ’mango, 3: ’banana`’}
  - Set literals- Eg. {“Tanya”, “Rohit”, “Mohan”}
  - Special literal- Python has 1 special literal None which is used to return a null variable.

### 26. How is memory managed in Python?
Memory is managed in Python in the following ways:
- Memory management in python is managed by Python private heap space. All Python objects and data structures are located in a private heap. The programmer does not have access to this private heap. The python interpreter takes care of this instead.
- The allocation of heap space for Python objects is done by Python’s memory manager. The core API gives access to some tools for the programmer to code.
- Python also has an inbuilt garbage collector, which recycles all the unused memory and so that it can be made available to the heap space.

### 27. What is namespace in Python?
A namespace is a naming system used to make sure that names are unique to avoid naming conflicts.

### 28. What is PYTHONPATH?
It is an environment variable which is used when a module is imported. Whenever a module is imported, PYTHONPATH is also looked up to check for the presence of the imported modules in various directories. The interpreter uses it to determine which module to load.

### 29. What are python modules? Name some commonly used built-in modules in Python?
Python modules are files containing Python code. This code can either be functions classes or variables. A Python module is a .py file containing executable code. Some of the commonly used built-in modules are:
- os
- sys
- math
- random
- data time
- JSON

### 30. What are local variables and global variables in Python?
- Global Variables: Variables declared outside a function or in global space are called global variables. These variables can be accessed by any function in the program.
- Local Variables: Any variable declared inside a function is known as a local variable. This variable is present in the local space and not in the global space.
```
a=2
def add():
    b=3
    c=a+b
    print(c)
add()

Output: 5
```
When you try to access the local variable outside the function add(), it will throw an error.

### 31.  Is python case sensitive?
Yes. Python is a case sensitive language.

### 32. What is type conversion in Python?
Type conversion refers to the conversion of one data type into another.
- int() – converts any data type into integer type
- float() – converts any data type into float type
- ord() – converts characters into integer
- hex() – converts integers to hexadecimal
- oct() – converts integer to octal
- tuple() – This function is used to convert to a tuple.
- set() – This function returns the type after converting to set.
- list() – This function is used to convert any data type to a list type.
- dict() – This function is used to convert a tuple of order (key, value) into a dictionary.
- str() – Used to convert integer into a string.
- complex(real,imag) – This function converts real numbers to complex(real,imag) number.

### 33.  What is the difference between Python Arrays and lists?
Arrays and lists, in Python, have the same way of storing data. But, arrays can hold only a single data type elements whereas lists can hold any data type elements.

Example:
```
import array as arr
My_Array=arr.array('i',[1,2,3,4])
My_list=[1,'abc',1.20]
print(My_Array)
print(My_list)

Output:
array(‘i’, [1, 2, 3, 4]) 
[1, ‘abc’, 1.2]
```

### 34.  What are functions in Python?
Ans: A function is a block of code which is executed only when it is called. To define a Python function, the def keyword is used.

Example:
```
def Newfunc():
    print("Hi, Welcome to Edureka")

Newfunc(); #calling the function
Output: Hi, Welcome to Edureka
```

### 35. What is __init__?
-  __init__ is a method or constructor in Python. This method is automatically called to allocate memory when a new object/ instance of a class is created. All classes have the __init__ method.

```
class Employee:
    def __init__(self, name, age,salary):
        self.name = name
        self.age = age
        self.salary = 20000

E1 = Employee("XYZ", 23, 20000)
# E1 is the instance of class Employee.
#__init__ allocates memory for E1. 
print(E1.name)
print(E1.age)
print(E1.salary)
```

### 36.What is a lambda function?
An anonymous function is known as a lambda function. This function can have any number of parameters but, can have just one statement.

```
a = lambda x,y : x+y
print(a(5, 6))
Output: 11
```
### 37. What is self in Python?
Self is an instance or an object of a class. In Python, this is explicitly included as the first parameter. It helps to differentiate between the methods and attributes of a class with local variables. The self variable in the init method refers to the newly created object while in other methods, it refers to the object whose method was called.

### 38. How does break, continue and pass work?
- Break Allows loop termination when some condition is met and the control is transferred to the next statement.
- Continue Allows skipping some part of a loop when some specific condition is met and the control is transferred to the beginning of the loop
- Pass Used when you need some block of code syntactically, but you want to skip its execution. This is basically a null operation. Nothing happens when this is executed.

### 39. What does [::-1] do?
-[::-1] is used to reverse the order of an array or a sequence.
For example:
```
import array as arr
My_Array=arr.array('i',[1,2,3,4,5])
My_Array[::-1]
Output: array(‘i’, [5, 4, 3, 2, 1])
```

[::-1] reprints a reversed copy of ordered data structures such as an array or a list. the original array or list remains unchanged.
 
### 40. How can you randomize the items of a list in place in Python?
```
from random import shuffle
x = ['Keep', 'The', 'Blue', 'Flag', 'Flying', 'High']
shuffle(x)
print(x)
```
The output of the following code is as below.
```
['Flying', 'Keep', 'Blue', 'High', 'The', 'Flag']
```

### 41. What are python iterators?
- Iterators are objects which can be traversed though or iterated upon.

### 42.How can you generate random numbers in Python?
- Random module is the standard module that is used to generate a random number. The Random class that is used and instantiated creates independent multiple random number generators. The method is defined as:

```
import random
random.random
```
The statement random.random() method return the floating-point number that is in the range of [0, 1). The function generates random float numbers. The methods that are used with the random class are the bound methods of the hidden instances. The instances of the Random can be done to show the multi-threading programs that creates a different instance of individual threads. The other random generators that are used in this are:
- randrange(a, b): it chooses an integer and define the range in-between [a, b). It returns the elements by selecting it randomly from the range that is specified. It doesn’t build a range object.
- uniform(a, b): it chooses a floating point number that is defined in the range of [a,b).Iyt returns the floating point number
- normalvariate(mean, sdev): it is used for the normal distribution where the mu is a mean and the sdev is a sigma that is used for standard deviation.

### 43. What is the difference between range & xrange?
- For the most part, xrange and range are the exact same in terms of functionality. They both provide a way to generate a list of integers for you to use, however you please. The only difference is that range returns a Python list object and x range returns an xrange object.
- This means that xrange doesn’t actually generate a static list at run-time like range does. It creates the values as you need them with a special technique called yielding. This technique is used with a type of object known as generators. That means that if you have a really gigantic range you’d like to generate a list for, say one billion, xrange is the function to use.
- This is especially true if you have a really memory sensitive system such as a cell phone that you are working with, as range will use as much memory as it can to create your array of integers, which can result in a Memory Error and crash your program. It’s a memory hungry beast.

### 44. What is pickling and unpickling?
Pickle module accepts any Python object and converts it into a string representation and dumps it into a file by using dump function, this process is called pickling. While the process of retrieving original Python objects from the stored string representation is called unpickling.

### 45. What are the generators in python?
Functions that return an iterable set of items are called generators.

### 46. How will you capitalize the first letter of string?
In Python, the capitalize() method capitalizes the first letter of a string. If the string already consists of a capital letter at the beginning, then, it returns the original string.

### 47. How will you convert a string to all lowercase?
To convert a string to lowercase, lower() function can be used.
```
stg='ABCD'
print(stg.lower())
Output: abcd
```
### 48. What are docstrings in Python?
Ans: Docstrings are not actually comments, but, they are documentation strings. These docstrings are within triple quotes. They are not assigned to any variable and therefore, at times, serve the purpose of comments as well.

```
"""
Using docstring as a comment.
This code divides 2 numbers
"""
```
### 49. What is the purpose of ‘is’, ‘not’ and ‘in’ operators?
Operators are special functions. They take one or more values and produce a corresponding result.
- is: returns true when 2 operands are true  (Example: “a” is ‘a’)
- not: returns the inverse of the boolean value
- in: checks if some element is present in some sequence

### 50. What is the usage of help() and dir() function in Python?
Help() and dir() both functions are accessible from the Python interpreter and used for viewing a consolidated dump of built-in functions. 
- Help() function: The help() function is used to display the documentation string and also facilitates you to see the help related to modules, keywords, attributes, etc.
- Dir() function: The dir() function is used to display the defined symbols.

### 51. Whenever Python exits, why isn’t all the memory de-allocated?
Whenever Python exits, especially those Python modules which are having circular references to other objects or the objects that are referenced from the global namespaces are not always de-allocated or freed.
It is impossible to de-allocate those portions of memory that are reserved by the C library.
On exit, because of having its own efficient clean up mechanism, Python would try to de-allocate/destroy every other object.

### 52. What is a dictionary in Python?
The built-in datatypes in Python is called dictionary. It defines one-to-one relationship between keys and values. Dictionaries contain pair of keys and their corresponding values. Dictionaries are indexed by keys.

```
dict={'Country':'India','Capital':'Delhi','PM':'Modi'}
print dict[Country]
Output:India

print dict[Capital]
Output:Delhi

print dict[PM]
Output:Modi
```

### 53. How can the ternary operators be used in python?
The Ternary operator is the operator that is used to show the conditional statements. This consists of the true or false values with a statement that has to be evaluated for it.

Syntax:
```
[on_true] if [expression] else [on_false]
```

### 54. What does this mean: *args, **kwargs? And why would we use it?
We use *args when we aren’t sure how many arguments are going to be passed to a function, or if we want to pass a stored list or tuple of arguments to a function. **kwargs is used when we don’t know how many keyword arguments will be passed to a function, or it can be used to pass the values of a dictionary as keyword arguments. The identifiers args and kwargs are a convention, you could also use *bob and **billy but that would not be wise.

### 55. What does len() do?
It is used to determine the length of a string, a list, an array, etc.

```
stg='ABCD'
len(stg)
Output:4
```

### 56. Explain split(), sub(), subn() methods of “re” module in Python.
To modify the strings, Python’s “re” module is providing 3 methods. They are:
- split() – uses a regex pattern to “split” a given string into a list.
- sub() – finds all substrings where the regex pattern matches and then replace them with a different string
- subn() – it is similar to sub() and also returns the new string along with the no. of replacements.

### 57. What are negative indexes and why are they used?
- The sequences in Python are indexed and it consists of the positive as well as negative numbers. The numbers that are positive uses ‘0’ that is uses as first index and ‘1’ as the second index and the process goes on like that.
- The index for the negative number starts from ‘-1’ that represents the last index in the sequence and ‘-2’ as the penultimate index and the sequence carries forward like the positive number.
- The negative index is used to remove any new-line spaces from the string and allow the string to except the last character that is given as S[:-1]. The negative index is also used to show the index to represent the string in correct order.

### 58. What are Python packages?
Python packages are namespaces containing multiple modules.

### 59. How can files be deleted in Python?
To delete a file in Python, you need to import the OS Module. After that, you need to use the os.remove() function.

```
import os
os.remove("xyz.txt")
```

### 60. What are the built-in types of python?
Built-in types in Python are as follows:
- Integers
- Floating-point
- Complex numbers
- Strings
- Boolean
- Built-in functions

### 61. What advantages do NumPy arrays offer over (nested) Python lists?
Python’s lists are efficient general-purpose containers. They support (fairly) efficient insertion, deletion, appending, and concatenation, and Python’s list comprehensions make them easy to construct and manipulate.
They have certain limitations: they don’t support “vectorized” operations like elementwise addition and multiplication, and the fact that they can contain objects of differing types mean that Python must store type information for every element, and must execute type dispatching code when operating on each element.
NumPy is not just more efficient; it is also more convenient. You get a lot of vector and matrix operations for free, which sometimes allow one to avoid unnecessary work. And they are also efficiently implemented.
NumPy array is faster and You get a lot built in with NumPy, FFTs, convolutions, fast searching, basic statistics, linear algebra, histograms, etc. 

### 62. How to add values to a python array?
Ans: Elements can be added to an array using the append(), extend() and the insert (i,x) functions.

```
a=arr.array('d', [1.1 , 2.1 ,3.1] )
a.append(3.4)
print(a)
a.extend([4.5,6.3,6.8])
print(a)
a.insert(2,3.8)
print(a)
Output:

array(‘d’, [1.1, 2.1, 3.1, 3.4])

array(‘d’, [1.1, 2.1, 3.1, 3.4, 4.5, 6.3, 6.8])

array(‘d’, [1.1, 2.1, 3.8, 3.1, 3.4, 4.5, 6.3, 6.8])
```

### 63. How to remove values to a python array?
Array elements can be removed using pop() or remove() method. The difference between these two functions is that the former returns the deleted value whereas the latter does not.
```
a=arr.array('d', [1.1, 2.2, 3.8, 3.1, 3.7, 1.2, 4.6])
print(a.pop())
print(a.pop(3))
a.remove(1.1)
print(a)
Output:
4.6
3.1
array(‘d’, [2.2, 3.8, 3.7, 1.2])
```
### 64. Does Python have OOps concepts?
Python is an object-oriented programming language. This means that any program can be solved in python by creating an object model. However, Python can be treated as a procedural as well as structural language.

Check out these AI and ML courses by E & ICT Academy NIT Warangal to learn Python usage in AI ML and build a successful career.

### 65. What is the difference between deep and shallow copy?
- Shallow copy is used when a new instance type gets created and it keeps the values that are copied in the new instance. Shallow copy is used to copy the reference pointers just like it copies the values. These references point to the original objects and the changes made in any member of the class will also affect the original copy of it. Shallow copy allows faster execution of the program and it depends on the size of the data that is used.
-  Deep copy is used to store the values that are already copied. Deep copy doesn’t copy the reference pointers to the objects. It makes the reference to an object and the new object that is pointed by some other object gets stored. The changes made in the original copy won’t affect any other copy that uses the object. Deep copy makes execution of the program slower due to making certain copies for each object that is been called.

### 66. How is Multithreading achieved in Python?
Python has a multi-threading package but if you want to multi-thread to speed your code up, then it’s usually not a good idea to use it. Python has a construct called the Global Interpreter Lock (GIL). The GIL makes sure that only one of your ‘threads’ can execute at any one time. A thread acquires the GIL, does a little work, then passes the GIL onto the next thread.
This happens very quickly so to the human eye it may seem like your threads are executing in parallel, but they are really just taking turns using the same CPU core. All this GIL passing adds overhead to execution. This means that if you want to make your code run faster then using the threading package often isn’t a good idea.

### 67. What is the process of compilation and linking in python?
The compiling and linking allow the new extensions to be compiled properly without any error and the linking can be done only when it passes the compiled procedure. If the dynamic loading is used then it depends on the style that is being provided with the system. The python interpreter can be used to provide the dynamic loading of the configuration setup files and will rebuild the interpreter.

The steps that are required in this as:
- Create a file with any name and in any language that is supported by the compiler of your system. For example file.c or file.cpp
- Place this file in the Modules/ directory of the distribution which is getting used.
- Add a line in the file Setup.local that is present in the Modules/ directory.
- Run the file using spam file.o
- After a successful run of this rebuild the interpreter by using the make command on the top-level directory.
- If the file is changed then run rebuildMakefile by using the command as ‘make Makefile’.

### 68. What are Python libraries? Name a few of them.
Python libraries are a collection of Python packages. Some of the majorly used python libraries are – Numpy, Pandas, Matplotlib, Scikit-learn and many more.

### 69. What is split used for?
The split() method is used to separate a given String in Python.
```
a="edureka python"
print(a.split())
Output:  [‘edureka’, ‘python’]
```

### 70. How to import modules in python?
Modules can be imported using the import keyword.  You can import modules in three ways-

```
import array           #importing using the original module name
import array as arr    # importing using an alias name
from array import *    #imports everything present in the array module
```

### 71. Explain Inheritance in Python with an example.
Inheritance allows One class to gain all the members(say attributes and methods) of another class. Inheritance provides code reusability, makes it easier to create and maintain an application. The class from which we are inheriting is called super-class and the class that is inherited is called a derived / child class.

They are different types of inheritance supported by Python:
- Single Inheritance – where a derived class acquires the members of a single super class.
- Multi-level inheritance – a derived class d1 in inherited from base class base1, and d2 are inherited from base2.
- Hierarchical inheritance – from one base class you can inherit any number of child classes
- Multiple inheritance – a derived class is inherited from more than one base class.

### 72.  How are classes created in Python? 
Class in Python is created using the class keyword.
```
class Employee:
    def __init__(self, name):
        self.name = name

E1=Employee("abc")
print(E1.name)
Output: abc
```

### 73. What is monkey patching in Python?
In Python, the term monkey patch only refers to dynamic modifications of a class or module at run-time.
```
# m.py
class MyClass:
    def f(self):
        print "f()"
```
We can then run the monkey-patch testing like this:
```
import m
def monkey_f(self):
    print "monkey_f()"
 
m.MyClass.f = monkey_f
obj = m.MyClass()
obj.f()
The output will be as below:
monkey_f()
```
As we can see, we did make some changes in the behavior of f() in MyClass using the function we defined, monkey_f(), outside of the module m.

### 74. Does python support multiple inheritance?
Multiple inheritance means that a class can be derived from more than one parent classes. Python does support multiple inheritance, unlike Java.

### 75. What is Polymorphism in Python?
Polymorphism means the ability to take multiple forms. So, for instance, if the parent class has a method named ABC then the child class also can have a method with the same name ABC having its own parameters and variables. Python allows polymorphism.

### 76. Define encapsulation in Python?
Encapsulation means binding the code and the data together. A Python class in an example of encapsulation.

### 77. How do you do data abstraction in Python?
Data Abstraction is providing only the required details and hiding the implementation from the world. It can be achieved in Python by using interfaces and abstract classes.

### 78. Does python make use of access specifiers?
Python does not deprive access to an instance variable or function. Python lays down the concept of prefixing the name of the variable, function or method with a single or double underscore to imitate the behavior of protected and private access specifiers.  

### 79. How to create an empty class in Python? 
Ans: An empty class is a class that does not have any code defined within its block. It can be created using the pass keyword. However, you can create objects of this class outside the class itself. IN PYTHON THE PASS command does nothing when its executed. it’s a null statement. 
```
class a:
  pass

obj=a()
obj.name="xyz"
print("Name = ",obj.name)
Output: 

Name =  xyz
```

### 80. What does an object() do?
- It returns a featureless object that is a base for all classes. Also, it does not take any parameters.
Next, let us have a look at some Basic Python Programs in these Python Interview Questions.
Basic Python Programs – Python Interview Questions

### 81.  Write a program in Python to execute the Bubble sort algorithm.
```
def bs(a):
# a = name of list
   b=len(a)-1nbsp; 
# minus 1 because we always compare 2 adjacent values
   for x in range(b):
        for y in range(b-x):
              a[y]=a[y+1]
   
   a=[32,5,3,6,7,54,87]
   bs(a)
Output:  [3, 5, 6, 7, 32, 54, 87]
```

### 82. Write a program in Python to produce Star triangle.
```
def pyfunc(r):
    for x in range(r):
        print(' '*(r-x-1)+'*'*(2*x+1))    
pyfunc(9)
Output:

        *
       ***
      *****
     *******
    *********
   ***********
  *************
 ***************
*****************
```

### 83. Write a program to produce Fibonacci series in Python.
```
# Enter number of terms needednbsp;#0,1,1,2,3,5....
a=int(input("Enter the terms"))
f=0;#first element of series
s=1#second element of series
if a=0:
   print("The requested series is",f)
else:
  print(f,s,end=" ")
   for x in range(2,a): 
         print(next,end=" ")
         f=s
         s=next
 

Output: Enter the terms 5 0 1 1 2 3
```

### 84. Write a program in Python to check if a number is prime.
```
a=int(input("enter number"))
if a=1:
   for x in range(2,a):
         if(a%x)==0:
          print("not prime")
   break
   else:
      print("Prime")
else:
   print("not prime")
Output:

enter number 3

Prime
```

### 85. Write a program in Python to check if a sequence is a Palindrome.
```
a=input("enter sequence")
b=a[::-1]
if a==b:
  print("palindrome")
else:
  print("Not a Palindrome")
Output:

enter sequence 323 palindrome
```

## 86. Write a one-liner that will count the number of capital letters in a file. Your code should work even if the file is too big to fit in memory.
Let us first write a multiple line solution and then convert it to one-liner code.
```
with open(SOME_LARGE_FILE) as fh:
count = 0
text = fh.read()
for character in text:
    if character.isupper():
count += 1
```
We will now try to transform this into a single line.
```
count sum(1 for line in fh for character in line if character.isupper())
```

## 87.  Write a sorting algorithm for a numerical dataset in Python.
The following code can be used to sort a list in Python:
```
list = ["1", "4", "0", "6", "9"]
list = [int(i) for i in list]
list.sort()
print (list)
```

## 88. Looking at the below code, write down the final values of A0, A1, …An.
```
A0 = dict(zip(('a','b','c','d','e'),(1,2,3,4,5)))
A1 = range(10)A2 = sorted([i for i in A1 if i in A0])
A3 = sorted([A0[s] for s in A0])
A4 = [i for i in A1 if i in A3]
A5 = {i:i*i for i in A1}
A6 = [[i,i*i] for i in A1]

print(A0,A1,A2,A3,A4,A5,A6)
Ans: The following will be the final outputs of A0, A1, … A6


A0 = {'a': 1, 'c': 3, 'b': 2, 'e': 5, 'd': 4} # the order may vary
A1 = range(0, 10) 
A2 = []
A3 = [1, 2, 3, 4, 5]
A4 = [1, 2, 3, 4, 5]
A5 = {0: 0, 1: 1, 2: 4, 3: 9, 4: 16, 5: 25, 6: 36, 7: 49, 8: 64, 9: 81}
A6 = [[0, 0], [1, 1], [2, 4], [3, 9], [4, 16], [5, 25], [6, 36], [7, 49], [8, 64], [9, 81]]
```



























































































