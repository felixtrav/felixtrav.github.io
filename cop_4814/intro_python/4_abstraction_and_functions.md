# Abstractions and Functions



## Abstraction and Decomposition

### Abstraction

The idea of **abstraction** is that you do not need to know how a system works in order to use it
-   In programming, think of a piece of code as a **black box**
    -   You cannot see details
    -   Do not need to see details
    -   Do not want to see details
    -   Hides tedious coding details
-   Achieve abstraction with **function specifications** or **docstrings**

### Decomposition

The idea of **decomposition** is that different devices can work together to achieve an end goal
-   The problem of creating **structure** in code
-   Divide code into **modules **that
    -   are **self-contained**
    -   are used to **break up** code
    -   are intended to be **reusable**
    -   keep code **organized**
    -   keep code **coherent**



## Functions

Write **reusable** pieces/chunks of **code**, called functions

Functions are not run in a program until they are "**called**" or "**invoked**" in a program

Function characteristics:
-   Has a **name**
-   Has **parameters** (0 or more)
-   Has a **docstring** (optional but highly recommended)
-   Has a **body**
-   **Returns** something

```python
def is_even(i): #Function definition
	"""
	Input: i, a positive int
	Returns True if i is even, otherwise returns False
	""" #End docstring
	return i % 2 == 0 #Return statement
```

```is_even(3)``` returns False

```is_even(4)``` returns True

You are able to use functions as **arguments** in expressions

```python
def sum(x, y):
    return x + y

num = 10 + sum(1, 15)
```



If **NO return** statement is given, Python returns the value **None**

-   **None** represents the absence of a value



#### Variable Scope

**Formal parameter** gets bound to value of **actual parameter** when function is called

-   Formal parameter is the variable that gets **passed**
-   Actual parameter is the variable **used** by the function

New **scope/frame/environment** created when a function is entered

**Scope** is mapping of names to objects

```python
def f(x):
	x = x + 1
	print("In f(x): x =", x)
	return x
```

Inside a function, you **can access** a variable defined outside

Inside a function, you **cannot modify** a variable defined outside
-   The exception is **global variables**, but using that practice is frowned upon
    -   Global variables allow you to **disregard** scopes which leads to messy codes

```python
def f(y):
	x = 1
	x += 1
	print(x)
	
x = 5
f(x)
print(x)
```

Here, the variable ```x``` defined inside the function ```f``` is not interfering with the variable ```x``` outside

```python
def g(y)
	print(x)
	print(x + 1)
	
x = 5
g(x)
print(x)
```

Here, function ```g``` doesn't have a value ```x``` defined within it's scope, so instead it goes out to the scope of the code that called it to find ```x```

```python
def h(y):
	x +=1

x = 5
h(x)
print(x)
```

Here, function ```h``` is attempting to modify variable ```x``` that is outside of it's scope

-   This results in a ```UnboundLocalError: Local variable 'x' referenced before assignment``` error

```python
def g(x):
	def h():
		x = 'abc'
	x = x + 1
	print("g: x =", x)
	h()
	return x

x = 3
z = g(x)
```

This code shows how you can **nest functions** like you would statements