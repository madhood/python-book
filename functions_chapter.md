# Functions in Python - Building Blocks of Modular Programming

## 1. Introduction: Why Do We Need Functions?

Imagine you're writing a recipe book, and every time you need to explain how to boil water, you write out the entire process: "Fill a pot with water, place it on the stove, turn the heat to high, wait until bubbles form..." This would make your book incredibly long and repetitive!
Programming faces the same challenge. Without functions, we'd repeat the same code over and over. Functions solve three critical problems:

### 1.1 Don't Repeat Yourself (DRY Principle)

Before we dive into the mechanics of functions, let's understand why they're essential. Consider this scenario: you're building a program that calculates the area of circles in multiple places. Without functions, you might write:

```python
# Calculating circle area in three different places
import math

# For geometry calculator
radius1 = 5
area1 = math.pi * radius1 * radius1
print(f"A circle with radius {radius1} has an area: {area1}")

# For graphics program
radius2 = 3
area2 = math.pi * radius2 * radius2
print(f"A circle with radius {radius2} has an area: {area2}")

# For physics simulation
radius3 = 7
area3 = math.pi * radius3 * radius3
print(f"A circle with radius {radius3} has an area: {area3}")
```

What happens if you discover a bug in your area calculation, or need to use a more precise value of π? You'd have to find and fix the same code in three different places. This violates the **DRY principle**—**Don't Repeat Yourself**.

Functions solve this problem by allowing us to write the code once and use it many times:

```python
import math

def calculate_circle_area(radius):
    """Calculate the area of a circle given its radius."""
    area = math.pi * radius * radius
    print(print(f"A circle with radius {radius} has an area: {area}"))

# Now we can reuse this function anywhere
calculate_circle_area(5)
calculate_circle_area(3)
calculate_circle_area(7)
```

### 1.2 Separation of Concerns

Each function has one clear responsibility. Instead of one giant block of code that's hard to understand and debug, we can break our program into smaller, focused pieces:

```python
import math


def get_radius():
   """Get radius from user."""
   while True:
      user_input = input("Enter radius: ")
      if user_input.isnumeric():
         return float(user_input)
      else:
         print("Radius must be a number")

def calculate_circle_area(radius):
   """Calculate area of circle."""
   return math.pi * radius * radius

def display_circle_area(area):
   """Display the calculated area."""
   print(f"The circle area is: {area:.2f}")

# Main program flow
radius = get_radius()
area = calculate_circle_area(radius)
display_circle_area(area)
```
Each function has a single, clear purpose, making the code easier to understand, test, and maintain.

### 1.3 Easier Testing
Testing small functions is much easier than testing entire programs:
```python
def add_numbers(a, b):
    return a + b

# Easy to test individual functions
if __name__ == '__main__':
   if add_numbers(2, 3) == 5 and add_numbers(-1, 1) == 0:
      print('All tests passed!')
```


### 1.4 Practice Tasks
1. **Identify Repetition**: Look at this code and identify what should be turned into a function:
```python
name1 = "Alice"
name1_upper = name1.upper()
name1_formatted = f"Hello, {name1_upper}!"
print(name1_formatted)
   
name2 = "Bob"
name2_upper = name2.upper()
name2_formatted = f"Hello, {name2_upper}!"
print(name2_formatted)

name3 = "Charlie"
name3_upper = name3.upper()
name3_formatted = f"Hello, {name3_upper}!"
print(name3_formatted)
```

2. **Design Functions**: Think about a simple calculator program. What functions would you create to separate concerns? List at least 4 functions with their responsibilities.

---

## 2. Function Basics

### 2.1 Function Definition: The Recipe
A function tells Python what to do when the function is called, but doesn't actually do anything until executed. Like writing down a recipe. The actual cooking (execution) happens when you decide to use that recipe.

```python
# def keyword: tells Python we're defining a function
def function_name(parameters): # Optional parameters
    """Optional docstring explaining what the function does."""
    # Function body - the actual code
    return result  # Optional return statement
```

Let's create a simple function:

```python
def greet_user(name):
    """This function greets a user by name."""
    message = f"Hello, {name}! Welcome to our program."
    return message

# At this point, we've only DEFINED the function
# No greeting has happened yet - it's just a recipe
```

