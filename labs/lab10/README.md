# Lab 10: translating python to rust

## Objective

The goal of this lab is to gain hands-on experience with Rust's fundamental syntax by converting familiar python code into Rust. This exercise will help solidify your understanding of Rust's type system, function definitions, and variable mutability.

## Background

Translating code from a language you know to one you are learning is an excellent way to map existing concepts to new syntax. You will find that Rust's compiler is a powerful partner. Pay close attention to its error messages, as they are famously helpful and will guide you toward the correct solution.

-----

## Instructions

1.  Open your terminal and navigate to your `is4010-labs` repository folder.
2.  Create a new Rust project for this lab by running the command: `cargo new lab10 --bin`.
3.  This creates a new folder named `lab10`. Open the `src/main.rs` file within this folder. This is where you will write all your Rust code for this lab.
4.  For each of the three python functions provided below, rewrite it in Rust inside your `src/main.rs` file.
5.  In your `main` function, call each of your new Rust functions to prove that they work and print the results to the console.
6.  You can run your code at any time using `cargo run` from inside the `lab10` directory.
7. You can test your code locally by running `cargo test`. This command will execute the test suite you added and show you if your functions are working correctly. This is a great way to verify your work before pushing to GitHub.

-----

## Python functions to translate

### Function 1: add two numbers

```python
# python
def add(num1, num2):
    return num1 + num2
```

**Hint**: Your Rust function should take two 32-bit signed integers (`i32`) and return an `i32`.

### Function 2: check for even numbers

```python
# python
def is_even(num):
    return num % 2 == 0
```

**Hint**: Your Rust function should take one `i32` and return a boolean (`bool`).

### Function 3: create a greeting

```python
# python
def greet(name):
    return f"Hello, {name}!"
```

**Hint**: Your Rust function should take a `String` and return a `String`. You can use the `format!` macro, which works similarly to Python's f-strings.

-----

## Adding the test suite

Append the following test module to the bottom of your `src/main.rs` file. The `cargo test` command, run by our CI/CD pipeline, will execute these tests to verify your solution.

```rust
#[cfg(test)]
mod tests {
    use super::*; // Import functions from parent module

    #[test]
    fn test_add() {
        assert_eq!(add(2, 2), 4);
        assert_eq!(add(-1, 1), 0);
    }

    #[test]
    fn test_is_even() {
        assert!(is_even(10));
        assert!(!is_even(7));
    }

    #[test]
    fn test_greet() {
        // Note: The function expects a String, but we can pass a &str
        // which Rust will deref coerce. Testing with a slice is common.
        assert_eq!(greet("world"), "Hello, world!");
    }
}
```

-----

## Submission

For this lab, you will commit and push your entire `lab10` project folder to your `is4010-labs` GitHub repository.

```
# From the root of your is4010-labs directory
git add lab10/
git commit -m "Complete lab 10"
git push origin main
```