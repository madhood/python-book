# **Project: Grocery Cart Tax Calculation with Design Patterns**

## **Overview**

Your mission is to build a `ShoppingCart` system that dynamically applies various tax calculations using three fundamental object-oriented design patterns: Strategy, Composite, and Decorator. This project will guide you through refactoring and extending a basic cart implementation to handle complex tax rules elegantly.

## **Core Requirements**

Your `ShoppingCart` system must implement the following features across four phases:

### **Phase 1: Basic Shopping Cart Implementation**

1.  **`CartItem` Class:**
    *   `__init__(self, name: str, price: float, category: str, quantity: int)`: Constructor.
    *   `name`: Item's name (e.g., "Apple").
    *   `price`: Price per unit.
    *   `category`: Category (e.g., "fruit", "vegetable", "herb").
    *   `quantity`: Number of units.
    *   `get_total_price(self) -> float`: Returns `price * quantity`.
    *   `__str__(self) -> str`: Returns `[category] name(price$) x quantity = total_price`.

2.  **`ShoppingCart` Class:**
    *   `__init__(self, items: List[CartItem] = None)`: Constructor, initializes with an optional list of `CartItem` objects.
    *   `items`: A list to store `CartItem` objects.
    *   `add_item(self, item: CartItem)`: Adds an item to the cart.
    *   `remove_item(self, item_name: str)`: Removes an item by its name.
    *   `get_subtotal(self) -> float`: Calculates the sum of `get_total_price()` for all items.
    *   `get_tax(self) -> float`: **Initially returns `0`**.
    *   `get_total(self) -> float`: Returns `get_subtotal() + get_tax()`.
    *   `__str__(self) -> str`: Returns the string representation of each cart item in a separate line.

### **Phase 2: Strategy Pattern for Tax Calculation**

1.  **`TaxStrategy` (Abstract Base Class/Interface):**
    *   `abstractmethod apply(self) -> float`: An abstract method for calculating tax.

2.  **Concrete `TaxStrategy` Implementations:**
    *   `FlatRateTaxStrategy(TaxStrategy)`: Calculates a flat percentage tax (e.g., 5% of subtotal).
        *   `__init__(self, rate: float)`
        *   `apply(self, cart: ShoppingCart) -> float`
    *   `CategoryBasedTaxStrategy(TaxStrategy)`: Applies different tax rates based on `CartItem` categories.
        *   `__init__(self, rates: Dict[str, float])` (e.g., `{"fruit": 0.02, "vegetable": 0.03}`)
        *   `apply(self, cart: ShoppingCart) -> float`
    *   `NoTaxStrategy(TaxStrategy)`: Always returns `0` tax.
        *   `apply(self, cart: ShoppingCart) -> float`

3.  **`ShoppingCart` Integration:**
    *   Modify `ShoppingCart` to hold an instance of `TaxStrategy` (e.g., `self.tax_strategy`).
    *   Update `get_tax()` to delegate the calculation to `self.tax_strategy.apply(self)`.

### **Phase 3: Composite Pattern for Combining Tax Strategies**

1.  **`CompositeTaxStrategy(TaxStrategy)`:**
    *   Implements the `TaxStrategy` interface.
    *   `__init__(self, strategies: List[TaxStrategy] = None)`: Initializes with a list of child strategies.
    *   `add_strategy(self, strategy: TaxStrategy)`: Adds a strategy to the composite.
    *   `apply(self, cart: ShoppingCart) -> float`: Iterates through its child strategies, sums their calculated taxes, and returns the total.

### **Phase 4: Decorator Pattern for Dependent Tax Calculations**

1.  **`TaxDecorator` (Abstract Base Class):**
    *   Inherits from `TaxStrategy`.
    *   `__init__(self, wrapped_strategy: TaxStrategy)`: Takes another `TaxStrategy` object to wrap.
    *   `wrapped_strategy`: The component being decorated.
    *   `apply(self, cart: ShoppingCart) -> float`: Abstract method. Concrete decorators will override this.

2.  **Concrete `TaxDecorator` Implementations:**
    *   `LuxuryTaxDecorator(TaxDecorator)`: Applies an additional percentage tax if the cart's subtotal exceeds a threshold.
        *   `__init__(self, wrapped_strategy: TaxStrategy, threshold: float, luxury_rate: float)`
        *   `apply(self, cart: ShoppingCart) -> float`: Calculates the base tax, then adds luxury tax if applicable.