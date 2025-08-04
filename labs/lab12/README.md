# Lab 12: building a command-line application

## Objective

The goal of this lab is to synthesize the concepts from this week to build a complete, real-world command-line (CLI) application in Rust. You will build a simplified version of the popular `grep` tool, which searches files for a specific query.

## Background

Building a CLI tool is a classic exercise for learning a new systems language like Rust. It requires you to handle user input (command-line arguments), interact with the file system, process data, and manage errors—all skills that are fundamental to programming.

-----

## Instructions

1.  Navigate to your `is4010-labs` repository and create a new Rust project for this lab by running: `cargo new lab12 --bin`.
2.  Open the `src/main.rs` file within the `lab12` folder. This is where you will write all your code.
3.  Your program must accept two command-line arguments: a `query` (the string to search for) and a `file_path` (the path to the file to search in).
4.  You will need to read the contents of the file specified by `file_path`.
5.  Your program should then iterate over each line of the file's contents and check if the line contains the `query` string.
6.  If a line contains the query, it should be printed to the console.
7.  Use `Result` and the `?` operator to handle potential errors, such as the file not being found.
8.  To test your program's executable, create a simple `.txt` file inside your `lab12` folder (e.g., `poem.txt`) with some sample text. You can then run your program from the terminal like this: `cargo run -- your_search_query poem.txt`.
9.  To verify your core logic against the automated tests, run `cargo test`.

### AI partnership

This is a great opportunity to use your AI partner. If you get stuck, try asking it a specific question like:

  * "How can I parse and validate command-line arguments in Rust?"
  * "What is the best way to handle file I/O errors in a Rust function that returns a `Result`?"
  * "Write a Rust function that takes a string slice for a query and another for contents, and returns a vector of matching lines."

-----

## Adding the test suite

Append the following test module to the bottom of your `src/main.rs` file. This will test the core search logic of your application.

```rust
#[cfg(test)]
mod tests {
    // Assuming your search function is in scope and named `search`.
    // You may need to make it public (`pub fn search...`) for the tests to see it.
    use super::search; 

    #[test]
    fn one_result() {
        let query = "duct";
        let contents = "\
Rust:
safe, fast, productive.
Pick three.
Duct tape.";
        assert_eq!(vec!["safe, fast, productive."], search(query, contents));
    }

    #[test]
    fn case_sensitive() {
        let query = "rUsT";
        let contents = "\
Rust:
safe, fast, productive.
Trust me.";
        assert_eq!(Vec::<&str>::new(), search(query, contents));
    }
}
```

-----

## Submission

For this lab, you will commit and push your entire `lab12` project folder to your `is4010-labs` GitHub repository.

```
# From the root of your is4010-labs directory
git add lab12/
git commit -m "Complete lab 12"
git push origin main
```