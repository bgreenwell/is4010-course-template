# Lab 03: Python basics and automated testing

## Objective

In this lab, you will practice python fundamentals by building two small applications. More importantly, you will set up an automated testing and continuous integration (ci/cd) pipeline for your repository using `pytest` and github actions. This is a one-time setup that will automatically check your work for all future labs.

## Background

This lab is divided into three parts. In parts 1 and 2, you will write python code to practice working with variables, input/output, and control flow (loops and conditionals). In part 3, you will implement a professional testing workflow that automatically verifies your code is correct every time you push it to github.

---

## Part 1: The mad libs generator

For this part, you will write a function that takes several words as input and combines them into a story. To make this function testable, it will not use the `input()` function directly. Instead, it will take the words as parameters and return a formatted string.

### Instructions

1.  In your `is4010-labs` repository, create a new file named `lab03.py`.
2.  Copy the following function stub into your `lab03.py` file.
3.  Complete the function. It should use a python f-string to combine the parameters into a story. The story can be anything you like, but it must use all the provided parameters.

### Python function stub

```python
def generate_mad_lib(adjective, noun, verb):
    """
    Generates a short story using the provided words.

    Parameters
    ----------
    adjective : str
        An adjective to use in the story.
    noun : str
        A noun to use in the story.
    verb : str
        A past-tense verb to use in the story.

    Returns
    -------
    str
        A formatted story string.
    """
    # Example story: "the {adjective} {noun} {verb} over the lazy dog."
    # Your story can be different, but it must use the three parameters.
    pass
````

-----

## Part 2: The number guessing game

This part will have you build a classic interactive game, which will give you practice with loops and conditional statements.

### Instructions

1.  In the same `lab03.py` file, copy the function stub below.
2.  Complete the function, following the logic described in the docstring.
3.  To make the game runnable, add the following two lines of code at the very bottom of your `lab03.py` file:
    ```python
    if __name__ == '__main__':
        guessing_game()
    ```

### Python function stub

```python
import random

def guessing_game():
    """
    Plays a number guessing game with the user.

    The function should:
    1. Generate a random secret number between 1 and 100.
    2. Prompt the user to guess the number.
    3. Use a while loop to continue until the user guesses correctly.
    4. Inside the loop, tell the user if their guess is too high or too low.
    5. When the user guesses correctly, print a success message and exit the loop.
    """
    pass
```

-----

## Part 3: Setting up automated testing (CI/CD)

This is the most important part of the lab. You will add two new files to your repository to enable automated testing.

### Step 3.1: Create the test file

This file contains tests that `pytest` will use to check your `generate_mad_lib` function.

1.  In the root of your `is4010-labs` repository, create a new file named `test_lab03.py`.
2.  Copy the entire code block below into this new file.

<!-- end list -->

```python
# test_lab03.py
from lab03 import generate_mad_lib

def test_generate_mad_lib():
    """
    Tests the generate_mad_lib function to ensure it uses the inputs correctly.
    """
    adj = "silly"
    noun = "cat"
    verb = "jumped"
    
    # Call the student's function
    story = generate_mad_lib(adj, noun, verb)
    
    # Assert that all the words are in the returned story
    assert adj in story
    assert noun in story
    assert verb in story
```

### Step 3.2: Create the github actions workflow

This file tells github to automatically run your tests every time you push new code.

1.  In the root of your `is4010-labs` repository, create a new folder named `.github`.
2.  Inside the `.github` folder, create another new folder named `workflows`.
3.  Inside the `workflows` folder, create a new file named `main.yml`.
4.  Copy the entire code block below into this new `main.yml` file.

<!-- end list -->

```yaml
# .github/workflows/main.yml
name: run-pytest

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: ["3.10"]
    steps:
      - uses: actions/checkout@v3
      - name: Set up python ${{ matrix.python-version }}
        uses: actions/setup-python@v4
        with:
          python-version: ${{ matrix.python-version }}
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install pytest
      - name: Test with pytest
        run: |
          pytest
```

-----

## Final step: Pushing and verification

1.  You should now have three new/modified files: `lab03.py`, `test_lab03.py`, and `.github/workflows/main.yml`.
2.  Use the `git add`, `git commit`, and `git push` commands to send all three files to your github repository.
3.  Navigate to your repository page on github and click on the **actions** tab.
4.  You should see your workflow running. After a minute or two, it should complete with a **green checkmark**. This checkmark is your confirmation that your code is correct and your automated grading is working\!

## Submission

For this lab, you do not need to submit anything on canvas. Your grade is determined by the successful completion of the github action, indicated by the green checkmark in your repository.
