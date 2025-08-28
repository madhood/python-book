### **Problem Statement**

You are tasked with creating the core logic for a self-checkout terminal at a grocery store. The program must process a customer's scanned items, calculate the total cost including discounts and taxes, and generate a formatted receipt. The entire program must be written as a single script without defining any functions, classes, or importing any modules.

The store has a special promotion:
*   **Membership Discount**: If a customer is a member (`is_member = True`) and their subtotal is \$30.00 or more, they receive a 10% discount on the subtotal.
*   **Loyalty Points**: The store calculates loyalty points using a complex number system. The real part of the number represents points earned from the total amount spent (1 point for every whole dollar), and the imaginary part represents a "bonus" for the number of items purchased (0.5 points per item).
*   **Sales Tax**: A 5% sales tax is applied to the final price after any discounts have been deducted.

### **Input/Output Format**

**Input:**
1.  A list of strings, where each string contains an item's details separated by commas: `SKU,Name,Price,Quantity`. The SKU is a unique integer identifier.
2.  A boolean value indicating the customer's membership status.

**Output:**
A single, multi-line string that represents the formatted customer receipt.

### **Constraints**

*   You must not use dictionaries, tuples, sets, functions, classes, or any imported modules. The entire solution must be a straight script using only loops, conditionals, and the data types provided.
*   Item prices and quantities can be integers or floats.
*   The solution should handle an empty list of items gracefully.

### **Example**

**Input Data:**
```python
# Customer's scanned items
scanned_items = [
    "47,Avocado,1.5,2",
    "255,Organic Milk,4.25,1",
    "30,Rye Bread,3.0,1"
]

# Customer's membership status
is_member = True
```

**Expected Output (as a single string):**
```
        *** FreshMart Receipt ***
========================================
SKU(hex)   Item             Qty    Total
----------------------------------------
0x2f       Avocado            2    $  3.00
0xff       Organic Milk       1    $  4.25
0x1e       Rye Bread          1    $  3.00

----------------------------------------
Subtotal:                    $ 10.25
Membership Discount (10.0%): $  0.00
Subtotal After Discount:     $ 10.25
Sales Tax (5.0%):            $  0.51
========================================
TOTAL:                       $ 10.76
========================================
Loyalty Points Earned: (10+1.5j)
Thank you for shopping with us!
```
*(Note: In this example, the subtotal is $10.25, which is less than $30, so the membership discount is not applied.)*

---