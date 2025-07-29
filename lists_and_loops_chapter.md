# Lists and Loops in Python

## 1. Understanding Collection Data Types

Collection data types in Python are containers that can hold multiple values or objects. They are fundamental building blocks that allow us to organize, store, and manipulate groups of related data efficiently. Python provides several built-in collection types, including lists, tuples, sets, and dictionaries. Each collection type has unique characteristics that make it suitable for different use cases.

Lists are one of the most versatile and commonly used collection data types in Python. They are ordered, mutable sequences that can store elements of different data types, making them perfect for scenarios where you need to maintain a sequence of items that can change over time.

## 2. Introduction to Lists

A list in Python is an ordered collection of items (elements) that can be of any data type. Lists are:
- **Ordered**: Elements have a defined position and maintain their order
- **Mutable**: Can be modified after creation (elements can be added, removed, or changed: best practice is to create new mutated version)
- **Allow duplicates**: The same value can appear multiple times
- **Heterogeneous**: Can contain elements of different data types (not best practice)

### 2.1 List Literals

Lists are created using square brackets `[]` with elements separated by commas.

```python
# Empty list
empty_list = []

# List with integers
numbers = [1, 2, 3, 4, 5]

# List with strings
fruits = ["apple", "banana", "orange"]

# List with mixed data types (avoid it)
mixed_list = [1, "hello", 3.14, True, [1, 2, 3]]

# List with duplicates
duplicates = [1, 2, 2, 3, 2]

print(empty_list)   # Output: []
print(numbers)      # Output: [1, 2, 3, 4, 5]
print(fruits)       # Output: ['apple', 'banana', 'orange']
print(mixed_list)   # Output: [1, 'hello', 3.14, True, [1, 2, 3]]
print(duplicates)   # Output: [1, 2, 2, 3, 2]
```
### 2.2 Lists are Reference Values (Very Important!)

This is a very important concept. In Python, data types like integers, floats, and strings are value types (primitives). When you assign them to another variable, a new copy of the value is made. However, collection data types like lists are reference types. When you assign a list to a new variable, you are not making a copy. Instead, you are making both variables point to the exact same list in your computer's memory.

#### Primitive Values vs. Reference Values

* ***Primitive Values***: These are stored directly in the variable. When you assign one variable to another, Python creates a copy of the value. Think of it like giving a friend a photocopy of a recipe: if they spill coffee on their copy, your original recipe remains unchanged. 
```python
a = 5  # Primitive value
b = a  # b gets a copy of 5
b = 10 # Changing b doesn’t affect a
print(a)  # Output: 5
```

* ***Reference Values***: These are stored in memory, and the variable holds a reference (or pointer) to that memory location. When you assign one variable to another, both point to the same object in memory. It’s like giving a friend a web address to an online recipe: if they edit the recipe at that address, you’ll see the changes too.
```python
a = [1, 2, 3]  # Reference value
b = a           # b points to the same list as a
b.append(4)     # Modifying b affects a
print(a)        # Output: [1, 2, 3, 4]

```

### 2.3 Exercises
1. Create a list `books` with five favorite books titles.
2. Create a list `even_numbers` with the first 10 even numbers (2, 4, ..., 20).
3. Create a list `personal_info` with your name (str), age (int), height (float), and a boolean for liking programming.
4. Create an empty list `empty` and print its length (should be 0).
5. Predict the output of this code before running it:
```python
list_x = [10, 20, 30]
list_y = list_x
list_z = [10, 20, 30]

list_x[1] = 999
print(f"list_x: {list_x}")
print(f"list_y: {list_y}")
print(f"list_z: {list_z}")
```

## 3. List Operators

Python provides several operators to work with lists efficiently.