### 2.1 Function Execution: Applying the Recipe

To actually use a function, we **call** or **invoke** or **execute** it:

```python
def greet_user(name):
    """This function greets a user by name."""
    message = f"Hello, {name}! Welcome to our program."
    return message

# NOW we execute the function
greeting = greet_user("Alice")  # Function call/execution
print(greeting)  # Output: Hello, Alice! Welcome to our program.

# We can call it multiple times
print(greet_user("Bob"))    # Output: Hello, Bob! Welcome to our program.
print(greet_user("Carol"))  # Output: Hello, Carol! Welcome to our program.
```

### 2.2 Function Arguments and Return Value: Ingredients and Final Product

Functions can accept different types of arguments, just like recipes can have required ingredients, optional ingredients, and specific measurements. Functions can return values back to the caller. Think of this as the final product from following your recipe.

```python
def calculate_rectangle_area(length, width):
    """Calculate area of rectangle."""
    return length * width       # Sends the area back

# Order matters!
area = calculate_rectangle_area(5, 3)  # length=5, width=3
print(area)     # Output: 15

# for better readability use named arguments 
area2 = calculate_rectangle_area(length = 5, width = 3)
print(area2)    # Output: 15


# arguments can have default values (optional arguments)
def greet_user(name, greeting="Hello"):
    """Greet user with customizable greeting."""
    return f"{greeting}, {name}!"

# Using default greeting
print(greet_user("Alice"))  # Output: Hello, Alice!

# Providing custom greeting
print(greet_user("Bob", "Hi"))      # Output: Hi, Bob!
print(greet_user("Carol", "Hey"))   # Output: Hey, Carol!

# Functions without a return statement automatically return None
def greet_user(name):
    """Print greeting (no return value)."""
    print(f"Hello, {name}!")
    # No return statement means it returns None
greeting_result = greet_user("Alice") # Output: Hello, Alice!
print(greeting_result)                # Output: None
```

### 2.3 Practice Tasks

1. **Function Creation**: Write a function called `calculate_tip` that takes a bill amount and tip percentage (default 15%) and returns the tip amount.

2. **Multiple Parameters**: Create a function `format_address` that takes street, city, state, and zip_code. Make state and zip_code optional with defaults.

3. **Practice Calls**: Given this function, write 3 different ways to call it:
   ```python
   def book_hotel(guest_name, nights=1, room_type="standard", breakfast=False):
       return f"Booking for {guest_name}: {nights} nights in {room_type} room, breakfast: {breakfast}"
   ```
---

## 3. Lambda Functions: Shorthand for Simple Operations
Sometimes we need very simple functions for quick tasks. Lambda functions provide a concise way to write them. A lambda function is an anonymous function (a function without a name) that can have only one expression:

```python
# Regular function
def square(x):
    return x * x

# Equivalent lambda function
square_lambda = lambda x: x * x

# Both work the same way
print(square(5))        # Output: 25
print(square_lambda(5)) # Output: 25

# Lambda with multiple parameters
add = lambda x, y: x + y
print(add(3, 4))  # Output: 7

# Lambda with default parameter
greet = lambda name, greeting="Hello": f"{greeting}, {name}!"
print(greet("Alice"))          # Output: Hello, Alice!
print(greet("Bob", "Hi"))      # Output: Hi, Bob!
```
The syntax is: `lambda parameters: expression`

### 3.1 Practice Tasks

1. **Lambda Basics**: Create lambda functions for:
   - Converting Celsius to Fahrenheit: `F = C * 9/5 + 32`
   - Calculating the area of a circle: `area = π * r²`
   - Checking if a number is positive

2. **Lambda with Built-ins**: Given this list of dictionaries:
   ```python
   products = [
       {"name": "laptop", "price": 999.99},
       {"name": "mouse", "price": 25.50},
       {"name": "keyboard", "price": 75.00}
   ]
   ```
   Use lambda functions to:
   - Sort products by price
   - Filter products under $50
   - Create a list of just the product names
---

## 4. Scope: Understanding Variable Visibility]

Imagine you're in a large building with different rooms, floors, and departments. A conversation happening in one room might not be heard in another room, and some announcements are only relevant to specific floors, while others (like fire alarms) need to be heard throughout the entire building. Variable scope in Python works similarly—it determines where in your code a variable can be "seen" and used.

