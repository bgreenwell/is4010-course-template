# Lab 06: object-oriented programming

**Due:** Sunday, October 12 at 11:59 PM
**Points:** 10

## Objective

The goal of this lab is to master the fundamental concepts of [object-oriented programming (OOP)](https://docs.python.org/3/tutorial/classes.html) by creating custom classes with constructors, methods, and inheritance. You will model real-world objects as [Python classes](https://docs.python.org/3/tutorial/classes.html) and use [AI assistance](https://claude.ai/) to explore different implementation approaches. Your work will be graded automatically by our [CI/CD pipeline](https://docs.github.com/en/actions).

## Background

[Object-oriented programming](https://docs.python.org/3/tutorial/classes.html) revolutionizes how we structure applications by allowing us to create custom data types that bundle together data (attributes) and behavior (methods). This powerful paradigm is used in every major software system, from web frameworks like [Django](https://docs.djangoproject.com/en/stable/topics/class-based-views/) to game engines and enterprise applications.

**What you'll learn:**
- **Class design**: Creating blueprints for objects with [constructors](https://docs.python.org/3/reference/datamodel.html#object.__init__) and [string representations](https://docs.python.org/3/reference/datamodel.html#object.__str__)
- **Method implementation**: Adding behavior to objects with instance methods
- **Inheritance**: Creating specialized classes that inherit from base classes using [`super()`](https://docs.python.org/3/library/functions.html#super)
- **Professional practices**: Writing clean, testable OOP code with proper documentation

**Key concepts applied:**
- [Classes and objects](https://docs.python.org/3/tutorial/classes.html#a-first-look-at-classes)
- [Instance attributes and methods](https://docs.python.org/3/tutorial/classes.html#class-objects)
- [Inheritance and method overriding](https://docs.python.org/3/tutorial/classes.html#inheritance)
- [The `super()` function](https://docs.python.org/3/library/functions.html#super) for calling parent class methods

This lab is divided into two parts:
- **Part 1**: Create a base `Book` class with constructors and string representation
- **Part 2**: Add methods and create an `EBook` child class using inheritance

-----

## Part 1: create a base class

### The challenge

Your first task is to create a class that serves as a blueprint for a `Book`. This will give you hands-on practice with the fundamental building blocks of object-oriented programming: class definition, constructors, and string representation.

**Key concepts applied:**
- [Class definition](https://docs.python.org/3/tutorial/classes.html#class-definition-syntax) with proper naming conventions
- [Constructor methods](https://docs.python.org/3/reference/datamodel.html#object.__init__) for object initialization
- [String representation](https://docs.python.org/3/reference/datamodel.html#object.__str__) for user-friendly output
- Instance attributes and data encapsulation

### Your task

1. In your `is4010-labs` repository, create a new file named `lab06.py`.
2. Inside this file, define a new class named `Book`.
3. Use an [AI assistant](https://claude.ai/) to help you write the `__init__` constructor method. It should accept `title` (str), `author` (str), and `year` (int) as parameters and store them as attributes on the object.
4. Next, ask your AI assistant to help you write the `__str__` dunder method. This method should return a user-friendly string that includes the book's title, author, and publication year.
5. At the bottom of your file, add a main execution block (`if __name__ == '__main__':`) to test your work. Inside this block, create at least one instance of your `Book` class and `print()` it to the console to verify that your `__str__` method works correctly.

### Understanding constructors and string representation

The [`__init__` method](https://docs.python.org/3/reference/datamodel.html#object.__init__) is a special "dunder" (double underscore) method that runs automatically when a new object is created. Think of it as the object's initialization blueprint:

```python
class Book:
    def __init__(self, title, author, year):
        # Store the parameters as instance attributes
        self.title = title
        self.author = author
        self.year = year
```

The [`__str__` method](https://docs.python.org/3/reference/datamodel.html#object.__str__) defines how your object appears when printed or converted to a string. This is essential for debugging and user interaction:

```python
def __str__(self):
    return f"\"{self.title}\" by {self.author} ({self.year})"
```

### AI assistant prompts for Part 1

Try these specific prompts to get started:

- *"Help me create a Python class called Book with a constructor that takes title, author, and year parameters. Include a __str__ method that formats the book information nicely."*
- *"I need to write a Book class in Python. The constructor should store title, author, and year as instance attributes. Show me how to write a good __str__ method too."*
- *"What's the best way to format the string representation of a Book object? I want it to look professional when printed."*

-----

## Part 2: add methods and inheritance

### The challenge

Now you will extend the functionality of your `Book` class and create a more specialized `EBook` class that inherits from it. This part demonstrates the power of [inheritance](https://docs.python.org/3/tutorial/classes.html#inheritance) for code reuse and specialization.

**Key concepts applied:**
- [Instance methods](https://docs.python.org/3/tutorial/classes.html#method-objects) for object behavior
- [Inheritance syntax](https://docs.python.org/3/tutorial/classes.html#inheritance) and relationships
- [Method overriding](https://docs.python.org/3/tutorial/classes.html#inheritance) for specialized behavior
- [The `super()` function](https://docs.python.org/3/library/functions.html#super) for calling parent methods

### Your task

1. **Add a method to `Book`**: In your `Book` class, create a new method called `get_age()`. This method should take no parameters (other than `self`) and should calculate and return the age of the book based on its publication year. You can assume the current year is **2025** for your calculation.

2. **Create a child class**: Below your `Book` class, define a new class named `EBook` that inherits from `Book`.

3. **Extend the constructor**: The `EBook`'s `__init__` method should accept all the same parameters as `Book`, plus a new one: `file_size` (int, representing megabytes). Inside this method, you must call the parent class's constructor using [`super()`](https://docs.python.org/3/library/functions.html#super) to handle the title, author, and year.

4. **Override a method**: In the `EBook` class, override the `__str__` method. The new version should call the parent's `__str__` method using `super()` to get the base string, and then append the file size information to it. The final output should include all the book's details plus its file size (e.g., "... (12 MB)").

5. **Test your new class**: In your main execution block, create an instance of your new `EBook` class and print it to the console. Also, call its `get_age()` method to verify that it correctly inherited it from the `Book` class.

### Understanding inheritance and `super()`

[Inheritance](https://docs.python.org/3/tutorial/classes.html#inheritance) allows one class to inherit attributes and methods from another class. The child class can use everything from the parent class, plus add its own unique features:

```python
class EBook(Book):  # EBook inherits from Book
    def __init__(self, title, author, year, file_size):
        super().__init__(title, author, year)  # Call parent constructor
        self.file_size = file_size  # Add new attribute
```

The [`super()` function](https://docs.python.org/3/library/functions.html#super) lets you call methods from the parent class. This is essential for maintaining the parent's functionality while adding new features:

```python
def __str__(self):
    # Get the parent's string representation
    parent_str = super().__str__()
    # Add our own information
    return f"{parent_str} ({self.file_size} MB)"
```

### AI assistant prompts for Part 2

Try these prompts to master inheritance:

- *"Help me add a get_age() method to my Book class that calculates the book's age based on its publication year. Assume the current year is 2025."*
- *"I need to create an EBook class that inherits from Book. The EBook should have an additional file_size parameter and override the __str__ method to include file size."*
- *"Show me how to use super() in Python to call the parent class constructor and methods. I'm working with a Book and EBook inheritance relationship."*
- *"How do I override a method in a child class while still using the parent's implementation? I want to extend, not replace, the functionality."*

-----

## Testing Your Code 🧪

You **must** create a test file for this lab to get full credit. This gives you hands-on experience with [pytest](https://docs.pytest.org/) testing for object-oriented code, which is essential for professional development.

### Setting up the test file

1. In your `lab06/` folder, create a new file named `test_lab06.py`.
2. Copy the entire code block below into this new file.
3. **Do not modify the test file** - it's designed to work with any correct implementation.

```python
# test_lab06.py
import pytest
from lab06 import Book, EBook


# Tests for the base Book class
def test_book_constructor():
    """Test that Book objects are created with correct attributes."""
    book = Book("The Hobbit", "J.R.R. Tolkien", 1937)
    assert book.title == "The Hobbit"
    assert book.author == "J.R.R. Tolkien"
    assert book.year == 1937


def test_book_str_method():
    """Test that Book objects have meaningful string representations."""
    book = Book("The Hobbit", "J.R.R. Tolkien", 1937)
    book_str = str(book)
    assert "The Hobbit" in book_str
    assert "J.R.R. Tolkien" in book_str
    assert "1937" in book_str


def test_book_get_age():
    """Test that Book.get_age() calculates age correctly."""
    book = Book("The Hobbit", "J.R.R. Tolkien", 1937)
    # Assuming current year is 2025 as per lab instructions
    assert book.get_age() == 2025 - 1937


def test_book_get_age_recent():
    """Test age calculation for a more recent book."""
    book = Book("Clean Code", "Robert Martin", 2008)
    assert book.get_age() == 2025 - 2008


# Tests for the EBook child class
def test_ebook_constructor():
    """Test that EBook objects inherit Book attributes and add file_size."""
    ebook = EBook("Dune", "Frank Herbert", 1965, 5)
    assert ebook.title == "Dune"
    assert ebook.author == "Frank Herbert"
    assert ebook.year == 1965
    assert ebook.file_size == 5


def test_ebook_str_method():
    """Test that EBook string representation includes all Book info plus file size."""
    ebook = EBook("Dune", "Frank Herbert", 1965, 5)
    ebook_str = str(ebook)
    # Should contain all Book information
    assert "Dune" in ebook_str
    assert "Frank Herbert" in ebook_str
    assert "1965" in ebook_str
    # Should also contain file size information
    assert "5" in ebook_str
    assert "MB" in ebook_str


def test_ebook_inherits_get_age():
    """Test that EBook inherits the get_age() method from Book."""
    ebook = EBook("Dune", "Frank Herbert", 1965, 5)
    assert ebook.get_age() == 2025 - 1965


def test_ebook_with_different_file_size():
    """Test EBook with different file size values."""
    small_ebook = EBook("Short Story", "Author Name", 2020, 2)
    large_ebook = EBook("Technical Manual", "Expert Author", 2018, 15)

    assert small_ebook.file_size == 2
    assert large_ebook.file_size == 15
    assert "2" in str(small_ebook) and "MB" in str(small_ebook)
    assert "15" in str(large_ebook) and "MB" in str(large_ebook)
```

### Running the tests locally

To run the tests on your local machine:

```bash
# Navigate to your lab06 directory
cd lab06/

# Run the tests
pytest test_lab06.py

# Or run with verbose output to see each test
pytest -v test_lab06.py
```

If all tests pass, you'll see output like:
```
========================= 8 passed in 0.05s =========================
```

If any tests fail, pytest will show you exactly which assertions failed and why, helping you debug your classes.

**💡 Understanding the tests:**

- **Book constructor tests**: Verify your `Book` class correctly stores title, author, and year attributes
- **String representation tests**: Check that your `__str__` methods produce meaningful, readable output
- **Method tests**: Ensure your `get_age()` method calculates correctly using 2025 as the current year
- **Inheritance tests**: Validate that `EBook` properly inherits from `Book` and adds its own functionality
- **Method override tests**: Confirm that `EBook.__str__()` includes both parent information and file size

-----

## Expected Repository Structure

By the end of this lab, your repository should have the following structure:

```
is4010-[your-username]-labs/
├── .github/
│   └── workflows/
│       └── main.yml          # GitHub Actions workflow (from Lab 03)
├── lab01/
│   └── hello.py              # Simple "Hello World" program from Lab 01
├── lab02/
│   ├── lab02.py              # AI-assisted functions from Lab 02
│   └── lab02_prompts.md      # Prompt engineering solutions from Lab 02
├── lab03/
│   ├── lab03.py              # Mad Libs function and guessing game from Lab 03
│   └── test_lab03.py         # Test file for Lab 03 functions
├── lab04/
│   ├── lab04.py              # Data structure functions from Lab 04
│   ├── lab04_prompts.md      # AI interaction documentation from Lab 04
│   └── test_lab04.py         # Test file for Lab 04 functions
├── lab05/
│   ├── lab05.py              # Refactored functions with error handling from Lab 05
│   └── test_lab05.py         # Test file for Lab 05 functions
├── lab06/
│   ├── lab06.py              # Book and EBook classes with inheritance (NEW)
│   └── test_lab06.py         # Test file for Lab 06 classes (REQUIRED)
└── README.md                 # Repository description (auto-created by GitHub)
```

**Key points about this structure:**
- **`lab06/lab06.py`**: Contains your `Book` and `EBook` classes with proper constructors, methods, and inheritance
- **`lab06/test_lab06.py`**: Required test file that validates your classes work correctly (provided test code must be copied exactly)
- **Cumulative structure**: Your repository now contains work from Labs 01-06, showing progression from basic scripts to object-oriented programming
- **Class requirements**: Your `lab06.py` should have both classes, a `get_age()` method, proper inheritance with `super()`, and an `if __name__ == '__main__':` testing block

This organized structure demonstrates your growing skills in Python programming, from procedural code to object-oriented design principles.

-----

## 🚨 Troubleshooting Guide

Object-oriented programming introduces new concepts that can be challenging! Here are solutions to common issues:

### **Problem: "I don't understand the difference between classes and objects"**
- **Cause**: Conceptual confusion about OOP fundamentals
- **Solution**:
  - Think of a **class** as a blueprint or template (like architectural plans)
  - Think of an **object** as a specific instance created from that blueprint (like a house built from the plans)
  - `Book` is the class; `my_book = Book("Title", "Author", 2023)` creates an object
  - Each object has its own unique data but follows the same class structure

### **Problem: "NameError: name 'self' is not defined"**
- **Cause**: Forgetting to include `self` as the first parameter in method definitions
- **Solution**:
  ```python
  # Wrong - missing self parameter
  def get_age():
      return 2025 - self.year

  # Correct - self is the first parameter
  def get_age(self):
      return 2025 - self.year
  ```

### **Problem: "AttributeError: 'Book' object has no attribute 'title'"**
- **Cause**: Not setting instance attributes in the `__init__` method
- **Solution**:
  ```python
  def __init__(self, title, author, year):
      # Make sure to assign to self.attribute_name
      self.title = title      # Not just: title = title
      self.author = author
      self.year = year
  ```

### **Problem: "TypeError: EBook.__init__() missing 1 required positional argument: 'file_size'"**
- **Cause**: Not calling the parent constructor correctly or missing parameters
- **Solution**:
  ```python
  class EBook(Book):
      def __init__(self, title, author, year, file_size):
          super().__init__(title, author, year)  # Call parent first
          self.file_size = file_size             # Then add new attributes
  ```

### **Problem: "My __str__ method doesn't work / objects print weird addresses"**
- **Cause**: Not implementing `__str__` method or syntax errors in the method
- **Solution**:
  ```python
  def __str__(self):
      return f"\"{self.title}\" by {self.author} ({self.year})"
      # Make sure to RETURN a string, not print it
      # Use self.attribute_name to access instance data
  ```

### **Problem: "TypeError: 'super' object is not callable"**
- **Cause**: Incorrect syntax for calling super()
- **Solution**:
  ```python
  # Wrong - missing parentheses
  super.__init__(title, author, year)

  # Correct - super() with parentheses
  super().__init__(title, author, year)
  ```

### **Problem: "My EBook's __str__ method doesn't show file size"**
- **Cause**: Not properly overriding the method or not calling super()
- **Solution**:
  ```python
  def __str__(self):
      # Get the parent's string first
      parent_str = super().__str__()
      # Add our additional information
      return f"{parent_str} ({self.file_size} MB)"
  ```

### **Problem: "ModuleNotFoundError: No module named 'lab06'"**
- **Cause**: Test file can't find your lab06.py file or import issues
- **Solution**:
  - Make sure both `lab06.py` and `test_lab06.py` are in the `lab06/` folder
  - Check that your file is named exactly `lab06.py` (not `Lab06.py` or `lab6.py`)
  - Ensure your classes are named exactly `Book` and `EBook`
  - Make sure you've saved the file before running tests

### **Problem: "AssertionError" in tests**
- **Cause**: Your implementation doesn't match what the tests expect
- **Solution**:
  - For string tests: Make sure your `__str__` method includes all required information
  - For age tests: Use exactly 2025 as the current year in your calculations
  - For inheritance tests: Ensure `EBook` properly inherits from `Book`
  - Read the test failure message carefully - it shows what was expected vs. what you returned

### **Problem: "IndentationError" or "SyntaxError"**
- **Cause**: Python syntax issues, often with class or method definition
- **Solution**:
  - Make sure class definitions end with a colon: `class Book:`
  - Ensure all method definitions are properly indented inside the class
  - Check that method definitions end with colons: `def __init__(self):`
  - Use consistent indentation (4 spaces, not tabs)

### **Problem: "My get_age() method returns the wrong value"**
- **Cause**: Incorrect calculation or using wrong current year
- **Solution**:
  ```python
  def get_age(self):
      current_year = 2025  # Use exactly 2025 as specified
      return current_year - self.year
  ```

### **Problem: "Tests pass locally but fail on GitHub Actions"**
- **Cause**: Environment differences or missing files
- **Solution**:
  - Make sure you've committed and pushed both `lab06.py` and `test_lab06.py`
  - Check that your class names are exactly `Book` and `EBook`
  - Verify that all required methods exist: `__init__`, `__str__`, `get_age`
  - Ensure your `EBook` class properly inherits from `Book`

### **AI assistant prompts for debugging:**

When you're stuck, try these specific prompts:

1. **For class structure issues:**
   ```
   "I'm getting this error when creating a Book class: [paste error]. Here's my code: [paste code]. What's wrong with my class definition?"
   ```

2. **For inheritance problems:**
   ```
   "My EBook class isn't properly inheriting from Book. Here's my code: [paste code]. How do I fix the inheritance and super() calls?"
   ```

3. **For method issues:**
   ```
   "My __str__ method isn't working correctly. When I print my Book object, I get [describe what you see]. Here's my code: [paste code]. How do I fix it?"
   ```

### **Final checklist before considering the lab complete**

- [ ] `lab06/lab06.py` file exists and contains both `Book` and `EBook` classes
- [ ] `Book` class has `__init__`, `__str__`, and `get_age` methods
- [ ] `EBook` class inherits from `Book` and overrides `__str__` method
- [ ] Both classes use proper [docstrings](https://docs.python.org/3/tutorial/controlflow.html#documentation-strings) for documentation
- [ ] File includes `if __name__ == '__main__':` block for testing
- [ ] `lab06/test_lab06.py` file exists with provided test code copied exactly
- [ ] Local testing: `pytest lab06/test_lab06.py` passes all tests
- [ ] All files have been committed and pushed to [GitHub](https://github.com/)
- [ ] [GitHub Actions](https://docs.github.com/en/actions) workflow shows a **green checkmark ✅**

**💡 Pro tip:** Start simple! Get the basic `Book` class working first, then add the `get_age` method, and finally tackle the `EBook` inheritance. Test each step before moving to the next!

-----

## Submission

To complete this lab, commit and push both your `lab06.py` and `test_lab06.py` files to your `is4010-labs` [GitHub](https://github.com/) repository.

```bash
git add lab06.py test_lab06.py
git commit -m "Complete lab 06: object-oriented programming"
git push origin main
```

Your grade for this lab is determined by the successful completion of the [GitHub Action](https://docs.github.com/en/actions), indicated by the green checkmark in your repository's "Actions" tab. The automated tests will verify that your classes are properly implemented with correct inheritance relationships and method functionality.

**Verification steps:**
1. Check that your local tests pass: `pytest lab06/test_lab06.py`
2. Verify both files are committed: `git status` should show "nothing to commit"
3. Confirm files are pushed: Check your GitHub repository online
4. Monitor the Actions tab for the green checkmark indicating successful automated testing

**🎉 Congratulations!** Completing this lab means you've mastered fundamental object-oriented programming concepts that are used throughout modern software development. These skills will be essential for your upcoming projects and professional programming career.