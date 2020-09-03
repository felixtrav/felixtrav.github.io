# Control Flow



## Strings

Sequences of ***characters***

-   Letters, special characters, spaces, digits

Are enclosed in ***quotation marks*** or ***single quotes***

```python
hi = "hello there"
```

You are able to ***concatenate*** strings

```python
name = "ana"
greeting = hi + name #hello thereana
greeting = hi + " " + name #hello there ana
```

String support some operations as defined in Python documentation

```python
silly = hi + " " + name * 3 #hello there anaanaana
```



## input("")

Prints whatever is in the quotes

User types in something and presses enter

-   What the user **enters** is now **bound** to a variable

```python
text = input("Type anything...")
print(5*text)
```

The input function gives you a string so you must cast it if working with numbers

```python
num = int(input("Type a number..."))
print(5*num)
```



## Operators



### Comparison Operators

Assume **i** and **j** are variable names.

The comparisons below evaluate to a ***Boolean*** 

-   ```i > j```
-   ```i >= j```
-   ```i < j```
-   ```i <= j```
-   ```i == j```
    -   ***Equality*** test, **True** if **i** is the **same** as **j**
-   ```i != j```
    -   ***Equality*** test, **True** if **i** is **not** the same as **j**



### Logic Operators on Booleans

Assume **a** and **b** are variable names with ***Boolean*** values

```python
not a #True if a is False | False if a is True
a and b #True if both are True
a or b #True if either or both are True
```

Some of these values can be represented in a table:

| A     | B     | A and B | A or B |
| :---- | ----- | ------- | ------ |
| True  | True  | True    | True   |
| True  | False | False   | True   |
| False | True  | False   | True   |
| False | False | False   | False  |



## Control Flow



#### if statements

To make decisions, programs use ***if*** statements to evaluate a condition.

-   If the condition is ***True***, then the expressions in the code block will be run.

```python
if <condition>:
	<expression>
	<expression>
	...
```

These ***if*** statements can also have an evaluation for when the condition is ***False***.
-   If the condition if ***True***, then the expressions in the ***if*** code block will be run.
-   If the condition is ***False***, then the expressions in the ***else*** code block will be run.

```python
if <condition>:
	<expression>
	<expression>
	...
else:
	<expression>
	<expression>
	..
```

If more than one choice is needed, then ***if*** statements can be used in a sequential manner.
1.  If the first condition is ***True***, then run the expressions in the ***if*** code block.
2.  If the first condition is ***False***, then try following condition.
3.  If the following condition is ***True***, run the expressions in the ***elif*** code block.
4.  If the following condition is ***False***, run the expressions in the ***else*** code block.

```python
if <condition>:
	<expression>
	<expression>
	...
elif <condition>:
	<expression>
	<expression>
	...
else:
	<expression>
	<expression>
	..
```



#### while Loops

If the condition is ***True***, evaluate all the expressions inside the code block, then check the condition again. If the condition is still ***True***, keep repeating until the condition is ***False***.

```python
while <condition>:
	<expression>
	<expression>
	...
```



#### for Loops

Each time through the loop the variable takes a **different value** and evaluates the expressions in the code block. Keeps evaluating through each iteration until the variable range is exhausted.

```python
for <variable> in range(<some_num>):
    <expression>
    <expression>
    ...
```

The **range** function can be modified.
-   ```range(start, stop, step)```
-   Default values are ```start = 0``` and ```step = 1```
-   Loops until value is ```stop - 1```
-   Defined values must be **int**



#### break Statement

The ```break``` statement **immediately exits** whatever **loop** it is in.

It **skips** the **remaining expressions** in the code block.

It **only exits** the **innermost loop**.



