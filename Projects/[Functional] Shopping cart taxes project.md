## **Project: Grocery Cart Tax Calculation with Functional Programming**

## **Overview**

Having successfully implemented the `ShoppingCart` system using object-oriented design patterns, your next mission is to refactor and reimplement the core tax calculation logic using a **functional programming style**. This will challenge you to think about data transformation, pure functions, and composition, drawing inspiration from the `pipe`, `map_by`, and `lambda` constructs we discussed.
```python
from functools import reduce

apply_left = lambda f, g: lambda *args, **kwargs: g(f(*args, **kwargs))
pipe = lambda *functions: reduce(apply_left, functions)
map_by = lambda fun: lambda itr: map(fun, itr)

# data layer
cart = [
    {'name': 'apple', 'category': 'fruit', 'price': 60, 'quantity': 3},
    {'name': 'banana', 'category': 'fruit', 'price': 40, 'quantity': 4},
    {'name': 'potato', 'category': 'vegetable', 'price': 20, 'quantity': 3},
    {'name': 'rosemary', 'category': 'herp', 'price': 5, 'quantity': 4},
    {'name': 'tomato', 'category': 'vegetable', 'price': 10, 'quantity': 5},
]

# business layer
get_item_total = lambda item: item['quantity'] * item['price']
get_subtotal = pipe(map_by(get_item_total), sum)

apply_item_discount = lambda percent: lambda item: {**item, 'price': item['price'] * (1 - percent / 100)}

apply_fixed_discount = lambda value: lambda price: price - value

apply_general_discount = lambda percent: lambda cart: map(apply_item_discount(percent),cart)

apply_10_percent_general_discount = apply_general_discount(10)
apply_50_dollar_voucher = apply_fixed_discount(50)

apply_total_discount = pipe(apply_10_percent_general_discount, get_subtotal, apply_50_dollar_voucher)


# View layer
format_item = lambda item: f'[{item['category']}] {item["name"]}({item["price"]}$) x {item["quantity"]} = {get_item_total(item)}$'
join_with_newline = lambda lines: '\n'.join(lines)

# format_cart = lambda cart: join_with_newline(map(format_item, cart))
format_cart = pipe(map_by(format_item), join_with_newline)
discounted_cart = apply_10_percent_general_discount(cart)
new_total = apply_total_discount(cart)

print(format_cart(cart))
print(f'Subtotal: {get_subtotal(cart)}')
print("="*30)
print(format_cart(discounted_cart))
print(f'Total: {new_total}')
```

## **Core Requirements & Phases**

You will refactor the `ShoppingCart` system's tax calculation, neglecting the specific "threshold" and "category" based taxes initially, and then reintroduce them using a functional decorator pattern.

### **Data layer: Functional `CartItem` and `ShoppingCart` Basics**

1. Represent the `ShoppingCart` as a list of `CartItem` dictionaries. 
2. Represent `CartItem` as a dictionary (e.g., `{'name': 'Apple', 'price': 1.0, 'category': 'fruit', 'quantity': 3}`).

### **Initial business Logic layer**

1. Create a pure function `get_item_total` that returns `item['price'] * item['quantity']`. 
2. Create a pure function `get_subtotal` that calculates the sum of `get_item_total` for all items in the cart.

### **Initial view layer**

1. Create a pure function `formate_item` that returns string in the formate of `[category] name(price$) x quantity = item_total`. 
2. Create a pure function `formate_cart` that returns formated items string separated by new lines.
3. Print cart subtotal

### **Update Business Layer to Support Tax Calculations**

1. **Fixed tax value**: using `apply_fixed_tax`: A higher-order curried function that takes a `value` then `price` and returns a price after adding this value.
2. **General Tax rate**: `apply_general_tax_rate`: A curried function that takes `rate` then `cart` add tax to every item.
3. **Compose tax strategies**: Apply both strategies at the same time.
4. **[Bonus] Apply threshold**:  using python decorators:

Now, let's reintroduce the more complex tax rules using a functional decorator approach. In Python, decorators are a powerful way to wrap functions (Higher order function).

**Concept:** A decorator is essentially a higher-order function that takes another function as an argument, adds some functionality, and returns a new function.

**Reference:** To understand Python decorators in depth, please refer to this excellent tutorial: [Real Python - Primer on Python Decorators](https://realpython.com/primer-on-python-decorators/)

**Required:** implement apply_if decorator builder:
- **Write decorator builder:** `apply_if(checker)(tax_function)` that applies the tax function if the checker function gives true.
- **Make a checker:** a `is_luxury` that check if the tax exceeded a luxury threshold
- **Make a `luxury_fixed_tax`:** that is decorated by `apply_if(is_luxury)`
- **Compose the luxury tax:** `apply_general_tax_rate` then `apply_fixed_tax` then `apply_luxury_tax`

### **[Bonus] Apply tax to certain category**
Use decorator to check for a certain category to apply tax for and compose it with the previous methods: `apply_category_tax` then `apply_general_tax_rate` then `apply_fixed_tax` then `apply_luxury_tax`
