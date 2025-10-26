# Week 12: Generics, Traits, and Testing - Interactive Exercises

**Course:** IS4010 - AI-Enhanced Application Development
**Topic:** Generic Types, Trait System, and Test-Driven Development in Rust
**Companion Materials:** [Slides](../IS4010_W12_Generics_Traits_and_Testing.qmd) | [Lecture Notes](./W12_Generics_Traits_and_Testing_notes.md) | [Lab 12](https://github.com/bgreenwell/is4010-course-template/tree/main/labs/lab12)

---

## 🎯 Overview

These hands-on exercises help you master generics, traits, and testing in Rust. Work through them sequentially - each builds foundational skills for Lab 12.

**How to use these exercises:**
1. Click the Rust Playground link for each exercise
2. Read the instructions and starter code
3. Try to solve it yourself first
4. Use the AI prompting tips if you get stuck
5. Experiment with variations after solving

---

## Exercise 1: Your First Generic Function

**Concept focus:** Converting concrete functions to generic functions

**Exercise:**
Convert these two functions into a single generic function.

**Rust Playground:** [Try it here](https://play.rust-lang.org/)

**Starter code:**
```rust
fn print_i32(value: i32) {
    println!("The value is: {}", value);
}

fn print_string(value: String) {
    println!("The value is: {}", value);
}

// TODO: Write a generic print_value<T> function
// that works for both types

fn main() {
    print_i32(42);
    print_string(String::from("hello"));

    // TODO: Use your generic function instead:
    // print_value(42);
    // print_value(String::from("hello"));
}
```

**Your task:**
1. Write a generic `print_value<T>` function
2. Add the necessary trait bound (T must be printable)
3. Replace the specific functions with your generic one

**AI prompting tips:**
- "How do I make a function generic in Rust?"
- "What trait bound do I need for printing values?"
- "What's the difference between {} and {:?} formatting?"

**Learning goals:**
- Understand generic function syntax
- Apply Display trait bound
- See how generics reduce code duplication

---

## Exercise 2: Generic Struct with Multiple Types

**Concept focus:** Defining structs with multiple type parameters

**Exercise:**
Create a generic `Pair` struct that can hold two values of potentially different types.

**Rust Playground:** [Try it here](https://play.rust-lang.org/)

**Starter code:**
```rust
// TODO: Define a Pair<T, U> struct with fields first and second

// TODO: Implement a constructor method new(first: T, second: U)

// TODO: Implement a method swap() that returns Pair<U, T>

fn main() {
    // TODO: Create pairs with different type combinations:
    // Pair of two integers
    // Pair of integer and string
    // Pair of string and float

    // TODO: Test the swap method
}
```

**Your task:**
1. Define `Pair<T, U>` struct
2. Implement `new()` constructor
3. Implement `swap()` method that reverses the types
4. Create examples in `main()`

**AI prompting tips:**
- "How do I define a struct with two different generic types?"
- "How do I write methods for a generic struct?"
- "Can I return a different generic type from a method?"

**Learning goals:**
- Use multiple type parameters
- Implement methods on generic structs
- Transform between different generic types

---

## Exercise 3: Trait Bounds in Action

**Concept focus:** Constraining generics with trait bounds

**Exercise:**
Fix the `largest` function by adding appropriate trait bounds.

**Rust Playground:** [Try it here](https://play.rust-lang.org/)

**Starter code:**
```rust
// TODO: Add trait bounds to make this compile
fn largest<T>(list: &[T]) -> &T {
    let mut largest = &list[0];
    for item in list {
        if item > largest {  // Error: can't compare without trait bound!
            largest = item;
        }
    }
    largest
}

fn main() {
    let numbers = vec![34, 50, 25, 100, 65];
    println!("The largest number is {}", largest(&numbers));

    let chars = vec!['y', 'm', 'a', 'q'];
    println!("The largest char is {}", largest(&chars));
}
```

**Your task:**
1. Add the trait bound needed for comparison (`>`)
2. Verify it works with both numbers and chars
3. Try with other types (strings, floats)

**AI prompting tips:**
- "What trait do I need to compare values with > in Rust?"
- "Why doesn't this generic function compile?"
- "Explain PartialOrd vs Ord traits"

**Learning goals:**
- Understand trait bounds purpose
- Use PartialOrd for comparisons
- See how trait bounds enable operations

---

## Exercise 4: Implementing a Custom Trait

**Concept focus:** Defining and implementing traits

**Exercise:**
Define a `Summarizable` trait and implement it for different types.

**Rust Playground:** [Try it here](https://play.rust-lang.org/)

**Starter code:**
```rust
// TODO: Define a Summarizable trait with a summarize() method
// that returns a String

struct Article {
    title: String,
    author: String,
    content: String,
}

struct Tweet {
    username: String,
    content: String,
}

// TODO: Implement Summarizable for Article
// Format: "[title] by [author]"

// TODO: Implement Summarizable for Tweet
// Format: "@[username]: [content]"

fn main() {
    let article = Article {
        title: String::from("Rust is Great"),
        author: String::from("Alice"),
        content: String::from("Rust provides memory safety..."),
    };

    let tweet = Tweet {
        username: String::from("rustacean"),
        content: String::from("Loving Rust!"),
    };

    // TODO: Call summarize() on both
}
```

**Your task:**
1. Define the `Summarizable` trait
2. Implement it for `Article`
3. Implement it for `Tweet`
4. Create instances and test in `main()`

**AI prompting tips:**
- "How do I define a trait in Rust?"
- "What's the syntax for impl Trait for Type?"
- "How do I use format! to create strings?"

**Learning goals:**
- Define traits with method signatures
- Implement traits for multiple types
- Use traits to share behavior

---

## Exercise 5: Default Trait Implementations

**Concept focus:** Providing default behavior in traits

**Exercise:**
Enhance the `Summarizable` trait with a default implementation.

**Rust Playground:** [Try it here](https://play.rust-lang.org/)

**Starter code:**
```rust
trait Summarizable {
    fn author_name(&self) -> String;

    // TODO: Add a summarize() method with default implementation
    // Format: "Summary by [author_name]"
}

struct Article {
    author: String,
    title: String,
}

struct Tweet {
    username: String,
    content: String,
}

// TODO: Implement Summarizable for Article
// Only implement author_name, use default summarize

// TODO: Implement Summarizable for Tweet
// Override both author_name and summarize

fn main() {
    let article = Article {
        author: String::from("Alice"),
        title: String::from("Rust Traits"),
    };

    let tweet = Tweet {
        username: String::from("rustacean"),
        content: String::from("Traits are powerful!"),
    };

    // TODO: Call summarize() on both and see the difference
}
```

**Your task:**
1. Add default `summarize()` implementation to trait
2. Implement for Article (using default)
3. Implement for Tweet (overriding default)
4. Test both implementations

**AI prompting tips:**
- "How do I provide default implementations in Rust traits?"
- "Can I call one trait method from another in the default implementation?"
- "When should I use default implementations vs require implementers to provide them?"

**Learning goals:**
- Create default trait implementations
- Override defaults when needed
- Understand when to use defaults

---

## Exercise 6: Writing Your First Test

**Concept focus:** Basic test structure and assertions

**Exercise:**
Write tests for a simple calculator function.

**Rust Playground:** [Try it here](https://play.rust-lang.org/)

**Starter code:**
```rust
fn add(a: i32, b: i32) -> i32 {
    a + b
}

fn subtract(a: i32, b: i32) -> i32 {
    a - b
}

fn multiply(a: i32, b: i32) -> i32 {
    a * b
}

// TODO: Add a #[cfg(test)] module
// TODO: Write test_add() - assert_eq!(add(2, 2), 4)
// TODO: Write test_subtract() - test with positive and negative numbers
// TODO: Write test_multiply() - test with zero and non-zero

fn main() {
    println!("2 + 2 = {}", add(2, 2));
}
```

**Your task:**
1. Create a `#[cfg(test)]` module
2. Write at least 3 test functions
3. Use `assert_eq!` for verification
4. Run tests with `cargo test` (or Playground's test button)

**AI prompting tips:**
- "How do I write tests in Rust?"
- "What's the purpose of #[cfg(test)]?"
- "What's the difference between assert! and assert_eq!?"

**Learning goals:**
- Write basic test functions
- Use assertion macros
- Understand test module structure

---

## Exercise 7: Test-Driven Development Practice

**Concept focus:** Red → Green → Refactor TDD cycle

**Exercise:**
Use TDD to implement a simple `Counter` struct.

**Rust Playground:** [Try it here](https://play.rust-lang.org/)

**Starter code:**
```rust
// TODO: Define Counter struct (after writing tests!)

// TODO: Implement methods (after writing tests!)

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_new_counter_starts_at_zero() {
        // TODO: Write this test FIRST
        // let counter = Counter::new();
        // assert_eq!(counter.value(), 0);
    }

    #[test]
    fn test_increment() {
        // TODO: Write this test SECOND
        // Test that increment increases value by 1
    }

    #[test]
    fn test_decrement() {
        // TODO: Write this test THIRD
        // Test that decrement decreases value by 1
    }

    #[test]
    fn test_reset() {
        // TODO: Write this test FOURTH
        // Test that reset sets value back to 0
    }
}

fn main() {
    // Will work after implementing based on tests
}
```

**Your task:**
1. Write all tests FIRST (they will fail)
2. Run tests - they should fail (RED)
3. Implement minimum code to pass each test (GREEN)
4. Refactor if needed while keeping tests green
5. Follow strict TDD: test first, then code

**AI prompting tips:**
- "Walk me through the TDD process in Rust"
- "I have this failing test [paste] - what's the minimum code to pass it?"
- "How do I know when to refactor in TDD?"

**Learning goals:**
- Practice TDD cycle
- Write tests before implementation
- Experience design benefits of TDD

---

## Exercise 8: Testing Error Cases

**Concept focus:** Testing Result and panic cases

**Exercise:**
Write tests for a division function that handles errors.

**Rust Playground:** [Try it here](https://play.rust-lang.org/)

**Starter code:**
```rust
fn divide(a: f64, b: f64) -> Result<f64, String> {
    if b == 0.0 {
        Err(String::from("Division by zero"))
    } else {
        Ok(a / b)
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_divide_success() {
        // TODO: Test successful division
        // Use .unwrap() or pattern matching
    }

    #[test]
    fn test_divide_by_zero() {
        // TODO: Test that dividing by zero returns Err
        // Use assert!(result.is_err())
        // Check error message
    }

    #[test]
    fn test_divide_negatives() {
        // TODO: Test with negative numbers
    }

    // BONUS: Add #[should_panic] test
}
```

**Your task:**
1. Write test for successful division
2. Write test for division by zero error
3. Test with negative numbers
4. (Bonus) Write a `#[should_panic]` test

**AI prompting tips:**
- "How do I test functions that return Result?"
- "What's the difference between testing Result and testing panics?"
- "How do I use #[should_panic] in Rust tests?"

**Learning goals:**
- Test success and failure cases
- Work with Result in tests
- Use `should_panic` attribute

---

## Exercise 9: Implementing Display Trait

**Concept focus:** Manual trait implementation for custom formatting

**Exercise:**
Implement the Display trait for a Point struct.

**Rust Playground:** [Try it here](https://play.rust-lang.org/)

**Starter code:**
```rust
use std::fmt;

#[derive(Debug)]
struct Point {
    x: i32,
    y: i32,
}

// TODO: Implement fmt::Display for Point
// Format as: "(x, y)"

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_display() {
        let p = Point { x: 3, y: 4 };
        assert_eq!(format!("{}", p), "(3, 4)");
    }

    #[test]
    fn test_display_negative() {
        let p = Point { x: -1, y: -2 };
        assert_eq!(format!("{}", p), "(-1, -2)");
    }
}

fn main() {
    let p = Point { x: 1, y: 2 };
    println!("Point: {}", p);  // Will work after implementing Display
    println!("Debug: {:?}", p);  // Works via derive(Debug)
}
```

**Your task:**
1. Implement `fmt::Display` for `Point`
2. Use `write!` macro to format output
3. Run tests to verify format
4. Test in `main()`

**AI prompting tips:**
- "How do I implement the Display trait in Rust?"
- "What's the difference between Display and Debug?"
- "How does the write! macro work?"

**Learning goals:**
- Implement Display manually
- Understand fmt::Formatter
- Distinguish Display from Debug

---

## Exercise 10: Generic Stack with Tests (Lab 12 Preview)

**Concept focus:** Bringing it all together - generics, traits, and TDD

**Exercise:**
Start building a generic Stack using TDD.

**Rust Playground:** [Try it here](https://play.rust-lang.org/)

**Starter code:**
```rust
// TODO: Define Stack<T> struct (after tests!)

// TODO: Implement methods (guided by tests!)

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_new_stack_is_empty() {
        let stack: Stack<i32> = Stack::new();
        assert!(stack.is_empty());
        assert_eq!(stack.len(), 0);
    }

    #[test]
    fn test_push_increases_length() {
        let mut stack = Stack::new();
        stack.push(1);
        assert_eq!(stack.len(), 1);
        assert!(!stack.is_empty());
    }

    #[test]
    fn test_pop_returns_last_pushed() {
        let mut stack = Stack::new();
        stack.push(42);
        assert_eq!(stack.pop(), Some(42));
    }

    #[test]
    fn test_pop_empty_returns_none() {
        let mut stack: Stack<i32> = Stack::new();
        assert_eq!(stack.pop(), None);
    }

    #[test]
    fn test_works_with_different_types() {
        let mut int_stack = Stack::new();
        int_stack.push(1);
        assert_eq!(int_stack.pop(), Some(1));

        let mut string_stack = Stack::new();
        string_stack.push(String::from("hello"));
        assert_eq!(string_stack.pop(), Some(String::from("hello")));
    }
}
```

**Your task:**
1. Write all tests first (copy from starter)
2. Run tests - they'll fail (RED)
3. Define `Stack<T>` struct
4. Implement `new()`, `push()`, `pop()`, `is_empty()`, `len()`
5. Run tests - they should pass (GREEN)
6. Celebrate! You've just done TDD!

**AI prompting tips:**
- "Help me design a generic Stack data structure in Rust"
- "What should Stack<T> contain internally to store items?"
- "How do I implement push and pop for a Stack?"
- "Why do my generic type annotations matter in tests?"

**Learning goals:**
- Combine generics with TDD
- Build a complete generic data structure
- Write comprehensive test suite
- Prepare for Lab 12

---

## 🎯 Bonus Challenge: Iterator Trait

**Exercise:**
Implement the Iterator trait for your Stack.

**Rust Playground:** [Start here](https://play.rust-lang.org/)

**Requirements:**
1. Implement `Iterator` for `Stack<T>`
2. Use `type Item = T` for associated type
3. Implement `next()` to pop items
4. Write tests that use iterator methods (`for` loop, `collect()`, etc.)

**AI prompting tips:**
- "How do I implement Iterator trait for my custom type?"
- "What are associated types in Rust traits?"
- "How does the next() method work for iterators?"
- "Can I use my Stack in a for loop after implementing Iterator?"

**Learning goals:**
- Understand associated types
- Implement more complex traits
- Enable iteration over custom types
- Use trait to enable language features

---

## 🚀 Next Steps

After completing these exercises:

1. **Review your solutions** - Compare with classmates or AI feedback
2. **Experiment with variations** - Try different types, test cases, implementations
3. **Apply to Lab 12** - Use these patterns in your lab assignment
4. **Practice TDD** - Make it your default workflow

**Additional practice resources:**
- [Rust by Example - Generics](https://doc.rust-lang.org/rust-by-example/generics.html)
- [Rust by Example - Traits](https://doc.rust-lang.org/rust-by-example/trait.html)
- [Rust by Example - Testing](https://doc.rust-lang.org/rust-by-example/testing.html)
- [Rustlings Exercises](https://github.com/rust-lang/rustlings) - generics and traits sections

---

**Remember:** These concepts are fundamental to Rust. Generics enable code reuse, traits enable shared behavior, and tests ensure correctness. Master them and you'll write professional-quality Rust code!

**Need help?** Post on [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/group-chat-software) or use AI tools with the prompting tips provided above.

---

**Last Updated:** 2025-01-26
**Related Materials:** [Week 12 Slides](../IS4010_W12_Generics_Traits_and_Testing.qmd) | [Week 12 Notes](./W12_Generics_Traits_and_Testing_notes.md)
