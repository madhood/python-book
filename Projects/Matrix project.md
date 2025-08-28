# **Project: Python Matrix Class Implementation**

## **Overview**

Your goal is to build a `Matrix` class in Python from scratch. This project will test your object-oriented programming skills by translating mathematical matrix concepts into a functional, intuitive class. You will implement initialization, element access, operator overloading, and a recursive determinant calculation.

## **Core Requirements**

Your `Matrix` class must implement the following features:

1.  **Initialization & Properties**
    *   `__init__(self, grid)`: Constructor that accepts a list of lists.
    *   `self.height` & `self.width`: Public attributes to store the matrix dimensions.

2.  **Representation & Indexing**
    *   `__str__(self)`: For user-friendly printing of the matrix grid.
    *   `__repr__(self)`: Return a string that can recreate the object (e.g., `"Matrix([[1, 2]])"`).
    *   `__getitem__(self, idx)`:
        *   If `idx` is an integer (e.g., `mat[row]`), return the row as a new `Matrix` object.
        *   If `idx` is a tuple (e.g., `mat[row, col]`), return the numerical element.
    *   `__setitem__(self, idx, value)`:
        *   If `idx` is a tuple (e.g., `mat[row, col] = 10`), update the single element.
        *   If `idx` is an integer (e.g., `mat[row] = [1, 2]`), replace the entire row.

3.  **Mathematical Operations (Operator Overloading)**
    *   `__add__(self, other)`: For `+` operator (supports both element-wise addition & scaler addition).
    *   `__sub__(self, other)`: For `-` operator (supports both element-wise subtraction & scaler subtraction).
    *   `__mul__(self, scalar)`: For `*` operator (supports both martix multiplication and scalar multiplication).
    *   All these methods must return a **new** `Matrix` object.

4. **Helper Methods**
   *    `is_square(self)`: Create a method that returns `True` if the matrix is square, `False` otherwise.
   *   `get_minor(self, r, c)`: returns a new `Matrix` object representing the sub-matrix formed by removing row `r` and column `c`. 

5. **Core Matrix Methods**
    *   `transpose(self)`: Return a new, transposed `Matrix` object.
    *   `determinant(self)`: Calculate the determinant for an `n x n` matrix **using recursion**. 

## **Bonus Tasks (Extra Credit)**

*   **Error Handling:** Add dimension checks to your mathematical operation methods (`__add__`, `__sub__`, `__matmul__`, `determinant`) and raise a `ValueError` for invalid operations.


## **Example Usage**

Your final class should support the following interactions:

```python
# Assuming your Matrix class is defined.

# 1. Initialization & Properties
m1 = Matrix([[1, 2], [3, 4]])
print(f"m_init: {m1.height}x{m1.width}")  # Expected: 2x2

# 2. Representation & Indexing
print(f"\n__str__:\n{m1}")
# Expected:
# 1 2
# 3 4
print(repr(m1))  # Expected: Matrix([[1, 2], [3, 4]])
print(m1[0, 1])  # Expected: 2
print(m1[0])  # Expected: Matrix([[1, 2]])

m2 = Matrix([[10, 20], [30, 40]])
m2[0, 0] = 5
print(m2)
# Expected:
# 5 20
# 30 40
m2[1] = [50, 60]
print(m2)
# Expected:
# 5 20
# 50 60
try:
    m2[0] = [1]
except ValueError as e:
    print(f"Set row error (expected): {e}")  # Expected: "Row length mismatch..."

# 3. Mathematical Operations
m_a = Matrix([[1, 2], [3, 4]])
m_b = Matrix([[5, 6], [7, 8]])
m_c = Matrix([[1, 2, 3], [4, 5, 6]])
m_d = Matrix([[7, 8], [9, 10], [11, 12]])
m_e = Matrix([[1, 2], [3, 4], [5, 6]])  # For incompatible matmul

print(m_a + m_b)
# Expected:
# 6 8
# 10 12
print(m_a + 10)
# Expected:
# 11 12
# 13 14
print(m_b - m_a)
# Expected:
# 4 4
# 4 4
print(m_a - 1)
# Expected:
# 0 1
# 2 3
print(m_a * 2)
# Expected:
# 2 4
# 6 8
print(m_c * m_d)
# Expected:
# 58 64
# 139 154
try:
    _ = m_a + m_c
except ValueError as e:
    print(f"Add incompatible error (expected): {e}")  # Expected: "Matrices must have same dimensions..."
try:
    _ = m_a * m_e  # 2x2 * 3x2
except ValueError as e:
    print(f"Mul incompatible error (expected): {e}")  # Expected: "Incompatible dimensions for matrix multiplication..."

# 4. Helper Methods
m_sq = Matrix([[1, 2], [3, 4]])
m_rect = Matrix([[1, 2, 3], [4, 5, 6]])
print(m_sq.is_square())  # Expected: True
print(m_rect.is_square())  # Expected: False

m_minor_test = Matrix([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
print(m_minor_test.get_minor(0, 0))
# Expected:
# 5 6
# 8 9

# 5. Core Matrix Methods
print(m_a.transpose())
# Expected:
# 1 3
# 2 4

m3 = Matrix([[1, 2], [3, 4]])
print(m3.determinant())  # Expected: -2

m4 = Matrix([[1, 2, 3], [0, 1, 4], [5, 6, 0]])
print(m4.determinant())  # Expected: 1

m5 = Matrix([[7]])
print(m5.determinant())  # Expected: 7

try:
    _ = m_rect.determinant()
except ValueError as e:
    print(
        f"Determinant non-square error (expected): {e}")  # Expected: "Determinant can only be calculated for square matrices..."

print("\n--- End of Example Usage ---")
```