### 3.1 Basic List Operators
| Operator | Description                                                                | Example | Result |
| :--- |:---------------------------------------------------------------------------| :--- | :--- |
| `+` | **Concatenation**: Combines two lists.                                     | `[1, 2] + [3, 4]` | `[1, 2, 3, 4]` |
| `*` | **Repetition**: Repeats the list's elements.                               | `['a', 'b'] * 3` | `['a', 'b', 'a', 'b', 'a', 'b']` |
| `in` | **Membership**: Checks if an element exists.                               | `3 in [1, 2, 3]` | `True` |
| `not in` | **Membership**: Checks if an element does not exist.                       | `4 not in [1, 2, 3]` | `True` |
| `[]` | **Indexing**: Positive indices count from the start (0, 1, 2...), while negative indices count from the end (-1, -2...). | `my_list = [10, 20, 30, 40]; my_list[1]; my_list[-1]` | `20; 40` |
| `[:]`, `[::]` | **Slicing**: Extracts a portion with an optional step `[start:stop:step]`. | `my_list = [10, 20, 30, 40, 50]; my_list[1:4]; my_list[::2]` | `[20, 30, 40]; [10, 30, 50]` |

```python
# Concatenation
list1 = [1, 2, 3]
list2 = [4, 5, 6]
combined = list1 + list2
print(combined)  # Output: [1, 2, 3, 4, 5, 6]

# Repetition
repeated = [1, 2] * 3
print(repeated)  # Output: [1, 2, 1, 2, 1, 2]

# Membership testing
fruits = ["apple", "banana", "orange"]
print("apple" in fruits)      # Output: True
print("grape" not in fruits)  # Output: True

# Indexing (positive: 0-based, negative: indexing from last element)
numbers = [10, 20, 30, 40, 50]
print(numbers[0])   # Output: 10 (first element)
print(numbers[-1])  # Output: 50 (last element)
print(numbers[-2])  # Output: 40 (second to last)
# print(numbers[10]) # Raises IndexError: list index out of range

# Slicing
print(numbers[1:4])   # Output: [20, 30, 40]
print(numbers[:3])    # Output: [10, 20, 30]
print(numbers[2:])    # Output: [30, 40, 50]
print(numbers[::2])   # Output: [10, 30, 50] (every second element)
print(numbers[::-1])  # Output: [50, 40, 30, 20, 10] (reversed)
print(numbers[4:2])   # Output: [] (empty slice, no error)

```

### 3.2 The Unpacking Operator (*)
The asterisk `(*)` can also be used as an unpacking operator. This allows you to unpack the elements of a list into individual elements for inserting into another list or passing to a function.

```python
# Unpacking in function calls
numbers = [1, 2, 3, 4, 5]
print(*numbers)  # Output: 1 2 3 4 5 (equivalent to print(1, 2, 3, 4, 5))

def sum_three(a, b, c):
    return a + b + c
values = [10, 20, 30]
result = sum_three(*values)  # Unpacks list into arguments
print(result)  # Output: 60

# Unpacking in list creation
list1 = [1, 2, 3]
list2 = [4, 5, 6]
combined = [*list1, *list2, 7, 8]
print(combined)  # Output: [1, 2, 3, 4, 5, 6, 7, 8]

# Variable unpacking
first, *middle, last = [1, 2, 3, 4, 5]
print(first)   # Output: 1
print(middle)  # Output: [2, 3, 4]
print(last)    # Output: 5
```

### 3.3 Exercises
1. Combine two lists of your choice using `+`.
2. Combine two lists of your choice using unpacking operator`*`.
3. Slice the middle three elements from a list `[1, 2, 3, 4, 5, 6, 7]`. 
4. Check if `42` is in `[10, 20, 30, 40, 50]`. 
5. Print all elements of a list using `*`.

## 4. List Methods

Like strings Lists come with a variety of built-in functions, called methods, that allow you to modify and interact with their contents. 

An important characteristic of lists is that they are mutable, meaning their contents can be changed after they are created. You can add, remove, or change elements in a list. This is in contrast to immutable data types like strings and tuples, which cannot be changed once created but can be used to create new ones.

### 4.1 Pure vs Non-Pure Methods
When working with list methods, it's helpful to understand the difference between pure and non-pure methods:

**Pure methods** (also called non-mutating methods) do not modify the original list. Instead, they return a new list or a value.

**Non-pure methods** (also called mutating methods) modify the original list in place and usually return `None`.

### 4.2 List Methods Reference Table

