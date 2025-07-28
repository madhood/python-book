# Strings in Python

## Introduction

Strings are one of the most fundamental and frequently used data types in Python. A string is a sequence of characters enclosed in quotes, and Python provides powerful tools for creating, manipulating, and formatting strings. In this chapter, we'll explore all aspects of working with strings in Python.

## 1. String Literals

### Creating Strings

Python offers several ways to create string literals:

```python
# Single quotes
single_quote = 'Hello, World!'
print(single_quote)
# Output: Hello, World!

# Double quotes
double_quote = "Hello, World!"
print(double_quote)
# Output: Hello, World!

# Triple quotes (for multiline strings)
multiline = """This is a
multiline string
that spans several lines."""
print(multiline)
# Output: This is a
#         multiline string
#         that spans several lines.

# Triple single quotes also work
another_multiline = '''Another way
to create multiline
strings.'''
print(another_multiline)
# Output: Another way
#         to create multiline
#         strings.
```

### When to Use Each Type

- **Single quotes**: Most common for simple strings
- **Double quotes**: When your string contains single quotes
- **Triple quotes**: For multiline strings or docstrings

```python
# Using double quotes when string contains single quotes
message = "It's a beautiful day!"
print(message)
# Output: It's a beautiful day!

# Using single quotes when string contains double quotes
quote = 'He said, "Python is amazing!"'
print(quote)
# Output: He said, "Python is amazing!"
```

### Exercise 1
Create three variables:
1. A string with your name using single quotes
2. A string containing a quote with double quotes inside using single quotes
3. A multiline string describing your favorite hobby

---

## 2 Escape Sequences

Escape sequences allow you to include special characters in strings that would otherwise be difficult or impossible to type directly.

### Common Escape Sequences

| Escape Sequence | Description | Example |
|-----------------|-------------|---------|
| `\'` | Single quote | `'It\'s working'` |
| `\"` | Double quote | `"He said \"Hello\""` |
| `\\` | Backslash | `"Path: C:\\Users"` |
| `\n` | Newline | `"Line 1\nLine 2"` |
| `\t` | Tab | `"Name:\tJohn"` |
| `\r` | Carriage return | `"Text\rNew"` |
| `\b` | Backspace | `"Hello\b World"` |
| `\0` | Null character | `"Text\0End"` |
| `\v` | Vertical tab | `"Text\vNext"` |
| `\f` | Form feed | `"Page\fBreak"` |

### Unicode Escape Sequences

| Sequence | Description | Example |
|----------|-------------|---------|
| `\uXXXX` | Unicode 16-bit hex | `\u03B1` (α) |
| `\UXXXXXXXX` | Unicode 32-bit hex | `\U0001F600` (😀) |
| `\xXX` | Hex character | `\x41` (A) |
| `\ooo` | Octal character | `\101` (A) |

### Examples

```python
# Basic escape sequences
print('It\'s a great day!')
# Output: It's a great day!

print("She said, \"Hello there!\"")
# Output: She said, "Hello there!"

print("Path: C:\\Users\\Documents")
# Output: Path: C:\Users\Documents

print("Line 1\nLine 2\nLine 3")
# Output: Line 1
#         Line 2
#         Line 3

print("Column1\tColumn2\tColumn3")
# Output: Column1    Column2    Column3

# Unicode examples
print("Greek letter alpha: \u03B1")
# Output: Greek letter alpha: α

print("Smiling face: \U0001F600")
# Output: Smiling face: 😀

print("Hex character: \x48\x65\x6C\x6C\x6F")
# Output: Hex character: Hello
```

### Raw Strings

Raw strings treat backslashes literally by prefixing with `r`:

```python
# Regular string
regular = "C:\new\folder"
print(regular)
# Output: C:
#         ew\folder (problematic due to \n)

# Raw string
raw = r"C:\new\folder"
print(raw)
# Output: C:\new\folder
```

### Exercise 2
1. Create a string that displays: `He said, "It's working!"`
2. Create a string with three lines using `\n`
3. Create a raw string for a Windows file path
4. Print your name with a tab before it

---

## 3 Formatted Strings

### F-strings (Formatted String Literals)

F-strings, introduced in Python 3.6, provide a concise and readable way to format strings:

```python
name = "Alice"
age = 30
salary = 75000.5

# Basic f-string
message = f"Hello, my name is {name} and I am {age} years old."
print(message)
# Output: Hello, my name is Alice and I am 30 years old.

# F-string with expressions
result = f"Next year, {name} will be {age + 1} years old."
print(result)
# Output: Next year, Alice will be 31 years old.
```

### Format Specifiers

Format specifiers control how values are displayed within f-strings and the `.format()` method.

#### Common Format Specifiers