Understanding scope is crucial because it helps you avoid naming conflicts, write cleaner code, and understand how Python finds and uses variables.

### 4.1 How Python Looks for Variables: The LEGB Rule

Python follows a specific order when looking for variables, known as the **LEGB rule**:

**L**ocal → **E**nclosing → **G**lobal → **B**uilt-in

Let's explore each level with simple examples:

Variables created inside a function exist only within that function:

```python
global_var = 21             # Global scope

def outer():
    enclosing_var = 99      # Enclosing scope
    
    def inner():
        local_var = 7       # Local scope
        print(f"Print 'local_var' from inner function: {local_var}")
        print(f"Print 'enclosing_var' from inner function: {enclosing_var}")
        print(f"Print 'global_var' from inner function: {global_var}")
        print(f"All of the above is using built-in function 'print'")
    inner()
    
    def inner2():
       nonlocal enclosing_var
       global global_var
       enclosing_var += 1
       global_var += 9
       print(f"Modifying enclosing_var using 'nonlocal' keyword: {enclosing_var}")
       print(f"Modifying global_var using 'global' keyword: {global_var}")
    
    inner2()
    
outer()
# Print 'local_var' from inner function: 7
# Print 'enclosing_var' from inner function: 99
# Print 'global_var' from inner function: 21
# All of the above is using built-in function 'print'
# Modifying enclosing_var using 'nonlocal' keyword: 100
# Modifying global_var using 'global' keyword: 30
```
* **global**: Refers to the module-level (global) variable.

* **nonlocal**: Refers to the nearest enclosing scope variable (not global, not local).

* **Avoid**: Modifying global variables inside functions.

### 4.2 Practice Tasks

1. **Scope Detective**: Predict what this code will print, then run it to check:
```python
x = "global"

def func1():
    x = "func1 local"
    print(f"In func1: {x}")

def func2():
    print(f"In func2: {x}")

func1()
func2()
print(f"Global: {x}")
```
2. **Variable Hunting**: In this code, identify the scope of each variable:
```python
total_users = 1000

def process_user(user_name):
    status = "processing"
    
    def validate_name():
        min_length = 2
        return len(user_name) >= min_length
    
    is_valid = validate_name()
    return is_valid
```

3. **Fix the Scope**: This code has scope-related bugs. Fix them:
```python
bank_balance = 100

def deposit(amount):
    bank_balance = bank_balance + amount
    return bank_balance

def withdraw(amount):
    bank_balance = bank_balance - amount
    return bank_balance

print(deposit(50))
print(withdraw(25))
print(bank_balance)
```
---

## 5. Organizing Your Code with Modules and Imports

As you progress in your programming journey, your programs will naturally grow larger and more complex. Keeping all your code in a single file can quickly become messy, making it difficult to read, debug, and maintain. This is where **modules** become essential.

A module is simply a Python file containing reusable code, such as functions, variables, or classes. By dividing your code into modules, you can organize it into smaller, logical pieces, each dedicated to a specific purpose. To use the code from one module in another file, you use the **`import`** statement.

Python also comes with a rich **standard library**, which is a collection of built-in modules for common tasks like performing mathematical calculations, generating random numbers, or working with dates. These ready-made modules save you from having to write everything from scratch.
---

## 5.1 Getting Started: A Hands-On Example

Let's build a simple shape area calculator to see how modules work in action. We will create a custom module for our shape calculations and also import a value from one of Python's built-in libraries.

### Step 1: Create a Custom Module

First, we'll create a module to handle the area calculations for different shapes.

1.  Create a new file and name it `shapes.py`.
2.  Inside this file, we will define functions to calculate the area of a circle, a square, and a rectangle.

Your `shapes.py` file should look like this:

```python
# shapes.py

from math import pi # Grab just the 'pi' constant from the built-in math library

def circle_area(radius):
  """Calculates the area of a circle."""
  return pi * radius ** 2

def square_area(side):
  """Calculates the area of a square."""
  return side * side

def rectangle_area(length, width):
  """Calculates the area of a rectangle."""
  return length * width
```

