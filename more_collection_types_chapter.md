# Beyond Lists - Dictionaries, Tuples, and Sets

Welcome back! In the previous chapter, we explored the versatile and powerful list data type, the workhorse of Python collections. While lists are fantastic for ordered sequences of data, Python offers other specialized collection types that are better suited for specific tasks.

In this chapter, we'll dive into three of these indispensable data structures:
* ***Dictionaries***: For creating associations or mappings between pieces of data.
* ***Tuples***: For creating immutable, or unchangeable, ordered sequences.
* ***Sets***: For managing unordered collections of unique elements.

Understanding when and how to use each of these types will make your code more efficient, more readable, and more "Pythonic."

## 1. Dictionaries

Dictionaries are one of Python's most versatile and commonly used data structures. They store data in key-value pairs, making them perfect for mapping relationships and organizing related information.

### 1.1 Dictionary Literal
A dictionary is created using curly braces `{}` and consists of a comma-separated list of key-value pairs. Each key is separated from its corresponding value by a colon `:`.

Dictionary keys must be of an immutable type, such as strings, numbers, or tuples. Values, on the other hand, can be of any data type, including mutable types like lists or even other dictionaries.

```python
# Empty dictionary
empty_dict = {}

# Dictionary with initial values
student = {
    "name": "Alice",
    "age": 20,
    "major": "Computer Science",
    "gpa": 3.8
}

# Dictionary with mixed types of keys and values
mixed_dict = {
    "string_key": "value",
    42: "numeric key",
    "list_value": [1, 2, 3],
    "nested_dict": {"inner": "value"},
    (1, 2): "tuple key"
}

# Dictionary comprehension
emoji_names = ["smile", "heart", "thumbs_up", "star", "fire"]
emoji_icons = ["😊", "❤️", "👍", "⭐", "🔥"]
emoji_dict = {emoji_names[i]: emoji_icons[i] for i in range(len(emoji_names))}
print(emoji_dict)  # Output: {"smile": "😊", "heart": "❤️", "thumbs_up": "👍", "star": "⭐", "fire": "🔥"}
```

### 1.2 Dictionary Usage
The Key-value pairs nature of dictionaries, makes them perfect for mapping relationships and organizing related information.

For example, you can use a dictionary to map between student name and scor or represent a person, a product, or any entity with various attributes.
```python
# storing students related data as lists
first_names = ["Alice", "Bob", "Charlie"]
last_names = ["Smith", "Johnson", "Lee"]
age = [20, 22, 19]
score = [85, 92, 78]

# mapping between student name and score 
students_scores = {
    'Alice Smith': 85,
    'Bob Johnson': 92,
    'Charlie Lee': 78
}

# storing data as array of dictionaries instead
students = [
    {'first_name': 'Alice', 'last_name': 'Smith', 'age': 20, 'score': 85},
    {'first_name': 'Bob', 'last_name': 'Johnson', 'age': 22, 'score': 92},
    {'first_name': 'Charlie', 'last_name': 'Lee', 'age': 19, 'score': 78}
]
```

### 1.3 Dictionary Operators

| Operator | Description                                  | Example              |
|----------|----------------------------------------------|----------------------|
| `[]`     | Access/assign value by key                   | `dict[key]`          |
| `in`     | Check if key exists                          | `key in dict`        |
| `not in` | Check if key doesn't exist                   | `key not in dict`    |
| `del`    | Deletes a key-value pair from the dictionary | `del dict['key']`    |
| `**`     | Dictionary unpacking                         | `{**dict1, **dict2}` |

```python
# Examples of dictionary operators
grades = {"Alice": 85, "Bob": 92, "Charlie": 78}

# Access and assignment and adding
print(grades["Alice"])  # Output: 85
grades["Alice"] = 88    # Modify Alice's grade to 88
grades["Ali"] = 97      # Adds new student Ali with grade of 97

# Membership testing
print("Alice" in grades)        # Output: True
print("Diana" not in grades)    # Output: True

# Delete key-value pairs
del grades["Bob"]
print(grades)                   # Output: {'Alice': 88, 'Charlie': 78, 'Ali': 97}

# Dictionary unpacking (merging)
dict1 = {"a": 1, "b": 2}
dict2 = {"c": 3, "d": 4}
merged = {**dict1, **dict2}
print(merged)  # Output: {'a': 1, 'b': 2, 'c': 3, 'd': 4}
```

