# Lab 11: ownership and data modeling

## Objective

This lab is a hands-on exercise in the two core concepts that make Rust unique: the ownership and borrowing system, and the creation of custom data types with `structs` and `enums`.

## Part 1: the borrow checker game

### Background

The Rust compiler's borrow checker enforces a strict set of rules to ensure memory safety. Learning to work *with* the borrow checker is the most important skill for a new Rust developer. In this part, you will be given several functions with common ownership errors. Your task is to fix them using the compiler's error messages as your guide.

### Instructions

1.  Navigate to your `is4010-labs` repository and create a new Rust project: `cargo new lab11_part1 --bin`.
2.  Replace the entire contents of `src/main.rs` with the code block below.
3.  In the `main` function, uncomment one function call at a time.
4.  Run `cargo run` and read the compiler error carefully.
5.  Fix the function so that the code compiles and runs correctly before moving to the next one.
6.  Once your code compiles, run `cargo test` to verify your fixes are correct.

### Buggy code to fix

```rust
// main.rs
fn main() {
    // Uncomment one function call at a time to tackle each problem.
    
    // problem_1();
    // problem_2();
    // problem_3();
}

// Problem 1: This function tries to use a value after it has been moved.
// Fix: The `calculate_length` function should borrow the string instead of taking ownership.
/*
fn problem_1() {
    let s1 = String::from("hello");
    let (s2, len) = calculate_length(s1);
    println!("The length of '{}' is {}.", s2, len);
}

fn calculate_length(s: String) -> (String, usize) {
    let length = s.len();
    (s, length)
}
*/

// Problem 2: This function tries to borrow a mutable reference while an immutable one exists.
// Fix: The immutable borrow `r1` must be out of scope before the mutable borrow `r2` is created.
/*
fn problem_2() {
    let mut s = String::from("hello");
    let r1 = &s; // immutable borrow
    let r2 = &mut s; // mutable borrow - ERROR
    println!("{}, {}", r1, r2);
}
*/


// Problem 3: This function tries to mutate a value through an immutable reference.
// Fix: The reference passed to `add_to_string` needs to be mutable.
/*
fn problem_3() {
    let s = String::from("hello");
    add_to_string(&s);
}

fn add_to_string(s: &String) {
    s.push_str(", world");
}
*/
```

### Part 1 Test Suite

Append the following test module to the bottom of your fixed `lab11_part1/src/main.rs` file to verify your logic.

```rust
#[cfg(test)]
mod tests {
    // Note: You may need to make your fixed functions public (`pub fn ...`)
    // for the tests to access them, or you can restructure your code.
    // For this lab, simply ensuring `cargo test` passes is sufficient.
    use super::{calculate_length, add_to_string};

    #[test]
    fn test_calculate_length() {
        let s = String::from("testing");
        assert_eq!(calculate_length(&s), 7);
    }

    #[test]
    fn test_add_to_string() {
        let mut s = String::from("hello");
        add_to_string(&mut s);
        assert_eq!(s, "hello, world");
    }
}
```

-----

## Part 2: data modeling challenge

### Background

Rust's `structs` and `enums` are powerful tools for modeling the data of your application in a clear and type-safe way. In this part, you will design the data structures for a simple library system.

### Instructions

1.  Navigate to your `is4010-labs` repository and create a new Rust project: `cargo new lab11_part2 --bin`.
2.  Open the new `src/main.rs` file.
3.  **Your goal**: Model a system for tracking library items.
      * An item can be a **Book** (with a `title` and `page_count`) or a **DVD** (with a `title` and `duration_in_minutes`).
      * Every item has a **status**, which can be `Available` or `CheckedOut` (which includes a `due_date` string).
4.  Use an AI assistant to help you. Ask it a prompt like: *"I need to model a library system in Rust. An item can be a `Book` or a `DVD`, and its status can be `Available` or `CheckedOut`. What combination of structs and enums should I use?"*
5.  Define the `structs` and `enums` recommended by your AI partner in your `src/main.rs` file.
6.  Add `#[derive(Debug)]` above your `struct` and `enum` definitions. This will allow you to print them for testing.
7.  In your `main` function, create at least one `Book` instance and one `DVD` instance with different statuses. Print them to the console to verify your data model.
8.  Run `cargo test` to verify your data structures pass the automated checks.

### Part 2 Test Suite

Append the following test module to the bottom of your `lab11_part2/src/main.rs` file.

```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_book_creation() {
        let book = LibraryItem::Book {
            title: String::from("The Rust Programming Language"),
            page_count: 550,
            status: ItemStatus::Available,
        };

        // The 'matches!' macro is great for checking enum variants
        assert!(matches!(book, LibraryItem::Book { .. }));
        if let LibraryItem::Book { title, page_count, status } = book {
            assert_eq!(title, "The Rust Programming Language");
            assert_eq!(page_count, 550);
            assert!(matches!(status, ItemStatus::Available));
        }
    }

    #[test]
    fn test_dvd_creation() {
        let due_date = String::from("2025-08-15");
        let dvd = LibraryItem::DVD {
            title: String::from("The Matrix"),
            duration_in_minutes: 136,
            status: ItemStatus::CheckedOut {
                due_date: due_date.clone(),
            },
        };
        
        assert!(matches!(dvd, LibraryItem::DVD { .. }));
        if let LibraryItem::DVD { title, duration_in_minutes, status } = dvd {
            assert_eq!(title, "The Matrix");
            assert_eq!(duration_in_minutes, 136);
            assert!(matches!(status, ItemStatus::CheckedOut { .. }));
            if let ItemStatus::CheckedOut { due_date: d } = status {
                assert_eq!(d, due_date);
            }
        }
    }
}
```

-----

## Submission

Commit and push both of your new lab folders (`lab11_part1` and `lab11_part2`) to your `is4010-labs` repository.

```
# From the root of your is4010-labs directory
git add lab11_part1/ lab11_part2/
git commit -m "Complete lab 11"
git push origin main
```