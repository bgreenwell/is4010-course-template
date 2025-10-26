# Lab 12: Generic stack with test-driven development

**Due:** Sunday, November 16, 2025, at 11:59 PM
**Points:** 10

## 📋 Enhanced objective

Build a fully-tested [generic stack data structure](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)) in Rust using [test-driven development](https://en.wikipedia.org/wiki/Test-driven_development) that demonstrates:
- **Generic programming** with [`<T>` type parameters](https://doc.rust-lang.org/book/ch10-01-syntax.html)
- **Trait implementation** for [`Display`](https://doc.rust-lang.org/std/fmt/trait.Display.html) and [`Iterator`](https://doc.rust-lang.org/std/iter/trait.Iterator.html)
- **Test-driven development** workflow (Red → Green → Refactor)
- **Comprehensive testing** with [`cargo test`](https://doc.rust-lang.org/cargo/commands/cargo-test.html)
- **Professional code organization** following Rust best practices

This lab synthesizes everything you've learned in Weeks 9-12 and demonstrates industry-standard development practices.

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

---

## 🔧 Prerequisites

- **Rust toolchain** - [Installation guide](../../resources/SETUP_GUIDE.md#rust-installation)
- **Git** for version control
- Knowledge of generics, traits, and testing from Week 12 lectures

---

## 🧪 Part 1: Test-driven development setup

### The TDD cycle

1. **🔴 RED**: Write a failing test
2. **🟢 GREEN**: Write minimal code to pass
3. **🔵 REFACTOR**: Improve code while keeping tests green
4. **Repeat**: Continue for next feature

### Create the project

```bash
# From your is4010-labs directory
cargo new lab12 --bin
cd lab12
```

### Set up test module

Replace `src/main.rs` contents:

```rust
fn main() {
    println!("Lab 12: Generic Stack with TDD");
}

#[cfg(test)]
mod tests {
    use super::*;

    // Tests will go here
}
```

Verify setup:
```bash
cargo test  # Should show 0 tests
```

---

## 📚 Part 2: Implement Stack with TDD

### Feature 1: new() and is_empty()

**Test first (RED):**
```rust
#[test]
fn test_new_stack_is_empty() {
    let stack: Stack<i32> = Stack::new();
    assert!(stack.is_empty());
}
```

Run: `cargo test` - it will fail (no Stack type exists)

**Implement (GREEN):**
```rust
struct Stack<T> {
    items: Vec<T>,
}

impl<T> Stack<T> {
    fn new() -> Stack<T> {
        Stack { items: Vec::new() }
    }

    fn is_empty(&self) -> bool {
        self.items.is_empty()
    }
}
```

Run: `cargo test` - it passes! ✅

### Feature 2: push() and len()

**Test first:**
```rust
#[test]
fn test_push_increases_length() {
    let mut stack = Stack::new();
    stack.push(1);
    stack.push(2);
    stack.push(3);
    assert_eq!(stack.len(), 3);
    assert!(!stack.is_empty());
}
```

**Implement:**
```rust
fn push(&mut self, item: T) {
    self.items.push(item);
}

fn len(&self) -> usize {
    self.items.len()
}
```

### Feature 3: pop()

**Tests:**
```rust
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
```

**Implement:**
```rust
fn pop(&mut self) -> Option<T> {
    self.items.pop()
}
```

### Feature 4: peek()

**Tests:**
```rust
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
```

**Implement:**
```rust
fn peek(&self) -> Option<&T> {
    self.items.last()
}
```

### Additional tests

Add tests for:
- Multiple types (int, String)
- Push/pop sequences
- Edge cases

You should have **at least 8 tests** for basic functionality.

---

## 🎨 Part 3: Implement Display trait

**Tests:**
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
```

**Implement:**
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

---

## 🔁 Part 4: Implement Iterator trait

**Tests:**
```rust
#[test]
fn test_iterator() {
    let mut stack = Stack::new();
    stack.push(1);
    stack.push(2);
    stack.push(3);

    let mut iter = stack.into_iter();
    assert_eq!(iter.next(), Some(3));  // LIFO!
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
    assert_eq!(results, vec![2, 1]);
}
```

**Implement:**
```rust
impl<T> Iterator for Stack<T> {
    type Item = T;

    fn next(&mut self) -> Option<Self::Item> {
        self.pop()
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

---

## ✅ Final requirements

Your test suite must have **at least 15 tests** covering:
- Basic functionality (new, push, pop, peek, len, is_empty)
- Edge cases (empty stack, multiple types)
- Display trait formatting
- Iterator behavior

Run all tests:
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

## 📦 Expected repository structure

```
is4010-labs/
├── .github/workflows/
│   └── lab12.yml
├── lab12/
│   ├── Cargo.toml
│   └── src/
│       └── main.rs
└── ...
```

---

## 📤 Submission

```bash
# From is4010-labs root
git add lab12/
git commit -m "Complete Lab 12: Generic Stack with TDD"
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
| Generic Stack implementation | 3 |
| Display trait | 1 |
| Iterator trait | 2 |
| Comprehensive tests (15+) | 2 |
| TDD process evidence | 1 |
| CI/CD passing | 1 |
| **Total** | **10** |

**Deductions:**
- -1: Compiler warnings
- -2: Tests failing
- -3: Missing trait implementations
- -5: Code doesn't compile

---

## 📚 Resources

- [Week 12 Slides](../../slides/IS4010_W12_Generics_Traits_and_Testing.qmd)
- [Week 12 Lecture Notes](../../resources/lecture-notes/W12_Generics_Traits_and_Testing_notes.md)
- [Week 12 Exercises](../../resources/lecture-notes/W12_Generics_Traits_and_Testing_exercises.md)
- [Rust Book - Generics](https://doc.rust-lang.org/book/ch10-01-syntax.html)
- [Rust Book - Testing](https://doc.rust-lang.org/book/ch11-00-testing.html)

---

**Remember:** Follow the TDD cycle strictly - test first, then implementation. This lab demonstrates professional software development practices you'll use throughout your career!

**Good luck!** 🦀