### 1.4 Dictionary Methods

| Method | Description | Example |
|--------|-------------|---------|
| `get(key, default)` | Get value or return default | `dict.get('key', 0)` |
| `keys()` | Return all keys | `dict.keys()` |
| `values()` | Return all values | `dict.values()` |
| `items()` | Return key-value pairs | `dict.items()` |
| `pop(key, default)` | Remove and return value | `dict.pop('key')` |
| `clear()` | Remove all items | `dict.clear()` |
| `update(other)` | Update with another dict | `dict.update(other)` |
| `copy()` | Create shallow copy | `dict.copy()` |

```python
# Dictionary methods examples
inventory = {"apples": 50, "bananas": 30, "oranges": 25}

# get() method - safe access
print(inventory.get("apples", 0))     # Output: 50
print(inventory.get("grapes", 0))     # Output: 0

# keys(), values(), items()
print(list(inventory.keys()))         # Output: ['apples', 'bananas', 'oranges']
print(list(inventory.values()))       # Output: [50, 30, 25]
print(list(inventory.items()))        # Output: [('apples', 50), ('bananas', 30), ('oranges', 25)]

# pop() method
removed_value = inventory.pop("bananas")
print(removed_value)                  # Output: 30
print(inventory)                      # Output: {'apples': 50, 'oranges': 25}

# update() method
new_items = {"grapes": 40, "apples": 60}
inventory.update(new_items)
print(inventory)                      # Output: {'apples': 60, 'oranges': 25, 'grapes': 40}

```

### 1.5 Dictionaries and JSON

Dictionaries have a close relationship with JSON (JavaScript Object Notation), which is a popular data interchange format. Python's `json` module allows easy conversion between dictionaries and JSON strings.

```python
import json

# Dictionary to JSON
student_data = {
    "name": "John Doe",
    "age": 22,
    "courses": ["Math", "Physics", "Chemistry"],
    "graduated": False
}

# Convert to JSON string
json_string = json.dumps(student_data, indent=2)
print(json_string)

# JSON string to dictionary
json_data = '{"name": "Jane Smith", "age": 25, "city": "New York"}'
student_dict = json.loads(json_data)
print(student_dict)  # Output: {'name': 'Jane Smith', 'age': 25, 'city': 'New York'}
```

### Exercise 7.1: Dictionary Practice

**Exercise 7.1.1**: Create a dictionary representing a library book with keys: title, author, year, isbn, and available. Then perform the following operations:
1. Add a new key "genre"
2. Update the year
3. Check if "publisher" key exists
4. Get the author using the get() method

**Exercise 7.1.2**: Write a function that takes a string and returns a dictionary with character frequencies.

**Exercise 7.1.3**: Create two dictionaries representing student grades in different subjects. Merge them and calculate the average grade for each student.

---

## 7.2 Tuples

Tuples are ordered collections of items that are immutable (cannot be changed after creation). They are similar to lists but with the key difference that they cannot be modified.

### 7.2.1 Tuple Literals

Tuples are created using parentheses `()` or simply by separating values with commas.

```python
# Empty tuple
empty_tuple = ()
# or
empty_tuple = tuple()

# Tuple with values
coordinates = (10, 20)
colors = ("red", "green", "blue")

# Single item tuple (comma is required)
single_item = (42,)
# or without parentheses
single_item = 42,

# Tuple without parentheses
point = 5, 10, 15

# Nested tuples
nested = ((1, 2), (3, 4), (5, 6))

# Tuple from other iterables
list_to_tuple = tuple([1, 2, 3, 4])
string_to_tuple = tuple("hello")
print(string_to_tuple)  # Output: ('h', 'e', 'l', 'l', 'o')
```

### 7.2.2 Tuple Usage

Tuples are commonly used for:
- Coordinates and points in space
- RGB color values
- Database records
- Function return values (multiple values)
- Dictionary keys (when immutable key is needed)
- Configuration data that shouldn't change

