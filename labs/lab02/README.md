# Lab 02: AI-Assisted Development

## Objective

In this lab, you will gain hands-on experience with the two types of AI development tools we discussed in class: an inline assistant (github copilot) and a conversational assistant (gemini or another large language model). You will learn how to leverage each tool for its specific strengths.

## Background

Github copilot excels at generating code in the flow of your work, while conversational AI is a powerful partner for debugging, refactoring, and explaining complex topics. A modern developer is proficient with both.

A key concept for this lab is the **docstring**. A docstring is a special comment, wrapped in triple quotes (`"""..."""`), that explains what a function or class does. In this course, we will use the **numpy docstring style**, which is clean and highly structured. A good docstring is the best way to communicate your intent to an AI assistant. You can find a full reference at the [numpy style guide](https://numpydoc.readthedocs.io/en/latest/format.html).

---

## Part 1: Copilot driving school

In this part, you will use github copilot to write the code for a series of python function "stubs."

### Instructions

1.  In your `is4010-labs` local repository, create a new file named `lab02.py`.
2.  Copy all the python function stubs from the section below into your `lab02.py` file.
3.  For each function, place your cursor inside the function body on a new line.
4.  Wait for github copilot to suggest an implementation based on the function name and the numpy-style docstring.
5.  Review the suggestion and press `tab` to accept it.

### Python function stubs

```python
def factorial(n):
    """Calculate the factorial of a non-negative integer.

    Parameters
    ----------
    n : int
        The non-negative integer to calculate the factorial of.

    Returns
    -------
    int
        The factorial of n. Returns 1 for n = 0.
    """
    pass

def is_prime(number):
    """Check if a number is a prime number.

    Parameters
    ----------
    number : int
        The integer to check.

    Returns
    -------
    bool
        True if the number is prime, False otherwise.
    """
    pass

def reverse_string(s):
    """Reverse a given string.

    Parameters
    ----------
    s : str
        The string to be reversed.

    Returns
    -------
    str
        The reversed string.
    """
    pass
````

-----

## Part 2: The prompt engineering challenge

In this part, you will use a conversational AI like [google gemini](https://gemini.google.com) to debug, refactor, and document provided code snippets.

### Instructions

1.  In your `is4010-labs` repository, create a new markdown file named `lab02_prompts.md`.
2.  For each of the three problems below, you will craft a high-quality prompt following the "context, persona, task, format" model.
3.  In your `lab02_prompts.md` file, create a section for each problem. For each problem, you must include:
      * A heading for the problem (e.g., "\#\#\# Problem 1: Debugging").
      * The **exact prompt** you used, placed in a code block.
      * The **final, corrected code snippet** that the AI provided, also in a code block.

### Problems

#### Problem 1: Debugging a buggy function

This function is supposed to calculate the sum of all even numbers in a list, but it contains a logical error.

**Your task:** craft a prompt that asks the AI to find and fix the bug.

```python
# Buggy code snippet
def sum_of_evens(numbers):
    """Calculates the sum of all even numbers in a list."""
    total = 0
    for num in numbers:
        if num % 2 == 1: # This line has a bug!
            total += num
    return total
```

#### Problem 2: Refactoring an unreadable function

This function works correctly, but it is written in a confusing way.

**Your task:** craft a prompt that asks the AI to refactor this code to be more clear, concise, and "pythonic."

```python
# Unreadable code snippet
def get_names_of_adults(users):
    """Given a list of user dictionaries, returns a list of names of users
    who are 18 or older."""
    results = []
    for i in range(len(users)):
        if users[i]['age'] >= 18:
            results.append(users[i]['name'])
    return results
```

#### Problem 3: Documenting a function

This function works, but it has no documentation.

**Your task:** craft a prompt that asks the AI to write a professional, high-quality **numpy-style** docstring for this function.

```python
# Undocumented code snippet
def calculate_area(length, width):
    if length <= 0 or width <= 0:
        raise ValueError("Length and width must be positive numbers.")
    return length * width
```

-----

## Submission

When you are finished with both parts of the lab, please commit and push your two new files to your `is4010-labs` github repository.

1.  `lab02.py`
2.  `lab02_prompts.md`
