- Dynamically typed programming language
# Data Types

## Primitive

- int : `10`
- string : `name` , sequence of characters
- boolean : `True/False`
- complex : `3 + 5j`
## Collections

- List :  `[]`
- Touple : `()`
- Set : `{}`
- Dictionary/Map : `{}`

# Arithmetic Operators

- Addition : `+`
- Subtraction : `-` 
- Division : `/`
- Multiplication : `*` 
- Modulo : `%`
- Power : `**`

```python
>>> a = 10;
>>> b = 3;
>>> >>> a*b
30
>>> a+b
13
>>> a-b
7
>>> a/b
3.3333333333333335
>>> a%b
1
>>> a**b
1000
```
# Relational Operators

- Greater than : `>` 
- Less than : `<`
- Greater than equal to : `>=`
- Less than equal to  : `<=`
- Equal to : `==`
- Not equal to : `!=`

```python
>>> 10>=10
True
>>> 5 <= 10
True
>>> 10 > 5
True
>>> 10 < 5
False
>>> 5 <= 10
True
>>> 5 >= 10
False
>>> 5!=10
True
>>> 5 == 10
False
```

# Logical Operators

- AND
- OR
- NOT

```python

>>> not True
False
>>> not False
True
>>> 10 > 5 and 15 < 10
False
>>> 10 > 5 and 15 > 10
True
>>> 10 > 15 or 15 < 10
False
>>> 10 < 15 or 15 < 10
True
```

# Identity Operators

- is 
- is not

```python
>>> a = 10
>>> b = 15
>>> a is b
False
>>> a = 10
>>> b = 10
>>> a is b
True
>>> a is not b
False
```

# Membership Operators

- in
- not in

```python
>>> s = "I love India"
>>> "In" in s
True
>>> "Ins" in s
False
>>> "Ins" not in s
True 
```
# Run Python Program

- Interpreter Mode (CLI Mode)
- Batch Mode : `$ python program.py`
# Variables

- `variable_name = value`
- Should not start with a number
- Keywords cannot be used for variable names
- Spaces do not work

```python
>>> a = 10;
>>> b = 10;
>>> type(a)
<class 'int'>
>>> name = True
>>> name
True
>>> type(name)
<class 'bool'>
>>> cmp = 3 + 4j
>>> type(cmp)
<class 'complex'>
>>> cmp
(3+4j)
>>> l = {10,20}
>>> type(l)
<class 'set'>
>>> m = [10,20]
>>> type(m)
<class 'list'>
>>> n = (10,20)
>>> type(n)
<class 'tuple'>
>>> o = {"IND":91, "USA":1}
>>> type(o)
<class 'dict'>
>>> type(x)
<class 'float'>
```

```python
# Python Program to find Area of Circle
# Run Command : python main.py

radius = 10
areaOfCircle = 3.14*radius**2
print(areaOfCircle)
```

```python
# Python Program to find Discounted Price
# Run Command : python main.py

name = "Mobile"
price = 25000
quantity = 2 
discount = 10

total = price * quantity
discounted = (total * discount)/100
final = total - discounted
print(final)
```

# Take Input

```python
# Take input from the user
# Run Command : python main.py

name = input("Product Name: ")
price = float(input("Product Price: "))
quantity = int(input("Quantity: "))
discount = float(input("Discount: "))

totalPrice = price * quantity
discountedPrice = (totalPrice * discount)/100
finalPrice = totalPrice - discounted

print("For {1} {0}'s you have saved {2} and you need to pay {3}".format(name, quantity,discounted,finalPrice))
```

```python
# Take input from the command line 
# Run Command : python main.py "name" age

from sys import argv

name = argv[1]
age = argv[2]

print("My name is {0} and I am {1} years old.".format(name, age))
```

# Flow control statements

- Sequential Execution : Program is executed line by line
- Decision Making : if/else statements
- Loop : For Loop and While Loop
## If/else

```python
# If Else Program with Single Condition
# Run Command: python main.py age

from sys import argv

age = int(argv[1])

if age >= 18 :
	print("You are eligible for voting!")
else : 
	print("You are not eligible for voting!")

# Output

$ python3 main.py 26
You are eligible for voting!
$ python3 main.py 16
You are not eligible for voting!
```

```python
# If Else Program with Multiple Conditions
# Run Command: python main.py username password

from sys import argv

username = argv[1]
password = argv[2]

if username == "admin" and password == "admnin@123" :
	print("Login Successful!")
else :
	print("Incorrect username or password!")

# Output

$ python main.py "admin" "admin@123"
Login Successful!
$ python main.py "admin" "12345678"
Incorrect username or password!
```