| Specifier | Description | Example | Output |
|-----------|-------------|---------|--------|
| `:d` | Integer | `f"{42:d}"` | `42` |
| `:f` | Float | `f"{3.14159:f}"` | `3.141590` |
| `:e` | Scientific notation (lowercase) | `f"{1234:e}"` | `1.234000e+03` |
| `:E` | Scientific notation (uppercase) | `f"{1234:E}"` | `1.234000E+03` |
| `:%` | Percentage | `f"{0.75:%}"` | `75.000000%` |
| `:b` | Binary | `f"{10:b}"` | `1010` |
| `:o` | Octal | `f"{10:o}"` | `12` |
| `:x` | Hexadecimal (lowercase) | `f"{255:x}"` | `ff` |
| `:X` | Hexadecimal (uppercase) | `f"{255:X}"` | `FF` |

#### Width and Alignment

| Specifier | Description | Example | Output |
|-----------|-------------|---------|--------|
| `:10` | Minimum width 10 | `f"{'hi':10}"` | `'hi        '` |
| `:>10` | Right align, width 10 | `f"{'hi':>10}"` | `'        hi'` |
| `:<10` | Left align, width 10 | `f"{'hi':<10}"` | `'hi        '` |
| `:^10` | Center align, width 10 | `f"{'hi':^10}"` | `'    hi    '` |
| `:*^10` | Center with asterisk fill | `f"{'hi':*^10}"` | `'****hi****'` |

#### Precision and Sign

| Specifier | Description | Example | Output |
|-----------|-------------|---------|--------|
| `:.2f` | 2 decimal places | `f"{3.14159:.2f}"` | `3.14` |
| `:+` | Always show sign | `f"{42:+}"` | `+42` |
| `: ` | Space for positive numbers | `f"{42: }"` | ` 42` |
| `:,` | Thousands separator | `f"{1234567:,}"` | `1,234,567` |

### Examples

```python
# Width and alignment
name = "Python"
print(f"'{name:10}'")     # Left align (default)
# Output: 'Python    '

print(f"'{name:>10}'")    # Right align
# Output: '    Python'

print(f"'{name:^10}'")    # Center align
# Output: '  Python  '

print(f"'{name:*^10}'")   # Center with asterisk fill
# Output: '**Python**'

# Numbers formatting
pi = 3.14159265359
print(f"Pi to 2 decimals: {pi:.2f}")
# Output: Pi to 2 decimals: 3.14

print(f"Pi in scientific: {pi:e}")
# Output: Pi in scientific: 3.141593e+00

# Large numbers
big_number = 1234567
print(f"With commas: {big_number:,}")
# Output: With commas: 1,234,567

# Different bases
number = 255
print(f"Binary: {number:b}")      # Output: Binary: 11111111
print(f"Octal: {number:o}")       # Output: Octal: 377
print(f"Hex: {number:x}")         # Output: Hex: ff
print(f"HEX: {number:X}")         # Output: HEX: FF

# Percentage
ratio = 0.75
print(f"Success rate: {ratio:.1%}")
# Output: Success rate: 75.0%

# Sign formatting
positive = 42
negative = -42
print(f"Always show sign: {positive:+}, {negative:+}")
# Output: Always show sign: +42, -42

print(f"Space for positive: {positive: }, {negative: }")
# Output: Space for positive:  42, -42
```

### Exercise 3
1. Create variables for your name, age, and GPA, then create an f-string introducing yourself
2. Format a number with 2 decimal places and thousands separators
3. Display a number in binary, octal, and hexadecimal
4. Create a formatted table showing product names and prices aligned properly

---

## 4 String Operators

String operators allow you to manipulate and combine strings in various ways.

### String Operators Table

| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `+` | Concatenation | `"Hello" + " World"` | `"Hello World"` |
| `*` | Repetition | `"Hi" * 3` | `"HiHiHi"` |
| `in` | Membership (contains) | `"lo" in "Hello"` | `True` |
| `not in` | Not membership | `"xyz" not in "Hello"` | `True` |
| `[]` | Indexing | `"Hello"[1]` | `"e"` |
| `[:]` | Slicing | `"Hello"[1:4]` | `"ell"` |

### Examples

```python
# Concatenation
first_name = "John"
last_name = "Doe"
full_name = first_name + " " + last_name
print(full_name)
# Output: John Doe

# Repetition
separator = "-" * 20
print(separator)
# Output: --------------------

greeting = "Hello! " * 3
print(greeting)
# Output: Hello! Hello! Hello! 

# Membership testing
text = "Python programming"
print("Python" in text)        # Output: True
print("Java" in text)          # Output: False
print("xyz" not in text)       # Output: True

# Indexing (remember: 0-based indexing)
word = "Python"
print(word[0])    # Output: P (first character)
print(word[5])    # Output: n (last character)
print(word[-1])   # Output: n (last character using negative index)
print(word[-6])   # Output: P (first character using negative index)

# Slicing [start:end:step]
text = "Programming"
print(text[0:4])      # Output: Prog (characters 0 to 3)
print(text[4:])       # Output: ramming (from index 4 to end)
print(text[:4])       # Output: Prog (from start to index 3)
print(text[::2])      # Output: Pormmn (every 2nd character)
print(text[::-1])     # Output: gnimmargorP (reverse string)
print(text[2:8:2])    # Output: orm (from index 2 to 7, every 2nd)
```

