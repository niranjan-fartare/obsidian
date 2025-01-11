- Dynamically typed programming language
# Data Types

## Primitive

- int : `10`
- string : `name`
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

# Inbuilt Functions

- `print()` : Prints anything in the, `print("Hello World!")`
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

# String Formatting

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