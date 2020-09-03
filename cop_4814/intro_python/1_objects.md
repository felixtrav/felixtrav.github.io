# Objects

Everything in Python is an object.

Programs in Python manipulate these data objects.

Objects have a type that defines the what a program can and can not do to them.

Objects can be:
-   Scalar
    -   Basic object type, can not be subdivided.
-   Non-Scalar
    -   Have internal structures that can be accessed and subdivided



## Scalar Objects

**int**

-   Represents integers - ex: ***5***

**float**

-   Represents real numbers - ex: ***3.27***

**bool** 

-   Represents Boolean values of ***True*** and ***False***

**NoneType**

-   Special object - has a value of ***None***

    

You can use the ***type()*** function to find an object type.

You can convert objects of one type to objects of another in a process called ***casting***.

```python
float(3) #converts integer 3 to float 3.0
int(3.9) #truncates float 3.9 to integer 3
```





## Expressions

Combine ***objects*** and ***operators*** to form expressions

An expression has a ***value***, which has a type

-   Every expression evaluates to a final value

The syntax for a simple expression is: 

-   ***<object> <operator> <object>***



### Operators

```python
i+j #gives the sum
i-j #gives the difference
i*j #gives the product
```

For these operators, if **both** the provided values are **int**, then the result will also be **int**.

However, if **either or both** of the values are **floats**, then the result will be a **float**.

```python
i/j #gives the quotient
```

The result is **always** a **float**

```python
i%j #gives the remainder of the division
i**j #gives i to the power of j
```



### Binding Variables and Values

An equal sign is an ***assignment*** of a value to a variable name

```python
pi = 3.14159
pi_approx = 22/7
```

The left side of the equal sign is the ***name***

The right side of the equal sign is the ***value***

An assignment ***binds*** the variable name to the value

Values are stored in computer memory

You can ***retrieve*** a ***value*** associated with a name or variable by ***invoking*** the name



#### Abstracting Expressions

Why give names to values of expressions?
-   To reuse names instead of values
-   Makes the code easier to read later on

```python
pi = 3.14159
radius = 2.2
area = pi*(radius**2)
```

This example is easier to read than the following:

```python
area = 3.14159*(2.2**2)
```

