# Lab 10: mastering ownership and borrowing

**Due:** Sunday, November 9 at 11:59 PM
**Points:** 10

## Objective

The goal of this lab is to build hands-on mastery of [Rust](https://www.rust-lang.org/)'s revolutionary [ownership system](https://doc.rust-lang.org/book/ch04-00-understanding-ownership.html) and [borrowing rules](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html). Through deliberate practice fixing ownership violations and implementing correct borrowing patterns, you'll develop the foundational skill that makes Rust unique: writing memory-safe code verified at compile time. This lab emphasizes learning to read and interpret [compiler error messages](https://doc.rust-lang.org/error_codes/error-index.html), leveraging [AI assistance](https://claude.ai/) to deepen understanding, and applying the fix-compile-test cycle that defines professional [Rust](https://www.rust-lang.org/) development.

---

## Background

### Why Ownership Matters

[Rust](https://www.rust-lang.org/)'s [ownership system](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html) solves one of the hardest problems in systems programming: **memory safety without garbage collection**. According to [Microsoft Security Response Center](https://msrc.microsoft.com/blog/2019/07/a-proactive-approach-to-more-secure-code/), approximately **70% of security vulnerabilities** in [Microsoft](https://www.microsoft.com/) and [Google](https://www.google.com/) products are memory safety issues - use-after-free, double-free, buffer overflows, and data races. These bugs simply **cannot exist** in safe [Rust](https://www.rust-lang.org/) code because the [borrow checker](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html#the-rules-of-references) catches them at compile time.

### The Three Ownership Rules

Every [Rust](https://www.rust-lang.org/) programmer must internalize these three rules, enforced by the compiler:

1. **Each value has one owner** - Every piece of data has exactly one variable responsible for it
2. **Only one owner at a time** - When ownership transfers (moves), the old variable becomes invalid
3. **Drop when out of scope** - When the owner goes out of [scope](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html#variable-scope), [Rust automatically calls `drop()`](https://doc.rust-lang.org/std/ops/trait.Drop.html) to free memory

### The Borrowing Rules

[References](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html) (borrowing) let you use data without taking ownership:

1. **At any time, you can have EITHER:**
   - One [mutable reference](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html#mutable-references) (`&mut T`)
   - OR any number of [immutable references](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html) (`&T`)

2. **References must always be valid** - No [dangling references](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html#dangling-references) pointing to freed memory

These rules prevent [data races](https://doc.rust-lang.org/nomicon/races.html) - one of the most insidious bugs in concurrent programming.

### Real-World Impact

Companies choose [Rust](https://www.rust-lang.org/) specifically for ownership and memory safety:

- **[Discord](https://discord.com/blog/why-discord-is-switching-from-go-to-rust)** - Reduced latency spikes from seconds to milliseconds (10x improvement)
- **[Microsoft](https://msrc.microsoft.com/blog/2019/07/a-proactive-approach-to-more-secure-code/)** - Eliminating 70% of CVEs by using Rust in [Windows](https://www.microsoft.com/en-us/windows)
- **[Dropbox](https://dropbox.tech/infrastructure/rewriting-the-heart-of-our-sync-engine)** - 2x memory reduction in sync engine rewrite
- **[npm](https://www.rust-lang.org/static/pdfs/Rust-npm-Whitepaper.pdf)** - 10x performance improvement rewriting services

This isn't academic theory - this is production-proven technology.

---

## Prerequisites

Before starting this lab, ensure you have:

- [Rust toolchain installed](https://www.rust-lang.org/tools/install) (`rustc`, [`cargo`](https://doc.rust-lang.org/cargo/), [`rustup`](https://rust-lang.github.io/rustup/))
- Completed [Lab 09](../lab09/README.md) (Introduction to Rust basics)
- Reviewed [Week 10 slides](../../resources/lecture-notes/) on ownership and borrowing
- Access to [Rust Playground](https://play.rust-lang.org/) for experimentation

**Installation troubleshooting:** If you encounter Rust installation issues, consult the [SETUP_GUIDE.md](../../resources/SETUP_GUIDE.md) for platform-specific instructions.

**Verifying your installation:**
```bash
rustc --version  # Should show 1.70 or later
cargo --version  # Should show 1.70 or later
```

---

## Part 1: The Borrow Checker Game

### Concept

The [borrow checker](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html#the-rules-of-references) is the part of the [Rust compiler](https://doc.rust-lang.org/rustc/what-is-rustc.html) that enforces ownership and borrowing rules. Learning to work **with** the borrow checker - not against it - is the most important skill for any [Rust](https://www.rust-lang.org/) developer. In this section, you'll fix intentional ownership violations, learning to interpret [error messages](https://doc.rust-lang.org/error_codes/error-index.html) and apply correct solutions.

### Instructions

1. **Create the project:**
   ```bash
   cd is4010-labs
   cargo new lab10 --bin
   cd lab10
   ```

2. **Replace `src/main.rs` with the starter code below** (includes 7 progressively challenging problems)

3. **Fix problems one at a time:**
   - Uncomment one `problem_X()` call in `main()`
   - Run [`cargo run`](https://doc.rust-lang.org/cargo/commands/cargo-run.html)
   - **Read the compiler error message carefully** - Rust's errors are exceptionally helpful!
   - Fix the function(s) to make the code compile and run correctly
   - Move to the next problem

4. **Test your solutions:**
   ```bash
   cargo test
   ```
   All tests must pass before submission.

5. **Verify with GitHub Actions:**
   - Push your code to [GitHub](https://github.com/)
   - Check that [GitHub Actions CI/CD pipeline](https://docs.github.com/en/actions) passes

---

### Starter Code for Part 1

Copy this entire code block into `lab10/src/main.rs`:

```rust
// Lab 10: The Borrow Checker Game
// Fix each problem one at a time by uncommenting the function call in main()

fn main() {
    println!("Lab 10: Mastering Ownership and Borrowing");
    println!("Uncomment one problem at a time and fix it!\n");

    // Uncomment problems one at a time:
    // problem_1();
    // problem_2();
    // problem_3();
    // problem_4();
    // problem_5();
    // problem_6();
    // problem_7();
}

// ============================================================================
// PROBLEM 1: Value used after move
// ============================================================================
// Error: This function tries to use a value after ownership has moved.
// Fix: Change calculate_length to borrow instead of taking ownership.
//
// Learning goal: Understand move semantics and when to use references
// ============================================================================
/*
fn problem_1() {
    println!("Problem 1: Value used after move");
    let s1 = String::from("hello");
    let (s2, len) = calculate_length(s1);
    println!("  The length of '{}' is {}.", s2, len);
}

fn calculate_length(s: String) -> (String, usize) {
    let length = s.len();
    (s, length)
}
*/

// ============================================================================
// PROBLEM 2: Immutable and mutable borrow conflict
// ============================================================================
// Error: Tries to create a mutable borrow while an immutable borrow exists.
// Fix: Ensure immutable borrows are no longer used before creating mutable borrow.
//
// Learning goal: Understand the "one mutable OR many immutable" rule
// ============================================================================
/*
fn problem_2() {
    println!("Problem 2: Mutable and immutable borrow conflict");
    let mut s = String::from("hello");
    let r1 = &s;      // Immutable borrow
    let r2 = &mut s;  // Mutable borrow - ERROR!
    println!("  {}, {}", r1, r2);
}
*/

// ============================================================================
// PROBLEM 3: Mutating through immutable reference
// ============================================================================
// Error: Tries to mutate a value through an immutable reference.
// Fix: Change both the variable declaration and function signature to accept &mut.
//
// Learning goal: Know when to use &T vs &mut T
// ============================================================================
/*
fn problem_3() {
    println!("Problem 3: Mutating through immutable reference");
    let s = String::from("hello");
    add_to_string(&s);
    println!("  Result: {}", s);
}

fn add_to_string(s: &String) {
    s.push_str(", world");
}
*/

// ============================================================================
// PROBLEM 4: Multiple mutable borrows
// ============================================================================
// Error: Creates two mutable references to the same data simultaneously.
// Fix: Use scopes to limit the lifetime of the first mutable borrow.
//
// Learning goal: Control borrow lifetimes with scopes
// ============================================================================
/*
fn problem_4() {
    println!("Problem 4: Multiple mutable borrows");
    let mut s = String::from("hello");

    let r1 = &mut s;
    let r2 = &mut s;  // ERROR: can't have two mutable borrows!

    println!("  {}, {}", r1, r2);
}
*/

// ============================================================================
// PROBLEM 5: Dangling reference
// ============================================================================
// Error: Returns a reference to data that will be dropped.
// Fix: Return the owned String instead of a reference.
//
// Learning goal: Prevent use-after-free bugs
// ============================================================================
/*
fn problem_5() {
    println!("Problem 5: Dangling reference");
    let r = create_string();
    println!("  Got: {}", r);
}

fn create_string() -> &String {
    let s = String::from("hello");
    &s  // ERROR: returning reference to local variable
}
*/

// ============================================================================
// PROBLEM 6: Ownership in loops
// ============================================================================
// Error: Tries to move a value multiple times in a loop.
// Fix: Clone the value in each iteration, or use a reference instead.
//
// Learning goal: Understand ownership with iteration
// ============================================================================
/*
fn problem_6() {
    println!("Problem 6: Ownership in loops");
    let data = String::from("Rust");

    for i in 0..3 {
        print_with_number(data, i);  // ERROR: moves data on first iteration
    }
}

fn print_with_number(s: String, n: i32) {
    println!("  {}: {}", n, s);
}
*/

// ============================================================================
// PROBLEM 7: Lifetime extension challenge
// ============================================================================
// Error: Reference doesn't live long enough.
// Fix: Restructure so the String lives long enough for the reference.
//
// Learning goal: Understand scope and lifetime relationships
// ============================================================================
/*
fn problem_7() {
    println!("Problem 7: Lifetime extension");
    let result;
    {
        let s = String::from("inner scope");
        result = &s;  // ERROR: s will be dropped at end of scope
    }
    println!("  Result: {}", result);
}
*/

// ============================================================================
// TEST SUITE
// ============================================================================
// These tests verify your fixes are correct.
// Run with: cargo test
// ============================================================================

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_calculate_length_borrows() {
        let s = String::from("testing");
        let (_s_ref, len) = calculate_length(&s);
        assert_eq!(len, 7);
        // s should still be valid here
        assert_eq!(s, "testing");
    }

    #[test]
    fn test_add_to_string_mutates() {
        let mut s = String::from("hello");
        add_to_string(&mut s);
        assert_eq!(s, "hello, world");
    }

    #[test]
    fn test_create_string_returns_owned() {
        let result = create_string();
        assert_eq!(result, "hello");
    }

    #[test]
    fn test_print_with_number_borrows() {
        let data = String::from("Rust");
        // Should work when passed as a reference
        for i in 0..3 {
            print_with_number(&data, i);
        }
        // data should still be valid
        assert_eq!(data, "Rust");
    }
}
```

---

## Part 2: Ownership Implementation Exercises

### Concept

Now that you've learned to **fix** ownership errors, it's time to **write correct code from scratch**. These exercises require you to implement functions that properly handle ownership and borrowing from the beginning.

### Instructions

1. **Continue in the same `lab10` project**

2. **Add the following exercises to your `src/main.rs`** (after the problem functions, before the test module)

3. **Implement each function** according to its specification

4. **Test your implementations:**
   ```bash
   cargo test
   ```

### Implementation Exercises

Add this code to your `src/main.rs`:

```rust
// ============================================================================
// IMPLEMENTATION EXERCISES
// Write these functions from scratch with correct ownership/borrowing
// ============================================================================

/// Takes ownership of a String, converts it to uppercase, and returns it.
/// This demonstrates the "consume and return" pattern.
///
/// # Arguments
/// * `s` - String to convert (ownership transferred)
///
/// # Returns
/// * New String with all characters in uppercase
fn to_uppercase_owned(s: String) -> String {
    // TODO: Implement this
    // Hint: Use .to_uppercase() method
    unimplemented!()
}

/// Borrows a String immutably and returns its length.
/// This demonstrates read-only borrowing.
///
/// # Arguments
/// * `s` - Reference to String to measure
///
/// # Returns
/// * Length of the string
fn string_length(s: &String) -> usize {
    // TODO: Implement this
    unimplemented!()
}

/// Borrows a String mutably and appends a suffix to it.
/// This demonstrates in-place modification through mutable borrowing.
///
/// # Arguments
/// * `s` - Mutable reference to String to modify
/// * `suffix` - String slice to append
fn append_suffix(s: &mut String, suffix: &str) {
    // TODO: Implement this
    // Hint: Use .push_str() method
    unimplemented!()
}

/// Creates a new String by concatenating two borrowed strings.
/// This demonstrates creating owned data from borrowed data.
///
/// # Arguments
/// * `s1` - First string slice
/// * `s2` - Second string slice
///
/// # Returns
/// * New String containing s1 + s2
fn concat_strings(s1: &str, s2: &str) -> String {
    // TODO: Implement this
    // Hint: format!() macro or String::from() + push_str()
    unimplemented!()
}

/// Finds the first word in a string and returns it as a string slice.
/// This demonstrates returning borrowed data with implicit lifetimes.
///
/// # Arguments
/// * `s` - String slice to search
///
/// # Returns
/// * String slice containing the first word (up to first space),
///   or the entire string if no space is found
fn first_word(s: &str) -> &str {
    // TODO: Implement this
    // Hint: Use .find(' ') to locate the first space
    // Hint: Use &s[start..end] to create a slice
    unimplemented!()
}
```

---

## Expected Repository Structure

After completing this lab, your `is4010-labs` repository should have this cumulative structure from all previous labs:

```
is4010-labs/
├── .git/                          # Git repository metadata
├── .github/
│   └── workflows/
│       └── rust.yml               # GitHub Actions for Rust projects (from Lab 09)
├── lab01/                         # Git and GitHub basics
├── lab02/                         # AI code assistants
├── lab03/                         # Python fundamentals
├── lab04/                         # Data structures
├── lab05/                         # Functions and error handling
├── lab06/                         # Object-oriented programming
├── lab07/                         # Files and JSON
├── lab09/                         # Rust introduction
└── lab10/                         # ⭐ THIS LAB
    ├── Cargo.toml                 # Rust project configuration
    ├── Cargo.lock                 # Dependency lock file
    ├── src/
    │   └── main.rs                # Your implementation with all fixes and exercises
    └── target/                    # Build artifacts (not committed)
```

**Verification:** Before pushing to GitHub, ensure:
- ✅ All 7 borrow checker problems are fixed (uncommented and working)
- ✅ All 5 implementation exercises are complete
- ✅ [`cargo test`](https://doc.rust-lang.org/cargo/commands/cargo-test.html) passes all tests
- ✅ [`cargo clippy`](https://doc.rust-lang.org/clippy/) shows no warnings
- ✅ Code is formatted with [`cargo fmt`](https://github.com/rust-lang/rustfmt)

---

## Testing Your Code 🧪

### Local Testing

[Rust](https://www.rust-lang.org/) has an excellent built-in testing framework. Run tests frequently as you work:

```bash
# Run all tests
cargo test

# Run tests with output shown
cargo test -- --nocapture

# Run a specific test
cargo test test_calculate_length_borrows

# Run tests and show which ones passed
cargo test -- --test-threads=1 --nocapture
```

**Understanding test output:**
- ✅ **Green "ok"** - Test passed
- ❌ **Red "FAILED"** - Test failed (read the assertion error carefully)
- **Compilation errors** - Fix syntax/borrow checker errors before tests can run

### Code Quality Checks

Before pushing to [GitHub](https://github.com/), run these professional quality checks:

```bash
# Check for common mistakes and style issues
cargo clippy

# Auto-format your code to Rust standards
cargo fmt

# Verify code compiles without running
cargo check
```

**Pro tip:** Set up your editor ([VS Code](https://code.visualstudio.com/)) with [rust-analyzer](https://rust-analyzer.github.io/) for real-time error checking and formatting on save!

### GitHub Actions CI/CD

When you push to [GitHub](https://github.com/), [GitHub Actions](https://docs.github.com/en/actions) will automatically:
1. Build your code with [`cargo build`](https://doc.rust-lang.org/cargo/commands/cargo-build.html)
2. Run tests with [`cargo test`](https://doc.rust-lang.org/cargo/commands/cargo-test.html)
3. Check code style with [`cargo clippy`](https://doc.rust-lang.org/clippy/) and [`cargo fmt`](https://github.com/rust-lang/rustfmt)

**Check your results:**
1. Go to your repository on [GitHub](https://github.com/)
2. Click the "Actions" tab
3. Find your latest push
4. ✅ Green checkmark = all tests passed!
5. ❌ Red X = something failed (click to see details)

---

## Comprehensive Troubleshooting Guide 🔧

### Problem 1: "value borrowed after move"

**Error message:**
```
error[E0382]: borrow of moved value: `s`
```

**What this means:** You tried to use a variable after ownership transferred to another variable or function.

**Solutions:**
1. **Use a reference instead of moving:**
   ```rust
   // Instead of:
   let s2 = s1;  // Moves ownership

   // Do:
   let s2 = &s1;  // Borrows
   ```

2. **Clone the data if you need two owners:**
   ```rust
   let s2 = s1.clone();  // Both s1 and s2 are valid
   ```

3. **Return ownership from the function:**
   ```rust
   fn process(s: String) -> String {
       // Do work
       s  // Return ownership
   }
   ```

**🤖 AI prompt:** *"Explain this Rust error: value borrowed after move. Show me three ways to fix it."*

---

### Problem 2: "cannot borrow as mutable more than once"

**Error message:**
```
error[E0499]: cannot borrow `s` as mutable more than once at a time
```

**What this means:** You tried to create two mutable references to the same data.

**Solutions:**
1. **Use scopes to separate borrows:**
   ```rust
   {
       let r1 = &mut s;
       // use r1
   }  // r1 goes out of scope

   let r2 = &mut s;  // Now OK
   ```

2. **Use only one mutable reference:**
   ```rust
   let r = &mut s;
   // Use r for everything
   ```

**🤖 AI prompt:** *"Why can't I have two mutable references in Rust? Explain the rule and show me how to fix my code: [paste code]"*

---

### Problem 3: "cannot borrow as mutable because also borrowed as immutable"

**Error message:**
```
error[E0502]: cannot borrow `s` as mutable because it is also borrowed as immutable
```

**What this means:** You tried to modify data while immutable references exist.

**Solutions:**
1. **Ensure immutable borrows are done before mutable borrow:**
   ```rust
   let r1 = &s;
   println!("{}", r1);  // Last use of r1
   // r1 scope ends here (Non-Lexical Lifetimes)

   let r2 = &mut s;  // Now OK
   ```

2. **Don't mix immutable and mutable references:**
   ```rust
   // Use immutable references first, then mutable
   ```

**🤖 AI prompt:** *"Help me fix this Rust borrow checker error: cannot borrow as mutable because also borrowed as immutable [paste code]"*

**Additional resource:** [Understanding Non-Lexical Lifetimes](https://doc.rust-lang.org/edition-guide/rust-2018/ownership-and-lifetimes/non-lexical-lifetimes.html)

---

### Problem 4: "this function's return type contains a borrowed value"

**Error message:**
```
error[E0106]: missing lifetime specifier
```

**What this means:** The compiler doesn't know how long the returned reference will be valid.

**Solutions:**
1. **Return an owned value instead:**
   ```rust
   fn create() -> String {  // Own it
       String::from("hello")
   }
   ```

2. **Add lifetime annotations (advanced):**
   ```rust
   fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
       if x.len() > y.len() { x } else { y }
   }
   ```

**🤖 AI prompt:** *"When should I return String vs &str in Rust? Explain lifetime annotations."*

---

### Problem 5: Cargo/Rust installation issues

**Windows-specific issues:**

If `cargo` command not found:
1. Install Rust via [rustup](https://rustup.rs/)
2. Restart your terminal (or reboot)
3. Verify: `rustc --version`

If you get "linker not found" error:
1. Install [Visual Studio Build Tools](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2022)
2. Select "Desktop development with C++"
3. Restart terminal

**macOS-specific issues:**

If you get compiler errors about missing tools:
```bash
xcode-select --install
```

**Linux-specific issues:**

If you get linker errors:
```bash
# Ubuntu/Debian
sudo apt-get install build-essential

# Fedora
sudo dnf install gcc
```

**All platforms:** See [SETUP_GUIDE.md](../../resources/SETUP_GUIDE.md) for comprehensive installation instructions.

---

### Problem 6: Tests failing but code compiles

**Symptoms:** `cargo test` shows failures even though `cargo run` works.

**Solutions:**
1. **Read the test assertion error carefully:**
   ```
   assertion failed: `(left == right)`
     left: `"hello"`
    right: `"hello, world"`
   ```

2. **Check function signatures match test expectations:**
   ```rust
   // Test expects:
   fn calculate_length(s: &String) -> usize

   // Not:
   fn calculate_length(s: String) -> usize
   ```

3. **Ensure you've implemented all required functions:**
   ```bash
   cargo test -- --nocapture
   ```
   Shows which functions are unimplemented.

**🤖 AI prompt:** *"My Rust tests are failing with this error: [paste error]. What does it mean and how do I fix it?"*

---

### Problem 7: "cannot move out of `*s` which is behind a shared reference"

**Error message:**
```
error[E0507]: cannot move out of `*s` which is behind a shared reference
```

**What this means:** You tried to move ownership of data that was only borrowed.

**Solutions:**
1. **Clone the data instead:**
   ```rust
   fn process(s: &String) -> String {
       s.clone()  // Create owned copy
   }
   ```

2. **Change to take ownership:**
   ```rust
   fn process(s: String) -> String {
       s  // Already owned
   }
   ```

**🤖 AI prompt:** *"Explain 'cannot move out of behind a reference' error in Rust and show me solutions"*

---

### Problem 8: String vs &str confusion

**Symptoms:** Type mismatch errors between `String` and `&str`.

**Understanding:**
- [`String`](https://doc.rust-lang.org/std/string/struct.String.html) - Owned, heap-allocated, growable
- [`&str`](https://doc.rust-lang.org/std/primitive.str.html) - Borrowed, immutable string slice

**Conversions:**
```rust
// &str → String
let s: String = my_str.to_string();
let s: String = String::from(my_str);

// String → &str
let slice: &str = &my_string;
let slice: &str = my_string.as_str();

// String literal → &str (automatic)
let s: &str = "hello";
```

**🤖 AI prompt:** *"Explain the difference between String and &str in Rust. When should I use each?"*

**Additional resource:** [Rust String Documentation](https://doc.rust-lang.org/std/string/struct.String.html)

---

### Problem 9: GitHub Actions failing

**Symptoms:** Tests pass locally but fail in GitHub Actions.

**Solutions:**
1. **Ensure all code is committed:**
   ```bash
   git status
   git add .
   git commit -m "Fix remaining issues"
   git push
   ```

2. **Check the Actions log:**
   - Go to GitHub repository → "Actions" tab
   - Click the failed workflow
   - Read the error output (same as local `cargo test`)

3. **Test the same commands locally:**
   ```bash
   cargo test
   cargo clippy
   cargo fmt --check
   ```

**🤖 AI prompt:** *"My GitHub Actions CI is failing with this error: [paste error from Actions]. What does it mean?"*

---

### Problem 10: "unresolved import" or "cannot find function"

**Symptoms:**
```
error[E0433]: failed to resolve: use of undeclared crate or module
```

**Solutions:**
1. **Check function names match exactly:**
   ```rust
   // If test calls calculate_length, your function must be named exactly that
   fn calculate_length(...) { ... }
   ```

2. **Ensure functions are not commented out:**
   ```rust
   // This won't work - still commented!
   /* fn problem_1() { ... } */

   // This works:
   fn problem_1() { ... }
   ```

3. **Verify test module can see functions:**
   ```rust
   // Add pub if tests are in separate module
   pub fn my_function() { ... }
   ```

---

## AI Integration Strategy 🤖

### The Learning-First Approach

**DO:**
1. ✅ Read the compiler error message first (Rust's are excellent!)
2. ✅ Try to understand what rule is being violated
3. ✅ Use AI to explain WHY that rule exists
4. ✅ Ask AI for the idiomatic solution
5. ✅ Understand the fix before applying it

**DON'T:**
1. ❌ Copy-paste AI solutions without understanding
2. ❌ Skip reading compiler errors
3. ❌ Ask AI before attempting the problem yourself
4. ❌ Use AI as a crutch instead of learning the concepts

### Effective AI Prompts for Ownership

**Understanding errors:**
- *"Explain this Rust ownership error in simple terms: [paste full error message]"*
- *"Why does Rust move String but copy i32? Explain with examples."*
- *"What's happening in this code that violates the borrow checker? [paste code]"*

**Learning concepts:**
- *"Explain Rust's ownership rules like I'm coming from Python"*
- *"When should I use &T vs &mut T vs T in function parameters?"*
- *"What's the difference between clone() and borrowing? When should I use each?"*
- *"Explain lifetimes in Rust with a simple example"*

**Debugging specific code:**
- *"Help me fix this borrow checker error: [paste error and code]"*
- *"Why can't I borrow this as mutable? [paste code]"*
- *"How do I restructure this code to satisfy the borrow checker? [paste code]"*

**Exploring solutions:**
- *"Show me three ways to fix 'value used after move' error"*
- *"What's the idiomatic Rust way to [describe your goal]?"*
- *"Is this the best way to handle ownership here? [paste code]"*

### Real AI Conversation Examples

**Example 1: Understanding a move error**

```
You: "I get this error: 'value borrowed after move'. Here's my code:
let s1 = String::from("hello");
let s2 = s1;
println!("{}", s1);
What's wrong?"

AI: "The issue is ownership transfer. When you write `let s2 = s1`,
ownership of the String moves from s1 to s2. s1 is no longer valid.

Three solutions:
1. Clone: let s2 = s1.clone();
2. Borrow: let s2 = &s1;
3. Don't use s1 after: just use s2

Which approach depends on your goal. If you just need to read the value,
use borrowing (&s1). If you need two independent copies, use clone()."

You: "Why doesn't i32 have this problem?"

AI: "Great question! i32 implements the Copy trait because it's stored
entirely on the stack (no heap allocation). Copying a few bytes is cheap,
so Rust copies instead of moves. String stores data on the heap, so
copying would be expensive. Rust makes you explicit about that cost with
clone()."
```

**Example 2: Fixing a borrow checker conflict**

```
You: "How do I fix this?
let mut s = String::from("hello");
let r1 = &s;
let r2 = &mut s;  // ERROR
println!("{}, {}", r1, r2);"

AI: "You can't have immutable and mutable borrows simultaneously. Rust
enforces this to prevent data races.

Fix using Non-Lexical Lifetimes:
let mut s = String::from("hello");
let r1 = &s;
println!("{}", r1);  // r1's last use - scope ends here
let r2 = &mut s;     // Now OK - no immutable borrows active
println!("{}", r2);

The key insight: r1's scope ends at its last use, not the closing brace.
So move r2's creation after r1 is done being used."

You: "Why does Rust have this rule?"

AI: "It prevents 'reading while writing' bugs. Imagine r1 is iterating
over data while r2 is modifying it - that's undefined behavior in C++,
a common source of crashes. Rust makes it impossible at compile time."
```

**Example 3: Lifetime annotations**

```
You: "Why does this need a lifetime annotation?
fn longest(x: &str, y: &str) -> &str {
    if x.len() > y.len() { x } else { y }
}"

AI: "The compiler doesn't know if the returned reference comes from x or y,
so it can't determine how long the return value is valid.

Add a lifetime parameter:
fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() { x } else { y }
}

This tells the compiler: 'the output lives as long as the shortest input'.
The 'a is just a label - you're describing the relationship so the
borrow checker can verify safety."

You: "Do I always need to annotate lifetimes?"

AI: "No! The compiler uses lifetime elision rules to infer them in most
cases. You typically only need explicit annotations when:
1. Function returns a reference from multiple inputs
2. Structs contain references
3. Complex reference relationships

In most Rust code, lifetimes are inferred automatically."
```

---

## Professional Submission Workflow

### Step 1: Final Code Quality Checks

Before committing, ensure your code meets professional standards:

```bash
# Navigate to your lab
cd lab10

# Run all tests
cargo test

# Check for common mistakes and style violations
cargo clippy

# Auto-format code to Rust community standards
cargo fmt

# Verify everything compiles
cargo check
```

**All four commands should complete without errors or warnings.**

---

### Step 2: Commit and Push

```bash
# Navigate to repository root
cd ..  # Now in is4010-labs/

# Stage your lab
git add lab10/

# Check what's being committed
git status

# Create a descriptive commit message
git commit -m "Complete Lab 10: Ownership and borrowing mastery

- Fixed all 7 borrow checker problems
- Implemented all 5 ownership exercises
- All tests passing (cargo test)
- Code formatted and linted (cargo fmt, cargo clippy)"

# Push to GitHub
git push origin main
```

**Pro tip:** Use descriptive commit messages that explain **what** and **why**, not just "lab 10 done".

---

### Step 3: Verify GitHub Actions CI/CD

1. Go to your `is4010-labs` repository on [GitHub](https://github.com/)
2. Click the "**Actions**" tab
3. Find your latest commit
4. Wait for the workflow to complete (usually 1-2 minutes)
5. Verify **green checkmark** ✅
6. If **red X** ❌:
   - Click the failed workflow
   - Read the error log
   - Fix issues locally
   - Commit and push again

**Common CI failures:**
- Code doesn't compile
- Tests fail
- `cargo clippy` warnings
- Code not formatted with `cargo fmt`

---

### Step 4: Self-Check Completion Checklist

Before considering the lab complete, verify:

**Code Completeness:**
- [ ] All 7 borrow checker problems are fixed and uncommented
- [ ] All 5 implementation exercises are complete (no `unimplemented!()`)
- [ ] Functions have correct signatures matching test expectations
- [ ] Code compiles without errors: `cargo build --release`

**Testing:**
- [ ] All tests pass locally: `cargo test`
- [ ] No warnings from: `cargo clippy`
- [ ] Code formatted: `cargo fmt --check` (no output = formatted correctly)
- [ ] GitHub Actions CI passing (green checkmark)

**Git & GitHub:**
- [ ] Code committed with descriptive message
- [ ] Code pushed to `origin main`
- [ ] Repository contains `lab10/` folder with all required files
- [ ] No build artifacts committed (target/ is in .gitignore)

**Learning Verification:**
- [ ] Can explain each of the three ownership rules
- [ ] Can explain the two borrowing rules
- [ ] Understand when to use `&T` vs `&mut T` vs `T`
- [ ] Can read and interpret Rust compiler error messages
- [ ] Know how to use AI effectively to debug ownership issues

---

## Additional Resources

### Official Rust Documentation
- [The Rust Programming Language - Chapter 4: Understanding Ownership](https://doc.rust-lang.org/book/ch04-00-understanding-ownership.html) - **Essential reading**
- [The Rust Programming Language - Chapter 10.3: Lifetime Syntax](https://doc.rust-lang.org/book/ch10-03-lifetime-syntax.html)
- [Rust by Example - Ownership and Moves](https://doc.rust-lang.org/rust-by-example/scope/move.html)
- [Rust by Example - Borrowing](https://doc.rust-lang.org/rust-by-example/scope/borrow.html)
- [Rust Error Codes Index](https://doc.rust-lang.org/error_codes/error-index.html)
- [The Rustonomicon - Advanced Ownership](https://doc.rust-lang.org/nomicon/)

### Interactive Practice
- [Rust Playground](https://play.rust-lang.org/) - Experiment with code in your browser
- [Rustlings - Ownership Exercises](https://github.com/rust-lang/rustlings/tree/main/exercises/move_semantics)
- [Rust by Example - Interactive Code](https://doc.rust-lang.org/rust-by-example/)

### Articles and Blog Posts
- [Discord: Why We Switched from Go to Rust](https://discord.com/blog/why-discord-is-switching-from-go-to-rust) - Real-world performance wins
- [Microsoft: A Proactive Approach to More Secure Code](https://msrc.microsoft.com/blog/2019/07/a-proactive-approach-to-more-secure-code/) - 70% of CVEs are memory safety
- [Visualizing Memory Layout of Rust's Data Types](https://www.youtube.com/watch?v=rDoqT-a6UFg)
- [Understanding Ownership in Rust](https://blog.thoughtram.io/ownership-in-rust/)

### Community Support
- [r/rust](https://www.reddit.com/r/rust/) - Active Rust community
- [The Rust Programming Language Discord](https://discord.gg/rust-lang)
- [Rust Users Forum](https://users.rust-lang.org/)
- Course [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/group-chat-software) channel - **Ask questions anytime!**

---

## Looking Ahead: Week 11

Next week we build on ownership to create custom data types:
- Creating structured data with [`struct`](https://doc.rust-lang.org/book/ch05-00-structs.html)
- Modeling possibilities with [`enum`](https://doc.rust-lang.org/book/ch06-00-enums.html)
- Pattern matching with [`match`](https://doc.rust-lang.org/book/ch06-02-match.html)
- AI-assisted data modeling strategies

**The Foundation:** Everything in Rust builds on ownership. Mastering it this week makes everything else easier!

---

**Questions or stuck?** Reach out on [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/group-chat-software) - we're here to support your Rust learning journey!

**Remember:** Fighting the borrow checker is normal and valuable. The struggle teaches you to write better, safer code in every language. Embrace the learning process! 🦀
