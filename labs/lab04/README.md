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

## Submission

To complete this lab, commit and push both your `lab04.py` and `lab04_prompts.md` files to your `is4010-labs` github repository.

```
git add lab04.py lab04_prompts.md
git commit -m "Complete lab 04"
git push origin main
```

Your grade for this lab is determined by the successful completion of the github action, indicated by the green checkmark in your repository's "actions" tab. Your prompts file will be reviewed separately.
