# Lab 06: object-oriented programming

## Objective

This lab is designed to give you hands-on practice with the fundamental concepts of object-oriented programming (oop). You will create a "base" class to model a real-world object, add methods to give it behavior, and then create a "child" class that inherits from it.

## Background

Oop allows us to create our own custom data types that bundle together data (attributes) and behavior (methods). This is a powerful way to structure applications, making them more organized and easier to scale. In this lab, you'll build your first custom classes in python.

-----

## Part 1: create a base class

### Your task

Your first task is to create a class that serves as a blueprint for a `Book`. You'll define its attributes and how it should be represented as a string.

1.  In your `is4010-labs` repository, create a new file named `lab06.py`.
2.  Inside this file, define a new class named `Book`.
3.  Use an AI assistant to help you write the `__init__` constructor method. It should accept `title` (str), `author` (str), and `year` (int) as parameters and store them as attributes on the object.
4.  Next, ask your AI assistant to help you write the `__str__` dunder method. This method should return a user-friendly string that includes the book's title, author, and publication year.
5.  At the bottom of your file, add a main execution block (`if __name__ == '__main__':`) to test your work. Inside this block, create at least one instance of your `Book` class and `print()` it to the console to verify that your `__str__` method works correctly.

-----

## Part 2: add methods and inheritance

### Your task

Now you will extend the functionality of your `Book` class and create a more specialized `EBook` class that inherits from it.

1.  **Add a method to `Book`**: In your `Book` class, create a new method called `get_age()`. This method should take no parameters (other than `self`) and should calculate and return the age of the book based on its publication year. You can assume the current year is **2025** for your calculation.
2.  **Create a child class**: Below your `Book` class, define a new class named `EBook` that inherits from `Book`.
3.  **Extend the constructor**: The `EBook`'s `__init__` method should accept all the same parameters as `Book`, plus a new one: `file_size` (int, representing megabytes). Inside this method, you must call the parent class's constructor using `super()` to handle the title, author, and year.
4.  **Override a method**: In the `EBook` class, override the `__str__` method. The new version should call the parent's `__str__` method using `super()` to get the base string, and then append the file size information to it. The final output should include all the book's details plus its file size (e.g., "... (12 MB)").
5.  **Test your new class**: In your main execution block, create an instance of your new `EBook` class and print it to the console. Also, call its `get_age()` method to verify that it correctly inherited it from the `Book` class.

-----

## Submission

When you are finished with both parts, commit and push your completed `lab06.py` file to your `is4010-labs` github repository. The automated tests will be run against your `Book` and `EBook` classes to verify their functionality.

```
git add lab06.py
git commit -m "Complete lab 06"
git push origin main
```