# Lab 05: functions and error handling

## Objective

The goal of this lab is to practice the two key skills from this week's sessions: refactoring procedural code into clean, reusable functions, and making that code robust by handling potential runtime errors. You will use an AI partner for both tasks.

## Background

Good software isn't just about writing code that works once; it's about writing code that is readable, maintainable, and resilient. Functions allow us to organize our logic, while error handling ensures our applications don't crash when faced with unexpected data or situations.

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
3.  Use a conversational AI to help you refactor the script. Your prompt should be something like: *"act as a senior python developer. refactor this script into clean, single-purpose functions with numpy-style docstrings. one function should calculate the average age, and another should get active user emails."*
4.  Your final `lab05.py` file should contain the `users` list, the new functions you created, and a main execution block (`if __name__ == '__main__':`) that calls your functions to produce the same output as the original script.

-----

## Part 2: bulletproof your code

### The problem

Your refactored code from part 1 is clean, but it's brittle. It makes assumptions about the data. What if the list of users is empty? What if a user dictionary is missing a required key? An unhandled exception will crash the program.

### Your task

1.  Continue working in your `lab05.py` file.
2.  Use an AI assistant to brainstorm potential runtime errors. Ask it: *"review these python functions. what are some potential runtime errors or edge cases? consider empty lists, missing dictionary keys, or incorrect data types."*
3.  Based on the AI's feedback, add `try...except` blocks to your functions to handle at least **two** different potential exceptions gracefully.
      * For example, your `calculate_average_age` function should not crash if the user list is empty (which would cause a `ZeroDivisionError`).
      * Your `get_active_user_emails` function should handle cases where a user might be missing an `'is_active'` or `'email'` key (which could cause a `KeyError`).
4.  Instead of crashing, your functions should print a user-friendly error message (e.g., `"error: cannot calculate average age of an empty list."`) and return a sensible default value (like `0` or `None` or an empty `list`).

-----

## Submission

When you are finished, commit and push your completed `lab05.py` file to your `is4010-labs` github repository. The automated tests in github actions will check your refactored functions for correctness.

```
git add lab05.py
git commit -m "Complete lab 05"
git push origin main
```