```python
# Coordinates example
point_2d = (100, 200)
point_3d = (100, 200, 50)

# RGB color
red_color = (255, 0, 0)
green_color = (0, 255, 0)

# Database-like record
student_record = ("John Doe", 20, "Computer Science", 3.7)

# Multiple return values
def get_name_age():
    return "Alice", 25

name, age = get_name_age()  # Tuple unpacking

# Using tuple as dictionary key
locations = {
    (0, 0): "Origin",
    (1, 1): "Point A",
    (2, 3): "Point B"
}

# Swapping variables using tuples
a, b = 10, 20
a, b = b, a  # Now a=20, b=10
```

### 7.2.3 Tuple Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `[]` | Access item by index | `tuple[0]` |
| `[:]` | Slice tuple | `tuple[1:3]` |
| `+` | Concatenate tuples | `tuple1 + tuple2` |
| `*` | Repeat tuple | `tuple * 3` |
| `in` | Check membership | `item in tuple` |
| `not in` | Check non-membership | `item not in tuple` |
| `==` | Compare tuples | `tuple1 == tuple2` |
| `!=` | Check inequality | `tuple1 != tuple2` |
| `<, >, <=, >=` | Lexicographic comparison | `tuple1 < tuple2` |

```python
# Tuple operators examples
numbers = (1, 2, 3, 4, 5)
colors = ("red", "blue")

# Indexing and slicing
print(numbers[0])        # Output: 1
print(numbers[-1])       # Output: 5
print(numbers[1:4])      # Output: (2, 3, 4)

# Concatenation
combined = numbers + colors
print(combined)          # Output: (1, 2, 3, 4, 5, 'red', 'blue')

# Repetition
repeated = colors * 3
print(repeated)          # Output: ('red', 'blue', 'red', 'blue', 'red', 'blue')

# Membership
print(3 in numbers)      # Output: True
print("green" not in colors)  # Output: True

# Comparison
tuple1 = (1, 2, 3)
tuple2 = (1, 2, 4)
print(tuple1 < tuple2)   # Output: True (lexicographic comparison)
```

### 7.2.4 Tuple Methods

Since tuples are immutable, they have only two methods:

| Method | Description | Example |
|--------|-------------|---------|
| `count(value)` | Count occurrences of value | `tuple.count(2)` |
| `index(value)` | Find first index of value | `tuple.index('a')` |

```python
# Tuple methods examples
numbers = (1, 2, 3, 2, 4, 2, 5)
letters = ('a', 'b', 'c', 'b', 'd')

# count() method
print(numbers.count(2))     # Output: 3
print(letters.count('b'))   # Output: 2

# index() method
print(numbers.index(4))     # Output: 4
print(letters.index('c'))   # Output: 2

# Note: index() raises ValueError if item not found
try:
    print(letters.index('z'))
except ValueError:
    print("Item not found")
```

### 7.2.5 Tuple Unpacking

One of the most powerful features of tuples is unpacking, which allows you to assign tuple elements to individual variables.

```python
# Basic unpacking
point = (10, 20, 30)
x, y, z = point
print(f"X: {x}, Y: {y}, Z: {z}")  # Output: X: 10, Y: 20, Z: 30

# Unpacking with functions
def get_user_info():
    return "Alice", 25, "Engineer"

name, age, job = get_user_info()

# Using * for extended unpacking
numbers = (1, 2, 3, 4, 5, 6)
first, second, *rest, last = numbers
print(first)    # Output: 1
print(second)   # Output: 2
print(rest)     # Output: [3, 4, 5]
print(last)     # Output: 6

# Unpacking in loops
points = [(1, 2), (3, 4), (5, 6)]
for x, y in points:
    print(f"Point: ({x}, {y})")
```

### Exercise 7.2: Tuple Practice

**Exercise 7.2.1**: Create a tuple containing information about a movie (title, year, director, rating). Practice accessing each element and unpacking the tuple.

**Exercise 7.2.2**: Write a function that returns the minimum and maximum values from a list as a tuple. Use tuple unpacking to get both values.

**Exercise 7.2.3**: Given a list of coordinate tuples, write a function to find the point closest to the origin (0, 0).

---

## 7.3 Sets

Sets are unordered collections of unique elements. They are particularly useful for eliminating duplicates and performing mathematical set operations.

### 7.3.1 Set Literals

