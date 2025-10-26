# Week 11: Structuring Code and Data - Lecture Notes

**Course:** IS4010 - AI-Enhanced Application Development
**Topic:** Rust's Module System, Structs, Enums, Error Handling, and Collections
**Companion Materials:** [Slides](../IS4010_W11_Structuring_Code_and_Data.qmd) | [Interactive Exercises](./W11_Structuring_Code_and_Data_exercises.md) | [Lab 11](https://github.com/bgreenwell/is4010-course-template/tree/main/labs/lab11)

---

## 📋 Learning Objectives

By the end of this session, you should be able to:
- **Organize** Rust code using modules, crates, and packages for maintainability
- **Create** custom data types using structs with methods and associated functions
- **Model** alternatives and states using enums with pattern matching
- **Handle** errors gracefully using `Option<T>` and `Result<T, E>` types
- **Work** with Rust's core collections: `Vec<T>`, `String`, and `HashMap<K, V>`
- **Apply** ownership principles to complex data structures
- **Leverage** AI tools to design and implement data structures effectively

---

## Part 1: The Module System

### Why Modules Matter

As programs grow, organizing code becomes critical. Rust's [module system](https://doc.rust-lang.org/book/ch07-00-managing-growing-projects-with-packages-crates-and-modules.html) provides powerful tools for:
- Breaking code into logical units
- Managing privacy and encapsulation
- Reusing code across projects
- Building libraries and applications

### Hierarchy of Organization

**[Packages](https://doc.rust-lang.org/book/ch07-01-packages-and-crates.html)**:
- Created with `cargo new`
- Contain one or more crates
- Defined by `Cargo.toml` manifest

**[Crates](https://doc.rust-lang.org/book/ch07-01-packages-and-crates.html)**:
- Binary crates: Compile to executables (with `main()`)
- Library crates: Reusable code modules (no `main()`)
- Unit of compilation and distribution

**[Modules](https://doc.rust-lang.org/book/ch07-02-defining-modules-to-control-scope-and-privacy.html)**:
- Organize code within crates
- Control privacy with `pub` keyword
- Create namespaces to avoid name conflicts

### Privacy and Visibility

**Default: Private**
- All items are private by default
- Promotes encapsulation and prevents accidental dependencies
- Explicit `pub` makes items public

**The `pub` keyword:**
- Makes functions, structs, enums, and modules public
- Enables controlled API boundaries
- Works with fields for fine-grained control

**The `use` keyword:**
- Brings paths into scope
- Creates convenient shortcuts
- Can rename with `as` for clarity

### When to Use Modules

**Single file is getting large:**
- Split into logical modules
- Each module focuses on one responsibility

**Need privacy boundaries:**
- Hide implementation details
- Expose only public API

**Building reusable code:**
- Create library crates
- Share code across projects

---

## Part 2: Structs - Custom Data Types

### What Are Structs?

[Structs](https://doc.rust-lang.org/book/ch05-00-structs.html) (short for "structures") let you create custom data types that group related data together. They're like classes in other languages, but with Rust's ownership rules built in.

### Three Kinds of Structs

**Named Field Structs:**
- Most common type
- Each field has a name and type
- Access fields with dot notation

**Tuple Structs:**
- Fields accessed by position (0, 1, 2...)
- Useful for simple data groupings
- Can create "newtype" pattern for type safety

**Unit Structs:**
- No fields at all
- Useful for implementing traits
- Zero-size types

### Methods and Associated Functions

**Methods** (`&self` parameter):
- Functions that operate on instances
- Defined in `impl` blocks
- First parameter is `&self`, `&mut self`, or `self`

**Associated Functions** (no `self`):
- Like static methods in other languages
- Often used for constructors (e.g., `::new()`)
- Called with `::` syntax (e.g., `String::from()`)

### When to Use Structs

**Modeling entities:**
- Users, products, transactions
- Any "thing" with multiple properties

**Grouping related data:**
- Configuration settings
- API responses
- Database records

**Building abstractions:**
- Encapsulate behavior with methods
- Hide implementation details
- Create clear interfaces

---

## Part 3: Enums - Modeling Alternatives

### What Are Enums?

[Enums](https://doc.rust-lang.org/book/ch06-00-enums.html) (enumerations) let you define a type that can be one of several variants. Unlike structs that group data together, enums represent alternatives.

### Why Enums Are Powerful in Rust

**Data-carrying variants:**
- Each variant can hold different types of data
- More flexible than enums in C or Java
- Enables rich type modeling

**Pattern matching:**
- Compiler ensures you handle all cases
- Makes impossible states unrepresentable
- Eliminates whole classes of bugs

**Memory efficiency:**
- Only stores the active variant
- Compiler optimizes layout
- No runtime overhead

### Common Enum Patterns

**State machines:**
- Model system states explicitly
- Transitions between states
- Prevent invalid state combinations

**Alternative representations:**
- Different ways to represent same concept
- Example: IP addresses (V4 vs V6)

**Command/message passing:**
- Model different operations
- Used in async systems
- Event handling

### The `match` Expression

[Pattern matching](https://doc.rust-lang.org/book/ch06-02-match.html) is how you work with enums:
- Must be exhaustive (handle all variants)
- Can extract data from variants
- Compiler enforces completeness

**Benefits:**
- No forgotten cases (compile error if you miss one)
- Refactor-friendly (adding variant shows all places to update)
- Self-documenting code

---

## Part 4: Error Handling with Option and Result

### Rust's Error Philosophy

Rust has no exceptions. Instead, it uses the type system to handle errors:
- Explicit is better than implicit
- Errors are values, not special control flow
- Compiler enforces error handling

### Option<T> - Representing Optional Values

[`Option<T>`](https://doc.rust-lang.org/std/option/enum.Option.html) is an enum with two variants:
- `Some(T)`: Contains a value of type T
- `None`: Represents absence of a value

**Use cases:**
- Functions that might not return a value
- Struct fields that are optional
- Avoiding null pointer errors (no null in Rust!)

**Working with Option:**
- `unwrap()`: Get value or panic (use sparingly)
- `unwrap_or()`: Provide default value
- `map()`: Transform the value if present
- Pattern matching for precise control

### Result<T, E> - Handling Recoverable Errors

[`Result<T, E>`](https://doc.rust-lang.org/std/result/enum.Result.html) is an enum with two variants:
- `Ok(T)`: Success case with value of type T
- `Err(E)`: Error case with error of type E

**Use cases:**
- File I/O operations
- Network requests
- Parsing and validation
- Any operation that might fail

**The `?` operator:**
- Shorthand for error propagation
- Returns early if error occurs
- Converts error types automatically
- Makes error handling code cleaner

### When to Use Each

**Use `Option<T>` when:**
- Value might not exist (but that's normal, not an error)
- No additional error information needed
- Example: finding an item in a collection

**Use `Result<T, E>` when:**
- Operation can fail with meaningful error
- Need to communicate why failure occurred
- Example: reading a file (permission denied vs file not found)

---

## Part 5: Collections - Dynamic Data Structures

### The Three Core Collections

Rust's [collections](https://doc.rust-lang.org/book/ch08-00-common-collections.html) are stored on the heap and can grow/shrink at runtime:

**[`Vec<T>`](https://doc.rust-lang.org/std/vec/struct.Vec.html) - Vectors:**
- Growable array (like Python list)
- All elements must be same type
- Fast indexed access
- Push/pop operations

**[`String`](https://doc.rust-lang.org/std/string/struct.String.html):**
- Growable, UTF-8 encoded text
- Owned (heap-allocated)
- Different from `&str` (string slice)
- Can modify and grow

**[`HashMap<K, V>`](https://doc.rust-lang.org/std/collections/struct.HashMap.html):**
- Key-value pairs (like Python dict)
- Fast lookup by key
- Keys must be hashable and comparable
- Values can be any type

### String vs &str - A Critical Distinction

**`String`** (owned):
- Heap-allocated, growable
- You can modify it
- Analogous to `Vec<u8>` for UTF-8 data

**`&str`** (borrowed):
- Reference to string data
- Immutable view
- String literals have type `&str`
- More efficient when you don't need ownership

**Conversion:**
- `&str` → `String`: Use `.to_string()` or `String::from()`
- `String` → `&str`: Use `&` (automatic coercion) or `.as_str()`

### Vector Operations

**Creation:**
- `Vec::new()`: Empty vector
- `vec![]` macro: Initialize with values

**Adding elements:**
- `.push()`: Add to end
- `.insert()`: Add at index

**Accessing elements:**
- `[]` indexing: Panics if out of bounds
- `.get()`: Returns `Option<T>` (safe)

**Iteration:**
- `for` loops
- Iterator methods (`.iter()`, `.iter_mut()`)

### HashMap Operations

**Creation:**
- `HashMap::new()`: Empty map
- Insert with `.insert(key, value)`

**Accessing:**
- `.get(&key)`: Returns `Option<&V>` (safe)
- `[]` indexing: Panics if key doesn't exist

**Updating:**
- Overwrite: `.insert()` again
- Insert if absent: `.entry().or_insert()`
- Update based on old value: `.entry().and_modify()`

### Performance Considerations

**Choose based on access patterns:**
- Need fast indexed access? → `Vec<T>`
- Need fast key lookup? → `HashMap<K, V>`
- Need sorted keys? → `BTreeMap<K, V>` (not covered today)

**Memory:**
- Collections grow dynamically
- May reallocate when capacity exceeded
- Pre-allocate with `with_capacity()` if size known

---

## Part 6: Ownership in Complex Data Structures

### Structs and Ownership

**Owning fields:**
- Struct owns its fields
- When struct is dropped, fields are dropped
- Natural for most use cases

**Borrowed fields:**
- Struct contains references
- Requires lifetime annotations
- Use when data outlives struct

**Trade-offs:**
- Owned fields: Simpler, more flexible
- Borrowed fields: More efficient, more complex

### Enums and Ownership

**Each variant can own its data:**
- Moving enum moves the active variant's data
- Pattern matching respects ownership
- Can consume enum by moving out data

**Borrowing from enums:**
- Use references in match arms
- `if let` for single-variant checks

### Collections and Ownership

**Vectors own their elements:**
- Pushing transfers ownership
- Removing gives ownership back
- Iterating can borrow or consume

**HashMaps own keys and values:**
- Inserting moves ownership
- Removing returns ownership
- `.get()` borrows, doesn't move

**String ownership:**
- `String` owns its buffer
- `&str` borrows from `String` or literal
- Be aware of lifetime requirements

---

## Part 7: Real-World Impact

### Industry Applications

**Discord:**
- Used enums to model message types
- Pattern matching for message routing
- Performance-critical message handling

**[Dropbox](https://dropbox.tech/infrastructure/rewriting-the-heart-of-our-sync-engine):**
- Rust structs for file metadata
- Collections for tracking sync state
- Error handling with `Result` for I/O

**[Cloudflare](https://blog.cloudflare.com/how-we-built-pingora-the-proxy-that-connects-cloudflare-to-the-internet/):**
- Module system for proxy architecture
- Custom data structures for HTTP handling
- Enums for protocol states

### Why These Concepts Matter

**Code organization:**
- Large codebases need structure
- Modules prevent "spaghetti code"
- Clear interfaces improve maintainability

**Type safety:**
- Structs and enums prevent invalid states
- Compiler catches bugs before runtime
- Self-documenting through types

**Error handling:**
- Explicit errors force you to think about failure
- No surprises from unexpected exceptions
- Users appreciate robust error handling

### Security Implications

**Memory safety extends to data structures:**
- No use-after-free in collections
- No iterator invalidation bugs
- No data races with shared state

**Type safety prevents vulnerabilities:**
- Can't mix up similar types
- Pattern matching ensures all cases handled
- Impossible states are unrepresentable

---

## Part 8: Career Relevance

### Why These Skills Matter

**Immediate benefits:**
- Write organized, maintainable Rust code
- Model complex domains with types
- Handle errors gracefully
- Work with dynamic data

**Long-term benefits:**
- Think about data modeling in all languages
- Appreciate strong type systems
- Write more robust code everywhere
- Understand systems programming deeply

### Interview Preparation

Common interview topics:
- "How do you organize large codebases?"
- "Explain how to handle errors without exceptions"
- "What's the difference between structs and classes?"
- "How do enums in Rust differ from other languages?"
- "When would you use a vector vs a hash map?"

### Skills That Transfer

Even if you don't use Rust daily:
- Module thinking applies to all languages (Python packages, Java packages, JavaScript modules)
- Error handling philosophy (Go's error values, Swift's Result type)
- Type-driven design (TypeScript, Haskell, F#)
- Performance awareness (choosing right data structure matters everywhere)

---

## Part 9: Working with AI on Data Structures

### Effective AI Prompts

**Designing structs:**
- "Help me model a user profile with email, name, and optional avatar"
- "What fields should a blog post struct have?"
- "Should this field be owned or borrowed?"

**Working with enums:**
- "Design an enum for payment methods (card, PayPal, crypto)"
- "How do I pattern match on this enum and extract data?"
- "Help me model different API responses with Result"

**Collections:**
- "Should I use a Vec or HashMap for storing user data?"
- "How do I update a value in a HashMap only if it exists?"
- "Explain the difference between String and &str"

**Error handling:**
- "Help me convert this code to use Result instead of panicking"
- "When should I use Option vs Result?"
- "How do I chain multiple Result-returning functions?"

### Best Practices with AI

1. **Start with requirements** - describe what you need before asking for code
2. **Ask for explanations** - understand why AI suggests certain designs
3. **Request alternatives** - "What's another way to model this?"
4. **Validate with Playground** - test AI-generated code immediately
5. **Build incrementally** - start simple, add complexity gradually

### Common AI-Assisted Patterns

**Data modeling workflow:**
1. Describe domain requirements to AI
2. AI suggests struct/enum design
3. Iterate on field types and visibility
4. Add methods and associated functions
5. Test with cargo check and cargo test

**Error handling workflow:**
1. Identify failure points in code
2. Ask AI to convert to Result/Option
3. Use ? operator for propagation
4. Add meaningful error types
5. Handle errors at appropriate levels

---

## Part 10: Key Takeaways

### Core Concepts to Remember

**Modules:**
- Organize code into logical units
- Control privacy with `pub`
- Use `use` to bring items into scope

**Structs:**
- Group related data
- Add behavior with methods
- Use associated functions for constructors

**Enums:**
- Model alternatives and states
- Pattern match to handle variants
- Make impossible states unrepresentable

**Error Handling:**
- `Option<T>` for optional values
- `Result<T, E>` for recoverable errors
- `?` operator for propagation

**Collections:**
- `Vec<T>` for sequences
- `String` for owned text, `&str` for borrowed
- `HashMap<K, V>` for key-value pairs

### The Mental Model Shift

**Coming from Python/Java:**
- Stop relying on null/None everywhere
- Start using `Option` and `Result` explicitly
- Think about ownership in data structures
- Use enums more (they're powerful in Rust!)

**The payoff:**
- More robust code (compiler catches errors)
- Better performance (zero-cost abstractions)
- Clearer intent (types document behavior)
- Easier refactoring (compiler guides you)

### Design Principles

**Type-driven design:**
- Let types guide your implementation
- Make illegal states unrepresentable
- Use the compiler as a partner

**Composition over inheritance:**
- Rust has no inheritance
- Compose structs and enums
- Use traits for shared behavior (next week!)

**Explicit is better:**
- Errors are visible in function signatures
- Ownership is clear from types
- No hidden behavior or surprises

---

## Part 11: Application to Lab 11

This week's lab focuses on building a complete application using these concepts:

### Lab 11 Preview: Student Management System

**What you'll build:**
- Module-based project structure
- Custom `Student` struct with methods
- `Grade` enum for letter grades
- Error handling with `Result` and `Option`
- Collections to manage multiple students

**Skills you'll practice:**
- Organizing code into modules
- Defining structs with methods and associated functions
- Using enums with pattern matching
- Handling errors gracefully
- Working with vectors and hash maps
- Applying ownership principles to real-world code

**AI integration:**
- Use AI to design your data structures
- Get help with error handling patterns
- Debug borrow checker issues in complex code
- Optimize collection usage

### What Makes This Different

**Previous labs:**
- Focused on syntax and basic concepts
- Simple, isolated problems
- Minimal error handling

**Lab 11:**
- Full application with multiple modules
- Real-world data modeling
- Comprehensive error handling
- Multiple interacting components

---

## Additional Resources

### Official Rust Documentation

- [The Rust Programming Language - Chapter 7: Managing Growing Projects](https://doc.rust-lang.org/book/ch07-00-managing-growing-projects-with-packages-crates-and-modules.html)
- [The Rust Programming Language - Chapter 5: Using Structs](https://doc.rust-lang.org/book/ch05-00-structs.html)
- [The Rust Programming Language - Chapter 6: Enums and Pattern Matching](https://doc.rust-lang.org/book/ch06-00-enums.html)
- [The Rust Programming Language - Chapter 8: Common Collections](https://doc.rust-lang.org/book/ch08-00-common-collections.html)
- [The Rust Programming Language - Chapter 9: Error Handling](https://doc.rust-lang.org/book/ch09-00-error-handling.html)
- [Rust Standard Library - Module std::collections](https://doc.rust-lang.org/std/collections/)
- [Rust by Example - Modules](https://doc.rust-lang.org/rust-by-example/mod.html)
- [Rust by Example - Structures](https://doc.rust-lang.org/rust-by-example/custom_types/structs.html)
- [Rust by Example - Enums](https://doc.rust-lang.org/rust-by-example/custom_types/enum.html)

### Interactive Learning

- [Rust Playground](https://play.rust-lang.org/) - Experiment with code in your browser
- [Rustlings](https://github.com/rust-lang/rustlings) - Interactive exercises for modules, structs, and enums
- [Exercism Rust Track](https://exercism.org/tracks/rust) - Practice problems with mentoring

### Videos and Articles

- [Rust Modules Explained](https://www.youtube.com/watch?v=969j0qnJGi8) - Video walkthrough
- [Understanding Rust's Module System](https://www.sheshbabu.com/posts/rust-module-system/)
- [Error Handling in Rust](https://www.sheshbabu.com/posts/rust-error-handling/)
- [Rust Collections](https://www.youtube.com/watch?v=Zs-pS-egQSs) - Video overview

### Community Resources

- [r/rust](https://www.reddit.com/r/rust/) - Active Rust community
- [The Rust Programming Language Discord](https://discord.gg/rust-lang)
- [Rust Users Forum](https://users.rust-lang.org/)

---

## Looking Ahead: Week 12

Next week we'll learn how to write flexible, reusable code:

**Topics:**
- Generics: Write code that works with multiple types
- Traits: Define shared behavior across types
- Automated testing: TDD with cargo test
- Real-world testing strategies

**Why modules/structs/enums come first:**
- Generics make structs and enums more flexible
- Traits add behavior to your custom types
- Testing validates your data structures work correctly
- Everything builds on this week's foundation

**Preview:**
- Generic `Stack<T>` data structure
- Custom traits and implementations
- Writing comprehensive test suites
- Test-driven development workflow

---

**Remember:** Good data modeling is the foundation of good software. Structs, enums, and collections give you the tools to represent your problem domain clearly and safely. The compiler is your partner - use it to guide you toward correct, robust code!

**Need help?** Reach out on [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/group-chat-software) - we're here to support your learning journey.

---

**Last Updated:** 2025-01-26
**Next Session:** Week 12 - Generics, Traits, and Testing
