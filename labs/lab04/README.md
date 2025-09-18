# Lab 04: AI-assisted data structure selection

## Objective

The goal of this lab is to practice using a conversational AI to select the most appropriate python data structure for a given problem, and then to implement the solution. Your work will be graded automatically by our ci/cd pipeline.

## Background

Choosing the right data structure (list, tuple, dictionary, or set) is a fundamental programming skill. Before writing code, a good developer thinks about the nature of the data and the operations they need to perform. In this lab, you will use an AI partner to help with this analysis. For each problem, you will first ask the AI to recommend a data structure and explain its reasoning, then you will write the code.

---

## Instructions

1.  In your `is4010-labs` repository, create a new markdown file named `lab04_prompts.md`. This is where you will document your AI interactions.
2.  For each of the three problems below:
    a.  Craft a prompt asking a conversational AI (like google gemini) to recommend the best data structure. Your prompt should describe the problem clearly.
    b.  In `lab04_prompts.md`, record the **exact prompt** you used and the **AI's recommendation and reasoning**.
    c.  Create a new file named `lab04.py`.
    d.  In `lab04.py`, write the python function that solves the problem, using the AI-recommended data structure. Use the function stubs provided below.
3.  You can test your work locally by creating a `test_lab04.py` file and using `pytest`, or you can commit and push your code to get feedback from the automated tests in github actions.

---

## Problems and python function stubs

Copy the function stubs below into your `lab04.py` file.

### Problem 1: Finding common items

**Scenario:** You have two very large lists of product IDs from two different suppliers. You need to find out which product IDs are present in *both* lists so you know which products you can source from either supplier. The order of the final list does not matter.

```python
def find_common_elements(list1, list2):
    """Find the common elements between two lists.

    This function should take two lists and return a new list containing
    only the elements that are present in both input lists. The final
    list can be in any order.

    Parameters
    ----------
    list1 : list
        The first list of elements.
    list2 : list
        The second list of elements.

    Returns
    -------
    list
        A list of elements common to both list1 and list2.
    """
    pass
````

### Problem 2: User profile lookup

**Scenario:** Your application loads a list of user profiles from a database. Each user has a unique username, an age, and an email address. You frequently need to look up a user's complete profile by their username. Performance is critical.

```python
def find_user_by_name(users, name):
    """Find a user's profile by name from a list of user data.

    Parameters
    ----------
    users : list of dict
        A list of dictionaries, where each dictionary represents a user
        and has 'name', 'age', and 'email' keys. It is recommended to
        convert this list into a more efficient data structure for lookups.
    name : str
        The name of the user to find.

    Returns
    -------
    dict or None
        The dictionary of the found user, or None if no user is found.
    """
    pass
```

### Problem 3: Listing even numbers in order

**Scenario:** You are given a list of integers representing sensor readings. You need to produce a report that contains only the even-numbered readings, and they must be presented in the exact same order they were received.

```python
def get_list_of_even_numbers(numbers):
    """Return a new list containing only the even numbers from the input list.

    The order of the numbers in the output list must be the same as the
    order of the even numbers in the input list.

    Parameters
    ----------
    numbers : list of int
        A list of integers.

    Returns
    -------
    list of int
        A new list containing only the even integers from the input list.
    """
    pass
```

-----

## Testing Your Code 🧪

You can test your functions locally using pytest. This helps ensure your implementation works correctly before submitting.

### Setting up the test file

1. In your `lab04/` folder, create a new file named `test_lab04.py`.
2. Copy the entire code block below into this new file.
3. **Do not modify the test file** - it's designed to work with any correct implementation.

```python
# test_lab04.py
import pytest
from lab04 import find_common_elements, find_user_by_name, get_list_of_even_numbers


# Tests for find_common_elements
def test_find_common_elements_with_common_items():
    """Test finding common elements when they exist."""
    l1 = [1, 2, 3, 4, 5]
    l2 = [4, 5, 6, 7, 8]
    # The order does not matter, so we compare sets
    assert set(find_common_elements(l1, l2)) == {4, 5}


def test_find_common_elements_with_no_common_items():
    """Test finding common elements when none exist."""
    l1 = [1, 2, 3]
    l2 = [4, 5, 6]
    assert find_common_elements(l1, l2) == []


def test_find_common_elements_with_empty_lists():
    """Test finding common elements with empty lists."""
    assert find_common_elements([], []) == []
    assert find_common_elements([1, 2, 3], []) == []


def test_find_common_elements_with_duplicates():
    """Test finding common elements with duplicates in lists."""
    l1 = [1, 1, 2, 3, 3]
    l2 = [1, 2, 2, 4, 5]
    result = find_common_elements(l1, l2)
    # Should contain 1 and 2, order doesn't matter
    assert set(result) == {1, 2}


# Tests for find_user_by_name
@pytest.fixture
def sample_users():
    """Fixture providing sample user data for testing."""
    return [
        {"name": "alice", "age": 30, "email": "alice@example.com"},
        {"name": "bob", "age": 25, "email": "bob@example.com"},
        {"name": "charlie", "age": 35, "email": "charlie@example.com"},
    ]