Sets are created using curly braces `{}` with comma-separated values, or using the `set()` constructor.

```python
# Empty set (must use set(), not {})
empty_set = set()

# Set with values
fruits = {"apple", "banana", "orange"}
numbers = {1, 2, 3, 4, 5}

# Set from other iterables
list_to_set = set([1, 2, 2, 3, 3, 4])
print(list_to_set)  # Output: {1, 2, 3, 4} (duplicates removed)

string_to_set = set("hello")
print(string_to_set)  # Output: {'h', 'e', 'l', 'o'} (duplicates removed)

# Set comprehension
squares = {x**2 for x in range(1, 6)}
print(squares)  # Output: {1, 4, 9, 16, 25}

# Note: Sets cannot contain mutable objects like lists
# This would cause an error: invalid_set = {[1, 2], [3, 4]}
```

### 7.3.2 Set Usage

Sets are ideal for:
- Removing duplicates from sequences
- Membership testing (very fast)
- Mathematical set operations (union, intersection, difference)
- Finding unique elements
- Checking relationships between collections

```python
# Remove duplicates
numbers_with_duplicates = [1, 2, 2, 3, 3, 3, 4, 5, 5]
unique_numbers = list(set(numbers_with_duplicates))
print(unique_numbers)  # Output: [1, 2, 3, 4, 5]

# Fast membership testing
large_set = set(range(1000000))
print(999999 in large_set)  # Very fast operation

# Finding common elements
students_math = {"Alice", "Bob", "Charlie", "Diana"}
students_physics = {"Bob", "Charlie", "Eve", "Frank"}
common_students = students_math & students_physics
print(common_students)  # Output: {'Bob', 'Charlie'}

# Finding unique visitors
website_visitors_day1 = {"user1", "user2", "user3", "user4"}
website_visitors_day2 = {"user3", "user4", "user5", "user6"}
all_unique_visitors = website_visitors_day1 | website_visitors_day2
print(all_unique_visitors)  # Output: {'user1', 'user2', 'user3', 'user4', 'user5', 'user6'}
```

### 7.3.3 Set Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `in` | Check membership | `item in set` |
| `not in` | Check non-membership | `item not in set` |
| `\|` or `union()` | Union (all elements) | `set1 \| set2` |
| `&` or `intersection()` | Intersection (common elements) | `set1 & set2` |
| `-` or `difference()` | Difference (in first, not second) | `set1 - set2` |
| `^` or `symmetric_difference()` | Symmetric difference | `set1 ^ set2` |
| `<=` or `issubset()` | Subset test | `set1 <= set2` |
| `>=` or `issuperset()` | Superset test | `set1 >= set2` |
| `<` | Proper subset test | `set1 < set2` |
| `>` | Proper superset test | `set1 > set2` |

```python
# Set operators examples
set_a = {1, 2, 3, 4, 5}
set_b = {4, 5, 6, 7, 8}
set_c = {1, 2, 3}

# Membership
print(3 in set_a)        # Output: True
print(9 not in set_a)    # Output: True

# Union - all elements from both sets
union_result = set_a | set_b
print(union_result)      # Output: {1, 2, 3, 4, 5, 6, 7, 8}

# Intersection - common elements
intersection_result = set_a & set_b
print(intersection_result)  # Output: {4, 5}

# Difference - elements in first set but not in second
difference_result = set_a - set_b
print(difference_result)    # Output: {1, 2, 3}

# Symmetric difference - elements in either set but not both
sym_diff_result = set_a ^ set_b
print(sym_diff_result)      # Output: {1, 2, 3, 6, 7, 8}

# Subset and superset tests
print(set_c <= set_a)       # Output: True (set_c is subset of set_a)
print(set_a >= set_c)       # Output: True (set_a is superset of set_c)
print(set_c < set_a)        # Output: True (set_c is proper subset of set_a)
```

### 7.3.4 Set Methods

