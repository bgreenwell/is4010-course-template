# Week 09: Welcome to Rust - Lecture Notes

**Course:** IS4010 - AI-Enhanced Application Development
**Topic:** Introduction to Rust Programming
**Companion Materials:** [Slides](../IS4010_W09_Welcome_to_Rust.qmd) | [Interactive Exercises](./W09_Welcome_to_Rust_exercises.md) | [Lab 09](https://github.com/bgreenwell/is4010-course-template/tree/main/labs/lab09)

---

## 📋 Learning Objectives

By the end of this session, you should be able to:
- **Explain** why Rust is important in modern software development and how it differs from Python
- **Create** and run Rust projects using the Cargo build system
- **Write** Rust code with proper variable declarations, type annotations, and mutability
- **Implement** functions with type signatures and return values
- **Test** Rust code using the built-in testing framework

---

## Part 1: Why Rust?

### The Performance-Safety Trade-off

Historically, programmers faced a choice:
- **High-level languages** (Python, JavaScript): Easy to use, safe, but slower
- **Low-level languages** (C, C++): Fast and efficient, but easy to make dangerous mistakes

**Rust breaks this trade-off** by offering:
- **Performance**: As fast as C/C++, compiles to native machine code
- **Safety**: Memory-safe without a garbage collector
- **Reliability**: Catches bugs at compile-time that would crash other languages at runtime

### Real-World Applications

Rust is used in production by major companies:
- **Microsoft**: Windows kernel components, Azure infrastructure
- **Amazon Web Services**: Firecracker (serverless computing), Bottlerocket (container OS)
- **Google**: Parts of Android, Fuchsia OS
- **Meta (Facebook)**: Backend services, source control tools
- **Discord**: Migrated from Go to Rust for 10x performance improvements
- **Dropbox**: File synchronization engine
- **Mozilla Firefox**: Browser rendering components

### Career Relevance
- Consistently highest-paid programming language in Stack Overflow surveys
- Growing demand for Rust developers in systems programming, embedded systems, WebAssembly, and blockchain
- Essential for cloud infrastructure, game engines, and performance-critical applications

---

## Part 2: Compiled vs. Interpreted Languages

### How Python Works (Interpreted)
- **Runtime**: Python interpreter reads and executes code line-by-line
- **Flexibility**: Can modify code on the fly, dynamic typing
- **Performance**: Slower execution due to interpretation overhead
- **Distribution**: Requires Python runtime installed on target system

### How Rust Works (Compiled)
- **Compile-time**: rustc compiler translates entire program to machine code before running
- **Optimization**: Compiler optimizes for speed and memory efficiency
- **Performance**: Runs at native CPU speed, no interpretation overhead
- **Distribution**: Compiled binary runs standalone, no runtime needed

### The Rust Compiler: Your Friendly Assistant
Unlike many compilers, Rust's error messages are incredibly helpful:
- Explains exactly what went wrong
- Suggests how to fix the problem
- Points to relevant documentation
- Prevents entire categories of bugs before code ever runs

---

## Part 3: The Cargo Ecosystem

### What is Cargo?

[Cargo](https://doc.rust-lang.org/cargo/) is Rust's official package manager and build tool, equivalent to Python's pip + pytest + setuptools combined.

**Core capabilities:**
- **Project creation**: `cargo new project_name` creates a complete project structure
- **Dependency management**: Handles external libraries (called "crates")
- **Building**: `cargo build` compiles your code
- **Running**: `cargo run` compiles and executes in one command
- **Testing**: `cargo test` runs your test suite
- **Documentation**: `cargo doc` generates HTML documentation

### Essential Cargo Commands

```bash
# Create a new project (includes Git initialization)
cargo new hello_rust

# Compile the project (creates target/debug/ or target/release/)
cargo build

# Compile and run immediately
cargo run

# Run tests
cargo test

# Check code without building (fast feedback - use this constantly!)
cargo check

# Get helpful code suggestions (like a mentor reviewing your code)
cargo clippy

# Format code to Rust community standards
cargo fmt

# Clean build artifacts
cargo clean
```

### Project Structure

Every Cargo project has this standard structure:
```
my_project/
├── Cargo.toml      # Project metadata and dependencies
├── Cargo.lock      # Exact dependency versions (auto-generated)
├── src/
│   └── main.rs     # Your source code
└── target/         # Compiled binaries (auto-generated)
```

### Cargo's Professional Tools

**cargo clippy** - Your personal Rust mentor:
- Catches common mistakes and anti-patterns
- Suggests more idiomatic Rust code
- Over 500 lints for code quality, performance, and style
- Example suggestions: "this loop can be simplified" or "this might panic"

**cargo fmt** - Automatic code formatting:
- Formats code to match Rust community style (like Python's black)
- No debates about spacing or indentation
- Run before every commit for consistent code
- Most Rust projects use this tool

**Professional Rust Workflow:**
1. Write code
2. `cargo check` - Fast compilation check
3. `cargo clippy` - Learn better patterns
4. `cargo test` - Verify correctness
5. `cargo fmt` - Format before committing
6. `cargo run` - Try it out!

---

## Part 4: Rust Playground

### Browser-Based Experimentation

The [Rust Playground](https://play.rust-lang.org/) is an official online environment for running Rust code:
- **No installation required**: Write and run Rust instantly in your browser
- **Shareable links**: Collaborate by sharing code snippets
- **Multiple modes**: Standard, debug, release builds
- **All editions**: Rust 2015, 2018, 2021 editions available

**When to use Playground:**
- Testing small code examples
- Sharing code snippets with classmates or instructors
- Exploring syntax without local setup
- Quick experiments during problem-solving

---

## Part 5: Variables and Mutability

### Immutable by Default

Rust's philosophy: **immutability by default** prevents bugs:
```rust
let x = 5;        // Immutable - cannot change
// x = 6;         // Compiler error!
```

This is the opposite of Python, where everything is mutable unless you take special measures.

### Explicit Mutability

To change a value, you must declare intent with `mut`:
```rust
let mut y = 10;   // Mutable - can change
y = 15;           // Allowed
```

### Why Immutability Matters
- **Prevents bugs**: Can't accidentally modify data
- **Concurrency safety**: Multiple threads can safely read immutable data
- **Clearer intent**: `mut` keyword shows where data changes
- **Compiler optimizations**: Immutable data enables better performance

---

## Part 6: Type System

### Static Typing

Rust is statically typed - every variable's type must be known at compile time:
```rust
let age: i32 = 20;           // Explicit type annotation
let temperature = 72.5;       // Type inferred as f64
```

### Scalar Types

**Integers:**
- Signed: `i8`, `i16`, `i32`, `i64`, `i128` (can be negative)
- Unsigned: `u8`, `u16`, `u32`, `u64`, `u128` (positive only)
- Default: `i32`

**Floating-point:**
- `f32`: Single-precision (32 bits)
- `f64`: Double-precision (64 bits) - default

**Boolean:**
- `bool`: Either `true` or `false`

**Character:**
- `char`: Single Unicode character (4 bytes)
- Uses single quotes: `'a'`, `'😀'`

### Compound Types

**Tuples** - Fixed-size, mixed types:
```rust
let person: (&str, i32, f64) = ("Alice", 20, 3.8);
let (name, age, gpa) = person;  // Destructuring
```

**Arrays** - Fixed-size, same type:
```rust
let scores: [i32; 5] = [95, 87, 92, 88, 91];
let first = scores[0];
```

---

## Part 7: Functions

### Function Syntax

Rust functions require explicit type annotations:
```rust
fn function_name(param: Type) -> ReturnType {
    // function body
}
```

**Key differences from Python:**
- Parameter types are required
- Return type must be declared
- No `return` keyword needed for final expression

### Expressions vs. Statements

**Expression** (returns a value):
```rust
fn add(a: i32, b: i32) -> i32 {
    a + b  // No semicolon - this is returned
}
```

**Statement** (doesn't return):
```rust
fn print_sum(a: i32, b: i32) {
    let sum = a + b;  // Semicolon makes this a statement
    println!("Sum: {}", sum);
}
```

The semicolon matters! It's the difference between returning a value and not.

---

## Part 8: Testing

### Built-in Testing Framework

Rust includes testing infrastructure in the standard library and Cargo:
```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_addition() {
        assert_eq!(add(2, 3), 5);
    }
}
```

### Test Anatomy

- **`#[cfg(test)]`**: Only compiles tests when running `cargo test`
- **`mod tests`**: Organizes tests in a module
- **`use super::*`**: Imports functions from parent module
- **`#[test]`**: Marks function as a test
- **Assertion macros**: Verify expectations

### Assertion Macros

- **`assert!(condition)`**: Passes if condition is true
- **`assert_eq!(left, right)`**: Passes if left equals right
- **`assert_ne!(left, right)`**: Passes if left doesn't equal right

Tests panic (fail) if assertions don't pass.

---

## Part 9: Lab Application

### Lab 09: Rust Basics

This week's lab introduces Rust development workflow:

**Part 0: Experimentation**
- Use Rust Playground to explore syntax without installation
- Complete interactive exercises

**Part 1: Installation**
- Install Rust toolchain with rustup
- Verify with `cargo --version`

**Part 2: First Project**
- Create project with `cargo new`
- Understand project structure
- Run "Hello, World!"

**Part 3-6: Core Concepts**
- Variables and mutability practice
- Data types and type annotations
- Writing functions with type signatures
- Creating and running tests

### Design Considerations
- **Incremental learning**: Build from simple to complex
- **Immediate feedback**: Run cargo test locally before submitting
- **AI assistance**: Use Copilot/Claude, but understand the code
- **Error-driven learning**: Read compiler messages carefully

---

## Key Takeaways

1. **Rust solves the performance-safety trade-off** that Python and C/C++ can't handle elegantly
2. **Cargo is an all-in-one tool** for project management, building, testing, and dependencies
3. **Immutability by default** prevents bugs and enables compiler optimizations
4. **Static typing catches errors** at compile time instead of runtime
5. **Built-in testing** makes test-driven development natural and easy

---

## Career Relevance

### Technical Interview Preparation
- **Systems programming questions**: Demonstrate understanding of memory management and performance
- **Language comparison**: Explain trade-offs between Rust, Python, C++, Go
- **Safety principles**: Show knowledge of memory safety without garbage collection

### Industry Applications
- **Cloud infrastructure**: AWS, Azure, Google Cloud use Rust for performance-critical components
- **Systems programming**: Operating systems, device drivers, embedded systems
- **WebAssembly**: Rust is the primary language for high-performance web applications
- **Game development**: Engines and performance-critical game logic
- **Blockchain/Cryptocurrency**: Many projects use Rust for security and performance

### Skills Employers Value
- Understanding of systems-level programming concepts
- Ability to write safe, performant code
- Experience with modern build tools and testing
- Knowledge of compiled vs. interpreted languages

---

## Additional Resources

### Official Rust Resources
- [The Rust Programming Language Book](https://doc.rust-lang.org/book/) - Free, comprehensive guide ("The Rust Book")
- [Rust by Example](https://doc.rust-lang.org/rust-by-example/) - Learn through annotated code examples
- [Rustlings](https://github.com/rust-lang/rustlings/) - Small exercises for practicing Rust syntax
- [Rust Playground](https://play.rust-lang.org/) - Browser-based Rust experimentation

### Learning Platforms
- [Comprehensive Rust](https://google.github.io/comprehensive-rust/) - Google's 4-day Rust course
- [Microsoft Rust Course](https://www.youtube.com/playlist?list=PLlrxD0HtieHjbTjrchBwOVks_sr8EVW1x) - Free video series
- [Exercism Rust Track](https://exercism.org/tracks/rust) - Practice problems with mentoring

### Community Resources
- [Rust Users Forum](https://users.rust-lang.org/) - Friendly community for questions
- [/r/rust](https://www.reddit.com/r/rust/) - Reddit community
- [Rust Discord](https://discord.gg/rust-lang) - Real-time chat and help

---

**Last Updated**: 2025-01-18
**Instructor**: Brandon M. Greenwell

---

## Tips for Success

### Working with the Rust Compiler
- **Read error messages carefully** - Rust errors are incredibly helpful
- **Don't fight the compiler** - It's catching bugs for you
- **Use `cargo check`** frequently - Fast way to verify code compiles
- **Run `cargo clippy`** regularly - It teaches you better Rust
- **Use `cargo fmt`** before commits - Keeps code professionally formatted

### Learning Strategy
- **Experiment in Playground** before writing local code
- **Run tests frequently** with `cargo test`
- **Read the Rust Book** chapters alongside labs
- **Use AI assistants** but always understand the generated code

### Common Beginner Mistakes
- Forgetting `mut` for variables you need to change
- Adding semicolons when you want to return a value
- Not specifying function parameter types
- Comparing different integer types without casting

### Getting Help
- Check compiler error messages first (they're very good!)
- Search the Rust Book for concept explanations
- Use the Rust Playground to share code when asking for help
- Ask in the course Teams channel - your classmates likely have similar questions!