```python
# If Else ladder
# Run Command : python main.py marks

from sys import argv

marks = int(argv[1])

if marks >= 70 : 
	print("Grade : A")
elif marks >= 60 :
	print("Grade : B")
elif marks >= 50 :
	print("Grade : C")
elif marks >= 40 :
	print("Grade : D")
elif marks >= 35 :
	print("Grade : Pass")
else :
	print("Grade : Fail)

# Output

$ python3 main.py 80
Grade : A
$ python3 main.py 35
Grade : Pass
$ python3 main.py 34
Grade : Fail
$ python3 main.py 41
Grade : D
$ python3 main.py 51
Grade : C
$ python3 main.py 61
Grade : B
$ python3 main.py 71
Grade : A
```

```python
# Nested If Else
# Run Command : python main.py "admin" "admin@123"

from sys import argv

username = argv[1]
password = argv[2]

if username == "admin" :
	if password == "admin@123" :
		print("Login Successful!")
	else :
		print("Incorrect Password!")
else :
	print("Incorrect Username!")

# Output

$ python main.py admin admin@123
Login Successful!
$ python main.py admin admin@1234
Incorrect Password!
$ python main.py guest admin@123
Incorrect Username!
```

## For

```python
# Simple For Loop

>>> for x in range(6): print(x)
...     
0
1
2
3
4
5
>>> for i in range(5, 0, -1): print(i)
... 
5
4
3
2
1
>>> for i in range(0,5,1) : print("India")
... 
India
India
India
India
India
>>> for i in ["SUN", "MON", "TUE", "WED", "THU", "FRI", "SAT"] : print(i)
... 
SUN
MON
TUE
WED
THU
FRI
SAT
```

```python
# Program to print numbers divisible by 3 from 0 to 1000
# Run Command : python main.py

for x in range(3,1001,3) :
	if x%3 == 0 and x%6 == 0 and x%9 == 0 :
		print(x)	

# Output

$ python main.py 
18
36
54
72
90
108
126
144
.
.
.
990
```
## While

```python
# Infinite While Loop
# Run Command : python main.py

while True :
	print("India")

# Output

$ python main.py
India
India
India
India
India
.
.
.
```

```python
# Increment 
# Run Command : python main.py

num = 0
while num <= 5 :
	print(num)
	num = num + 1

# Output

$ python main.py 
0
1
2
3
4
5
```

```python
# Decrement 
# Run Command : python main.py

num = 10
while num >= 5 :
	print(num)
	num = num - 1

# Output

$ python main.py 
10
9
8
7
6
5
```

```python
# Nested For Loop
# Run Command : python main.py

for i in ["SUN", "MON", "TUE", "WED", "THU", "FRI", "SAT"] :
	for j in ["WORKING", "HOLIDAY"] :
		print(i,j)

# Output

$ python main.py 
SUN WORKING
SUN HOLIDAY
MON WORKING
MON HOLIDAY
TUE WORKING
TUE HOLIDAY
WED WORKING
WED HOLIDAY
THU WORKING
THU HOLIDAY
FRI WORKING
FRI HOLIDAY
SAT WORKING
SAT HOLIDAY
```

```python
# Nested For Loop with If else
# Run Command : python main.py

for i in ["SUN", "MON", "TUE", "WED", "THU", "FRI", "SAT"] :
	for j in ["WORKING", "HOLIDAY"] :
		if (i in ("SAT", "SUN")) and (j in ("HOLIDAY")) :
			print(i,j)
		if (i not in ("SAT", "SUN")) and (j not in ("HOLIDAY")) :
			print(i,j)

# Output

$ python main.py 
SUN HOLIDAY
MON WORKING
TUE WORKING
WED WORKING
THU WORKING
FRI WORKING
SAT HOLIDAY
```

```python
# break statement : Break out of current loop
# Run Command : python main.py

for i in range(1,10) :
	if i == 5 :
		break
	print(i)

# Output

$ python main.py 
1
2
3
4
```

```python
# continue statement : Skip the current iteration
# Run Command : python main.py

for i in range(1,10) :
	if i == 5 :
		continue
	print(i)

# Output

$ python main.py 
1
2
3
4
6
7
8
9
```

```python
# pass : Placeholder for a code block
# Run Command : python main.py

for i in range(1,10) :
	pass
if 1 <= 5 :
	pass

# Output

$ python main.py

$
```

# String

 - Sequence of characters
 - Case sensitive
 - Index starts at 0
 - Supports -ve indexing
## Access String

### Using Index

```python
>>> str = "I love India"
>>> str[0]
I
>>> str[3]
o
```
### Using For Loop

```python
# Print String characters using For Loop
# Run Command : python main.py

str = "I Love India"

for i in str :
	print(i)

# Output
$ python main.py
I
 
L
o
v
e
 
I
n
d
i
a
```
### Using slicing

