# Lab 12: Generic stack implementation

**Due:** Sunday, November 16, 2025, at 11:59 PM
**Points:** 10

## 📋 Enhanced objective

Build a fully-functional [generic stack data structure](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)) in Rust that demonstrates:
- **Generic programming** with [`<T>` type parameters](https://doc.rust-lang.org/book/ch10-01-syntax.html)
- **Trait implementation** for [`Display`](https://doc.rust-lang.org/std/fmt/trait.Display.html) and [`Iterator`](https://doc.rust-lang.org/std/iter/trait.Iterator.html)
- **Trait bounds** to constrain generic types
- **Polymorphism** through generics (same code works with any type)
- **Professional code organization** following Rust best practices

This lab synthesizes the generics and traits concepts from Week 12, demonstrating how to build reusable, type-safe data structures in Rust.

---

## 🎯 Background

### Why stacks matter

[Stacks](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)) are fundamental data structures used throughout computer science:

**Applications:**
- **Function calls**: Call stack in every programming language
- **Expression evaluation**: Calculators, compilers
- **Undo/redo**: Text editors, graphics programs
- **Browser history**: Back/forward navigation

**Stack operations (LIFO - Last In, First Out):**
- **push**: Add element to top
- **pop**: Remove and return top element
- **peek**: View top element without removing
- **is_empty**: Check if stack has no elements
- **len**: Get number of elements

### Why generics matter

Your `Stack<T>` will work with **any type**:
```rust
let int_stack: Stack<i32> = Stack::new();
let string_stack: Stack<String> = Stack::new();
let vec_stack: Stack<Vec<f64>> = Stack::new();
```

This is the power of **generic programming** - write once, use everywhere!

---

## 🔧 Prerequisites

- **Rust toolchain** - [Installation guide](../../resources/SETUP_GUIDE.md#rust-installation)
- **Git** for version control
- Knowledge of generics and traits from Week 12 lectures

---

## 📁 Part 1: Project setup

### Create the project

```bash
# From your is4010-labs directory
cargo new lab12 --bin
cd lab12
```

### Set up the initial structure

Replace `src/main.rs` contents:

```rust
fn main() {
    println!("Lab 12: Generic Stack Implementation");

    // You'll test your stack here
    let mut stack = Stack::new();
    stack.push(1);
    stack.push(2);
    stack.push(3);

    println!("Stack: {}", stack);
    println!("Popped: {:?}", stack.pop());
    println!("Peek: {:?}", stack.peek());
}

// Your Stack implementation will go here

#[cfg(test)]
mod tests {
    use super::*;

    // Tests will go here
}
```

Verify setup:
```bash
cargo build  # Should compile (but main won't work yet)
```

---

## 📚 Part 2: Implement the generic Stack

### Define the generic struct

Add this above `main()`:

```rust
struct Stack<T> {
    items: Vec<T>,
}
```

**Key concepts:**
- `<T>` is a **type parameter** - it can be any type
- `Vec<T>` is also generic - our stack uses a vector internally
- When you create `Stack<i32>`, `T` becomes `i32` everywhere

### Implement basic methods

```rust
impl<T> Stack<T> {
    /// Creates a new empty stack
    fn new() -> Stack<T> {
        Stack { items: Vec::new() }
    }

    /// Returns true if the stack has no elements
    fn is_empty(&self) -> bool {
        self.items.is_empty()
    }

    /// Adds an item to the top of the stack
    fn push(&mut self, item: T) {
        self.items.push(item);
    }

    /// Returns the number of items in the stack
    fn len(&self) -> usize {
        self.items.len()
    }

    /// Removes and returns the top item, or None if empty
    fn pop(&mut self) -> Option<T> {
        self.items.pop()
    }

    /// Returns a reference to the top item without removing it
    fn peek(&self) -> Option<&T> {
        self.items.last()
    }
}
```

**Understanding the syntax:**
- `impl<T>` - "For any type T..."
- `&self` - Immutable borrow (doesn't change the stack)
- `&mut self` - Mutable borrow (modifies the stack)
- `Option<T>` - Returns `Some(value)` or `None`

### Test your implementation

Try running:
```bash
cargo run
```

You should see output showing the stack operations working!

### Add comprehensive tests

Add these tests to the test module:

```rust
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
    stack.push(2);
    stack.push(3);
    assert_eq!(stack.len(), 3);
    assert!(!stack.is_empty());
}

#[test]
fn test_pop_returns_last_pushed() {
    let mut stack = Stack::new();
    stack.push(1);
    stack.push(2);
    assert_eq!(stack.pop(), Some(2));
    assert_eq!(stack.pop(), Some(1));
    assert_eq!(stack.pop(), None);
}

#[test]
fn test_pop_empty_stack() {
    let mut stack: Stack<i32> = Stack::new();
    assert_eq!(stack.pop(), None);
}

#[test]
fn test_peek_without_removing() {
    let mut stack = Stack::new();
    stack.push(42);
    assert_eq!(stack.peek(), Some(&42));
    assert_eq!(stack.len(), 1);
}

#[test]
fn test_peek_empty_stack() {
    let stack: Stack<i32> = Stack::new();
    assert_eq!(stack.peek(), None);
}

#[test]
fn test_with_strings() {
    let mut stack = Stack::new();
    stack.push(String::from("hello"));
    stack.push(String::from("world"));
    assert_eq!(stack.pop(), Some(String::from("world")));
}

#[test]
fn test_push_pop_sequence() {
    let mut stack = Stack::new();
    stack.push(1);
    stack.push(2);
    assert_eq!(stack.pop(), Some(2));
    stack.push(3);
    assert_eq!(stack.pop(), Some(3));
    assert_eq!(stack.pop(), Some(1));
}
```

Run tests:
```bash
cargo test
```

You should have **at least 8 tests passing** for basic functionality.

---

## 🎨 Part 3: Implement the Display trait

The [`Display` trait](https://doc.rust-lang.org/std/fmt/trait.Display.html) allows your stack to be printed with `println!("{}", stack)`.

### Add the implementation

Add this to your code:

```rust
use std::fmt;

impl<T: fmt::Display> fmt::Display for Stack<T> {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "[")?;
        for (i, item) in self.items.iter().enumerate() {
            if i > 0 {
                write!(f, ", ")?;
            }
            write!(f, "{}", item)?;
        }
        write!(f, "]")
    }
}
```

**Understanding the syntax:**
- `impl<T: fmt::Display>` - "For any type T that implements Display..."
- This is a **trait bound** - we can only display T if T is displayable
- `write!` and `?` operator for error handling

### Test Display implementation

Add these tests:

```rust
#[test]
fn test_display_format() {
    let mut stack = Stack::new();
    stack.push(1);
    stack.push(2);
    stack.push(3);
    assert_eq!(format!("{}", stack), "[1, 2, 3]");
}

#[test]
fn test_display_empty() {
    let stack: Stack<i32> = Stack::new();
    assert_eq!(format!("{}", stack), "[]");
}

#[test]
fn test_display_strings() {
    let mut stack = Stack::new();
    stack.push("hello");
    stack.push("world");
    assert_eq!(format!("{}", stack), "[hello, world]");
}
```

---

## 🔁 Part 4: Implement the Iterator trait

The [`Iterator` trait](https://doc.rust-lang.org/std/iter/trait.Iterator.html) allows your stack to be used in `for` loops and with iterator methods.

### Add the implementation

```rust
impl<T> Iterator for Stack<T> {
    type Item = T;

    fn next(&mut self) -> Option<Self::Item> {
        self.pop()  // Iterates in LIFO order!
    }
}

impl<T> IntoIterator for Stack<T> {
    type Item = T;
    type IntoIter = Stack<T>;

    fn into_iter(self) -> Self::IntoIter {
        self
    }
}
```

**Understanding the syntax:**
- `type Item = T;` - Associated type declaration
- `IntoIterator` trait allows using the stack in `for` loops
- Iterator consumes the stack (pops items in LIFO order)

### Test Iterator implementation

Add these tests:

```rust
#[test]
fn test_iterator() {
    let mut stack = Stack::new();
    stack.push(1);
    stack.push(2);
    stack.push(3);

    let mut iter = stack.into_iter();
    assert_eq!(iter.next(), Some(3));  // LIFO order!
    assert_eq!(iter.next(), Some(2));
    assert_eq!(iter.next(), Some(1));
    assert_eq!(iter.next(), None);
}

#[test]
fn test_for_loop() {
    let mut stack = Stack::new();
    stack.push(1);
    stack.push(2);

    let mut results = Vec::new();
    for item in stack {
        results.push(item);
    }
    assert_eq!(results, vec![2, 1]);  // LIFO!
}

#[test]
fn test_iterator_with_strings() {
    let mut stack = Stack::new();
    stack.push(String::from("first"));
    stack.push(String::from("second"));

    let collected: Vec<String> = stack.into_iter().collect();
    assert_eq!(collected, vec![String::from("second"), String::from("first")]);
}
```

---

## ✅ Part 5: Comprehensive testing

### Final test requirements

Your test suite must have **at least 15 tests** covering:
- Basic functionality (new, push, pop, peek, len, is_empty)
- Multiple data types (integers, strings, etc.)
- Edge cases (empty stack, single element)
- Display trait formatting
- Iterator behavior

Add one more test demonstrating polymorphism:

```rust
#[test]
fn test_polymorphism() {
    // Same Stack code works with different types!
    let mut int_stack = Stack::new();
    int_stack.push(1);
    int_stack.push(2);
    assert_eq!(int_stack.pop(), Some(2));

    let mut string_stack = Stack::new();
    string_stack.push(String::from("hello"));
    string_stack.push(String::from("world"));
    assert_eq!(string_stack.pop(), Some(String::from("world")));

    let mut float_stack = Stack::new();
    float_stack.push(3.14);
    float_stack.push(2.71);
    assert_eq!(float_stack.pop(), Some(2.71));
}
```

### Run all tests

```bash
cargo test
```

Expected output:
```
running 15 tests
...
test result: ok. 15 passed; 0 failed
```

---

## 🎯 Part 6: Update main() for demonstration

Update your `main()` function to demonstrate all capabilities:

```rust
fn main() {
    println!("Lab 12: Generic Stack Implementation\n");

    // Demonstrate with integers
    println!("=== Integer Stack ===");
    let mut int_stack = Stack::new();
    int_stack.push(10);
    int_stack.push(20);
    int_stack.push(30);
    println!("Stack: {}", int_stack);
    println!("Popped: {:?}", int_stack.pop());
    println!("Peek: {:?}", int_stack.peek());
    println!();

    // Demonstrate with strings
    println!("=== String Stack ===");
    let mut string_stack = Stack::new();
    string_stack.push(String::from("Rust"));
    string_stack.push(String::from("is"));
    string_stack.push(String::from("awesome"));
    println!("Stack: {}", string_stack);

    // Demonstrate iterator
    println!("\nIterating (LIFO order):");
    for item in string_stack {
        println!("  {}", item);
    }
}
```

Run:
```bash
cargo run
```

---

## 📦 Expected repository structure

```
is4010-labs/
├── .github/workflows/
│   └── rust.yml          # GitHub Actions for Rust testing
├── lab09/
├── lab10/
├── lab11/
├── lab12/
│   ├── Cargo.toml
│   ├── Cargo.lock
│   └── src/
│       └── main.rs       # Your generic stack implementation
└── ...
```

---

## 🤖 Using AI assistance

### Strategic AI prompts

**Understanding generics:**
- *"Explain how Rust's generic type parameters work. Why do I write `impl<T>` instead of just `impl`?"*
- *"What's the difference between `Stack<T>` and `Vec<T>` in terms of generics?"*
- *"Show me examples of using my Stack with 3 different types and explain why the same code works for all of them."*

**Trait implementations:**
- *"Explain what `T: fmt::Display` means in my Display trait implementation. Why is this trait bound necessary?"*
- *"I'm getting a compiler error when implementing Iterator. Here's my code [paste code]. What does the error mean?"*
- *"How does the IntoIterator trait differ from the Iterator trait? Why do I need both?"*

**Debugging:**
- *"My stack compiles but the tests fail. Here's the test output [paste output]. What's wrong?"*
- *"I'm getting 'trait bounds not satisfied' error. Here's my code [paste code]. How do I fix it?"*

**Testing:**
- *"What edge cases should I test for a generic stack data structure?"*
- *"Help me write a test that demonstrates my stack works with custom types (not just i32 and String)."*

---

## 📤 Submission

### Final checklist

- [ ] All 15+ tests passing
- [ ] `cargo build` compiles without warnings
- [ ] `cargo run` demonstrates stack with multiple types
- [ ] Display trait implemented
- [ ] Iterator trait implemented
- [ ] GitHub Actions CI/CD passing

### Submit your work

```bash
# From is4010-labs root
git add lab12/
git commit -m "Complete Lab 12: Generic Stack Implementation"
git push origin main
```

Submit repository URL on Canvas:
```
https://github.com/yourusername/is4010-labs
```

---

## 🎯 Grading rubric

| Category | Points |
|----------|--------|
| Generic Stack implementation (all methods) | 3 |
| Display trait implementation | 1 |
| Iterator trait implementation | 2 |
| Comprehensive tests (15+, all passing) | 2 |
| Code organization and documentation | 1 |
| GitHub Actions CI/CD passing | 1 |
| **Total** | **10** |

**Deductions:**
- -1: Compiler warnings
- -2: Tests failing
- -3: Missing trait implementations
- -5: Code doesn't compile

---

## 📚 Resources

**Week 12 Materials:**
- [Week 12 Slides](https://bgreenwell.github.io/is4010-instructor-materials/IS4010_W12_Generics_and_Traits.html)
- [Week 12 Lecture Notes](../../resources/lecture-notes/W12_Generics_and_Traits_notes.md)
- [Week 12 Exercises](../../resources/lecture-notes/W12_Generics_and_Traits_exercises.md)

**Official Documentation:**
- [Rust Book - Generic Types](https://doc.rust-lang.org/book/ch10-01-syntax.html)
- [Rust Book - Traits](https://doc.rust-lang.org/book/ch10-02-traits.html)
- [Rust Book - Advanced Traits](https://doc.rust-lang.org/book/ch19-03-advanced-traits.html)
- [Display Trait](https://doc.rust-lang.org/std/fmt/trait.Display.html)
- [Iterator Trait](https://doc.rust-lang.org/std/iter/trait.Iterator.html)

---

**Remember:** This lab demonstrates the power of generic programming - write code once that works with any type! The Stack you build here uses the same generics concepts found throughout Rust's standard library (Vec, HashMap, Option, Result, etc.).

**Good luck!** 🦀