| Method | Type | Description | Returns | Example |
|--------|------|-------------|---------|---------|
| `append(item)` | Non-pure | Adds item to end | `None` | `lst.append(5)` |
| `insert(index, item)` | Non-pure | Inserts item at index | `None` | `lst.insert(0, 'first')` |
| `extend(iterable)` | Non-pure | Adds all items from iterable | `None` | `lst.extend([1, 2, 3])` |
| `remove(item)` | Non-pure | Removes first occurrence | `None` | `lst.remove('apple')` |
| `pop(index)` | Non-pure | Removes and returns item | Item | `item = lst.pop()` |
| `clear()` | Non-pure | Removes all items | `None` | `lst.clear()` |
| `index(item)` | Pure | Returns index of item | `int` | `idx = lst.index('apple')` |
| `count(item)` | Pure | Counts occurrences | `int` | `n = lst.count(5)` |
| `sort()` | Non-pure | Sorts list in place | `None` | `lst.sort()` |
| `reverse()` | Non-pure | Reverses list in place | `None` | `lst.reverse()` |
| `copy()` | Pure | Creates shallow copy | `list` | `new_lst = lst.copy()` |

### 4.3 Adding Elements

```python
# append() - adds single element to end
fruits = ["apple", "banana"]
fruits.append("orange")
print(fruits)  # Output: ['apple', 'banana', 'orange']

# insert() - adds element at specific position
fruits.insert(1, "grape")
print(fruits)  # Output: ['apple', 'grape', 'banana', 'orange']

# extend() - adds multiple elements
fruits.extend(["mango", "kiwi"])
print(fruits)  # Output: ['apple', 'grape', 'banana', 'orange', 'mango', 'kiwi']

# append vs extend
list1 = [1, 2, 3]
list2 = [1, 2, 3]
list1.append([4, 5])  # Adds list as one element
list2.extend([4, 5])  # Adds individual elements
print(list1)  # Output: [1, 2, 3, [4, 5]]
print(list2)  # Output: [1, 2, 3, 4, 5]
```

### 4.4 Removing Elements

```python
# remove() - removes first occurrence of value
numbers = [1, 2, 3, 2, 4, 2]
numbers.remove(2)  # Removes first 2
print(numbers)  # Output: [1, 3, 2, 4, 2]

# pop() - removes and returns element by index
numbers = [10, 20, 30, 40, 50]
last_item = numbers.pop()      # Removes last element
print(last_item)  # Output: 50
print(numbers)    # Output: [10, 20, 30, 40]

second_item = numbers.pop(1)   # Removes element at index 1
print(second_item)  # Output: 20
print(numbers)      # Output: [10, 30, 40]

# clear() - removes all elements
numbers.clear()
print(numbers)  # Output: []

```

### 4.5 Searching and Counting

```python
# index() - finds position of element
fruits = ["apple", "banana", "orange", "banana"]
position = fruits.index("banana")
print(position)  # Output: 1 (first occurrence)

# count() - counts occurrences
count = fruits.count("banana")
print(count)  # Output: 2

```

### 4.6 Sorting and Reversing

```python
# sort() - sorts in place
numbers = [3, 1, 4, 1, 5, 9, 2, 6]
numbers.sort()
print(numbers)  # Output: [1, 1, 2, 3, 4, 5, 6, 9]

# sort() with reverse parameter
numbers.sort(reverse=True)
print(numbers)  # Output: [9, 6, 5, 4, 3, 2, 1, 1]

# sorted() - pure function alternative 
original = [3, 1, 4, 1, 5]
sorted_list = sorted(original)
print(original)     # Output: [3, 1, 4, 1, 5] (unchanged)
print(sorted_list)  # Output: [1, 1, 3, 4, 5]

# reverse() - reverses in the list
letters = ['a', 'b', 'c', 'd']
letters.reverse()
print(letters)  # Output: ['d', 'c', 'b', 'a']

```

### 4.7 Exercise
1. Create a list of numbers and use appropriate methods to:
   - Add a number to the end
   - Insert a number at the beginning
   - Remove a specific number
   - Sort the list in descending order
2. Create a shopping list and demonstrate the difference between `append()` and `extend()`
3. Count how many times your favorite letter appears in your name (convert name to list first)

## 5. For Loops with Lists

The `for` loop is the most common way to iterate through lists in Python. It provides a clean, readable syntax for processing each element.

### 5.1 Basic For Loop with Lists