def test_find_user_by_name_existing(sample_users):
    """Test finding a user that exists."""
    assert find_user_by_name(sample_users, "alice") == {
        "name": "alice",
        "age": 30,
        "email": "alice@example.com",
    }


def test_find_user_by_name_not_existing(sample_users):
    """Test searching for a user that doesn't exist."""
    assert find_user_by_name(sample_users, "david") is None


def test_find_user_by_name_empty_list():
    """Test searching in an empty user list."""
    assert find_user_by_name([], "alice") is None


def test_find_user_by_name_case_sensitivity(sample_users):
    """Test that user search is case-sensitive."""
    assert find_user_by_name(sample_users, "Alice") is None  # Capital A
    assert find_user_by_name(sample_users, "alice") is not None  # lowercase a


# Tests for get_list_of_even_numbers
def test_get_list_of_even_numbers_mixed():
    """Test filtering even numbers from a mixed list."""
    assert get_list_of_even_numbers([1, 2, 3, 4, 5, 6]) == [2, 4, 6]


def test_get_list_of_even_numbers_all_odd():
    """Test filtering even numbers from a list of all odd numbers."""
    assert get_list_of_even_numbers([1, 3, 5, 7]) == []


def test_get_list_of_even_numbers_all_even():
    """Test filtering even numbers from a list of all even numbers."""
    assert get_list_of_even_numbers([2, 4, 6, 8]) == [2, 4, 6, 8]


def test_get_list_of_even_numbers_empty():
    """Test filtering even numbers from an empty list."""
    assert get_list_of_even_numbers([]) == []


def test_get_list_of_even_numbers_with_zero():
    """Test that zero is correctly identified as even."""
    assert get_list_of_even_numbers([0, 1, 2, 3]) == [0, 2]


def test_get_list_of_even_numbers_preserves_order():
    """Test that the order of even numbers is preserved."""
    assert get_list_of_even_numbers([10, 1, 8, 3, 6, 5, 4]) == [10, 8, 6, 4]


def test_get_list_of_even_numbers_negative():
    """Test filtering even numbers including negative numbers."""
    assert get_list_of_even_numbers([-4, -3, -2, -1, 0, 1, 2]) == [-4, -2, 0, 2]
```

### Running the tests locally

To run the tests on your local machine:

```bash
# Navigate to your lab04 directory
cd lab04/

# Run the tests
pytest test_lab04.py

# Or run with verbose output to see each test
pytest -v test_lab04.py
```

If all tests pass, you'll see output like:
```
========================= 14 passed in 0.05s =========================
```

If any tests fail, pytest will show you exactly which assertions failed and why, helping you debug your functions.

**💡 Understanding the tests:**

- **`find_common_elements` tests**: Verify your function correctly finds elements that appear in both lists, handles edge cases like empty lists, and works with duplicates.
- **`find_user_by_name` tests**: Check that your function can locate users by name, returns `None` for non-existent users, and handles empty lists. Uses a pytest fixture to provide consistent test data.
- **`get_list_of_even_numbers` tests**: Ensure your function correctly identifies even numbers (including zero and negatives), preserves order, and handles edge cases.

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
│   ├── lab04.py              # Data structure functions (NEW)
│   ├── lab04_prompts.md      # AI interaction documentation (NEW)
│   └── test_lab04.py         # Test file for Lab 04 functions (OPTIONAL)
└── README.md                 # Repository description (auto-created by GitHub)
```

**Key points about this structure:**
- **`lab04/lab04.py`**: Contains your three completed functions using AI-recommended data structures
- **`lab04/lab04_prompts.md`**: Documents your AI interactions and the reasoning behind data structure choices
- **`lab04/test_lab04.py`**: Optional test file for local testing (the GitHub Actions workflow will run similar tests automatically)
- **Cumulative structure**: Your repository now contains work from Labs 01-04, showing progression through the course

This organized structure makes it easy to track your learning progression and demonstrates professional code organization practices.

-----

## 🚨 Troubleshooting Guide

Working with data structures and AI assistance can present unique challenges! Here are solutions to common issues:

### **Problem: "I don't know which data structure to choose"**
- **Cause**: Unclear understanding of the problem requirements or data structure characteristics
- **Solution**:
  - Carefully re-read the problem scenario and think about the operations needed
  - Ask yourself: Do I need fast lookups? Do I need to preserve order? Do I need to eliminate duplicates?
  - Use your AI assistant! Ask: "What data structure should I use for [describe your specific problem]?"

### **Example AI prompts for data structure selection:**
- "I need to find items that appear in both of two large lists. Performance is important. What Python data structure should I use?"
- "I need to look up user profiles by username frequently. What's the most efficient data structure for this in Python?"
- "I need to filter a list but keep the original order. What approach should I take?"