| Method | Description | Example |
|--------|-------------|---------|
| `add(item)` | Add single item | `set.add(5)` |
| `update(iterable)` | Add multiple items | `set.update([1, 2, 3])` |
| `remove(item)` | Remove item (raises KeyError if not found) | `set.remove(5)` |
| `discard(item)` | Remove item (no error if not found) | `set.discard(5)` |
| `pop()` | Remove and return arbitrary item | `set.pop()` |
| `clear()` | Remove all items | `set.clear()` |
| `copy()` | Create shallow copy | `set.copy()` |
| `union(other)` | Return union | `set.union(other)` |
| `intersection(other)` | Return intersection | `set.intersection(other)` |
| `difference(other)` | Return difference | `set.difference(other)` |
| `symmetric_difference(other)` | Return symmetric difference | `set.symmetric_difference(other)` |
| `issubset(other)` | Check if subset | `set.issubset(other)` |
| `issuperset(other)` | Check if superset | `set.issuperset(other)` |
| `isdisjoint(other)` | Check if no common elements | `set.isdisjoint(other)` |

```python
# Set methods examples
fruits = {"apple", "banana", "orange"}

# Adding elements
fruits.add("grape")
print(fruits)  # Output: {'apple', 'banana', 'orange', 'grape'}

fruits.update(["mango", "kiwi"])
print(fruits)  # Output: {'apple', 'banana', 'orange', 'grape', 'mango', 'kiwi'}

# Removing elements
fruits.remove("banana")  # Raises KeyError if not found
print(fruits)

fruits.discard("pear")   # No error if not found
print(fruits)

# Pop arbitrary element
removed_fruit = fruits.pop()
print(f"Removed: {removed_fruit}")

# Set operations using methods
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}

print(set1.union(set2))              # Output: {1, 2, 3, 4, 5, 6}
print(set1.intersection(set2))       # Output: {3, 4}
print(set1.difference(set2))         # Output: {1, 2}
print(set1.symmetric_difference(set2))  # Output: {1, 2, 5, 6}

# Relationship tests
set3 = {1, 2}
print(set3.issubset(set1))          # Output: True
print(set1.issuperset(set3))        # Output: True
print(set1.isdisjoint({7, 8, 9}))   # Output: True
```

### 7.3.5 Frozen Sets

Python also provides `frozenset`, which is an immutable version of a set.

```python
# Creating frozen sets
frozen_fruits = frozenset(["apple", "banana", "orange"])
frozen_numbers = frozenset([1, 2, 3, 4, 5])

# Frozen sets can be used as dictionary keys or elements in other sets
set_of_sets = {frozenset([1, 2]), frozenset([3, 4]), frozenset([5, 6])}

# Frozen sets support all set operations except modification methods
print(frozen_fruits | frozenset(["grape"]))  # Union operation
print(frozen_numbers & frozenset([3, 4, 5, 6]))  # Intersection

# This would cause an error (frozen sets are immutable):
# frozen_fruits.add("grape")  # AttributeError
```

### Exercise 7.3: Set Practice

**Exercise 7.3.1**: Given two lists of student names, find:
1. Students who are in both classes
2. Students who are only in the first class
3. Students who are in either class but not both

**Exercise 7.3.2**: Write a function that takes a string and returns the set of unique characters, ignoring spaces and case.

**Exercise 7.3.3**: Create a program that manages a library's book inventory using sets. Implement functions to:
1. Add new books
2. Remove books
3. Find books that are available in multiple branches
4. Find books unique to each branch

---

## Chapter Summary

In this chapter, we explored three essential Python collection types:

**Dictionaries** provide key-value mapping functionality, making them perfect for organizing related data and creating lookup tables. They're mutable, ordered (as of Python 3.7+), and extremely efficient for data retrieval operations.

**Tuples** offer immutable, ordered collections that are ideal for representing fixed data structures like coordinates, database records, or function return values. Their immutability makes them suitable as dictionary keys and ensures data integrity.

**Sets** provide collections of unique elements with powerful mathematical set operations. They excel at removing duplicates, fast membership testing, and finding relationships between collections of data.

Understanding when and how to use each collection type is crucial for writing efficient and maintainable Python code. The combination of lists, dictionaries, tuples, and sets gives you a complete toolkit for handling virtually any data organization challenge you'll encounter in Python programming.

These collection types often work together in real-world applications - for example, using dictionaries with lists as values, tuples as dictionary keys, or sets to process data before storing it in other collections. Mastering all four collection types will significantly enhance your ability to solve complex programming problems elegantly and efficiently.