```python
# Iterating through elements
fruits = ["apple", "banana", "orange", "grape"]

for fruit in fruits:
    print(f"I like {fruit}")

# Output:
# I like apple
# I like banana
# I like orange
# I like grape

# Processing elements
numbers = [1, 2, 3, 4, 5]
squared = []

for num in numbers:
    squared.append(num ** 2)

print(squared)  # Output: [1, 4, 9, 16, 25]
```

### 5.2 Using range() and len() for Index Access

When you need both the index and the value, use `range(len())`:

```python
# Printing numbered list
colors = ["red", "green", "blue", "yellow"]

for i in range(len(colors)):
    print(f"{i + 1}. {colors[i]}")

# Output:
# 1. red
# 2. green
# 3. blue
# 4. yellow

# Modifying list elements using indices
numbers = [1, 2, 3, 4, 5]

for i in range(len(numbers)):
    numbers[i] = numbers[i] * 2

print(numbers)  # Output: [2, 4, 6, 8, 10]
```

### 5.3 Using enumerate() for Index and Value

A more Pythonic approach when you need both index and value:

```python
# enumerate() provides both index and value
fruits = ["apple", "banana", "orange"]

for index, fruit in enumerate(fruits):
    print(f"{index + 1}. {fruit}")

# Output:
# 1. apple
# 2. banana
# 3. orange
```

### 5.4 Nested Lists and Nested Loops

```python
# Working with nested lists
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Printing matrix elements
for row in matrix:
    for element in row:
        print(element, end=" ")
    print()  # New line after each row

# Output:
# 1 2 3 
# 4 5 6 
# 7 8 9 

# Finding sum of all elements
total = 0
for row in matrix:
    for element in row:
        total += element

print(f"Sum of all elements: {total}")  # Output: Sum of all elements: 45
```

### Exercise 5.5.1
1. Create a list of temperatures in Celsius and convert them to Fahrenheit using a for loop
2. Find the largest number in a list without using the `max()` function
3. Create a multiplication table (nested list) and print it in a formatted way.

Expected output:
```text
Multiplication Table (1-10):
   1    2    3    4    5    6    7    8    9   10
   2    4    6    8   10   12   14   16   18   20
   3    6    9   12   15   18   21   24   27   30
   4    8   12   16   20   24   28   32   36   40
   5   10   15   20   25   30   35   40   45   50
   6   12   18   24   30   36   42   48   54   60
   7   14   21   28   35   42   49   56   63   70
   8   16   24   32   40   48   56   64   72   80
   9   18   27   36   45   54   63   72   81   90
  10   20   30   40   50   60   70   80   90  100
```
4. Count how many positive numbers are in a mixed list of integers

## 6 List Comprehensions

List comprehensions provide a concise way to create lists based on existing iterables. They are more Pythonic and often more efficient than traditional for loops.

### 6.1 Basic List Comprehensions

The basic syntax is: `[expression for item in iterable]`

```python
# Traditional approach
numbers = [1, 2, 3, 4, 5]
squared = []
for num in numbers:
    squared.append(num ** 2)

# List comprehension approach
squared = [num ** 2 for num in numbers]
print(squared)  # Output: [1, 4, 9, 16, 25]

# String processing
words = ["hello", "world", "python", "programming"]
uppercased = [word.upper() for word in words]
print(uppercased)  # Output: ['HELLO', 'WORLD', 'PYTHON', 'PROGRAMMING']

# Mathematical operations
celsius = [0, 20, 30, 40]
fahrenheit = [(temp * 9/5) + 32 for temp in celsius]
print(fahrenheit)  # Output: [32.0, 68.0, 86.0, 104.0]
```

### 6.2 Conditional List Comprehensions (Filtering)

Add conditions to filter elements: `[expression for item in iterable if condition]`

