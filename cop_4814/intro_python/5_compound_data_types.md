# Compound Data Types



## Tuples

**Strings** are **sequences** of **characters**

**Tuples** are similar to strings, as they are **sequences** of other ***data types***

-   You can have **multiple data types** in the same tuple

Tuples are **immutable** just like strings

They are represented by **parentheses**
-   ```t = ()``` initializes an **empty** tuple
-   ``` t = (2, "MIT", 3)``` initializes a tuple with 3 values
-   ```t[0]``` **indexes** the tuple and returns ```2```
-   ```t = (2, "MIT", 3) + (5, 6)``` **concatenate** tuples together, evaluates to ```(2, "MIT", 3, 5, 6)```
-   ```t[1:2]``` **slices** the tuple, evaluates to ```("MIT",)``` --- **comma** is a ***tuple element***
-   ```t[1:3]``` **slices** the tuple, evaluates to ```("MIT", 3)```
-   ```len(t)```evaluates to ```3```
-   ```t[1] = 4``` gives **error**, can't modify object

Can be used to conveniently **swap variable values**

-   ```(x, y) = (y, x)```

Used to **return** **multiple values** from a function

```python
def quotient_and_remainder(x,y):
	q = x // y
	r = x % y
	return (q, r)
	
(quot, rem) = quotient_and_remainder(4,5)	
```

You can **iterate** over tuples

```python 
def get_data(aTuple):
	nums = ()
	words = ()
	
	for t in aTuple:
		nums = nums + (t[0],)
		if t[1] not in words:
			words = words + (t[1],)
			
	min_n = min(nums)
	max_n = max(nums)
	unique_words = len(words)
	
	return(min_n, max_n, unique_words)
```



## Lists

Lists are **like tuples** with some **distinctions**.

Unlike tuples, lists are **mutable**.

Lists are denoted by **brackets**.

-   ```a_list = []``` **empty** list
-   ```L = [2, "a", 4, [1,2]]```list with different variable types
-   ```len(L)``` evaluates to *4*
-   ```L[0]``` evaluates to 2
-   ```L[2] + 1``` evaluates to 5
-   ```L[3]``` evaluates to [1,2], another list
-   ```L[4]``` gives an error
-   ```L[i - 1]``` evaluates to ```"a"``` if ```i == 2```

Because lists are **mutable**, **assigning** to an **element** at an **index** changes the value

```python
L = [2, 1, 3]
L[1] = 5
```

```L``` is now `[2, 5, 3]`

-   **Note:** This is the **same object** ```L```

You can also **iterate** over a list

```python
total = 0

for i in L:
	total += i

print total
```



### List Operations



#### Expanding Lists

You can **add** elements to the end of a list with ```L.append(element)```

-   This **mutates** the list

```python
L = [2, 1, 3]
L.append(5)
```

L is now ```[2, 1, 3, 5]```

You can combine lists together using **concatenation** to give you a new list

```python
L1 = [2, 1, 3]
L2 = [4, 5, 6]
L3 = L1 + L2
```

```L3``` is now ```[2, 1, 3 ,4 ,5, 6]``` and ```L1``` and ```L2``` are unchanged 

You can **mutate** a list with ```L.extend(some_list)```

```python
L1 = [2, 1, 3]
L1.extend([0, 6])
```

```L1``` mutated to ```[2, 1, 3 ,0 ,6]```



#### Shrinking Lists

**Delete** and element at a **specific index** with ```del(L[index])```

**Remove** elements at the **end** of the list with ```L.pop()```, **returns** the **removed element**

**Remove** a **specific element** with ```L.remove(element)```

-   Looks for the element and removes it
-   If element occurs **multiple** times, **removes first** occurrence
-   If element **not in list**, returns an **error**

```python
L = [2, 1, 3, 6, 3, 7, 0]
L.remove(2) #Mutates L = [1, 3, 6, 3, 7, 0]
L.remove(3) #Mutates L = [1, 6, 3, 7, 0]
del(L[1]) #Mutates L=[1, 3, 7, 0]
L.pop() #Returns 0 and mutates L=[1, 3, 7]
```



#### Converting and Casting

Convert **string to list** with ```list(s)```, returns a list with every character from ```s``` as an element in ```L```

Can use ```s.split()```, to **split** a **string** on a **character** parameter, splits on **spaces** by default

Use ```"".join(L)``` to **turn** a **list of characters** into a **string**, can give a character in quotes to add between every element

```python
s = 'I <3 cs'
list(s) #Returns ['I', '<', '3', ' ', 'c', 's']
s.split('<') #Returns ['I', '3 cs']
L = ['a', 'b', 'c']
"".join(L) #Returns 'abc'
"_".join(L) #Returns 'a_b_c'
```



#### Sorting Lists

```L.sort()``` and ```sorted(L)```

```reverse()```

More found in [documentation](https://docs.python.org/3/tutorial/datastructures.html).

```python
L = [9, 6, 0, 3]
sorted(L) #Returns sorted list, does NOT mutate L
L.sort() #Mutates L=[0, 3, 6, 9]
L.reverse() #Mutates L==[9, 6, 3, 0]
```

Calling ```L.sort()``` **mutates** the list, and **returns nothing**

Calling ```sorted(L)``` does **not mutate** list, must assign result to a variable



### Aliases

```python
warm = ['red', 'yellow', 'orange']
hot = warm
hot.append('pink')
print(hot)
print(warm)
```

Both ```hot``` and ```warm``` will print out ```['red', 'yellow', 'orange', 'pink']```

The ```.append()``` operation has this issue of **aliases**

To create a **new list** and **copy every element** use:

-   ```chill = cool[:]``` 



### Mutation and Iteration

**Avoid mutating** a list as you are **iterating** over it 

```python
def remove_dups(L1, L2):
	for e in L1:
		if e in L2:
			L1.remove(e)
			
L1 = [1, 2, 3, 4]
L2 = [1, 2, 5, 6]
remove_dups(L1, L2)
```

```L1``` is ```[2, 3, 4]``` not ```[3, 4]```
-   Python uses an **internal counter** to keep track of index it is in the loop
-   Mutating **changes** the **list length** but Python **doesn't update** the counter
-   Loop **never sees element 2**