```python
>>> greet="Good Morning"
>>> greet[0:12:1]
'Good Morning'
>>> greet[0:12]
'Good Morning'
>>> greet[0:]
'Good Morning'
>>> greet[:]
'Good Morning'
>>> greet[3:8]
'd Mor'
>>> greet[6:10]
'orni'
>>> greet[4:10:2]
' on'
>>> greet[9:2:-1]
'inroM d'
>>> greet[::-1]
'gninroM dooG'
```
## String Operations

### String Formatting

```python
# Ways to Declare String
# Run Command : python main.py

s = 'Niranjan'

str = "This some text"

str1 = ''' 
This
is 
a 
String '''

str2 = """
This
is
also
a 
String """

# String Formatting

name = "Mobile"
price = 25000
quantity = 2 
discount = 10

totalPrice = price * quantity
discountedPrice = (totalPrice * discount)/100
finalPrice = totalPrice - discountedPrice

print("For",quantity,name,"s you have saved",discounted,"and you need to pay", final,".")

print("For {1} {0}'s you have saved {2} and you need to pay {3}.".format(name, quantity,discountedPrice,finalPrice))

print("For {} {}'s you have saved {} and you need to pay {}.".format(quantity, name, discountedPrice,finalPrice))
```

### String Concatenation

```python
>>> fname = "Niranjan"
>>> lname = "Fartare"
>>> fname + lname
'NiranjanFartare'
>>> fname + " " + lname
'Niranjan Fartare'
```

### String Multiplication

```python
>>> greet = "Good Morning"
>>> greet*5
'Good MorningGood MorningGood MorningGood MorningGood Morning'
```

###  Identity Operators

```python
>>> str = "Pune"
>>> str1 = "pune"
>>> str is str1
False
>>> str is not str1
True
>>> 
```

### Membership Operators

```python
>>> str = "Good Morning"
>>> "Good" in str
True
>>> "IN" in str
False
>>> "IN" not in str
True
>>> "Good" not in str
False
```

# Functions

-  Reusable block of code

## Inbuilt Functions

- `print()` : Prints anything in the `()`, `print("Hello World!")`
- `type()` : Prints datatype of the variables, `a = 100`
- `input()` : Take input from the user, `name = input("Enter your age: ")`
- `range()` : Generate sequence of numbers, `range(start, stop, step)`
	- Prints sequence from `start` to `stop-1`  increasing/decreasing by `step`

```python
# range()

>>> for x in range(1,10,1): print(x)
... 
1
2
3
4
5
6
7
8
9
>>> for i in range(5, 0, -1): print(i)     
... 
5
4
3
2
1
>>> 
```
# String Functions

- `lower()`
- `upper()`
- `title()`
- `len()`
- `count()`
- `find()`
- `trim()`

```python
>>> str
'Good Morning'
>>> str.lower()
'good morning'
>>> str.upper()
'GOOD MORNING'
>>> str.title()
'Good Morning'
>>> len(str)
12
>>> str.strip # Removes extra space from the Left and Right
'Good Morning'
>>> str.count('o')
3
>>> str.find("India")
7
>>> str.find("USA") # Not Found
-1
>>> str.find("USA") 
-1
>>> str.replace("Love", "Like")
'I Like India, India is a developing country'
>>> str.replace(',',';')
'I Love India; India is a developing country'
>>> str.replace(" ", "")
'ILoveIndia,Indiaisadevelopingcountry'
>>> names = "Niranjan,Ganesh,Gaurav"
>>> names.split(',')
['Niranjan', 'Ganesh', 'Gaurav']
>>> "niranjan@gmail.com".split('@')
['niranjan', 'gmail.com']
>>> greet.swapcase()
'gOOD mORNING'
>>> str.isalnum()
False
>>> str.isalpha()
False
>>> str.isdigit()
False
>>> "101".isdigit()
True
```

# User Defined Functions (UDFs)

- Parameterized Functions
- Non Parameterized Functions

```python
# Non Parameterized Functions
# Run Command : python main.py

def display():
    print("This is the display function.")

def greetings():
    print("Hello, Welcome!")

display()
greetings()

# output

$ python main.py 
This is the display function.
Hello, Welcome!

```

```python
# Parameterized Functions
# Run Command : python main.py

def sum(a,b):
	print(a+b)
def greetigs(name):
	print("Welcome!, {}!!".format(name))
sum(100+200)
greetings("Niranjan")

# Output

$ python main.py 
300
Welcome!, Niranjan!! 
```

```python
def sub(a,b):
	print("a =",a)
	print("b =",b)
	print(a+b)
sub(b=100,a=50)

```

```python
# Program to find salary after tax deduction, 10% income tax, 7% Policy Premium and 200 Professional tax
# Run Command : python main.py "Niranjan" 100000

from sys import argv

name = argv[1]
sal = float(argv[2])

def inHandSal(name, sal):
    print("Hello, {0}, your in hand salary after tax deduction is {1}.".format(name, sal - (sal * 0.10) - (sal * 0.07) - 200))
inHandSal(name, sal)
```