```python
# Filtering even numbers
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
evens = [x for x in numbers if x % 2 == 0]
print(evens)  # Output: [2, 4, 6, 8, 10]

# Filtering and transforming
words = ["apple", "banana", "cherry", "date"]
long_words = [word.upper() for word in words if len(word) > 5]
print(long_words)  # Output: ['BANANA', 'CHERRY']

# Multiple conditions
numbers = range(1, 21)
special_numbers = [x for x in numbers if x % 2 == 0 and x % 3 == 0]
print(special_numbers)  # Output: [6, 12, 18]

# Working with strings
sentence = "The quick brown fox jumps over the lazy dog"
words = sentence.split()
short_words = [word for word in words if len(word) < 5]
print(short_words)  # Output: ['The', 'fox', 'over', 'the', 'lazy', 'dog']

# Finding common elements
list1 = [1, 2, 3, 4, 5]
list2 = [4, 5, 6, 7, 8]
common = [x for x in list1 if x in list2]
print(common)  # Output: [4, 5]
```

### 6.3 Conditional Expressions in List Comprehensions

Use conditional expressions to transform elements differently: `[expr1 if condition else expr2 for item in iterable]`

```python
# Conditional transformation
numbers = [1, -2, 3, -4, 5, -6]
absolute_values = [x if x >= 0 else -x for x in numbers]
print(absolute_values)  # Output: [1, 2, 3, 4, 5, 6]

# Categorizing values
scores = [85, 92, 78, 96, 88, 71]
grades = ["A" if score >= 90 else "B" if score >= 80 else "C" for score in scores]
print(grades)  # Output: ['B', 'A', 'C', 'A', 'B', 'C']

# Replacing values
data = [1, 2, None, 4, None, 6]
cleaned = [x if x is not None else 0 for x in data]
print(cleaned)  # Output: [1, 2, 0, 4, 0, 6]
```

### 6.4 Nested List Comprehensions (Advanced)

```python
# Creating a matrix
matrix = [[i * j for j in range(1, 4)] for i in range(1, 4)]
print(matrix)  # Output: [[1, 2, 3], [2, 4, 6], [3, 6, 9]]

# Flattening a nested list
nested_list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flattened = [item for sublist in nested_list for item in sublist]
print(flattened)  # Output: [1, 2, 3, 4, 5, 6, 7, 8, 9]
```
### 6.5 Exercises
1. Use list comprehension to create a list of squares for numbers 1-20 that are divisible by 3 fell free to use `range()` function
2. Convert a list of words to their lengths using list comprehension
3. Filter and transform: from a list of mixed positive and negative numbers, create a new list with only positive numbers doubled
4. Create a list of lists `[number, "even"/"odd"]` for numbers 1-10

## 7. The immutable workflow: A modern approach

While the mutability of lists is powerful, it can sometimes lead to unexpected behavior, especially in larger programs where a list might be passed to multiple functions. A modern and often safer approach is to favor an immutable workflow. This means that instead of modifying lists in-place, you create new lists with the desired changes.

This approach often leads to code that is easier to reason about and debug. List comprehensions are a great tool for implementing an immutable workflow.

### 7.1 Understanding the Two Approaches

**Mutable Approach** - Changes the original list:
```python
# Modifying the original list
original_list = [1, 2, 3, 4, 5]
original_list.append(6)  # Changes original_list
print(original_list)  # Output: [1, 2, 3, 4, 5, 6]
# The original list is now different!
```

**Immutable Approach** - Creates new lists:
```python
# Creating new lists without changing the original
original_list = [1, 2, 3, 4, 5]
new_list = original_list + [6]  # Creates a new list
print(original_list)  # Output: [1, 2, 3, 4, 5] (unchanged!)
print(new_list)       # Output: [1, 2, 3, 4, 5, 6]
```

### 7.2 Safe Ways to Add Elements

```python
# Instead of using append() or extend()
original = [1, 2, 3]

# Adding using '+' operator
new_plus_at_end = original + [4]
new_plus_at_start = [-1, 0] + original
new_plus_at_start_end = [-1, 0] + original + [4]

print(f"Original: {original}")              # Output: Original: [1, 2, 3]
print(f"New: {new_plus_at_end}")            # Output: New: [1, 2, 3, 4]
print(f"New: {new_plus_at_start}")          # Output: New: [-1, 0, 1, 2, 3]
print(f"New: {new_plus_at_start_end}")      # Output: New: [-1, 0, 1, 2, 3, 4]

# Adding using unpacking operator (modern approach)
new_unpacking_at_end = [*original, 4]
new_unpacking_at_start = [-1, 2, *original]
new_unpacking_at_start_end = [-1, 2, *original, 4]

print(f"Original: {original}")              # Output: Original: [1, 2, 3]
print(f"New: {new_unpacking_at_end}")       # Output: New: [1, 2, 3, 4]
print(f"New: {new_unpacking_at_start}")     # Output: New: [-1, 0, 1, 2, 3]
print(f"New: {new_unpacking_at_start_end}") # Output: New: [-1, 0, 1, 2, 3, 4]

```

