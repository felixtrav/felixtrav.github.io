# String Manipulations and Algorithms



## String Manipulation

Think of strings as a **sequence** of **case sensitive** characters

You can **compare** strings with **==**, **>**, **<**, etc.

The ```len()``` function is used to get the **length** of the string in the parenthesis.

Strings are ***immutable*** - cannot be modified

```python
s = "hello"
s[0] = 'y' #Gives an error
s = 'y'+s[1:len(s)] #Is allowed | s is bound to a new object
```

#### Indexing

Square brackets can be used to perform **indexing** into a string to get the value at a certain index/position
-   ```s = "abc"```
-   ```s[0]``` evaluates to "**a**"
-   ```s[1]``` evaluates to "**b**"
-   ```s[2]``` evaluates to "**c**"
-   ```s[3]``` trying to index **out of bound** gives an **error**
-   ```s[-1]``` evaluates to "**c**"
-   ```s[-2]``` evaluates to "**b**"
-   ```s[-3]``` evaluates to "**a**"

#### Slicing

You can **slice** strings using ```[start:stop:step]```

If you give only 2 numbers (```[start,stop]```), then ```step = 1 ```by **default**

You may also **omit** numbers and just leave colons
-   ```s = "abcdefgh"```
-   ```s[3:6]``` evaluates to ```def```, same as ```s[3:6:1]```
-   ```s[3:6:2]``` evaluates to ```df```
-   ```s[::]``` evaluates to ```abcdefgh```, same as ```s[0:len(s):1]```
-   ```s[::-1]``` evaluates to ```hgfedbca```, same as ```s[-1:-(len(s)+1:-1]```
-   ```s[4:1:-2]``` evaluates to ```ec```



#### Iterating Through Strings

There are multiple ways to **iterate**, or loop through, the **characters** of a **string**

```python
s = "abcdefgh"

for index in range(len(s)):
	if s[index] == "i" or s[index] == "u":
		print("There is an i or u")
		
for char in s:
	if char == 'i' or char == 'u':
		print("There is an i or u")
	
```

Both loops **iterate** through the **string**, however the bottom loop is more "***pythonic***" and **easier** to **read**



## Algorithms

#### Guess and Check

```python
cube = 8
for guess in range(cube+1):
	if guess**3 == cube:
		print("Cube root of", cube, "is", guess)   
```

Checks for the **cube root** of a number, however it does not work for numbers that are not perfect cubes.

#### Approximate Solutions

**Good enough** solution

Start with a **guess** and **increment** by some **small value**

Keep guessing if $|guess^3-cube| >= epsilon$ for some small epsilon

**Decreasing increment** size will give you a **slower program**

**Increasing epsilon** will give you a **less accurate** answer

```python
cube = 27
epsilon = 0.01
guess = 0.00
increment = 0.0001
num_guesses = 0

while abs(guess**3 - cube) >= epsilon and guess <= cube:
	guess += increment
	num_guesses += 1

print("num_guesses ="", num_guesses)

if abs(guess**3 - cube) >= epsilon:
	print("Failed on cube root of", cube)
else:
	print(guess, "is close to the cube root of", cube)  
```

#### Bisection Method

Half interval each iteration

New guess is halfway in between

```python
cube  = 27
epsilon = 0.01
num_guesses = 0
low = 0
high = cube
guess = (high + low)/2.0

while abs(guess**3 - cube) >= epsilon:

	if guess**3 < cube:
		low = guess
	else:
		high = guess
		
	guess = (high + low)/2.0
	num_guesses += 1

print ("num_guesses =", num_guesses)
print (guess, "is close to the cube root of", cube)
```

Search space
-   First guess: $N/2$
-   Second guess: $N/4$
-   k^th^ guess: $\frac{N}{2^k}$

$\frac{N}{2^k} = 1$

$2^k = N$

$k = log_2N$

-   Guess converges on the order of $log_2N$ steps
-   Bisection search works when value of function varies monotonically with input

Code as shown only works for positive cubes > 1 --- why?

**Challenge**:
-   Modify the code to work with negative cubes
-   Modify to work with x < 1