In the code above, we used `from math import pi`. This is a great example of using a built-in Python module. Instead of importing the entire `math` library, we are only pulling in the `pi` constant, which is all we need. This keeps our code tidy.

### Step 2: Import and Use Your Module

Now that we have our `shapes` module, let's use it in another program.

1.  In the **same directory** as `shapes.py`, create a new file named `area_calculator.py`.
2.  This file will contain the main logic of our program, including the user interface.

Your `area_calculator.py` should look like this:

```python
# area_calculator.py

# Import the entire 'shapes' module
import shapes

 print("Shape Area Calculator")
 print("-------------------")
 print("1. Circle")
 print("2. Square")
 print("3. Rectangle")
 
 choice = input("Pick a shape (1-3): ")

 if choice == '1':
     radius = float(input("Enter the radius: "))
     area = shapes.circle_area(radius)
     print(f"The area of the circle is: {area:.2f}")
 elif choice == '2':
     side = float(input("Enter the side length: "))
     area = shapes.square_area(side)
     print(f"The area of the square is: {area:.2f}")
 elif choice == '3':
     length = float(input("Enter the length: "))
     width = float(input("Enter the width: "))
     area = shapes.rectangle_area(length, width)
     print(f"The area of the rectangle is: {area:.2f}")
 else:
     print("Oops! That's not a valid choice.")

# This is a standard Python convention. It ensures that the main() function
# runs only when this file is executed directly.
```

Notice the key difference here: we used `import shapes`. This loads the entire module. To access a function inside it, you must use the module name as a prefix, followed by a dot (e.g., `shapes.circle_area(radius)`). This method is very explicit and helps prevent naming conflicts if you have functions with the same name in different modules.

Additionally, Python allows you to use the `as` keyword when importing modules or objects to give them a different name in your code. For example, you could import the entire `shapes` module and give it a shorter alias:
```python
import shapes as s
print(s.circle_area(radius = 5))
```

This can make your code cleaner and easier to read, especially when dealing with long module names. The as keyword is particularly useful for shortening module names, avoiding naming conflicts, or improving readability by assigning a more descriptive name.

---

## 5.2 Common Mistakes to Avoid

When you're starting out with modules, you might run into a few common issues. Keep an eye out for these:

*   **Unsaved Files**: Always save your module file (`.py`) before you try to import it into another file. An unsaved file hasn't been written to disk, so Python can't find it.
*   **Spelling Errors**: Double-check that the module name in your `import` statement matches the filename exactly (e.g., `import shapes`, not `import shpaes`).
*   **File Location**: For now, make sure your module file and the file you are importing it into are in the same directory. Python looks in the current directory by default.
*   **Circular Imports**: Avoid creating a situation where two modules try to import each other. This can lead to errors that are difficult to track down.

With these skills, you’re now ready to write cleaner, more organized, and more powerful Python programs! Try expanding the `shapes` module with more functions (e.g., for a triangle or trapezoid) to practice.

---

### Testing a Module with `if __name__ == "__main__"`

It's a common practice to include a special block of code at the end of a module that allows you to test its functions when the file is run directly. This code will not execute when the module is imported into another file. This is achieved using the conditional `if __name__ == "__main__"`.

The `__name__` variable is a special built-in variable that Python sets to `"__main__"` when you run the file directly. If the file is imported, `__name__` is set to the module's filename (e.g., `"shapes"`).

Here’s how you can add a testing block to your `shapes.py` file:

