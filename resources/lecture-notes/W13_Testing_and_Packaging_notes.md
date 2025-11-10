# Week 13: Testing and Packaging - Lecture Notes

**Course:** IS4010 - AI-Enhanced Application Development
**Topic:** Testing and Packaging Rust Applications
**Companion Materials:** [Slides](../IS4010_W13_Testing_and_Packaging.qmd) | [Lab Focus](https://github.com/bgreenwell/is4010-course-template) - Final Project

---

## 📋 Learning Objectives

By the end of this session, you should be able to:
- **Practice** test-driven development (TDD) workflow in Rust
- **Write** unit tests and integration tests with cargo test
- **Understand** when to use Result vs Option for error handling
- **Apply** the `?` operator for error propagation
- **Build** command-line applications that read files and process arguments
- **Package** Rust applications with proper Cargo.toml configuration
- **Install** and distribute Rust binaries

---

## Part 1: Testing in Rust

### Why Testing Matters

**Professional standard:**
- All production code needs tests
- Tests enable confident refactoring
- Tests document expected behavior
- Rust makes testing easy with built-in tools

**Industry examples:**
- [Rust compiler](https://github.com/rust-lang/rust): 100,000+ tests
- [Servo](https://github.com/servo/servo): Comprehensive coverage
- [Tokio](https://github.com/tokio-rs/tokio): Multiple testing strategies

### Test-Driven Development (TDD)

**The cycle:**
1. **Red**: Write a failing test first
2. **Green**: Write minimum code to pass
3. **Refactor**: Improve code while tests stay green
4. Repeat

**Benefits:**
- Better API design (think about usage first)
- Higher confidence (tests written upfront)
- Living documentation (tests show how to use code)
- Prevents over-engineering

### Basic Test Structure

```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_addition() {
        assert_eq!(2 + 2, 4);
    }

    #[test]
    fn test_function() {
        let result = my_function();
        assert!(result.is_ok());
    }
}
```

**Key components:**
- `#[cfg(test)]` - only compiles when testing
- `#[test]` - marks function as a test
- Assertion macros verify behavior

### Assertion Macros

**Built-in macros:**
- [`assert!`](https://doc.rust-lang.org/std/macro.assert.html) - boolean condition
- [`assert_eq!`](https://doc.rust-lang.org/std/macro.assert_eq.html) - equality
- [`assert_ne!`](https://doc.rust-lang.org/std/macro.assert_ne.html) - inequality

**Custom messages:**
```rust
assert_eq!(x, 5, "x should be 5, but was {}", x);
```

### Testing Error Cases

**Test panics:**
```rust
#[test]
#[should_panic(expected = "Division by zero")]
fn test_divide_by_zero() {
    divide(10.0, 0.0).unwrap();
}
```

**Test Result errors:**
```rust
#[test]
fn test_error_case() {
    let result = function_that_fails();
    assert!(result.is_err());
}
```

### Running Tests

```bash
# Run all tests
cargo test

# Run specific test
cargo test test_name

# Show output
cargo test -- --nocapture

# Run sequentially
cargo test -- --test-threads=1
```

### Test Organization

**Unit tests** (same file):
- Test individual functions
- Can access private items
- In `#[cfg(test)]` module

**Integration tests** (`tests/` directory):
- Test public API
- Each file is separate crate
- Test how pieces work together

**Documentation tests:**
- Code examples in `///` comments
- Automatically tested
- Keep docs current

### Testing Best Practices

**Good tests are:**
1. **Fast** - run quickly
2. **Independent** - no dependencies between tests
3. **Repeatable** - deterministic results
4. **Self-validating** - clear pass/fail
5. **Thorough** - cover edge cases

**AAA pattern:**
- **Arrange** - set up test data
- **Act** - execute code
- **Assert** - verify results

---

## Part 2: Error Handling in Rust

### Recoverable vs Unrecoverable Errors

**Unrecoverable** (`panic!`):
- Serious problems with no recovery
- Array out of bounds
- Assertion failures
- Immediately stops program

**Recoverable** ([`Result<T, E>`](https://doc.rust-lang.org/std/result/)):
- Expected issues (file not found, parse errors)
- Returns `Ok(T)` on success
- Returns `Err(E)` on failure

### The Result and Option Enums

**Option<T>** - value or nothing:
```rust
enum Option<T> {
    Some(T),
    None,
}
```

**Result<T, E>** - success or failure:
```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

**Usage:**
```rust
fn divide(a: f64, b: f64) -> Result<f64, String> {
    if b == 0.0 {
        Err(String::from("Division by zero"))
    } else {
        Ok(a / b)
    }
}
```

### The `?` Operator

**Shortcut for error propagation:**

```rust
// Without ?
fn read_file() -> Result<String, io::Error> {
    let mut file = match File::open("data.txt") {
        Ok(f) => f,
        Err(e) => return Err(e),
    };
    // ... more code
}

// With ?
fn read_file() -> Result<String, io::Error> {
    let mut file = File::open("data.txt")?;
    // ... more code
}
```

**How it works:**
- If `Ok`, unwraps value and continues
- If `Err`, returns error immediately
- Only works in functions returning `Result` or `Option`

### Error Handling Patterns

**Pattern matching:**
```rust
match File::open("config.txt") {
    Ok(file) => process(file),
    Err(error) => match error.kind() {
        ErrorKind::NotFound => create_default(),
        other => panic!("Error: {:?}", other),
    },
}
```

**Unwrapping:**
```rust
// Panic on error
let file = File::open("data.txt").unwrap();

// Better message
let file = File::open("data.txt")
    .expect("Failed to open data.txt");
```

**With defaults:**
```rust
let config = read_config().unwrap_or_default();
let port = env::var("PORT").unwrap_or(String::from("8080"));
```

---

## Part 3: Building CLI Applications

### Reading Command-Line Arguments

```rust
use std::env;

fn main() {
    let args: Vec<String> = env::args().collect();

    if args.len() < 3 {
        eprintln!("Usage: {} <query> <filename>", args[0]);
        std::process::exit(1);
    }

    let query = &args[1];
    let filename = &args[2];
}
```

**Note**: `args[0]` is always the program name

### Reading Files

**Simple approach:**
```rust
use std::fs;

fn read_file(filename: &str) -> Result<String, std::io::Error> {
    fs::read_to_string(filename)
}
```

**Processing lines:**
```rust
fn search<'a>(query: &str, contents: &'a str) -> Vec<&'a str> {
    contents
        .lines()
        .filter(|line| line.contains(query))
        .collect()
}
```

### Using External Crates

**Add to Cargo.toml:**
```toml
[dependencies]
clap = { version = "4.0", features = ["derive"] }
```

**Use in code:**
```rust
use clap::Parser;

#[derive(Parser)]
struct Args {
    query: String,
    filename: String,
}

fn main() {
    let args = Args::parse();
}
```

---

## Part 4: Packaging with Cargo

### Cargo.toml Configuration

**Basic package info:**
```toml
[package]
name = "myapp"
version = "0.1.0"
edition = "2021"
authors = ["Your Name <you@example.com>"]
description = "A CLI application"
license = "MIT OR Apache-2.0"

[[bin]]
name = "myapp"
path = "src/main.rs"

[dependencies]
clap = "4.0"

[profile.release]
opt-level = 3
lto = true
```

### Building and Installing

**Build commands:**
```bash
# Development (fast compile, debug symbols)
cargo build

# Release (optimized, slower compile)
cargo build --release

# Install locally
cargo install --path .

# Run without installing
cargo run -- arg1 arg2
```

**Binary locations:**
- Development: `target/debug/myapp`
- Release: `target/release/myapp`
- Installed: `~/.cargo/bin/myapp`

### Release Optimization

**Profile settings:**
- `opt-level = 3` - maximum optimization
- `lto = true` - link-time optimization
- `codegen-units = 1` - better optimization (slower compile)

**Release builds are 10-100x faster than debug builds!**

---

## Part 5: Real-World Examples

### Professional CLI Tools in Rust

**[ripgrep](https://github.com/BurntSushi/ripgrep)** (`rg`):
- Grep alternative, 10-100x faster
- 40,000+ lines of Rust
- Used by millions

**[bat](https://github.com/sharkdp/bat)**:
- Cat with syntax highlighting
- Git integration
- Beautiful output

**[fd](https://github.com/sharkdp/fd)**:
- User-friendly find replacement
- Fast and intuitive

**[exa](https://github.com/ogham/exa)** / **[eza](https://github.com/eza-community/eza)**:
- Modern ls replacement
- Colorful, informative

---

## Part 6: Working with AI

### Effective AI Prompts

**Testing:**
- "What tests should I write for this function?"
- "Help me write a test suite for error handling"
- "Generate edge case tests for string parsing"

**Error handling:**
- "How should I handle file not found errors?"
- "When should I use Result vs Option?"
- "Convert these panics to Result-based errors"

**CLI development:**
- "How do I parse command-line arguments in Rust?"
- "What's the best crate for CLI apps?"
- "Help me add progress bars to my tool"

**Packaging:**
- "How do I optimize my Cargo.toml for release?"
- "What metadata should I include?"
- "How do I cross-compile for different platforms?"

---

## Part 7: Career Relevance

### Why These Skills Matter

**Testing:**
- Expected in all professional roles
- Common interview topic
- Demonstrates code quality awareness

**Error handling:**
- Production code must handle failures gracefully
- Shows maturity as developer
- Interview questions about error strategies

**CLI tools:**
- Common entry point for Rust projects
- Great for portfolio projects
- Demonstrates end-to-end skills

### Interview Preparation

**Common questions:**
- "Explain Result vs exceptions"
- "How would you test this error handling code?"
- "Walk me through packaging a Rust application"
- "What's your testing strategy?"

---

## Part 8: Key Takeaways

### Testing

**Core concepts:**
- Built into Cargo with `cargo test`
- TDD improves design
- Unit tests vs integration tests
- Documentation tests keep examples current

**Best practices:**
- Test behavior, not implementation
- Cover edge cases
- Keep tests fast and independent
- Use descriptive test names

### Error Handling

**Core concepts:**
- `Result<T, E>` for recoverable errors
- `Option<T>` prevents null pointer errors
- `?` operator for clean propagation
- Pattern matching for control

**When to use:**
- `Result` when operation can fail
- `Option` when value might not exist
- `panic!` only for unrecoverable errors

### Packaging

**Core concepts:**
- Cargo.toml configures package
- `cargo build --release` for production
- External crates from crates.io
- `cargo install` for distribution

**Best practices:**
- Optimize release builds
- Include metadata
- Document dependencies
- Version appropriately

---

## Part 9: Application to Final Projects

### Apply These Concepts

**For your final project:**

1. **Testing:**
   - Write tests for core functionality
   - Use TDD where appropriate
   - Include both unit and integration tests
   - Test error cases thoroughly

2. **Error Handling:**
   - Use `Result` for operations that can fail
   - Provide helpful error messages
   - Handle errors gracefully
   - Document error cases

3. **Packaging:**
   - Configure Cargo.toml properly
   - Build release binaries
   - Make it installable
   - Include documentation

4. **CLI Design:**
   - Clear command-line interface
   - Helpful error messages
   - Process files or data
   - Professional output

### Making It Portfolio-Worthy

**Professional touches:**
- Comprehensive test coverage
- Clean error handling
- Easy installation
- Good documentation
- Real-world utility

---

## Additional Resources

**Official documentation:**
- [The Rust Book - Chapter 11: Testing](https://doc.rust-lang.org/book/ch11-00-testing.html)
- [The Rust Book - Chapter 9: Error Handling](https://doc.rust-lang.org/book/ch09-00-error-handling.html)
- [The Rust Book - Chapter 12: CLI Program](https://doc.rust-lang.org/book/ch12-00-an-io-project.html)
- [The Cargo Book](https://doc.rust-lang.org/cargo/)

**Useful crates:**
- [clap](https://docs.rs/clap/) - CLI argument parsing
- [anyhow](https://docs.rs/anyhow/) - Flexible error handling
- [thiserror](https://docs.rs/thiserror/) - Custom error types

**Tools:**
- [cargo-tarpaulin](https://crates.io/crates/cargo-tarpaulin) - Code coverage
- [cargo-watch](https://crates.io/crates/cargo-watch) - Auto-run tests

---

## Next Week Preview

**Week 14: Publishing and Distribution**

Topics:
- Semantic versioning
- Publishing to crates.io
- GitHub releases and tags
- Cross-platform builds
- Package manager distribution

**Goal**: Complete the development lifecycle from code to published packages

---

**Focus on your final projects this week!** Apply testing, error handling, and packaging concepts to make your project professional and portfolio-worthy.