### **Problem: "ModuleNotFoundError: No module named 'lab04'"**
- **Cause**: The test file can't find your `lab04.py` file
- **Solution**:
  - Make sure `lab04.py` and `test_lab04.py` are both in the `lab04/` folder
  - Check that your file is named exactly `lab04.py` (not `Lab04.py` or `lab4.py`)
  - Ensure you've saved the file before running tests

### **Problem: "AttributeError: module 'lab04' has no attribute 'find_common_elements'"**
- **Cause**: Your function name doesn't match exactly what the test expects
- **Solution**:
  - Check that your function is named exactly `find_common_elements` (with underscore, not camelCase)
  - Make sure there are no indentation errors that put the function inside another function
  - Verify you've defined all three required functions

### **Problem: "AssertionError: assert set(...) == {4, 5}"**
- **Cause**: Your function returns the wrong elements or wrong data type
- **Solution**:
  - For `find_common_elements`: Make sure you're finding elements that appear in BOTH lists
  - Consider using set intersection: `list(set(list1) & set(list2))`
  - For `get_list_of_even_numbers`: Check that you're filtering correctly with `number % 2 == 0`
  - For `find_user_by_name`: Ensure you're comparing the 'name' field correctly

### **Problem: "My find_user_by_name function is too slow"**
- **Cause**: Using a linear search through the list for each lookup
- **Solution**:
  - Convert the list to a dictionary for O(1) lookups: `{user['name']: user for user in users}`
  - Remember: the function gets called multiple times, so optimize for lookup speed

### **Problem: "Tests pass locally but fail on GitHub Actions"**
- **Cause**: Environment differences or missing files
- **Solution**:
  - Make sure you've committed and pushed both `lab04.py` and `test_lab04.py`
  - Check that your imports are correct
  - Verify your function names match exactly
  - Ensure your functions handle edge cases (empty lists, None values, etc.)

### **Problem: "SyntaxError" or "IndentationError"**
- **Cause**: Python syntax issues
- **Solution**:
  - Check that all parentheses, quotes, and brackets are properly closed
  - Ensure consistent indentation (use 4 spaces, not tabs)
  - Make sure your function definitions are properly formatted
  - Use VS Code's Python extension for syntax highlighting and error detection

### **Problem: "My AI recommended a complex solution, but it's not working"**
- **Cause**: Sometimes AI suggests advanced techniques that may have subtle issues
- **Solution**:
  - Start with a simple, working solution first
  - Ask the AI to explain the approach step-by-step
  - Test with simple examples before complex ones
  - Don't hesitate to ask for a "simpler approach" if the first suggestion is complex

### **Problem: "I'm getting different results than expected"**
- **Cause**: Misunderstanding the problem requirements
- **Solution**:
  - For `find_common_elements`: Returns elements in BOTH lists (intersection)
  - For `find_user_by_name`: Returns the entire user dictionary, not just a field
  - For `get_list_of_even_numbers`: Must preserve the original order
  - Double-check the function docstrings for exact requirements

### **Still stuck? Use AI assistance strategically! 🤖**

**Effective AI prompting strategies for this lab:**

1. **Be specific about your problem:**
   ```
   "My find_common_elements function should return [4, 5] when given [1,2,3,4,5] and [4,5,6,7,8], but it returns []. Here's my code: [paste code]. What's wrong?"
   ```

2. **Ask for explanation of concepts:**
   ```
   "Can you explain the difference between using a list vs. a dictionary for user lookups in Python? Which is faster and why?"
   ```

3. **Request debugging help:**
   ```
   "I'm getting this pytest error: [paste error]. Here's my function: [paste code]. How do I fix it?"
   ```

**Recommended AI tools:**
- **[ChatGPT](https://chat.openai.com/)** - Great for explaining data structure concepts and debugging code
- **[Claude](https://claude.ai/)** - Excellent for step-by-step problem analysis and optimization suggestions
- **[Gemini](https://gemini.google.com/)** - Helpful for understanding pytest errors and Python best practices

### **Final checklist before considering the lab complete**

- [ ] `lab04/lab04.py` file exists and contains all three required functions
- [ ] `lab04/lab04_prompts.md` file exists with your AI interactions documented
- [ ] `lab04/test_lab04.py` file exists (optional for local testing)
- [ ] All functions use appropriate data structures as recommended by AI
- [ ] Functions handle edge cases (empty lists, non-existent users, etc.)
- [ ] If testing locally: `pytest lab04/test_lab04.py` passes all tests
- [ ] All files have been committed and pushed to GitHub
- [ ] GitHub Actions workflow shows a **green checkmark ✅**

**💡 Pro tip:** Document your AI interactions in `lab04_prompts.md` as you work. This helps you remember the reasoning behind your choices and demonstrates your prompt engineering skills!

-----

## Submission

To complete this lab, commit and push both your `lab04.py` and `lab04_prompts.md` files to your `is4010-labs` github repository.

```
git add lab04.py lab04_prompts.md
git commit -m "Complete lab 04"
git push origin main
```

Your grade for this lab is determined by the successful completion of the github action, indicated by the green checkmark in your repository's "actions" tab. Your prompts file will be reviewed separately.