```python
# shapes.py

from math import pi # Grab just the 'pi' constant from the built-in math library

def circle_area(radius):
  """Calculates the area of a circle."""
  return pi * radius ** 2

def square_area(side):
  """Calculates the area of a square."""
  return side * side

def rectangle_area(length, width):
  """Calculates the area of a rectangle."""
  return length * width

# This block runs only when the file is executed directly
if __name__ == "__main__":
    print("Testing the functions in the 'shapes' module...")
    test_cases = [
       {"function": circle_area, "parameters": [5], "expected": 78.53981633974483},  # Radius 5
       {"function": circle_area, "parameters": [0], "expected": 0.0},  # Zero radius
       {"function": circle_area, "parameters": [2.5], "expected": 19.634954084936208},  # Radius 2.5
       {"function": square_area, "parameters": [4], "expected": 16},  # Side 4
       {"function": square_area, "parameters": [0], "expected": 0},  # Zero side
       {"function": square_area, "parameters": [10], "expected": 100},  # Side 10
       {"function": rectangle_area, "parameters": [3, 6], "expected": 18},  # Length 3, width 6
       {"function": rectangle_area, "parameters": [0, 5], "expected": 0},  # Zero length
       {"function": rectangle_area, "parameters": [2, 2], "expected": 4},  # Length 2, width 2
    ]
    
    for test in test_cases:
        params = test["parameters"]
        expected = test["expected"]
        func = test["function"]
        result = func(*params)  # Unpack parameters and call the function
        if abs(result - expected) < 0.0001:  # Use small delta for floating-point comparison
            print(f"✓ Test for {func.__name__} with parameters {params} passed")
        else:
            print(f"[✗] Test for {func.__name__} with parameters {params} failed: expected {expected}, got {result}")
```

Now, if you run `python shapes.py` in your terminal, it will execute the print statements and show you the output of the functions, providing a quick and easy way to verify that your module is working correctly. If you run `area_calculator.py`, this block will be ignored, and the functions will be available for import as intended.

### 5.3 Practice Tasks
1. **Travel Distance Converter**
Objective: Create a modular program to convert distances between different units for travel planning.

Create a module called distance.py with the following functions:
* `km_to_miles(km)`: Converts kilometers to miles (1 km = 0.621371 miles).
* `miles_to_km(miles)`: Converts miles to kilometers (1 mile = 1.60934 km).
* `travel_time(distance, speed)`: Calculates travel time in hours given a distance (in km) and speed (in km/h). 
* Add an if __name__ == "__main__" block in distance.py to test each function (e.g., convert 100 km to miles, 50 miles to km, and calculate time for 200 km at 80 km/h). 
* Create a travel_app.py file that imports distance.py and provides a user interface to:
  * Convert distances between kilometers and miles. 
  * Calculate travel time based on user-entered distance and speed.

### 6. The Power of Pure Functions (advanced)

Now that we've explored modules and how to import code, let's delve into a concept that will significantly improve the quality and reliability of your programs: **pure functions**. By understanding and utilizing pure functions, you can write code that is easier to test, reason about, and less prone to bugs.

#### What is a Pure Function?

A pure function is a function that adheres to two simple rules:

1.  **It always returns the same output for the same input.** Given a specific set of arguments, a pure function will consistently produce the same result. It doesn't rely on any external state or information that might change.
2.  **It has no side effects.** A pure function does not modify any data outside of its own scope. This means it doesn't change variables outside the function, alter data structures in place, print to the console, or write to a file. Its only job is to take input and produce output.

Let's look at an example. Imagine a function that calculates the area of a circle.

**Pure Functions:**

```python
def add_numbers(a, b):
    """Pure function - always returns the same result for same inputs"""
    return a + b

def calculate_area(length, width):
    """Pure function - no side effects, predictable output"""
    return length * width

def get_full_name(first_name, last_name):
    """Pure function - deterministic string manipulation"""
    return f"{first_name} {last_name}"

```

**Impure Functions:**

```python
import random
from datetime import datetime

# IMPURE: Different output for same input
def roll_dice():
    return random.randint(1, 6)

# IMPURE: Output depends on current time
def get_current_hour():
    return datetime.now().hour

# IMPURE: Modifies global state (side effect)
counter = 0
def increment_counter():
    global counter
    counter += 1  # Side effect!
    return counter

# IMPURE: Modifies the input list (side effect)
def add_item_impure(items, new_item):
    items.append(new_item)  # Modifies original list
    return items
```

#### The Advantage of Testability

Pure functions are incredibly easy to test because they're predictable. You don't need to worry about external dependencies or changing states.

#### Isolating Side Effects for a Bug-Free Codebase

The second major advantage of pure functions is the isolation of side effects. Side effects, like modifying a global variable or printing to the console, can make your code difficult to debug. When a function has a side effect, its impact is not contained within the function itself, which can lead to unexpected behavior in other parts of your program.

By keeping most of your functions pure, you create a codebase that is largely predictable and easy to reason about. The core logic of your application is encapsulated in these pure functions, and any parts of your code that need to interact with the outside world (like user input or file I/O) can be kept separate and small. This separation makes it much easier to find and fix bugs.

