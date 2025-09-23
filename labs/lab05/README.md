# Lab 05: functions and error handling

**Due:** Sunday, September 28 at 11:59 PM
**Points:** 10

## Objective

The goal of this lab is to practice the two key skills from this week's sessions: refactoring procedural code into clean, reusable functions, and making that code robust by handling potential runtime errors. You will use an [AI partner](https://claude.ai/) for both tasks. Your work will be graded automatically by our [CI/CD pipeline](https://docs.github.com/en/actions).

## Background

Good software isn't just about writing code that works once; it's about writing code that is readable, maintainable, and resilient. [Functions](https://docs.python.org/3/tutorial/controlflow.html#defining-functions) allow us to organize our logic, while [error handling](https://docs.python.org/3/tutorial/errors.html) ensures our applications don't crash when faced with unexpected data or situations.

-----

## Part 1: the refactor challenge

### The messy script

Below is a python script that processes a list of user data. It works, but it's hard to read and all the logic is mixed together in one place.

```python
# Messy script to be refactored
users = [
    {"name": "alice", "age": 30, "is_active": True, "email": "alice@example.com"},
    {"name": "bob", "age": 25, "is_active": False},
    {"name": "charlie", "age": 35, "is_active": True, "email": "charlie@example.com"},
    {"name": "david", "age": "unknown", "is_active": False}
]

# Calculate total age and count users for average
total_age = 0
user_count_for_age = 0
for user in users:
    if isinstance(user.get("age"), int):
        total_age += user["age"]
        user_count_for_age += 1
average_age = total_age / user_count_for_age
print(f"average user age: {average_age:.2f}")

# Get a list of all active user emails
active_user_emails = []
for user in users:
    if user.get("is_active") and user.get("email"):
        active_user_emails.append(user["email"])
print(f"active user emails: {active_user_emails}")
```

### Your task

1.  In your `is4010-labs` repository, create a new file named `lab05.py`.
2.  Copy the messy script's data (the `users` list) into your `lab05.py` file.
3.  Use a conversational AI to help you refactor the script. Your prompt should be something like: *"act as a senior python developer. refactor this script into clean, single-purpose functions with [NumPy-style docstrings](https://numpydoc.readthedocs.io/en/latest/format.html). one function should calculate the average age, and another should get active user emails."*
4.  Your final `lab05.py` file should contain the `users` list, the new functions you created, and a main execution block (`if __name__ == '__main__':`) that calls your functions to produce the same output as the original script.

### Understanding `if __name__ == '__main__':`

This is a common [Python idiom](https://docs.python.org/3/library/__main__.html) that allows you to write code that runs only when the script is executed directly, not when it's imported as a module. Here's a simple example:

```python
def greet(name):
    """Print a greeting message."""
    print(f"Hello, {name}!")

if __name__ == '__main__':
    # This code only runs when the script is executed directly
    greet("World")
```

For Lab 05, your main block should look something like:

```python
if __name__ == '__main__':
    # Call your functions and print results
    avg_age = calculate_average_age(users)
    print(f"average user age: {avg_age:.2f}")

    active_emails = get_active_user_emails(users)
    print(f"active user emails: {active_emails}")
```

-----

## Part 2: bulletproof your code

### The problem

Your refactored code from part 1 is clean, but it's brittle. It makes assumptions about the data. What if the list of users is empty? What if a user dictionary is missing a required key? An unhandled exception will crash the program.

### Your task

1.  Continue working in your `lab05.py` file.
2.  Use an AI assistant to brainstorm potential runtime errors. Ask it: *"review these python functions. what are some potential runtime errors or edge cases? consider empty lists, missing dictionary keys, or incorrect data types."*
3.  Based on the AI's feedback, add [`try...except`](https://docs.python.org/3/tutorial/errors.html#handling-exceptions) blocks to your functions to handle at least **two** different potential exceptions gracefully.
      * For example, your `calculate_average_age` function should not crash if the user list is empty (which would cause a [`ZeroDivisionError`](https://docs.python.org/3/library/exceptions.html#ZeroDivisionError)).
      * Your `get_active_user_emails` function should handle cases where a user might be missing an `'is_active'` or `'email'` key (which could cause a [`KeyError`](https://docs.python.org/3/library/exceptions.html#KeyError)).
4.  Instead of crashing, your functions should print a user-friendly error message (e.g., `"error: cannot calculate average age of an empty list."`) and return a sensible default value (like `0` or `None` or an empty `list`).

-----

## Testing Your Code 🧪

You **must** create a test file for this lab to get full credit. This gives you hands-on experience with [pytest](https://docs.pytest.org/) testing, which is essential for professional development.

### Setting up the test file

1. In your `lab05/` folder, create a new file named `test_lab05.py`.
2. Copy the entire code block below into this new file.
3. **Do not modify the test file** - it's designed to work with any correct implementation.

```python
# test_lab05.py
import pytest
from lab05 import calculate_average_age, get_active_user_emails


@pytest.fixture
def sample_users():
    return [
        {"name": "alice", "age": 30, "is_active": True, "email": "alice@example.com"},
        {"name": "bob", "age": 25, "is_active": False},
        {
            "name": "charlie",
            "age": 35,
            "is_active": True,
            "email": "charlie@example.com",
        },
        {"name": "david", "age": "unknown", "is_active": False},
        {"name": "eve", "is_active": True, "email": "eve@example.com"},
    ]


# Tests for calculate_average_age
def test_calculate_average_age_normal(sample_users):
    # (30 + 25 + 35) / 3 = 30.0
    assert calculate_average_age(sample_users) == 30.0


def test_calculate_average_age_empty_list():
    # Should handle the error and return a default value
    assert calculate_average_age([]) == 0.0


# Tests for get_active_user_emails
def test_get_active_user_emails_normal(sample_users):
    expected_emails = ["alice@example.com", "charlie@example.com", "eve@example.com"]
    assert set(get_active_user_emails(sample_users)) == set(expected_emails)


def test_get_active_user_emails_no_active_users():
    users = [{"name": "bob", "age": 25, "is_active": False}]
    assert get_active_user_emails(users) == []


def test_get_active_user_emails_empty_list():
    assert get_active_user_emails([]) == []
```

### Running the tests locally

To run the tests on your local machine:

```bash
# Navigate to your lab05 directory
cd lab05/

# Run the tests
pytest test_lab05.py

# Or run with verbose output to see each test
pytest -v test_lab05.py
```

If all tests pass, you'll see output like:
```
========================= 5 passed in 0.05s =========================
```

If any tests fail, pytest will show you exactly which assertions failed and why, helping you debug your functions.

**💡 Understanding the tests:**

- **`calculate_average_age` tests**: Verify your function correctly calculates the average age from valid integer ages (skipping invalid data like "unknown") and gracefully handles empty lists by returning 0.0.
- **`get_active_user_emails` tests**: Check that your function can collect emails from active users, handles users missing email fields, and returns empty lists for edge cases.
- **Error handling**: Tests verify that your functions don't crash on edge cases and return sensible default values.

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
│   └── test_lab04.py         # Test file for Lab 04 functions (optional)
├── lab05/
│   ├── lab05.py              # Refactored functions with error handling (NEW)
│   └── test_lab05.py         # Test file for Lab 05 functions (REQUIRED)
└── README.md                 # Repository description (auto-created by GitHub)
```

**Key points about this structure:**
- **`lab05/lab05.py`**: Contains your refactored functions (`calculate_average_age` and `get_active_user_emails`) with proper error handling and a main execution block
- **`lab05/test_lab05.py`**: Required test file that validates your functions work correctly (provided test code must be copied exactly)
- **Cumulative structure**: Your repository now contains work from Labs 01-05, showing progression through the course
- **Function requirements**: Your `lab05.py` should have the original `users` list, two main functions with error handling, and an `if __name__ == '__main__':` block

This organized structure demonstrates your growing skills in Python programming, from basic scripts to well-structured, error-resistant code.

-----

## 🚨 Troubleshooting Guide

Functions and error handling can present unique challenges! Here are solutions to common issues:

### **Problem: "I don't understand how to refactor the messy script"**
- **Cause**: Unclear understanding of how to break code into functions
- **Solution**:
  - Look at the messy script - it does TWO main things: calculates average age and gets active emails
  - Create one function for each task: `calculate_average_age(users)` and `get_active_user_emails(users)`
  - Each function should take the `users` list as a parameter and return a result
  - Copy the relevant logic from the messy script into each function

### **Example AI prompts for refactoring:**
- "Help me turn this Python script into two separate functions. The first should calculate average age, the second should get active user emails."
- "How do I write a function that takes a list of user dictionaries and returns the average age of users with valid ages?"
- "Show me how to refactor this code into functions with proper docstrings."

### **Problem: "ModuleNotFoundError: No module named 'lab05'"**
- **Cause**: The test file can't find your `lab05.py` file
- **Solution**:
  - Make sure `lab05.py` and `test_lab05.py` are both in the `lab05/` folder
  - Check that your file is named exactly `lab05.py` (not `Lab05.py` or `lab5.py`)
  - Ensure you've saved the file before running tests

### **Problem: "AttributeError: module 'lab05' has no attribute 'calculate_average_age'"**
- **Cause**: Your function name doesn't match exactly what the test expects
- **Solution**:
  - Check that your functions are named exactly `calculate_average_age` and `get_active_user_emails`
  - Make sure there are no indentation errors that put the functions inside other functions
  - Verify both functions are defined at the top level of your file

### **Problem: "ZeroDivisionError: division by zero"**
- **Cause**: Your `calculate_average_age` function tries to divide by zero when there are no valid ages
- **Solution**:
  - Add a `try...except` block around the division
  - Check if the count is zero before dividing
  - Return a default value like `0.0` when there are no valid ages
  ```python
  try:
      return total_age / count
  except ZeroDivisionError:
      print("error: cannot calculate average age of an empty list.")
      return 0.0
  ```

### **Problem: "KeyError: 'email'" or "KeyError: 'is_active'"**
- **Cause**: Your code assumes all users have certain keys, but some don't
- **Solution**:
  - Use `.get()` method instead of direct key access: `user.get('email')` instead of `user['email']`
  - Add `try...except` blocks to handle missing keys gracefully
  - Check if keys exist before using them: `if 'email' in user:`

### **Problem: "My function doesn't handle the 'unknown' age correctly"**
- **Cause**: Not checking if age is a valid integer before using it
- **Solution**:
  - Use `isinstance(user.get("age"), int)` to check if age is an integer
  - Skip users with non-integer ages when calculating average
  - This matches the logic from the original messy script

### **Problem: "Tests pass locally but fail on GitHub Actions"**
- **Cause**: Environment differences or missing error handling
- **Solution**:
  - Make sure you've committed and pushed `lab05.py`
  - Check that your functions handle ALL edge cases (empty lists, missing keys, invalid data)
  - Verify your function names match exactly: `calculate_average_age` and `get_active_user_emails`
  - Ensure your functions return the correct data types (float for average, list for emails)

### **Problem: "My if __name__ == '__main__': block isn't working"**
- **Cause**: Syntax or indentation issues with the main block
- **Solution**:
  - Make sure the line is exactly: `if __name__ == '__main__':`
  - Don't forget the colon at the end
  - Indent the code inside the block with 4 spaces
  - Make sure it's at the very end of your file, after all function definitions

### **Problem: "SyntaxError" or "IndentationError"**
- **Cause**: Python syntax issues
- **Solution**:
  - Check that all parentheses, quotes, and brackets are properly closed
  - Ensure consistent indentation (use 4 spaces, not tabs)
  - Make sure function definitions start with `def` and end with `:`
  - Use [VS Code](https://code.visualstudio.com/)'s Python extension for syntax highlighting

### **Problem: "My error handling isn't working as expected"**
- **Cause**: Incorrect exception handling or logic
- **Solution**:
  - Make sure you're catching the right exception types (`ZeroDivisionError`, `KeyError`, etc.)
  - Test your error handling by deliberately creating error conditions
  - Print informative error messages that help users understand what went wrong
  - Always return appropriate default values (numbers for math operations, empty lists for collections)

### **Problem: "I'm getting different results than the original script"**
- **Cause**: Logic differences during refactoring
- **Solution**:
  - Compare your function outputs with the original script outputs
  - For average age: should be (30 + 25 + 35) / 3 = 30.0 with the sample data
  - For active emails: should include Alice, Charlie, and Eve's emails
  - Make sure you're filtering the same way the original script does

### **Still stuck? Use AI assistance strategically! 🤖**

**Effective AI prompting strategies for this lab:**

1. **Be specific about your error:**
   ```
   "My calculate_average_age function is giving a ZeroDivisionError when the user list is empty. Here's my code: [paste code]. How do I add error handling?"
   ```

2. **Ask for refactoring help:**
   ```
   "I have this messy Python script that calculates average age and gets active emails. Help me split it into two clean functions with proper error handling."
   ```

3. **Request debugging assistance:**
   ```
   "My function should return 30.0 for average age but it's returning [wrong value]. Here's my code: [paste code]. What's wrong with my logic?"
   ```

**Recommended AI tools:**
- **[ChatGPT](https://chat.openai.com/)** - Great for explaining function design patterns and error handling concepts
- **[Claude](https://claude.ai/)** - Excellent for step-by-step refactoring guidance and debugging help
- **[Gemini](https://gemini.google.com/)** - Helpful for understanding pytest errors and Python best practices

### **Final checklist before considering the lab complete**

- [ ] `lab05/lab05.py` file exists and contains the original `users` list
- [ ] File contains `calculate_average_age(users)` function with proper error handling
- [ ] File contains `get_active_user_emails(users)` function with proper error handling
- [ ] Both functions have [NumPy-style docstrings](https://numpydoc.readthedocs.io/en/latest/format.html)
- [ ] File has `if __name__ == '__main__':` block that calls both functions
- [ ] Functions handle edge cases gracefully (empty lists, missing keys, invalid data)
- [ ] `lab05/test_lab05.py` file exists with the provided test code copied exactly
- [ ] Local testing: `pytest lab05/test_lab05.py` passes all tests
- [ ] All files have been committed and pushed to [GitHub](https://github.com/)
- [ ] [GitHub Actions](https://docs.github.com/en/actions) workflow shows a **green checkmark ✅**

**💡 Pro tip:** Test your error handling by temporarily modifying the `users` list to create edge cases (empty list, users with missing keys, etc.) and make sure your functions don't crash!

-----

## Submission

To complete this lab, commit and push both your `lab05.py` and `test_lab05.py` files to your `is4010-labs` [GitHub](https://github.com/) repository.

```bash
git add lab05.py test_lab05.py
git commit -m "Complete lab 05"
git push origin main
```

Your grade for this lab is determined by the successful completion of the [GitHub Action](https://docs.github.com/en/actions), indicated by the green checkmark in your repository's "Actions" tab. The automated tests will verify that your functions work correctly and handle errors gracefully.