### 7.3 Safe Ways to Remove Elements

```python
# Instead of using remove() or pop()
numbers = [1, 2, 3, 4, 5, 4, 6]

# Removing using list comprehension with filtering
without_fours = [x for x in numbers if x != 4]
print(f"Original: {numbers}")           # Output: Original: [1, 2, 3, 4, 5, 4, 6]
print(f"Without 4s: {without_fours}")   # Output: Without 4s: [1, 2, 3, 5, 6]

# Removing by index using slicing
original = [1, 2, 3, 4, 5]
without_middle = original[:2] + original[3:]  # Remove index 2
print(f"Original: {original}")     # Output: Original: [1, 2, 3, 4, 5]
print(f"Without middle: {without_middle}")  # Output: Without middle: [1, 2, 4, 5]
```

### 7.4 Safe Ways to Transform Lists

```python
# Instead of modifying elements in place 
original_numbers = [1, 2, 3, 4, 5]

# Transform using 
doubled = [x * 2 for x in original_numbers]
squared = [x ** 2 for x in original_numbers]
strings = [str(x) for x in original_numbers]

print(f"Original: {original_numbers}")  # Output: Original: [1, 2, 3, 4, 5]
print(f"Doubled: {doubled}")            # Output: Doubled: [2, 4, 6, 8, 10]
print(f"Squared: {squared}")            # Output: Squared: [1, 4, 9, 16, 25]
print(f"Strings: {strings}")            # Output: Strings: ['1', '2', '3', '4', '5']

```

### 7.5 Safe Sorting

```python
# Instead of using sort() method
original = [3, 1, 4, 1, 5, 9, 2, 6]

# Create sorted versions without changing original
ascending = sorted(original)
descending = sorted(original, reverse=True)

print(f"Original: {original}")      # Output: Original: [3, 1, 4, 1, 5, 9, 2, 6]
print(f"Ascending: {ascending}")    # Output: Ascending: [1, 1, 2, 3, 4, 5, 6, 9]
print(f"Descending: {descending}")  # Output: Descending: [9, 6, 5, 4, 3, 2, 1, 1]
```
### 7.6 Exercises
1. Take a list of numbers and create three new lists: one with only positive numbers, one with numbers doubled, and one sorted in reverse order
2. Practice removing elements safely: from a list of names, create a new list without names that start with 'A'

## 8. While Loops: When and Why
While `for` loops are ideal for iterating over a known sequence, there are times when you need to loop based on a condition rather than a sequence. This is where the `while` loop shines. A `while` loop continues to execute as long as a certain condition is True.

You should use a `while` loop when the number of iterations is unknown beforehand this includes:
- You need to loop until a specific condition is met
- Working with user input or external data sources

### 8.1 The `while` Loop Syntax

The basic syntax of a `while` loop is straightforward:

```python
while condition:
    # Code to be executed as long as the condition is True
```

The loop will continuously execute the indented block of code as long as the `condition` evaluates to `True`. The condition is checked before each iteration. If the condition is `False` from the start, the loop will never execute.

Let's look at a simple example where we simulate a countdown:

```python
countdown = 5

while countdown > 0:
    print(f"Countdown: {countdown}")
    countdown -= 1  # This is crucial to prevent an infinite loop

print("Blast off!")
```

In this example, the loop continues as long as `countdown` is greater than 0. Inside the loop, we print the current value of `countdown` and then decrement it by one. Once `countdown` reaches 0, the condition `countdown > 0` becomes `False`, and the loop terminates.

### 8.2 Infinite Loops and the `break` Statement

A common pitfall with `while` loops is creating an "infinite loop." This occurs when the loop's condition never becomes `False`. An infinite loop will run forever, potentially causing your program to freeze or crash.

Here's an example of an infinite loop:

```python
# This is an infinite loop!
# The value of 'x' never changes, so the condition is always True.
x = 10
while x == 10:
    print("This will run forever...")
```

