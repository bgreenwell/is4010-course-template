# Lab 09: Rust basics

**Due:** Sunday, October 26 at 11:59 PM
**Points:** 10

## Objective

The goal of this lab is to take your first steps into [Rust programming](https://www.rust-lang.org/) by installing the [Rust toolchain](https://www.rust-lang.org/tools/install), creating your first [Cargo project](https://doc.rust-lang.org/cargo/), and writing basic Rust code with variables, functions, and tests. You'll practice Rust's syntax fundamentals and experience the power of the [Rust compiler](https://doc.rust-lang.org/rustc/what-is-rustc.html) catching bugs before you run your code. Your work will be verified automatically by our [CI/CD pipeline](https://docs.github.com/en/actions).

## Background

[Rust](https://doc.rust-lang.org/book/) is a modern systems programming language that combines the performance of [C](https://en.wikipedia.org/wiki/C_(programming_language)) and [C++](https://en.wikipedia.org/wiki/C%2B%2B) with memory safety guarantees that prevent entire categories of bugs. Unlike Python, which uses [garbage collection](https://en.wikipedia.org/wiki/Garbage_collection_(computer_science)) and runs in an interpreter, Rust achieves safety through its unique [ownership system](https://doc.rust-lang.org/book/ch04-00-understanding-ownership.html) and catches errors at [compile time](https://en.wikipedia.org/wiki/Compile_time).

**What you'll learn:**
- **Toolchain installation**: Setting up [rustup](https://rustup.rs/), [cargo](https://doc.rust-lang.org/cargo/), and the [Rust compiler](https://doc.rust-lang.org/rustc/)
- **Project structure**: Understanding [Cargo project layout](https://doc.rust-lang.org/cargo/guide/project-layout.html) and configuration
- **Variables and mutability**: Rust's [immutability-by-default](https://doc.rust-lang.org/book/ch03-01-variables-and-mutability.html) philosophy
- **Type system**: Working with [static types](https://doc.rust-lang.org/book/ch03-02-data-types.html) and type inference
- **Functions**: Writing [functions](https://doc.rust-lang.org/book/ch03-03-how-functions-work.html) with type annotations
- **Testing**: Using Rust's [built-in test framework](https://doc.rust-lang.org/book/ch11-00-testing.html)

**Key concepts applied:**
- [Variables and mutability](https://doc.rust-lang.org/book/ch03-01-variables-and-mutability.html)
- [Data types](https://doc.rust-lang.org/book/ch03-02-data-types.html) (integers, floats, booleans, characters)
- [Function definitions](https://doc.rust-lang.org/book/ch03-03-how-functions-work.html) with parameters and return types
- [Testing with `cargo test`](https://doc.rust-lang.org/book/ch11-01-writing-tests.html)

This lab is divided into five parts:
- **Part 0**: Experiment in the [Rust Playground](https://play.rust-lang.org/) (no installation needed)
- **Part 1**: Install the Rust toolchain and verify your setup
- **Part 2**: Create your first Cargo project and explore the structure
- **Part 3**: Write Rust functions and tests
- **Part 4**: Update GitHub Actions to auto-test Rust code

---

## Part 0: warm up in the Rust Playground

### The challenge

Before installing anything on your computer, let's get comfortable with Rust syntax using the [Rust Playground](https://play.rust-lang.org/) - an online environment where you can write and run Rust code directly in your browser.

**Key concepts applied:**
- [The `println!` macro](https://doc.rust-lang.org/std/macro.println.html) for printing output
- [Variable declarations](https://doc.rust-lang.org/book/ch03-01-variables-and-mutability.html) with `let`
- [Mutability](https://doc.rust-lang.org/book/ch03-01-variables-and-mutability.html#mutability) with `let mut`
- Basic [arithmetic operations](https://doc.rust-lang.org/book/appendix-02-operators.html)

### Your task

1. Open the [Rust Playground](https://play.rust-lang.org/) in your browser
2. Complete the **interactive exercises** provided in the [Week 09 Exercise Guide](../../resources/lecture-notes/W09_Welcome_to_Rust_exercises.md)
3. Work through at least **Exercises 1-4** (Hello World, Variables, Data Types, Booleans)
4. **Save your work**: Use the Playground's "Share" button to create permanent links to your solutions
5. You'll submit these Playground links as part of your lab submission

### AI assistant prompts for Part 0

**🤖 AI Strategy for Playground Experimentation:**

Since you're experimenting without consequences, this is the PERFECT time to use AI to explore! Try a conversational approach:

**Example conversation with [GitHub Copilot](https://github.com/features/copilot) or [Claude](https://claude.ai/):**

```
You: I'm brand new to Rust, coming from Python. Can you explain how to create
variables and why they're immutable by default? Show me a simple example I can
try in the Rust Playground.

AI: [Explanation with example]

You: Thanks! Now can you show me what error I'd get if I try to modify an
immutable variable? I want to see the compiler error message.

AI: [Shows example with error]

You: That makes sense. Can you now show me THREE examples: one with an immutable
variable, one with a mutable variable, and one that demonstrates why immutability
is safer in concurrent code?
```

**More effective prompts:**
- *"I'm learning Rust for the first time. Explain [concept] like I'm a Python programmer. Give me runnable Playground examples."*
- *"Show me the WRONG way to do [task] in Rust, explain why it fails, then show the RIGHT way."*
- *"Create a Rust Playground example that demonstrates the difference between [concept A] and [concept B] with clear comments."*
- *"I tried this code in Playground [paste code] and got this error [paste error]. Explain what's happening in simple terms, then show me how to fix it."*

---

## Part 1: install the Rust toolchain

### The challenge

To compile and run Rust programs on your local machine, you need to install the official [Rust toolchain](https://www.rust-lang.org/tools/install), which includes [rustup](https://rustup.rs/) (the installer), [cargo](https://doc.rust-lang.org/cargo/) (the build tool), and [rustc](https://doc.rust-lang.org/rustc/) (the compiler).

**Key concepts applied:**
- [Rustup](https://rustup.rs/) for managing Rust versions
- [Cargo](https://doc.rust-lang.org/cargo/guide/) as the Rust package manager
- [Command-line tools](https://doc.rust-lang.org/book/ch01-01-installation.html) for Rust development

### Your task

1. **Install Rust** by following the instructions in the [course SETUP_GUIDE.md](../../resources/SETUP_GUIDE.md#5-rust)
   - The guide covers all platforms (Windows, macOS, Linux)
   - **Windows users**: Make sure you're using Git Bash as recommended in the [SETUP_GUIDE](../../resources/SETUP_GUIDE.md#recommendations-for-windows-users)

2. **Restart your terminal** after installation

3. **Verify your installation** by running these commands:
   ```bash
   rustc --version
   cargo --version
   rustup --version
   ```

4. All three commands should print version numbers. **Take a screenshot** showing the output of these three commands - you'll need this for your submission.

### What gets installed?

The Rust toolchain includes:
- **`rustc`**: The [Rust compiler](https://doc.rust-lang.org/rustc/) that translates your code to machine code
- **`cargo`**: The [build system and package manager](https://doc.rust-lang.org/cargo/) for Rust
- **`rustup`**: The [toolchain installer](https://rust-lang.github.io/rustup/) for managing Rust versions
- **Standard library**: Core Rust functionality available in every program

### AI assistant prompts for Part 1

If you encounter installation issues:

- *"I'm trying to install Rust on [your operating system] but getting an error: [paste error]. How can I fix this?"*
- *"After installing Rust, when I run 'cargo --version' it says 'command not found'. How do I add Cargo to my PATH?"*
- *"I installed Rust but my terminal doesn't recognize the cargo command. Do I need to restart something?"*

---

## Part 2: create your first Cargo project

### The challenge

Now that Rust is installed, you'll create your first [Cargo project](https://doc.rust-lang.org/cargo/guide/creating-a-new-project.html). Cargo automatically sets up a complete project structure with [version control](https://git-scm.com/) initialized and a "Hello, World!" program ready to run.

**Key concepts applied:**
- [Cargo project structure](https://doc.rust-lang.org/cargo/guide/project-layout.html)
- [The `Cargo.toml` manifest](https://doc.rust-lang.org/cargo/reference/manifest.html)
- [The `src/main.rs` entry point](https://doc.rust-lang.org/book/ch01-02-hello-world.html)
- [Building and running](https://doc.rust-lang.org/cargo/commands/cargo-run.html) with `cargo run`

### Your task

1. Navigate to your `is4010-labs` repository folder:
   ```bash
   cd path/to/is4010-labs
   ```
   > **Note for all platforms**: Forward slashes (`/`) work in Git Bash, PowerShell, and Unix terminals

2. Create a new subdirectory for Lab 09:
   ```bash
   mkdir lab09
   cd lab09
   ```

3. Create a new Cargo project named `rust_basics`:
   ```bash
   cargo new rust_basics
   cd rust_basics
   ```

4. Explore the project structure that Cargo created:
   ```
   rust_basics/
   ├── Cargo.toml          # Project configuration
   ├── src/
   │   └── main.rs         # Your code goes here
   └── .gitignore          # Git ignore rules (auto-generated)
   ```

5. Run the default "Hello, world!" program:
   ```bash
   cargo run
   ```

6. You should see output like:
   ```
   Compiling rust_basics v0.1.0 (/path/to/rust_basics)
   Finished dev [unoptimized + debuginfo] target(s) in 0.50s
   Running `target/debug/rust_basics`
   Hello, world!
   ```

### Understanding Cargo.toml

Open `Cargo.toml` in [VS Code](https://code.visualstudio.com/). This is your [project manifest](https://doc.rust-lang.org/cargo/reference/manifest.html) where you configure metadata and dependencies:

```toml
[package]
name = "rust_basics"
version = "0.1.0"
edition = "2021"

[dependencies]
# External crates (libraries) will be listed here
```

**Key fields:**
- `name`: Your project's name
- `version`: [Semantic versioning](https://semver.org/) number
- `edition`: The Rust language edition (2021 is the latest)
- `dependencies`: External libraries from [crates.io](https://crates.io/)

### AI assistant prompts for Part 2

- *"Explain the purpose of each file that Cargo creates when I run 'cargo new'. What is Cargo.toml used for?"*
- *"What's the difference between 'cargo build' and 'cargo run'? When should I use each one?"*
- *"I see a 'target' folder after running cargo build. What's in there and should I commit it to Git?"*

---

## Part 3: write Rust functions and tests

### The challenge

Now you'll write real Rust code! You'll implement several functions that demonstrate Rust's type system, then write tests to verify they work correctly using [Rust's built-in testing framework](https://doc.rust-lang.org/book/ch11-00-testing.html).

**Key concepts applied:**
- [Function syntax](https://doc.rust-lang.org/book/ch03-03-how-functions-work.html) with type annotations
- [Return types](https://doc.rust-lang.org/book/ch03-03-how-functions-work.html#functions-with-return-values)
- [Test modules](https://doc.rust-lang.org/book/ch11-01-writing-tests.html)
- [Assertion macros](https://doc.rust-lang.org/book/ch11-01-writing-tests.html#checking-results-with-the-assert-macro)

### Your task

1. Open `src/main.rs` in [VS Code](https://code.visualstudio.com/)

2. **Replace the entire contents** of `src/main.rs` with the following code:

```rust
// Lab 09: Rust Basics
// Implement the functions below and pass all tests

/// Adds two i32 integers and returns the result
fn add(a: i32, b: i32) -> i32 {
    // TODO: Implement this function
    // HINT: Just return the sum of a and b
    0  // Replace this
}

/// Multiplies two i32 integers and returns the result
fn multiply(a: i32, b: i32) -> i32 {
    // TODO: Implement this function
    0  // Replace this
}

/// Returns true if the number is even, false otherwise
fn is_even(n: i32) -> bool {
    // TODO: Implement this function
    // HINT: Use the modulo operator % to check divisibility by 2
    false  // Replace this
}

/// Returns the larger of two i32 integers
fn max(a: i32, b: i32) -> i32 {
    // TODO: Implement this function
    // HINT: Use an if expression
    0  // Replace this
}

/// Squares a number (multiplies it by itself)
fn square(n: i32) -> i32 {
    // TODO: Implement this function
    0  // Replace this
}

fn main() {
    // Test your functions here before running cargo test
    println!("5 + 3 = {}", add(5, 3));
    println!("4 * 7 = {}", multiply(4, 7));
    println!("Is 10 even? {}", is_even(10));
    println!("Max of 42 and 17: {}", max(42, 17));
    println!("Square of 6: {}", square(6));
}

// Test module - DO NOT MODIFY
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_add() {
        assert_eq!(add(2, 3), 5);
        assert_eq!(add(-1, 1), 0);
        assert_eq!(add(0, 0), 0);
    }

    #[test]
    fn test_multiply() {
        assert_eq!(multiply(3, 4), 12);
        assert_eq!(multiply(-2, 5), -10);
        assert_eq!(multiply(0, 100), 0);
    }

    #[test]
    fn test_is_even() {
        assert!(is_even(4));
        assert!(is_even(0));
        assert!(!is_even(7));
        assert!(!is_even(-3));
    }

    #[test]
    fn test_max() {
        assert_eq!(max(5, 10), 10);
        assert_eq!(max(10, 5), 10);
        assert_eq!(max(-5, -10), -5);
        assert_eq!(max(0, 0), 0);
    }

    #[test]
    fn test_square() {
        assert_eq!(square(5), 25);
        assert_eq!(square(0), 0);
        assert_eq!(square(-3), 9);
    }
}
```

3. **Implement each function** by replacing the placeholder return values

4. **Test as you go** by running:
   ```bash
   cargo test
   ```

5. All tests should pass before you submit. You'll see output like:
   ```
   running 5 tests
   test tests::test_add ... ok
   test tests::test_multiply ... ok
   test tests::test_is_even ... ok
   test tests::test_max ... ok
   test tests::test_square ... ok

   test result: ok. 5 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out
   ```

### Understanding the code structure

**Function syntax:**
```rust
fn function_name(param: Type) -> ReturnType {
    // body
}
```

**Test module:**
```rust
#[cfg(test)]        // Only compiles when testing
mod tests {          // Module named "tests"
    use super::*;    // Import functions from parent

    #[test]          // Marks this as a test function
    fn test_name() {
        assert_eq!(function(input), expected);
    }
}
```

### AI assistant prompts for Part 3

**🤖 AI Strategy for Implementation:**

Use AI as a **pair programming partner**, not a solution generator. Here's the recommended workflow:

**Step 1: Understand Before Coding**
```
You: I need to implement a function called is_even that takes an i32 and returns
a bool. Before you show me code, explain the concept of the modulo operator and
how it helps determine if a number is even.

AI: [Explains modulo operator]

You: Got it! Now show me pseudocode first, then the actual Rust implementation.
```

**Step 2: Learn from Compiler Errors**
```
You: I wrote this is_even function in Rust:

fn is_even(n: i32) -> bool {
    n % 2 == 0;
}

But cargo test says "mismatched types: expected `bool`, found `()`". What does
that mean and how do I fix it? Explain the semicolon rule.

AI: [Explains the error and solution]
```

**Step 3: Compare Approaches**
```
You: I implemented the max function like this [paste code]. Can you show me TWO
other ways to implement it? Explain the trade-offs of each approach.
```

**Effective implementation prompts:**
- *"Walk me through implementing [function] step-by-step. After each step, pause and let me try it before showing the next step."*
- *"I'm getting this compiler error [paste]. Don't just give me the fix - explain WHY this is an error and what Rust concept I'm misunderstanding."*
- *"Show me how a Python programmer would solve [problem], then show the Rust equivalent. Explain the key differences."*
- *"My tests are failing: [paste test output]. Help me debug by asking ME questions about my logic before showing the solution."*

**🎯 Pro Tip:** Use GitHub Copilot inline suggestions, but ALWAYS understand what it suggests before accepting. Ask Copilot Chat to explain any suggestions you don't fully understand.

---

## Expected Repository Structure

After completing all parts, your `is4010-labs` repository should include:

```
is4010-labs/
├── .github/
│   └── workflows/
│       └── main.yml              # UPDATED: Now tests both Python AND Rust!
├── lab01/
├── lab02/
├── lab03/
│   ├── lab03.py
│   └── test_lab03.py
├── ... (other Python labs)
├── lab09/
│   ├── rust_basics/              # Your Cargo project
│   │   ├── Cargo.toml            # Project manifest
│   │   ├── Cargo.lock            # Dependency lock file (auto-generated)
│   │   ├── src/
│   │   │   └── main.rs           # Your Rust code with functions and tests
│   │   └── target/               # Compiled binaries (DO NOT commit - in .gitignore)
│   └── playground_links.md       # Your saved Playground exercise links
└── .gitignore
```

**IMPORTANT**:
- Do NOT commit the `target/` directory! Cargo automatically builds binaries there, but they're large and shouldn't be in version control. The default `.gitignore` created by `cargo new` handles this automatically.
- The `.github/workflows/main.yml` file is now **multi-language** and will test both your Python and Rust labs automatically!

---

## Part 4: update GitHub Actions for Rust testing

### The challenge

You set up GitHub Actions in Lab 03 to automatically run Python tests. Now you need to **update** your workflow to also test Rust code. This ensures your Rust labs are automatically graded just like your Python labs!

**Key concepts applied:**
- [GitHub Actions workflows](https://docs.github.com/en/actions/using-workflows)
- [Rust toolchain installation](https://github.com/actions-rs/toolchain)
- Multi-language CI/CD pipelines
- Automated testing across multiple languages

### Your task

1. **Open your existing workflow file**: `.github/workflows/main.yml` in your `is4010-labs` repository

2. **Add Rust support** by modifying the file to include both Python AND Rust testing:

```yaml
# .github/workflows/main.yml
name: run-tests

# Trigger: Run this workflow every time code is pushed to any branch
on: [push]

jobs:
  test-python:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        python-version: ["3.10"]

    steps:
      - uses: actions/checkout@v3

      - name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v4
        with:
          python-version: ${{ matrix.python-version }}

      - name: Install Python dependencies
        run: |
          python -m pip install --upgrade pip
          pip install pytest

      - name: Test Python labs with pytest
        run: |
          pytest || echo "No Python tests found or tests failed"

  test-rust:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Install Rust toolchain
        uses: actions-rs/toolchain@v1
        with:
          toolchain: stable
          override: true

      - name: Test Rust labs with cargo test
        run: |
          # Find all Rust projects (directories with Cargo.toml) and test them
          find . -name "Cargo.toml" -not -path "*/target/*" | while read cargo_file; do
            project_dir=$(dirname "$cargo_file")
            echo "Testing Rust project in $project_dir"
            cd "$project_dir"
            cargo test --verbose
            cd - > /dev/null
          done
```

3. **Save the file** and commit the changes:
   ```bash
   git add .github/workflows/main.yml
   git commit -m "Add Rust testing to GitHub Actions workflow"
   git push origin main
   ```

4. **Verify it works**: Go to your repository on GitHub and click the "Actions" tab. You should see your workflow running!

### Understanding the updated workflow

**What changed:**
- **Two jobs** instead of one: `test-python` and `test-rust`
- **Parallel execution**: Both jobs run at the same time (faster!)
- **Rust toolchain**: Uses the official [`actions-rs/toolchain`](https://github.com/actions-rs/toolchain) action to install Rust
- **Auto-discovery**: Finds all `Cargo.toml` files and tests each Rust project
- **Robust**: Continues even if some tests fail (reports overall status)

**Why this is awesome:**
- ✅ Automatically tests BOTH Python and Rust code
- ✅ Works for all future labs (no more manual updates!)
- ✅ Green checkmark ✅ means everything passes
- ✅ Professional CI/CD practice used by real companies

---

## Submission & Grading

**IMPORTANT**: You will be graded **entirely** based on the code in your GitHub repository. There is no separate Canvas submission.

### Grading Criteria

Your grade is determined by:
1. **✅ GitHub Actions tests pass** (70% - automated testing)
2. **📝 Code quality and completion** (30% - manual review)
   - All 5 functions implemented correctly
   - Code follows Rust conventions (`cargo fmt` applied)
   - No `target/` directory committed
   - Proper repository structure

### Submission Checklist

**Before the deadline, ensure:**

1. ✅ **All tests pass locally**:
   ```bash
   cd lab09/rust_basics
   cargo test
   ```

2. ✅ **Optional: Document your Playground work**:
   ```bash
   cd ..  # Back to lab09/
   touch playground_links.md
   # Paste share links from Rust Playground exercises
   ```

3. ✅ **Format your code**:
   ```bash
   cd rust_basics
   cargo fmt
   ```

4. ✅ **Commit and push all changes**:
   ```bash
   cd ../..  # Back to repo root
   git add lab09/
   git commit -m "Complete Lab 09: Rust basics"
   git push origin main
   ```

5. ✅ **Verify GitHub Actions passes**:
   - Go to your repository on GitHub
   - Click the "Actions" tab
   - Your most recent workflow should show **green checkmarks ✅**
   - Both `test-python` and `test-rust` jobs should succeed

6. ✅ **Verify repository structure on GitHub**:
   - `lab09/rust_basics/src/main.rs` exists (your code)
   - `lab09/rust_basics/Cargo.toml` exists
   - `lab09/playground_links.md` exists (optional but recommended)
   - **NO** `lab09/rust_basics/target/` directory (should be in .gitignore)

### How You'll Be Graded

**Automated Testing (70 points):**
- GitHub Actions runs `cargo test` on your code
- Each of 5 functions has tests worth 14 points
- Tests must pass for full credit
- Instructor can see test results in GitHub Actions

**Code Quality (30 points):**
- Instructor manually reviews your repository
- Checks for proper implementation
- Verifies code is formatted (`cargo fmt`)
- Ensures no build artifacts committed

### Deadline

**Due: Sunday, October 26 at 11:59 PM**

After the deadline, the instructor will:
1. Clone your repository
2. Check GitHub Actions results
3. Review your code manually
4. Post grades to Canvas

**No Canvas submission required** - your GitHub repository IS your submission!

---

## Comprehensive Troubleshooting Guide

### Installation Issues

**Problem**: "Command not found: cargo" after installation
- **Solution**: Restart your terminal. The PATH environment variable needs to be reloaded to include Cargo
- **Windows users**: Make sure you're using Git Bash (see [SETUP_GUIDE.md](../../resources/SETUP_GUIDE.md#recommendations-for-windows-users))
- **Why**: The PATH environment variable needs to be reloaded to include Cargo

**Problem**: Rust installation issues on Windows
- **Solution**: See the [course SETUP_GUIDE.md](../../resources/SETUP_GUIDE.md#5-rust) for complete Rust installation instructions
- **Common fix**: Ensure you're using Git Bash, not Command Prompt or PowerShell alone
- **Terminal setup**: Follow the [Windows Terminal + Git Bash setup guide](../../resources/SETUP_GUIDE.md#recommendations-for-windows-users)

**Problem**: Permission denied during installation
- **Solution**: Don't use `sudo` with rustup. It installs to your user directory (`~/.cargo`), not system-wide

### Cargo Project Issues

**Problem**: "cargo new" creates project but won't compile
- **Solution**: Make sure you're inside the project directory: `cd rust_basics` before running `cargo build` or `cargo run`
- **Why**: Cargo commands must be run from the directory containing `Cargo.toml`

**Problem**: "cargo clippy" or "cargo fmt" command not found
- **Solution**: These come with rustup. Run `rustup component add clippy rustfmt`
- **Why**: While usually installed by default, sometimes they need to be added explicitly

**Problem**: "cargo clippy" gives lots of warnings
- **Solution**: This is GOOD! Clippy is teaching you better Rust. Read each warning and fix them - you'll learn a lot
- **Why**: Clippy has over 500 lints to help you write better code

**Problem**: "could not compile" error mentioning Cargo.lock
- **Solution**: Delete `Cargo.lock` and run `cargo build` again: `rm Cargo.lock && cargo build`

**Problem**: Changes to code aren't reflected when running `cargo run`
- **Solution**: Make sure you saved the file! VS Code should show no dot next to the filename
- **Alternative**: Run `cargo clean` then `cargo build` to force a complete rebuild

### Syntax and Compilation Errors

**Problem**: "expected `;`, found `}`" error
- **Solution**: You likely forgot a semicolon after a statement, OR you added a semicolon to the return expression
- **Remember**: In Rust, the last expression in a function is returned *without* a semicolon

**Problem**: "mismatched types: expected `i32`, found `()`"
- **Solution**: You're not returning a value. Remove the semicolon from your return expression or add an explicit `return` statement

**Problem**: "cannot assign twice to immutable variable"
- **Solution**: Add `mut` to make the variable mutable: `let mut x = 5;`

**Problem**: "cannot find function `add` in this scope"
- **Solution**: Make sure your function is defined before it's called, or put the tests module at the bottom with `use super::*;`

### Test Failures

**Problem**: Tests fail with "assertion `left == right` failed"
- **Solution**: Your function implementation is incorrect. The error shows expected vs actual values
- **Debug**: Print the actual values in `main()` to see what your function returns: `println!("{}", your_function(test_input));`

**Problem**: "test result: ok. 0 passed; 0 failed"
- **Solution**: No tests ran. Make sure your test module has `#[cfg(test)]` and each test has `#[test]`

**Problem**: "overflow when multiplying" panic in tests
- **Solution**: With `i32`, large multiplications can overflow. This lab uses small test values, so this shouldn't happen unless your logic is wrong

### Git and GitHub Issues

**Problem**: `target/` directory keeps appearing in Git
- **Solution**: Make sure `target/` is in your `.gitignore`. If it's already committed, remove it: `git rm -r --cached lab09/rust_basics/target`

**Problem**: Cargo.lock shows merge conflicts
- **Solution**: It's auto-generated, so just regenerate it: Delete `Cargo.lock`, run `cargo build`, then commit the new version

**Problem**: VS Code shows red squiggles everywhere in Rust code
- **Solution**: Install the [rust-analyzer](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer) extension for VS Code
- **Alternative**: The code might still compile fine. Try `cargo build` in the terminal

### Performance and Speed Issues

**Problem**: First `cargo build` takes a very long time
- **Solution**: This is normal! Cargo compiles the standard library the first time. Subsequent builds are much faster

**Problem**: `cargo test` is slow
- **Solution**: Use `cargo test --release` for optimized builds, or just accept it - testing is thorough!

### AI Assistant Help

**Problem**: AI generates Rust code that doesn't compile
- **Solution**: Always read the compiler error messages carefully. They're incredibly helpful and often suggest fixes
- **Better prompt**: "I'm learning Rust. Please explain the concept first, then show simple example code. I'm coming from Python background."

**Problem**: AI uses advanced Rust features you haven't learned yet
- **Solution**: Ask it to simplify: *"Can you rewrite this using only basic Rust concepts like let, if, and simple functions? No iterators or closures yet."*

### When All Else Fails

1. **Read the error message** - Rust's compiler is exceptionally helpful
2. **Try the Rust Playground** - Isolate your function in the playground to test it
3. **Ask on Teams** - Your classmates likely encountered the same issue
4. **Check the Rust Book** - [Chapter 3](https://doc.rust-lang.org/book/ch03-00-common-programming-concepts.html) covers these concepts
5. **Use `cargo clean`** - Sometimes a fresh build solves mysterious issues

---

## AI Integration Strategy

Rust is PERFECT for AI-assisted learning because the compiler gives you immediate, detailed feedback. Use AI to help you understand what the compiler is telling you!

### The Rust Learning Cycle with AI

```
1. Write code → 2. Compiler error → 3. Ask AI to explain error →
4. Understand concept → 5. Fix code → REPEAT
```

### Real-World AI Conversation Examples

**Example 1: Understanding Compiler Errors**

```
You: I'm getting this error when I compile my Rust code:

error[E0384]: cannot assign twice to immutable variable `x`
 --> src/main.rs:3:5
  |
2 |     let x = 5;
  |         - first assignment to `x`
3 |     x = 6;
  |     ^^^^^ cannot assign twice to immutable variable

What does this mean? I come from Python where this would work fine.

AI: In Python, variables are mutable by default - you can change them anytime.
Rust is the opposite: variables are immutable by default for safety...
[explanation continues]

You: So if I add 'mut', like 'let mut x = 5;', it will work?

AI: Exactly! Here's why Rust does this...

You: Can you show me a real-world example where immutability prevents a bug
that would be hard to catch in Python?
```

**Example 2: Pair Programming Workflow**

```
You: I need to implement a function that returns the maximum of two numbers.
Don't give me the code yet - first, quiz me on what I need to think about
for the function signature.

AI: Great approach! Let me ask you:
1. What should the function be named?
2. What type should the parameters be?
3. What should it return?

You: max, i32 for both parameters, returns i32

AI: Perfect! Now, what Rust feature lets you return a value from different
code paths (like if one number is bigger vs the other)?

You: An if expression?

AI: Exactly! Now try implementing it. Show me what you write.

You: [pastes attempt]

AI: Great start! You're almost there. The issue is with your semicolons...
```

**Example 3: Learning from Tests**

```
You: My test is failing:

---- tests::test_square stdout ----
thread 'tests::test_square' panicked at 'assertion failed: `(left == right)`
  left: `0`,
 right: `25`', src/main.rs:45:9

But I don't understand WHY it's returning 0 instead of 25. Here's my function:

fn square(n: i32) -> i32 {
    n * n;
}

What's wrong?

AI: Ah! This is a classic Rust beginner mistake with semicolons. Let me explain...

You: Oh! So the semicolon makes it a statement instead of an expression?
Should I remove it OR use 'return n * n;'?

AI: Both work! But Rustaceans prefer the expression style without 'return'...
```

### Effective Prompts by Learning Goal

**Understanding Concepts:**
- *"I'm learning Rust after Python. Compare Python's [feature] to Rust's [feature]. What are the key differences and why did Rust make that choice?"*
- *"Explain [Rust concept] using an analogy or real-world example, not just code."*
- *"I understand [concept] in theory, but show me three progressively complex examples that demonstrate it in practice."*

**Debugging Compiler Errors:**
- *"I got this error: [paste full error]. Before you tell me the fix, explain what the compiler is trying to tell me and what Rust principle I'm violating."*
- *"This error mentions 'expected X, found Y'. Help me understand Rust's type system and why this mismatch matters."*
- *"The compiler suggests I do [suggestion]. Explain WHY that's the right fix, not just HOW to do it."*

**Implementation Patterns:**
- *"I need to solve [problem]. Show me how to break this into smaller functions with proper type signatures."*
- *"Compare THREE different ways to implement [function]. Explain when to use each approach and why."*
- *"I implemented this [paste code]. Code review it like a senior Rust developer. What would you change and why?"*

**Test-Driven Learning:**
- *"I have this test [paste test]. Before implementing, explain what the test is checking and what Rust features I'll need."*
- *"My test fails with [error]. Don't fix the code - instead, explain what the test reveals about my understanding."*
- *"Write three edge case tests for this function [paste function]. Explain why these cases matter."*

### Learning Best Practices

✅ **DO**:
- **Always read the compiler error FIRST** before asking AI - the Rust compiler is one of the best teachers
- **Ask AI to explain the "why"** behind errors and solutions, not just the "what"
- **Request Python/Rust comparisons** when learning new concepts - leverage your Python knowledge
- **Use AI to generate test cases** you didn't think of
- **Ask for multiple approaches** to understand trade-offs
- **Have AI quiz you** instead of just giving answers
- **Share your attempts** with AI and ask for feedback

❌ **DON'T**:
- **Skip compiler messages** to go straight to AI - you'll learn slower
- **Copy-paste AI code** without typing it yourself and understanding every line
- **Ask for complete solutions** - ask for guidance and hints instead
- **Use advanced features** AI suggests before understanding basics
- **Ignore AI warnings** about safety or best practices
- **Expect AI to catch all bugs** - run `cargo test` frequently yourself

### GitHub Copilot-Specific Tips for Rust

**Inline Suggestions:**
```rust
// Start typing a function signature and let Copilot suggest the body
fn is_even(n: i32) -> bool {
    // Copilot will suggest: n % 2 == 0
}

// But DON'T just accept - ask Copilot Chat: "Why no semicolon here?"
```

**Using Copilot Chat:**
- **Before accepting a suggestion**: Select the code, Ctrl+I (or Cmd+I), ask "Explain this Rust code and why it works"
- **For errors**: Select error in terminal, ask "What is this Rust error telling me?"
- **For learning**: "Show me three ways to write this function, from beginner to idiomatic Rust"

### AI Tools Comparison for Rust Learning

| Tool | Best For | Rust Learning Tip |
|------|----------|-------------------|
| **GitHub Copilot** | Inline code completion, quick examples | Use Copilot Chat to explain suggestions before accepting |
| **Claude** | Deep conceptual explanations, Python comparisons | Ask for "explain like I'm a Python developer" framing |
| **ChatGPT** | Step-by-step walkthroughs, debugging | Request interactive quizzing instead of direct answers |
| **Rust Playground + AI** | Experimentation without local setup | Share Playground links with AI for collaborative debugging |

### The Golden Rule: Understand Before Accepting

**BAD Workflow:**
1. Get compiler error
2. Ask AI for fix
3. Copy-paste solution
4. Move on ❌

**GOOD Workflow:**
1. Get compiler error
2. Read error message carefully
3. Try to fix it yourself
4. If stuck, ask AI to **explain the error**
5. Implement the fix yourself based on understanding
6. Ask AI "Is there a better way?" ✅

---

## Documenting Your AI Usage (Academic Integrity)

This course encourages AI use, but you must be able to **explain every line of code you submit**. Here's how to use AI responsibly:

### Required: AI Interaction Log (Optional for Lab 09, Required in Future)

While not required for this first Rust lab, we **strongly encourage** you to start documenting your AI interactions. In future labs and projects, you'll be required to submit an AI log.

**Create a file: `lab09/AI_LOG.md`**

```markdown
# Lab 09 AI Interaction Log

## Part 0: Playground Exploration

**Prompt**: I'm brand new to Rust. Explain immutability with a simple example.

**AI Tool**: Claude

**Response Summary**: AI explained that Rust variables are immutable by default,
unlike Python. Provided example showing compiler error when trying to mutate
immutable variable.

**What I Learned**: Rust requires explicit `mut` keyword for mutability. This
prevents accidental mutations and makes code safer.

**Code I Used**: Modified the example to test mutable vs immutable variables
in Playground.

---

## Part 3: Implementing is_even()

**Prompt**: I got error "expected `bool`, found `()`" on my is_even function.
Here's my code: [pasted code]. Don't fix it - explain the error.

**AI Tool**: GitHub Copilot Chat

**Response Summary**: Explained that adding a semicolon makes it a statement
instead of expression, so function returns () (unit type) instead of bool.

**What I Learned**: Semicolons matter in Rust! Last expression without semicolon
is automatically returned.

**Code I Used**: Removed semicolon from `n % 2 == 0;` → `n % 2 == 0`
```

### What to Document

**DO Document:**
- ✅ Prompts you used to understand concepts
- ✅ How AI helped you debug compiler errors
- ✅ Questions you asked about Rust features
- ✅ Code AI suggested that you used (with explanation of why)

**DON'T Need to Document:**
- ❌ Every single Copilot inline suggestion you accepted
- ❌ Basic syntax lookups
- ❌ AI suggestions you rejected or didn't use

### Quick Template for Each AI Interaction

```
**What I asked**: [Your question/prompt]
**Tool used**: [Copilot/Claude/ChatGPT/etc.]
**Key learning**: [What concept you now understand]
**Code impact**: [Did this change your code? How?]
```

### Why This Matters

- **Academic integrity**: Shows you're learning, not just copying
- **Learning reinforcement**: Writing what you learned cements understanding
- **Debugging help**: If code doesn't work, you can show instructor your thought process
- **Future reference**: You'll build a library of effective Rust prompts

### Example: Good vs. Bad AI Usage

**❌ BAD (Academic Dishonesty):**
```
Prompt: "Write the is_even function in Rust"
*Copies code without understanding*
*Submits without knowing why it works*
```

**✅ GOOD (AI-Enhanced Learning):**
```
Prompt: "Explain how the modulo operator works for checking even numbers"
*Reads explanation*
Prompt: "Now show me a Rust function signature for is_even"
*Studies type annotations*
*Writes implementation myself*
Prompt: "Review my implementation: [paste code]. What could be improved?"
*Documents the learning in AI log*
```

---

## Additional Resources

### Official Rust Resources
- [The Rust Programming Language Book](https://doc.rust-lang.org/book/) - Free, comprehensive guide ("The Rust Book")
- [Rust by Example](https://doc.rust-lang.org/rust-by-example/) - Learn through annotated examples
- [Rustlings](https://github.com/rust-lang/rustlings/) - Small exercises for practicing Rust syntax
- [Rust Playground](https://play.rust-lang.org/) - Online Rust environment

### Quick Reference
- [Rust Cheat Sheet](https://cheats.rs/) - Quick reference for syntax and concepts
- [Cargo Book](https://doc.rust-lang.org/cargo/) - Complete Cargo documentation
- [Rust API Documentation](https://doc.rust-lang.org/std/) - Standard library reference

### Community Help
- [Rust Users Forum](https://users.rust-lang.org/) - Friendly community for questions
- [r/rust](https://www.reddit.com/r/rust/) - Reddit community
- [Rust Discord](https://discord.gg/rust-lang) - Real-time chat

### Learning Platforms
- [Comprehensive Rust](https://google.github.io/comprehensive-rust/) - Google's Rust course
- [Exercism Rust Track](https://exercism.org/tracks/rust) - Practice problems with mentoring

---

## Pro Tips

💡 **Run `cargo check` frequently** - It's faster than `cargo build` and catches syntax errors

💡 **Use `cargo clippy`** - It catches mistakes and teaches you better Rust patterns (like having a mentor review your code!)

💡 **Run `cargo fmt` before committing** - Automatically formats your code to Rust community standards

💡 **Read compiler errors carefully** - Rust's error messages are some of the best in any language

💡 **Use the Playground for quick experiments** - Test small code snippets without creating a full project

💡 **Don't fight the compiler** - If Rust won't compile your code, there's usually a good reason

💡 **Ask for help early** - Rust has a steep learning curve, and the community is very welcoming

💡 **cargo check → cargo clippy → cargo test → cargo fmt** - This is the professional workflow!

---

Congratulations on starting your Rust journey! 🦀 The compiler might seem strict at first, but it's catching bugs that would crash programs in other languages. Trust the process!