### Advanced Slicing Examples

```python
sentence = "The quick brown fox jumps over the lazy dog"

# Get first 10 characters
print(sentence[:10])
# Output: The quick 

# Get last 10 characters
print(sentence[-10:])
# Output:  lazy dog

# Get every third character
print(sentence[::3])
# Output: T kc o ujsoet z g

# Reverse the string
print(sentence[::-1])
# Output: god yzal eht revo spmuj xof nworb kciuq ehT

# Get characters from index 4 to 15
print(sentence[4:16])
# Output: quick brown 
```

### Exercise 4
1. Create two strings and concatenate them with a space
2. Create a decorative border using the `*` operator
3. Check if the word "programming" contains the substring "gram"
4. Extract the first 5 characters from a string
5. Reverse a string using slicing

---

## 5 String Methods

Strings in Python are immutable, meaning they cannot be changed after creation. However, string methods return new strings with the desired modifications.

### String Methods Reference Table

| Method | Description | Example | Result |
|--------|-------------|---------|--------|
| `len(string)` | Length of string | `len("Hello")` | `5` |
| `.lower()` | Convert to lowercase | `"HELLO".lower()` | `"hello"` |
| `.upper()` | Convert to uppercase | `"hello".upper()` | `"HELLO"` |
| `.title()` | Title case | `"hello world".title()` | `"Hello World"` |
| `.capitalize()` | Capitalize first letter | `"hello".capitalize()` | `"Hello"` |
| `.strip()` | Remove whitespace | `" hello ".strip()` | `"hello"` |
| `.replace(old, new)` | Replace substring | `"hello".replace("l", "x")` | `"hexxo"` |
| `.count(sub)` | Count occurrences | `"hello".count("l")` | `2` |
| `.find(sub)` | Find substring index | `"hello".find("l")` | `2` |
| `.split(sep)` | Split into list | `"a,b,c".split(",")` | `["a", "b", "c"]` |
| `.join(list)` | Join list elements | `",".join(["a", "b"])` | `"a,b"` |
| `.startswith(str)` | Check if starts with | `"hello".startswith("he")` | `True` |
| `.endswith(str)` | Check if ends with | `"hello".endswith("lo")` | `True` |

### Case Conversion Methods

```python
text = "python PROGRAMMING language"

print(text.lower())
# Output: python programming language

print(text.upper())
# Output: PYTHON PROGRAMMING LANGUAGE

print(text.title())
# Output: Python Programming Language

print(text.capitalize())
# Output: Python programming language

# swapcase() - swaps case of each character
print(text.swapcase())
# Output: PYTHON programming LANGUAGE
```

### Whitespace and Cleaning Methods

```python
# strip() - removes whitespace from both ends
messy_string = "   Hello, World!   \n\t"
print(f"'{messy_string.strip()}'")
# Output: 'Hello, World!'

# lstrip() - removes whitespace from left
print(f"'{messy_string.lstrip()}'")
# Output: 'Hello, World!   \n\t'

# rstrip() - removes whitespace from right
print(f"'{messy_string.rstrip()}'")
# Output: '   Hello, World!'

# Remove specific characters
data = "###Hello, World!###"
print(data.strip("#"))
# Output: Hello, World!

# replace() - replace all occurrences
text = "Hello World Hello Universe"
print(text.replace("Hello", "Hi"))
# Output: Hi World Hi Universe

# Replace with limit
print(text.replace("Hello", "Hi", 1))  # Replace only first occurrence
# Output: Hi World Hello Universe
```

### Search and Count Methods

```python
sentence = "The quick brown fox jumps over the lazy dog"

# count() - count occurrences
print(sentence.count("the"))
# Output: 1

print(sentence.count("o"))
# Output: 4

# find() - find first occurrence (returns -1 if not found)
print(sentence.find("quick"))
# Output: 4

print(sentence.find("cat"))
# Output: -1

# index() - like find() but raises exception if not found
print(sentence.index("fox"))
# Output: 16

# rfind() - find last occurrence
text = "hello world hello universe"
print(text.find("hello"))     # Output: 0 (first occurrence)
print(text.rfind("hello"))    # Output: 12 (last occurrence)
```