When a bug does occur, you can be confident that the issue is not hidden within your pure functions, as they are guaranteed to work as expected given the correct inputs. This allows you to focus your debugging efforts on the smaller, impure parts of your code.

By striving to write pure functions whenever possible, you'll build a strong foundation for creating robust, maintainable, and largely bug-free applications.

### Practice Tasks

1. **Identify Pure vs Impure**: Classify each function as pure or impure and explain why:
   ```python
   def multiply(x, y):
       return x * y
   
   def get_user_input():
       return input("Enter a number: ")
   
   def format_currency(amount):
       return f"${amount:.2f}"
   
   def save_to_database(data):
       # Simulated database save
       print(f"Saving {data} to database")
       return True
   
   def is_adult(age):
       return age >= 18
   ```

2. **Purify Functions**: Convert these impure functions to pure functions:
   ```python
   import datetime
   
   current_year = 2024
   
   def calculate_age_impure(birth_year):
       return current_year - birth_year
   
   def greet_user_impure(name):
       greeting = f"Hello, {name}!"
       print(greeting)
       return greeting
   
   scores = []
   def add_score_impure(score):
       scores.append(score)
       return len(scores)
   ```

3. **Create Pure Functions**: Write pure functions for:
   - Converting temperature between Celsius and Fahrenheit
   - Calculating compound interest
   - Determining if a year is a leap year
   - Finding the maximum value in a list

---

## 7. Chapter Summary and Comprehensive Project

### 7.1 Key Concepts Recap

Throughout this chapter, we've explored the fundamental building blocks of modular programming in Python:

**Functions as Blueprints**: Functions are reusable recipes that organize our code and eliminate repetition, following the DRY principle.

**Function Anatomy**: We learned how to define functions with parameters (including defaults and named arguments), execute them, and return values to create flexible, reusable code blocks.

**Lambda Functions**: These provide a concise way to create simple, one-expression functions, particularly useful with built-in functions like `map()`, `filter()`, and `sort()`.

**Scope (LEGB Rule)**: Python searches for variables in Local, Enclosing, Global, then Built-in scopes, determining where variables can be accessed and modified.

**Modularity**: Breaking complex problems into smaller, focused modules makes code more readable, testable, and maintainable through separation of concerns.

**Pure Functions**: These mathematical-style functions are deterministic, have no side effects, and depend only on their input parameters, making them incredibly reliable and easy to test.

### 7.2 Student Challenge Projects

Now that you've mastered functions, here are some challenging projects that will test and expand your skills:

**Project 1: Grade Calculator with GPA**
Create a program that:
- Manages multiple students and courses
- Calculates letter grades from percentages
- Computes GPA using a 4.0 scale
- Generates transcript reports
- Uses pure functions for all calculations

**Project 2: Simple Inventory Management**
Build a system that:
- Tracks product inventory (name, quantity, price)
- Handles stock additions and sales
- Calculates inventory value
- Identifies low-stock items
- Generates sales reports

**Project 3: Text Adventure Game**
Create a text-based adventure game with:
- Multiple rooms/locations
- Player inventory system
- Combat or puzzle mechanics
- Save/load game state
- Modular functions for each game mechanic

**Project 4: Recipe Calculator**
Develop a program that:
- Stores recipes with ingredients and quantities
- Scales recipes up or down for different serving sizes
- Calculates total cost based on ingredient prices
- Suggests recipes based on available ingredients
- Handles unit conversions (cups to liters, etc.)

**Project 5: Simple Banking System**
Design a banking simulator that:
- Manages multiple accounts
- Handles deposits, withdrawals, and transfers
- Calculates compound interest
- Maintains transaction history
- Generates account statements
- Uses pure functions for all financial calculations

Each of these projects should demonstrate:
- Proper use of pure functions where possible
- Good modularity and separation of concerns
- Input validation and error handling
- Clear function documentation
- Simple test functions for critical calculations

Remember: Start small, build incrementally, and test your functions as you go. Great programmers aren't those who write perfect code immediately—they're those who break problems down into manageable pieces and solve them step by step!

---

*"The best functions are like good tools: they do one thing exceptionally well, and they do it the same way every time."*