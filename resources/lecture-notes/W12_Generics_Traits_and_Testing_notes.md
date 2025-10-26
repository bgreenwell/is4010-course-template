# Week 12: Generics, Traits, and Testing - Lecture Notes

**Course:** IS4010 - AI-Enhanced Application Development
**Topic:** Generic Types, Trait System, and Test-Driven Development in Rust
**Companion Materials:** [Slides](../IS4010_W12_Generics_Traits_and_Testing.qmd) | [Interactive Exercises](./W12_Generics_Traits_and_Testing_exercises.md) | [Lab 12](https://github.com/bgreenwell/is4010-course-template/tree/main/labs/lab12)

---

## 📋 Learning Objectives

By the end of this session, you should be able to:
- **Write** generic functions and data structures that work with multiple types
- **Define** and implement traits to specify shared behavior
- **Use** trait bounds to constrain generic types
- **Implement** common standard library traits (Debug, Clone, Display, Iterator)
- **Practice** test-driven development (TDD) workflow
- **Write** comprehensive test suites with cargo test
- **Apply** generics and traits together to build reusable, well-tested code

---

## Part 1: Understanding Generics

### The Problem: Code Duplication

Without generics, you'd need separate functions for each type:

```rust
fn largest_i32(list: &[i32]) -> &i32 { /* ... */ }
fn largest_f64(list: &[f64]) -> &f64 { /* ... */ }
fn largest_char(list: &[char]) -> &char { /* ... */ }
// Duplicate logic for every type!
```

This is unmaintainable and violates the DRY (Don't Repeat Yourself) principle.

### Generics: Write Once, Use Everywhere

[Generics](https://doc.rust-lang.org/book/ch10-01-syntax.html) let you write code that works with multiple types:

```rust
fn largest<T: PartialOrd>(list: &[T]) -> &T {
    // Works with ANY type that can be compared
}
```

**Key benefits:**
- Code reuse without duplication
- Type safety maintained
- Zero runtime cost (monomorphization)
- Compile-time guarantees

### Generic Data Structures

**Generic structs:**
```rust
struct Point<T> {
    x: T,
    y: T,
}
```

**Multiple type parameters:**
```rust
struct Point<T, U> {
    x: T,
    y: U,  // Can be different types
}
```

**Generic enums** (you've been using them!):
- `Option<T>` - represents optional values
- `Result<T, E>` - represents success or failure
- `Vec<T>` - dynamic arrays

### Generic Methods

```rust
impl<T> Point<T> {
    fn x(&self) -> &T {
        &self.x
    }
}

// Methods for specific types only
impl Point<f32> {
    fn distance_from_origin(&self) -> f32 {
        (self.x.powi(2) + self.y.powi(2)).sqrt()
    }
}
```

### Performance: Monomorphization

Rust generates specialized code for each concrete type at compile time:

```rust
let integer_point = Point { x: 5, y: 10 };     // Point<i32>
let float_point = Point { x: 1.0, y: 4.0 };    // Point<f64>
```

Compiler creates two separate implementations - no runtime overhead!

---

## Part 2: The Trait System

### What Are Traits?

[Traits](https://doc.rust-lang.org/book/ch10-02-traits.html) define shared behavior that types can implement. Think of them as:
- Interfaces (Java, C#)
- Protocols (Swift)
- Type classes (Haskell)

**Key difference from inheritance:** Traits describe *what something can do*, not *what it is*.

### Defining Traits

```rust
pub trait Summary {
    fn summarize(&self) -> String;
}
```

### Implementing Traits

```rust
struct NewsArticle {
    headline: String,
    content: String,
}

impl Summary for NewsArticle {
    fn summarize(&self) -> String {
        format!("{}: {}", self.headline, self.content)
    }
}
```

### Default Implementations

Traits can provide default behavior:

```rust
pub trait Summary {
    fn summarize_author(&self) -> String;

    // Default implementation
    fn summarize(&self) -> String {
        format!("(Read more from {}...)", self.summarize_author())
    }
}
```

Types can use the default or override it.

### Trait Bounds

[Trait bounds](https://doc.rust-lang.org/book/ch10-02-traits.html#trait-bounds) constrain generic types:

```rust
// T must implement PartialOrd
fn largest<T: PartialOrd>(list: &[T]) -> &T { /* ... */ }

// Multiple bounds with +
fn notify<T: Summary + Display>(item: &T) { /* ... */ }

// Where clause for readability
fn some_function<T, U>(t: &T, u: &U) -> i32
where
    T: Display + Clone,
    U: Clone + Debug,
{
    // ...
}
```

### Traits as Parameters

```rust
// Short syntax
pub fn notify(item: &impl Summary) {
    println!("Breaking news! {}", item.summarize());
}

// Trait bound syntax (equivalent)
pub fn notify<T: Summary>(item: &T) {
    println!("Breaking news! {}", item.summarize());
}
```

### Returning Trait Types

```rust
fn returns_summarizable() -> impl Summary {
    Tweet {
        username: String::from("rustacean"),
        content: String::from("Rust is awesome!"),
    }
}
```

**Important limitation:** Can only return ONE concrete type (not different types in different branches).

---

## Part 3: Common Standard Library Traits

### Derivable Traits

These can be automatically implemented with `#[derive(...)]`:

**[`Debug`](https://doc.rust-lang.org/std/fmt/trait.Debug.html)**
- Enables `{:?}` formatting
- Essential for debugging
- Almost always derive this

**[`Clone`](https://doc.rust-lang.org/std/clone/trait.Clone.html)**
- Create deep copies with `.clone()`
- Useful when you need to duplicate data

**[`Copy`](https://doc.rust-lang.org/std/marker/trait.Copy.html)**
- Types copied by just copying bits
- Can't have heap allocations
- Integers, floats, bools implement Copy

**[`PartialEq`](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html) and [`Eq`](https://doc.rust-lang.org/std/cmp/trait.Eq.html)**
- Enable `==` and `!=` comparisons
- Eq requires reflexivity (a == a always true)

**[`PartialOrd`](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html) and [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html)**
- Enable `<`, `>`, `<=`, `>=` comparisons
- Ord requires total ordering

**[`Default`](https://doc.rust-lang.org/std/default/trait.Default.html)**
- Provides default values
- Useful for builder patterns

**[`Hash`](https://doc.rust-lang.org/std/hash/trait.Hash.html)**
- Enable use as HashMap keys
- Requires Eq implementation

### Manually Implemented Traits

Some traits must be implemented by hand:

**[`Display`](https://doc.rust-lang.org/std/fmt/trait.Display.html)**
- User-facing formatting with `{}`
- Implement for types users will see

**[`Iterator`](https://doc.rust-lang.org/std/iter/trait.Iterator.html)**
- Make types iterable
- Provides 50+ methods for free once implemented

**[`From`](https://doc.rust-lang.org/std/convert/trait.From.html) and [`Into`](https://doc.rust-lang.org/std/convert/trait.Into.html)**
- Type conversions
- Implementing From automatically gives you Into

---

## Part 4: Implementing Key Traits

### Display Trait

```rust
use std::fmt;

impl fmt::Display for Point {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "({}, {})", self.x, self.y)
    }
}
```

**When to use:**
- User-facing output
- Types that have natural string representation
- Error messages

### Iterator Trait

```rust
impl Iterator for Counter {
    type Item = u32;  // Associated type

    fn next(&mut self) -> Option<Self::Item> {
        if self.count < 5 {
            self.count += 1;
            Some(self.count)
        } else {
            None
        }
    }
}
```

**Benefits:**
- Use in for loops
- Access to iterator methods (map, filter, collect, etc.)
- Lazy evaluation

### From/Into for Conversions

```rust
impl From<i32> for MyType {
    fn from(value: i32) -> Self {
        MyType { inner: value }
    }
}

// Now you can do:
let my_value = MyType::from(42);
let my_value: MyType = 42.into();  // Into provided for free
```

---

## Part 5: Test-Driven Development (TDD)

### The TDD Cycle

**Red → Green → Refactor:**

1. **Red**: Write a failing test
2. **Green**: Write minimum code to pass the test
3. **Refactor**: Improve code while keeping tests green
4. Repeat

### Why TDD?

**Benefits:**
- Better design (think about usage first)
- Higher confidence (tests written upfront)
- Living documentation (tests show how to use code)
- Easier refactoring (safety net)

**Industry adoption:**
- Standard practice in many companies
- Required for critical systems
- Common in open-source projects

### TDD vs. Test-After

**TDD (write tests first):**
- Forces you to think about API design
- Prevents over-engineering
- Tests are easier to write

**Test-After (write tests after code):**
- Easy to forget edge cases
- Temptation to skip testing
- Tests might be influenced by implementation

---

## Part 6: Testing in Rust

### Basic Test Structure

```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_something() {
        let result = function_to_test();
        assert_eq!(result, expected_value);
    }
}
```

**Key components:**
- `#[cfg(test)]`: Only compile when testing
- `#[test]`: Marks function as a test
- Assertions: Verify expected behavior

### Assertion Macros

**[`assert!`](https://doc.rust-lang.org/std/macro.assert.html)**
- Check boolean conditions
- `assert!(true)`, `assert!(!false)`

**[`assert_eq!`](https://doc.rust-lang.org/std/macro.assert_eq.html) and [`assert_ne!`](https://doc.rust-lang.org/std/macro.assert_ne.html)**
- Check equality/inequality
- `assert_eq!(2 + 2, 4)`
- `assert_ne!(2 + 2, 5)`

**Custom messages:**
```rust
assert_eq!(x, 5, "x should be 5, but was {}", x);
```

### Testing Panics and Errors

**Expected panics:**
```rust
#[test]
#[should_panic(expected = "Division by zero")]
fn test_divide_by_zero() {
    divide(10.0, 0.0).unwrap();
}
```

**Testing Result:**
```rust
#[test]
fn test_error_case() {
    let result = function_that_returns_result();
    assert!(result.is_err());
    assert_eq!(result.unwrap_err(), "Expected error message");
}
```

### Running Tests

```bash
# Run all tests
cargo test

# Run specific test
cargo test test_name

# Run tests matching pattern
cargo test pattern

# Show println! output
cargo test -- --nocapture

# Run tests sequentially
cargo test -- --test-threads=1
```

### Test Organization

**Unit tests** (same file as code):
- Test individual functions
- Can access private items
- Located in `#[cfg(test)]` module

**Integration tests** (`tests/` directory):
- Test public API
- Test how pieces work together
- Each file is a separate crate

**Documentation tests**:
- Code examples in `///` comments
- Automatically tested
- Ensures docs stay current

---

## Part 7: Building Testable Code

### Design for Testability

**Good practices:**
- Small, focused functions
- Minimize dependencies
- Use dependency injection
- Separate I/O from logic

**Example:**
```rust
// Hard to test (I/O mixed with logic)
fn process_file() {
    let data = read_file("data.txt");  // Hard-coded file
    let result = process_data(data);
    write_file("output.txt", result);
}

// Easy to test (logic separated)
fn process_data(data: &str) -> String {
    // Pure function - easy to test!
}
```

### Test Coverage

**What to test:**
- Happy path (normal usage)
- Edge cases (empty, zero, max values)
- Error cases (invalid input)
- Boundary values
- Interactions between components

**Don't test:**
- Compiler-generated code
- Third-party libraries (trust their tests)
- Trivial getters/setters

### Writing Good Tests

**Characteristics of good tests:**
1. **Fast**: Run quickly to encourage frequent testing
2. **Independent**: Don't depend on other tests or order
3. **Repeatable**: Same input → same output
4. **Self-validating**: Pass or fail clearly
5. **Timely**: Written before or with code (TDD)

**AAA pattern:**
- **Arrange**: Set up test data
- **Act**: Execute code under test
- **Assert**: Verify results

---

## Part 8: Real-World Impact

### Industry Adoption

**[Rust compiler](https://github.com/rust-lang/rust)**:
- 100,000+ tests
- Multiple test suites (unit, integration, UI)
- Tests run on every commit

**[Servo browser engine](https://github.com/servo/servo)**:
- Comprehensive test coverage
- Performance benchmarks
- Crash testing and fuzzing

**[Tokio async runtime](https://github.com/tokio-rs/tokio)**:
- Property-based testing
- Concurrency testing with Loom
- Undefined behavior detection with Miri

### Generics in the Wild

**[Serde](https://serde.rs/)**: Generic serialization framework
- Works with any data format (JSON, YAML, etc.)
- Powered entirely by traits and generics

**[Diesel](https://diesel.rs/)**: Type-safe database ORM
- Compile-time SQL verification
- Generic query builders

**[Tokio](https://tokio.rs/)**: Async runtime
- Generic futures and streams
- Zero-cost async abstractions

---

## Part 9: Career Relevance

### Why These Skills Matter

**Generics:**
- Universal concept across modern languages
- Essential for library development
- Interview topic: "Design a generic data structure"

**Traits/Interfaces:**
- Core to object-oriented and functional design
- Composition over inheritance (modern best practice)
- Common interview question: "Design an interface for..."

**Testing:**
- Expected in all professional development
- Demonstrates code quality awareness
- TDD is industry standard in many companies

### Interview Preparation

**Common questions:**
- "Explain generics and when to use them"
- "What's the difference between a trait and a class?"
- "How do you test this function?"
- "Walk me through TDD process"
- "What makes a good test?"

### Transferable Skills

**Generics thinking:**
- Identify common patterns
- Abstract over differences
- Reusable code design

**Trait/interface design:**
- Define clear contracts
- Minimal but complete APIs
- Composition strategies

**Testing discipline:**
- Automated quality assurance
- Regression prevention
- Documentation through tests

---

## Part 10: Working with AI on Generics and Testing

### Effective AI Prompts

**Generic design:**
- "Help me design a generic cache data structure in Rust"
- "What trait bounds do I need for this generic function?"
- "Convert this concrete type to a generic implementation"

**Trait implementation:**
- "How do I implement the Iterator trait for my type?"
- "What traits should my custom type implement?"
- "Help me understand this trait bound error: [paste error]"

**Test development:**
- "Generate test cases for this function: [paste code]"
- "What edge cases should I test for string parsing?"
- "Help me write a property-based test for this algorithm"

**TDD workflow:**
- "I'm using TDD to build a Stack. Help me write the first test"
- "This test is failing: [paste]. What's the minimal code to make it pass?"
- "Suggest refactorings now that my tests are green"

### AI Testing Strategies

**Test generation:**
- AI excels at generating comprehensive test cases
- Ask for edge cases you might miss
- Request both positive and negative tests

**Test debugging:**
- Paste failing tests for diagnosis
- Ask for alternative test approaches
- Clarify assertion strategies

**Code review:**
- "Are these trait bounds idiomatic?"
- "Is my test suite comprehensive?"
- "Suggest improvements to this generic implementation"

---

## Part 11: Key Takeaways

### Core Concepts to Remember

**Generics:**
- Enable code reuse across types
- Zero runtime cost (monomorphization)
- Constrained with trait bounds
- Work with structs, enums, functions, methods

**Traits:**
- Define shared behavior
- Enable polymorphism without inheritance
- Can have default implementations
- Foundation of Rust's standard library design

**Trait Bounds:**
- Constrain generic types
- Specify required behavior
- Enable compile-time verification
- Use `where` clauses for readability

**Testing:**
- Built into Cargo (`cargo test`)
- TDD improves design
- Comprehensive tests enable confident refactoring
- Tests are documentation

### The Mental Model Shift

**Coming from Python/Java:**
- Generics are more powerful than you expect
- Traits are interfaces++
- Testing is painless (no separate framework needed)
- Type system is your friend

**The payoff:**
- Write less code (through generics)
- Catch bugs earlier (trait bounds)
- Refactor fearlessly (comprehensive tests)
- Ship confident code (compiler guarantees)

### Design Principles

**Generic programming:**
- Abstract over differences
- Keep constraints minimal
- Let the type system guide you

**Trait design:**
- Small, focused traits
- Composition over complexity
- Provide useful defaults

**Testing approach:**
- Write tests first (TDD)
- Test behavior, not implementation
- Cover edge cases
- Keep tests fast

---

## Part 12: Application to Lab 12

This week's lab brings everything together:

### Lab 12: Generic Stack with TDD

**What you'll build:**
- Generic `Stack<T>` data structure
- Methods: `push`, `pop`, `peek`, `is_empty`, `len`
- Trait implementations: `Display`, `Iterator`
- Comprehensive test suite (15+ tests)

**Skills you'll practice:**
- Writing generic structs and methods
- Implementing standard library traits
- Using trait bounds appropriately
- Test-driven development workflow
- Writing thorough test coverage

**TDD process:**
1. Write test for `new()` and `is_empty()`
2. Implement minimal code to pass
3. Write test for `push()` and `len()`
4. Implement and pass
5. Continue for all methods
6. Implement traits
7. Refactor with confidence

**Why it matters:**
- Synthesizes Weeks 9-12 concepts
- Mirrors real-world development
- Demonstrates professional practices
- Builds portfolio-worthy code

---

## Additional Resources

### Official Rust Documentation

- [The Rust Programming Language - Chapter 10: Generic Types, Traits, and Lifetimes](https://doc.rust-lang.org/book/ch10-00-generics.html)
- [The Rust Programming Language - Chapter 11: Writing Automated Tests](https://doc.rust-lang.org/book/ch11-00-testing.html)
- [Rust by Example - Generics](https://doc.rust-lang.org/rust-by-example/generics.html)
- [Rust by Example - Traits](https://doc.rust-lang.org/rust-by-example/trait.html)
- [Rust by Example - Testing](https://doc.rust-lang.org/rust-by-example/testing.html)
- [Rust Reference - Traits](https://doc.rust-lang.org/reference/items/traits.html)

### Interactive Learning

- [Rust Playground](https://play.rust-lang.org/) - Test generic code online
- [Rustlings](https://github.com/rust-lang/rustlings) - Exercises for generics and traits
- [Exercism Rust Track](https://exercism.org/tracks/rust) - Practice problems

### Articles and Guides

- [Rust Traits: A Deep Dive](https://oswalt.dev/2021/09/rust-traits-a-deep-dive/)
- [Understanding Trait Objects](https://www.lurklurk.org/effective-rust/trait-objects.html)
- [Generic Associated Types Explained](https://blog.rust-lang.org/2022/10/28/gats-stabilization.html)
- [Effective Testing in Rust](https://www.lurklurk.org/effective-rust/testing.html)
- [Test-Driven Development in Rust](https://blog.logrocket.com/test-driven-development-rust/)

### Testing Tools

- [cargo-tarpaulin](https://crates.io/crates/cargo-tarpaulin) - Code coverage
- [cargo-llvm-cov](https://crates.io/crates/cargo-llvm-cov) - Cross-platform coverage
- [proptest](https://crates.io/crates/proptest) - Property-based testing
- [quickcheck](https://crates.io/crates/quickcheck) - Property testing
- [criterion](https://crates.io/crates/criterion) - Benchmarking

### Videos

- [Rust Generics Explained](https://www.youtube.com/watch?v=nvur2Ast8hE)
- [Traits and Trait Objects](https://www.youtube.com/watch?v=Chi3d6_qKPE)
- [Testing in Rust](https://www.youtube.com/watch?v=18-7NoNPO30)

### Community Resources

- [Rust Users Forum](https://users.rust-lang.org/)
- [r/rust subreddit](https://www.reddit.com/r/rust/)
- [Rust Discord](https://discord.gg/rust-lang)
- [This Week in Rust](https://this-week-in-rust.org/) - Weekly newsletter

---

## Looking Ahead: Week 13

Next week we'll learn idiomatic Rust patterns:

**Topics:**
- Closures and function pointers
- Iterator patterns and combinators
- Smart pointers (Box, Rc, RefCell, Arc)
- Common Rust idioms and patterns
- When to use each pattern

**Why generics/traits come first:**
- Closures use trait system (Fn, FnMut, FnOnce)
- Iterators are based on Iterator trait
- Smart pointers use generic types
- Everything builds on this foundation

**Lab 13:**
- Refactor existing code to use idiomatic patterns
- Replace loops with iterators
- Use closures for callbacks
- Apply smart pointers appropriately

---

**Remember:** Generics and traits are the heart of Rust's power. Master them and you'll write code that's both flexible and type-safe. TDD ensures your code works correctly from day one!

**Need help?** Reach out on [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/group-chat-software) - we're here to support your learning journey.

---

**Last Updated:** 2025-01-26
**Next Session:** Week 13 - Idiomatic Rust Patterns