To control and exit a loop, especially in cases where the condition for termination is complex or depends on events inside the loop, you can use the `break` statement. The `break` statement immediately terminates the loop (`for` or `while`), and the program continues to execute the code that follows.

This is particularly useful when you want to create a loop that runs until a specific user input is received:

```python
while True:  # This creates an intentional infinite loop
    user_input = input("Enter 'quit' to exit: ")
    if user_input.lower() == 'quit':
        break  # Exit the loop if the user enters 'quit'
    print(f"You entered: {user_input}")

print("Loop terminated.")
```

In this example, `while True` creates a loop that will run indefinitely. The `break` statement provides a clean way to exit the loop based on a condition inside it.

### 8.3 The `continue` Statement

Sometimes, you may want to skip the rest of the code in the current iteration of `for` or `while` loop and move on to the next iteration. The `continue` statement allows you to do this.

Let's consider an example where we want to process only even numbers:

```python
number = 0
while number < 10:
    number += 1
    if number % 2 != 0:  # If the number is odd
        continue  # Skip the rest of the loop and go to the next iteration
    print(f"Found an even number: {number}")
```

In this case, if `number` is odd, the `continue` statement is executed, and the `print()` function is skipped for that iteration. The loop then proceeds to the next value of `number`.

#### A Note on `continue` and Readability

While the `continue` statement can be useful, it's worth noting that some developers argue against its frequent use. The primary concern is that `continue` can sometimes make the flow of a loop harder to follow. When you encounter a `continue`, you have to mentally jump back to the start of the loop, which can interrupt the linear reading of the code.

Often, you can achieve the same result by restructuring your logic with an `if` statement. For instance, the previous example could be rewritten as:

```python
number = 0
while number < 10:
    number += 1
    if number % 2 == 0:  # If the number is even
        print(f"Found an even number: {number}")
```

This version is often considered more straightforward because the primary logic is not nested inside a condition that leads to skipping code. The main action is directly inside a clear conditional block.

However, the debate is not one-sided. Proponents of `continue` argue that it can actually improve readability by reducing nested `if` statements, especially in more complex loops. The key takeaway is to use `continue` judiciously. If it makes your code clearer and more concise, it's a perfectly acceptable tool. If it complicates the logic, it's often better to refactor your code to avoid it.

### 8.4 The `else` Clause in a `while` Loop

Similar to `for` loops, `while` loops can also have an `else` clause. The `else` block is executed when the loop's condition becomes `False`. However, if the loop is terminated by a `break` statement, the `else` block will be skipped.

This can be useful for running a piece of code only when the loop completes "naturally."

Here's our countdown example with an `else` clause:

```python
countdown = 5

while countdown > 0:
    print(f"Countdown: {countdown}")
    countdown -= 1
else:
    print("The loop finished without a 'break'.")

print("Blast off!")
```

Now, let's see an example where the `else` block is skipped due to a `break`:

```python
attempts = 3
password = "python"

while attempts > 0:
    user_guess = input("Enter the password: ")
    if user_guess == password:
        print("Access granted!")
        break
    attempts -= 1
    print(f"Wrong password. You have {attempts} attempts left.")
else:
    print("You have run out of attempts. Access denied.")
```

In this scenario, if the user guesses the password correctly, the `break` statement is executed, and the "Access denied" message in the `else` block is not printed.

### 8.5 Key Takeaways
*   Use a `while` loop when the number of iterations is unknown.
*   The loop continues as long as the condition is `True`.
*   Be cautious of infinite loops and ensure the loop's condition will eventually become `False`.
*   Use the `break` statement to exit a loop immediately.
*   Use the `continue` statement to skip the current iteration and move to the next, but be mindful of its impact on readability.
*   The optional `else` block runs only if the loop terminates naturally (i.e., not via a `break`).

### 8.6 Exercises
1. Write a while loop that finds the largest number in a list without using the `max()` built-in
2. Create a guessing game where the user tries to guess a number between 1-10, and the program keeps asking until they get it right
3. Use a while loop to remove all occurrences of a specific value from a list (using the immutable approach)
4. Build a program that keeps asking for student grades and stops when the user enters -1, then calculates the average