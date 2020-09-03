# Recursion

## What is recursion?

Recursion is the process of repeating items in a self-similar way.

Algorithmically:
-   A way to design solutions to problems by **divide-and-conquer** or **decrease-and-conquer**.
    -   Reduce a problem to simpler versions of the same problem

Semantically:
-   A programming technique where a ***function calls itself***.
    -   In programming, the goal is to **NOT** have infinite recursion
    -   Must have **1 or more base cases** that are easy to solve
    -   Must solve the same problem on **some other input** with the goal of simplifying the larger problem input.

## Iterative Algorithms so Far

Looping constructs (`while` and `for` loops)

Can capture computation in a set of **state variables** that update on each iteration through a loop.

## Multiplication - Iterative Solution

"Multiply `a * b`" is equivalent to "add `a` to itself `b` times"

Capture **state** by having

-   an **iteration** number `i` that starts at b
    -   `i = i - 1` and stop when `i = 0`
-   a current **value of computation (result)**
    -   `result = result + a`

**Iterative Solution**:

```python
def mult_iter(a, b):
    result = 0
    while b > 0:
        result += a
        b -= 1
    return result      
```

## Multiplication - Recursive Solution

**Recursive Step**

-   Think of how to reduce the problem to a **simpler/smaller version** of the same problem.

**Base Case**

-   Keep reducing problem until it reaches a simple case that can be **solved directly.**
-   When `b = 1` then `a * b = a`

**Recursive Solution**:

```python
def mult(a, b):
	if b == 1:
		return a
	else:
        return a + mult(a, b - 1)
```

## Factorial

$n! = n * (n - 1) * (n - 2) * (n - 3) * ... * 1 $

For what `n` do we know factorial?

-   `n = 1`

```python
if n == 1:
	return 1
```

How to reduce problem? Rewrite in terms of something simpler to reach base case.

-   `n * (n - 1)!`

```python
else:
	return n * factorial(n - 1)
```

## Recursive Function Scope Example

```python
def fact(n):
	if n == 1:
		return 1
	else:
		return n * fact(n - 1)
		 
print(fact(4))
```

**Observations**:

-   Each recursive call to a function creates its **own scope/environment**.
-   **Bindings of variables** in a scope are not changed by a recursive call.
-   Flow of control passes back to the **previous scope** once function call returns value.

## Iteration vs. Recursion

**Iterative**:

```python
def factorial_iter(n):
	prod = 1
	for i in range(1, n + 1):
		prod *= i
	return prod
```

**Recursive**:

```python
def factorial(n):
	if n == 1:
		return 1
    else:
    	return n * factorial(n-1)
```

Recursion may be simpler, more intuitive.

Recursion may be efficient from programmer POV.

Recursion may not be efficient from computer POV.



