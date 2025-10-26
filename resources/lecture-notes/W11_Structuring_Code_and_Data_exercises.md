# Week 11: Structuring Code and Data - Interactive Exercises

**Course:** IS4010 - AI-Enhanced Application Development
**Topic:** Rust's Module System, Structs, Enums, Error Handling, and Collections
**Companion Materials:** [Slides](../IS4010_W11_Structuring_Code_and_Data.qmd) | [Lecture Notes](./W11_Structuring_Code_and_Data_notes.md) | [Lab 11](https://github.com/bgreenwell/is4010-course-template/tree/main/labs/lab11)

---

## 🎯 Overview

These hands-on exercises are designed to give you practical experience with Rust's data structuring capabilities. Work through them sequentially - each builds on concepts from the previous exercises.

**How to use these exercises:**
1. Click the Rust Playground link for each exercise
2. Read the instructions and starter code
3. Try to solve it yourself first
4. Use the AI prompting tips if you get stuck
5. Experiment with variations after solving

---

## Exercise 1: Module Organization Basics

**Concept focus:** Creating and using modules with `mod`, `pub`, and `use`

**Exercise:**
You're building a library management system. Create a module structure that organizes book-related functionality.

**Rust Playground:** [Try it here](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021)

**Starter code:**
```rust
// TODO: Create a 'library' module with a 'books' submodule
// The 'books' module should have a public function 'add_book'
// that prints "Adding book to library"

fn main() {
    // TODO: Use the module and call add_book()
    println!("Library management system");
}
```

**Your task:**
1. Define a `library` module
2. Inside it, define a `books` submodule
3. Make `add_book()` function public
4. Import and use the function in `main()`

**AI prompting tips:**
- "How do I create nested modules in Rust?"
- "Explain the difference between `mod`, `pub`, and `use` keywords"
- "Why am I getting 'function is private' error?"

**Learning goals:**
- Understand module hierarchy
- Practice visibility control with `pub`
- Use `use` to bring items into scope

---

## Exercise 2: Building Your First Struct

**Concept focus:** Defining structs with named fields

**Exercise:**
Create a `Book` struct to represent books in the library. Each book should have a title, author, ISBN, and publication year.

**Rust Playground:** [Try it here](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021)

**Starter code:**
```rust
// TODO: Define a Book struct with:
// - title: String
// - author: String
// - isbn: String
// - year: u16

fn main() {
    // TODO: Create a Book instance
    // title: "The Rust Programming Language"
    // author: "Steve Klabnik and Carol Nichols"
    // isbn: "978-1718503106"
    // year: 2023

    // TODO: Print the book's title and author
}
```

**Your task:**
1. Define the `Book` struct with appropriate field types
2. Create an instance in `main()`
3. Access and print the fields

**AI prompting tips:**
- "How do I define a struct with multiple fields in Rust?"
- "What's the difference between String and &str for struct fields?"
- "How do I access struct fields?"

**Learning goals:**
- Define structs with named fields
- Choose appropriate types for fields
- Instantiate and use structs

---

## Exercise 3: Adding Methods to Structs

**Concept focus:** Implementing methods with `impl` blocks

**Exercise:**
Enhance the `Book` struct with methods to display information and check if it's a recent publication.

**Rust Playground:** [Try it here](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021)

**Starter code:**
```rust
struct Book {
    title: String,
    author: String,
    isbn: String,
    year: u16,
}

// TODO: Implement methods for Book:
// 1. display() - prints book info in a nice format
// 2. is_recent() - returns true if published after 2020

fn main() {
    let book = Book {
        title: String::from("The Rust Programming Language"),
        author: String::from("Steve Klabnik and Carol Nichols"),
        isbn: String::from("978-1718503106"),
        year: 2023,
    };

    // TODO: Call display() and is_recent()
}
```

**Your task:**
1. Create an `impl` block for `Book`
2. Add `display(&self)` method that prints formatted information
3. Add `is_recent(&self) -> bool` method
4. Call both methods in `main()`

**AI prompting tips:**
- "How do I add methods to a struct in Rust?"
- "What's the difference between &self, &mut self, and self?"
- "How do I format strings nicely in Rust?"

**Learning goals:**
- Write methods that borrow `self`
- Use methods to encapsulate behavior
- Return values from methods

---

## Exercise 4: Associated Functions (Constructors)

**Concept focus:** Creating "constructor" functions with associated functions

**Exercise:**
Add a `new()` associated function to `Book` to make creating books more convenient.

**Rust Playground:** [Try it here](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021)

**Starter code:**
```rust
struct Book {
    title: String,
    author: String,
    isbn: String,
    year: u16,
}

impl Book {
    // TODO: Create a 'new' associated function
    // Takes title, author, isbn, and year as parameters
    // Returns a Book instance
}

fn main() {
    // TODO: Use Book::new() to create a book
    let book = /* ... */;
    println!("Created: {}", book.title);
}
```

**Your task:**
1. Add `new()` function (no `self` parameter)
2. It should take parameters for all fields
3. Return a `Book` instance
4. Use it in `main()` with `Book::new()`

**AI prompting tips:**
- "What's an associated function in Rust?"
- "How do I create a constructor in Rust?"
- "Why is ::new() called with :: instead of ."

**Learning goals:**
- Understand associated functions vs methods
- Create convenient constructors
- Use `::` syntax for calling associated functions

---

## Exercise 5: Enums for Modeling Choices

**Concept focus:** Defining enums with variants and pattern matching

**Exercise:**
Create a `BookStatus` enum to track whether books are available, checked out, or reserved.

**Rust Playground:** [Try it here](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021)

**Starter code:**
```rust
// TODO: Define BookStatus enum with variants:
// - Available
// - CheckedOut (with due date as String)
// - Reserved (with reserver name as String)

fn print_status(status: /* TODO: parameter type */) {
    // TODO: Use match to print appropriate message
    // for each variant
}

fn main() {
    let status1 = /* TODO: Available variant */;
    let status2 = /* TODO: CheckedOut with "2025-02-15" */;
    let status3 = /* TODO: Reserved with "Alice" */;

    print_status(status1);
    print_status(status2);
    print_status(status3);
}
```

**Your task:**
1. Define `BookStatus` enum with three variants
2. `CheckedOut` and `Reserved` should carry data
3. Implement `print_status()` with `match`
4. Handle all three variants in the match

**AI prompting tips:**
- "How do I define enums with data in Rust?"
- "How does pattern matching work with match?"
- "How do I extract data from enum variants?"

**Learning goals:**
- Create enums with data-carrying variants
- Use pattern matching to handle variants
- Extract data from variants in match arms

---

## Exercise 6: Working with Option<T>

**Concept focus:** Using `Option<T>` to handle optional values

**Exercise:**
Implement a function that searches for a book by ISBN and returns `Option<Book>`.

**Rust Playground:** [Try it here](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021)

**Starter code:**
```rust
struct Book {
    title: String,
    isbn: String,
}

fn find_book_by_isbn(books: &[Book], isbn: &str) -> Option<Book> {
    // TODO: Search through books
    // Return Some(book) if found, None if not found
    // Hint: Use a for loop and clone the book if found
    todo!()
}

fn main() {
    let books = vec![
        Book { title: String::from("Rust Book"), isbn: String::from("123") },
        Book { title: String::from("Python Book"), isbn: String::from("456") },
    ];

    // TODO: Search for ISBN "123" and handle the result
    // Print "Found: [title]" or "Not found"
}
```

**Your task:**
1. Implement `find_book_by_isbn()` to return `Option<Book>`
2. In `main()`, use `match` or `if let` to handle the result
3. Print appropriate message for found/not found

**AI prompting tips:**
- "When should I use Option in Rust?"
- "How do I return Some and None in Rust?"
- "What's the best way to handle Option values?"
- "What's the difference between match and if let?"

**Learning goals:**
- Return `Option<T>` from functions
- Handle `Some` and `None` cases
- Understand when `Option` is appropriate

---

## Exercise 7: Error Handling with Result<T, E>

**Concept focus:** Using `Result<T, E>` for operations that can fail

**Exercise:**
Create a function that validates a book year and returns a `Result`.

**Rust Playground:** [Try it here](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021)

**Starter code:**
```rust
fn validate_year(year: u16) -> Result<u16, String> {
    // TODO: Return Ok(year) if year is between 1450 and 2025
    // Return Err with descriptive message otherwise
    // (Gutenberg printing press invented ~1440)
    todo!()
}

fn main() {
    let years = vec![1500, 2024, 2030, 1200];

    for year in years {
        // TODO: Call validate_year and handle Result
        // Print "Valid: [year]" or "Error: [message]"
    }
}
```

**Your task:**
1. Implement `validate_year()` with validation logic
2. Return `Ok(year)` for valid years
3. Return `Err(String)` with descriptive error for invalid
4. Handle the `Result` in `main()` with `match`

**AI prompting tips:**
- "When should I use Result instead of Option?"
- "How do I create Ok and Err variants?"
- "How do I handle Result with match?"

**Learning goals:**
- Use `Result` for failable operations
- Provide meaningful error messages
- Handle success and error cases

---

## Exercise 8: Working with Vectors

**Concept focus:** Creating and manipulating `Vec<T>` collections

**Exercise:**
Build a simple library catalog using a vector of books.

**Rust Playground:** [Try it here](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021)

**Starter code:**
```rust
struct Book {
    title: String,
    year: u16,
}

fn main() {
    // TODO: Create an empty Vec<Book>
    let mut catalog = /* ... */;

    // TODO: Add 3 books using push()

    // TODO: Print total number of books

    // TODO: Iterate through books and print each title

    // TODO: Filter and print only books from 2020 or later
    // Hint: Use a for loop with if condition
}
```

**Your task:**
1. Create empty vector with `Vec::new()` or `vec![]`
2. Add books with `.push()`
3. Use `.len()` to get count
4. Iterate with `for book in &catalog`
5. Filter recent books

**AI prompting tips:**
- "How do I create and use vectors in Rust?"
- "What's the difference between for book in catalog vs &catalog?"
- "How do I filter a vector in Rust?"

**Learning goals:**
- Create and grow vectors
- Iterate over vector elements
- Borrow vectors in loops

---

## Exercise 9: String vs &str Understanding

**Concept focus:** Understanding owned `String` and borrowed `&str`

**Exercise:**
Practice converting between `String` and `&str` types.

**Rust Playground:** [Try it here](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021)

**Starter code:**
```rust
fn shout(text: &str) -> String {
    // TODO: Convert text to uppercase and return as String
    // Hint: Use .to_uppercase()
    todo!()
}

fn first_word(text: &str) -> &str {
    // TODO: Return the first word (up to first space)
    // Return entire string if no space
    // Hint: Use .find(' ') and string slicing
    todo!()
}

fn main() {
    let owned = String::from("hello world");

    // TODO: Call shout with &owned (String -> &str)
    let loud = /* ... */;
    println!("Loud: {}", loud);

    // TODO: Call first_word with &owned
    let first = /* ... */;
    println!("First word: {}", first);

    // TODO: Call first_word with a string literal
    let first_lit = first_word("rust programming");
    println!("First literal: {}", first_lit);
}
```

**Your task:**
1. Implement `shout()` to return uppercase `String`
2. Implement `first_word()` to return a `&str` slice
3. Call functions with both `String` and `&str` arguments
4. Understand automatic coercion

**AI prompting tips:**
- "What's the difference between String and &str in Rust?"
- "How do I convert between String and &str?"
- "When should I use String vs &str in function parameters?"
- "How does string slicing work in Rust?"

**Learning goals:**
- Distinguish owned vs borrowed strings
- Convert between `String` and `&str`
- Use string slicing
- Understand string literals

---

## Exercise 10: HashMap for Key-Value Storage

**Concept focus:** Using `HashMap<K, V>` for fast lookups

**Exercise:**
Create an inventory system using a `HashMap` to track book quantities by ISBN.

**Rust Playground:** [Try it here](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021)

**Starter code:**
```rust
use std::collections::HashMap;

fn main() {
    // TODO: Create a HashMap<String, u32> for ISBN -> quantity
    let mut inventory: HashMap<String, u32> = /* ... */;

    // TODO: Add these items:
    // ISBN "123" -> 5 copies
    // ISBN "456" -> 3 copies
    // ISBN "789" -> 8 copies

    // TODO: Print total number of different ISBNs

    // TODO: Look up quantity for ISBN "456"
    // Use .get() which returns Option<&u32>
    // Print "ISBN 456: X copies" or "ISBN 456 not found"

    // TODO: Try to get quantity for ISBN "999" (not in map)

    // TODO: Increase quantity for ISBN "123" by 2
    // Hint: Get current value, add 2, insert back

    // TODO: Print all ISBN and quantity pairs
}
```

**Your task:**
1. Create a `HashMap` with `HashMap::new()`
2. Insert key-value pairs with `.insert()`
3. Look up values with `.get()` (returns `Option<&V>`)
4. Update existing values
5. Iterate over entries

**AI prompting tips:**
- "How do I create and use HashMap in Rust?"
- "How do I safely look up values in a HashMap?"
- "How do I update a value in a HashMap?"
- "How do I iterate over HashMap entries?"

**Learning goals:**
- Create and populate `HashMap`
- Perform safe lookups with `Option`
- Update values in place
- Iterate over key-value pairs

---

## 🎯 Bonus Challenge: Putting It All Together

**Exercise:**
Combine everything you've learned to build a mini library management system.

**Requirements:**
1. Create a `Library` struct that contains:
   - A `Vec<Book>` for the catalog
   - A `HashMap<String, BookStatus>` for book statuses (ISBN -> status)
2. Define `Book` struct with title, author, ISBN, year
3. Define `BookStatus` enum (Available, CheckedOut, Reserved)
4. Implement methods on `Library`:
   - `new()` - create empty library
   - `add_book()` - add a book (returns `Result` if duplicate ISBN)
   - `find_by_isbn()` - returns `Option<&Book>`
   - `checkout_book()` - mark book as checked out (returns `Result`)
   - `list_available()` - print all available books

**Rust Playground:** [Start here](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021)

**AI prompting tips:**
- "Help me design a Library struct that manages books and their statuses"
- "How do I check if a HashMap already contains a key?"
- "How do I borrow from a Vec inside a struct method?"
- "Why am I getting borrowing errors with multiple fields?"

**Learning goals:**
- Combine structs, enums, and collections
- Manage ownership in complex data structures
- Implement a complete, working system
- Practice real-world API design

---

## 🚀 Next Steps

After completing these exercises:

1. **Experiment with variations** - modify the exercises to explore edge cases
2. **Test your understanding** - try writing similar code without looking at examples
3. **Apply to Lab 11** - use these patterns in your lab assignment
4. **Use the Rust Playground** - keep experimenting and learning interactively

**Additional practice resources:**
- [Rust by Example - Structs](https://doc.rust-lang.org/rust-by-example/custom_types/structs.html)
- [Rust by Example - Enums](https://doc.rust-lang.org/rust-by-example/custom_types/enum.html)
- [Rust by Example - Error Handling](https://doc.rust-lang.org/rust-by-example/error.html)
- [Rustlings Exercises](https://github.com/rust-lang/rustlings)

---

**Remember:** These concepts are the building blocks of Rust programs. Master them now, and everything else will build naturally on this foundation. Don't rush - understanding is more important than speed!

**Need help?** Post on [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/group-chat-software) or use AI tools with the prompting tips provided above.

---

**Last Updated:** 2025-01-26
**Related Materials:** [Week 11 Slides](../IS4010_W11_Structuring_Code_and_Data.qmd) | [Week 11 Notes](./W11_Structuring_Code_and_Data_notes.md)