### Split and Join Methods

```python
# split() - split string into list
csv_data = "apple,banana,orange,grape"
fruits = csv_data.split(",")
print(fruits)
# Output: ['apple', 'banana', 'orange', 'grape']

# Split with limit
text = "one-two-three-four-five"
print(text.split("-", 2))  # Split only twice
# Output: ['one', 'two', 'three-four-five']

# splitlines() - split by line breaks
multiline = "Line 1\nLine 2\nLine 3"
lines = multiline.splitlines()
print(lines)
# Output: ['Line 1', 'Line 2', 'Line 3']

# join() - join list elements into string
words = ["Python", "is", "awesome"]
sentence = " ".join(words)
print(sentence)
# Output: Python is awesome

# Join with different separator
print("-".join(words))
# Output: Python-is-awesome

# Join numbers (need to convert to strings first)
numbers = [1, 2, 3, 4, 5]
number_string = ",".join(str(num) for num in numbers)
print(number_string)
# Output: 1,2,3,4,5
```

### Boolean String Methods

```python
text = "Hello World"

# startswith() and endswith()
print(text.startswith("Hello"))    # Output: True
print(text.startswith("Hi"))       # Output: False
print(text.endswith("World"))      # Output: True
print(text.endswith("Universe"))   # Output: False

# Check multiple possibilities
print(text.startswith(("Hi", "Hello", "Hey")))  # Output: True

# Character type checking
print("123".isdigit())      # Output: True
print("abc".isalpha())      # Output: True
print("abc123".isalnum())   # Output: True
print("   ".isspace())      # Output: True
print("Hello World".isupper())    # Output: False
print("HELLO WORLD".isupper())    # Output: True
print("hello world".islower())    # Output: True
print("Hello World".istitle())    # Output: True
```

### Practical Examples

```python
# Processing user input
def clean_name(name):
    """Clean and format a user's name"""
    return name.strip().title()

user_input = "  john DOE  "
clean_name_result = clean_name(user_input)
print(f"Cleaned name: '{clean_name_result}'")
# Output: Cleaned name: 'John Doe'

# Parsing CSV-like data
def parse_grades(grade_string):
    """Parse a string of comma-separated grades"""
    grades = grade_string.split(",")
    return [float(grade.strip()) for grade in grades if grade.strip()]

grade_data = "85.5, 92.0, 78.5, , 95.0"
parsed_grades = parse_grades(grade_data)
print(f"Grades: {parsed_grades}")
# Output: Grades: [85.5, 92.0, 78.5, 95.0]

# Creating formatted output
def format_report(name, score, total):
    """Create a formatted score report"""
    percentage = (score / total) * 100
    bar_length = 20
    filled = int((score / total) * bar_length)
    bar = "█" * filled + "░" * (bar_length - filled)
    
    return f"""
Student Report
{"-" * 30}
Name: {name.title()}
Score: {score}/{total} ({percentage:.1f}%)
Progress: [{bar}]
""".strip()

report = format_report("alice johnson", 85, 100)
print(report)
# Output: Student Report
#         ------------------------------
#         Name: Alice Johnson
#         Score: 85/100 (85.0%)
#         Progress: [█████████████████░░░]
```

### Exercise 5
1. Create a function that takes a sentence and returns it with each word capitalized
2. Write code to count how many times each vowel appears in a given string
3. Create a function that removes all spaces from a string and converts it to lowercase
4. Parse a string containing "name:age:city" format and extract each component
5. Create a password validator that checks if a password contains uppercase, lowercase, and digits

---

## Strings Summary

In this chapter, we covered the comprehensive world of Python strings:

1. **String Literals**: Different ways to create strings using single, double, and triple quotes
2. **Escape Sequences**: Special characters and Unicode representations
3. **Formatted Strings**: F-strings and format specifiers for professional output
4. **String Operators**: Concatenation, repetition, membership testing, indexing, and slicing
5. **String Methods**: Extensive built-in methods for string manipulation and analysis

### Key Takeaways

- Strings are immutable in Python - methods return new strings rather than modifying originals
- F-strings provide the most readable and efficient way to format strings
- String methods are chainable: `text.strip().lower().replace(" ", "_")`
- Slicing with `[start:end:step]` is a powerful way to extract parts of strings
- Always consider edge cases when working with user input strings

### Best Practices

1. Use f-strings for string formatting when possible
2. Use raw strings (`r""`) for file paths and regular expressions
3. Always strip user input to remove unwanted whitespace
4. Use meaningful variable names when working with string data
5. Remember that string indices start at 0 and can be negative

### Next Steps

In the next chapter, we'll explore lists and how they work together with strings for more complex data processing tasks. The string methods you've learned here will be essential for text processing and data cleaning tasks throughout your Python programming journey.