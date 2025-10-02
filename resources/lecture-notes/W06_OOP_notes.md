# Week 6: Object-Oriented Programming - Lecture Notes

**Course:** IS4010 - AI-Enhanced Application Development
**Topic:** Object-Oriented Programming (OOP)
**Companion Materials:** [Slides](../IS4010_W06_OOP.qmd) | [Interactive Notebook](../../notebooks/IS4010_W06_OOP.ipynb) | [Lab 06](https://github.com/bgreenwell/is4010-course-template/tree/main/labs/lab06)

---

## 📋 Learning Objectives

By the end of this session, you should be able to:
- **Distinguish** when to use classes instead of functions for complex state management
- **Create classes** with constructors (`__init__`) and string representations (`__str__`)
- **Implement methods** that give objects behavior and encapsulate functionality
- **Use inheritance** to create specialized classes and enable code reuse
- **Apply advanced OOP concepts** like properties, class methods, and static methods

---

## Part 1: From Functions to Objects

### When Functions Aren't Enough

As programs grow in complexity, managing state with functions alone becomes challenging:
- **Parameter passing chaos**: Functions need many parameters to track related data
- **State management nightmares**: Keeping related data synchronized across function calls
- **Code duplication**: Similar logic repeated across multiple functions

### Why Classes Excel

Classes solve these problems by bundling data and behavior together:
- **Encapsulation**: Related data and operations live in one place
- **State management**: Objects maintain their own state without parameter passing
- **Extensibility**: Easy to add new capabilities without breaking existing code
- **Reusability**: Create multiple independent instances with shared structure
- **Maintainability**: Changes are localized to the class definition

### Real-World Applications
- **Social media**: User, Post, Comment, Story classes
- **E-commerce**: Product, ShoppingCart, Order, Payment classes
- **Games**: Player, Inventory, Character, Weapon classes
- **Banking**: Account, Transaction, Customer classes

---

## Part 2: Understanding Classes and Objects

### The `__init__` Method (Constructor)

The constructor is a special method that runs when you create a new object:
- **Purpose**: Initialize object attributes with starting values
- **The `self` parameter**: References the specific instance being created
- **Always first parameter** in instance methods
- **Each object gets its own copy** of attributes in separate memory

### The `__str__` Method (String Representation)

Defines how objects appear when printed:
- **Purpose**: Return user-friendly string representation
- **Called automatically** by `print()` and `str()`
- **Essential for debugging**: Makes testing and troubleshooting easier
- **Professional practice**: All production classes should have meaningful `__str__` methods

### Key Concepts
- **Instance attributes**: Each object has its own independent data
- **Type hints**: Modern Python practice for parameter and return types
- **Default parameters**: Provide flexibility in object creation

---

## Part 3: Methods and Behavior

### What Methods Define

Methods define what objects **DO**, not just what data they store:
- **Action methods**: Change object state (deposit, attack, add_item)
- **Query methods**: Return information without changing state (get_balance, is_alive)
- **Behavior encapsulation**: Related actions grouped with related data
- **Interface design**: Methods define how other code interacts with objects

### Method Types
- **Public methods**: Normal methods for external use
- **Private methods**: Use `_method_name` convention for internal helpers
- **Method chaining**: Methods can call other methods on the same object

### Design Principles
- **Single Responsibility**: Each method should do one thing well
- **Good naming**: Use action verbs for methods that change state
- **Validation**: Methods should ensure object stays in valid state

---

## Part 4: Inheritance - Code Reuse

### Core Inheritance Principles

Inheritance allows creating specialized classes based on existing ones:
- **Base class (parent)**: Common attributes and methods shared by all subclasses
- **Derived class (child)**: Inherits and adds specialized behavior
- **Method overriding**: Child replaces parent methods with specialized versions
- **`super()` function**: Calls parent class methods from child class
- **Code reuse**: Write common functionality once, use everywhere

### When to Use Inheritance

- **"Is-a" relationships**: ElectricCar IS-A Vehicle (not "has-a")
- **Shared behavior**: Multiple classes need similar functionality
- **Specialization**: Different types need slightly different behavior
- **Framework design**: Plugin architectures often use inheritance

### Design Considerations

- **Inheritance represents "is-a"**, not just code sharing
- **Inheritance vs Composition**: Sometimes composition (has-a) is better choice
- **Method Resolution Order (MRO)**: Python searches parent classes in specific order
- **Interface consistency**: All subclasses should work with same method calls

### Professional Examples
- **Web frameworks**: Django's BaseView, ListView, DetailView
- **Game engines**: GameObject, Player, Enemy, Projectile hierarchies
- **GUI frameworks**: Widget, Button, TextBox, Menu systems

---

## Part 5: Advanced OOP Concepts

### Properties (`@property`)

Control how attributes are accessed and modified:
- **When to use**: Data validation, computed values, API compatibility
- **Pattern**: `@property` for getter, `@property.setter` for validation
- **Private attributes**: Use `_attribute_name` convention
- **Computed properties**: Calculate values on-the-fly without storing them

### Class Methods (`@classmethod`)

Methods that operate on the class rather than instances:
- **When to use**: Alternative constructors (factory pattern), class-level operations
- **First parameter**: `cls` (the class itself)
- **Access**: Can modify class variables, not instance variables
- **Common uses**: Creating objects from different data formats

### Static Methods (`@staticmethod`)

Utility functions that belong with the class:
- **When to use**: Related functions that don't need instance or class data
- **No special first parameter**: Just regular function inside class
- **Organizational**: Groups related functionality with the class

### Class Variables

Variables shared across all instances:
- **Shared data**: Not unique per object
- **Access**: Via class name or instance
- **Common uses**: Counters, configuration settings, constants
- **Modification**: Changes affect all instances

---

## Part 6: Lab 06 Application

### Book and EBook Classes

The lab applies OOP concepts to a digital library system:

**Book class features:**
- Constructor with title, author, and year
- `get_age()` method to calculate book age
- `__str__` method for readable representation

**EBook inheritance:**
- Extends Book with `file_size` attribute
- Overrides `__str__` to include file size
- Demonstrates when to use inheritance

### Design Decisions
- **Specialized attributes**: `file_size` belongs only to EBook
- **Code reuse**: EBook inherits common book functionality
- **Future extensibility**: Easy to add AudioBook, PhysicalBook classes

### Real-World Relevance
- Digital libraries: Kindle, Apple Books, Google Books
- Content management systems
- Library catalog systems

---

## Key Takeaways

1. **OOP solves complexity** that functions alone can't handle elegantly
2. **Classes are blueprints** for objects with shared structure and behavior
3. **Inheritance enables code reuse** through "is-a" relationships
4. **Methods define behavior**, attributes store state
5. **Professional frameworks** extensively use OOP patterns

---

## Career Relevance

### Technical Interview Preparation
- **System design questions**: "How would you model a social media platform?"
- **OOP principles**: Demonstrate encapsulation, inheritance, polymorphism
- **Code quality**: Show maintainable, extensible code design

### Industry Applications
- **Web frameworks**: Django models, Flask-SQLAlchemy classes
- **Game development**: Unity/Unreal Engine component systems
- **Data science**: Scikit-learn estimators, pandas DataFrames
- **Mobile development**: iOS/Android framework design patterns

---

## Additional Resources

### Python Documentation
- [Python Classes Tutorial](https://docs.python.org/3/tutorial/classes.html)
- [Data Model Reference](https://docs.python.org/3/reference/datamodel.html) - Special methods
- [Object-Oriented Programming](https://docs.python.org/3/tutorial/classes.html#inheritance)

### Professional Development
- [Real Python OOP Tutorial](https://realpython.com/python3-object-oriented-programming/)
- [Design Patterns in Python](https://refactoring.guru/design-patterns/python)
- [PEP 8 Style Guide](https://www.python.org/dev/peps/pep-0008/)

---

**Last Updated**: 2025-01-15
**Instructor**: Brandon M. Greenwell
