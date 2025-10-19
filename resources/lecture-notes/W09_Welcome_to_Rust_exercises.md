# Week 09: Welcome to Rust - Interactive Exercises

**Course:** IS4010 - AI-Enhanced Application Development
**Topic:** Introduction to Rust
**Companion Materials:** [Slides](../IS4010_W09_Welcome_to_Rust.qmd) | [Lecture Notes](./W09_Welcome_to_Rust_notes.md) | [Lab 09](https://github.com/bgreenwell/is4010-course-template/tree/main/labs/lab09)

---

## 🎯 About These Exercises

These hands-on exercises use the [Rust Playground](https://play.rust-lang.org/) to let you experiment with Rust code directly in your browser - no installation required! Each exercise includes a pre-filled Playground link with starter code. Simply click the link, modify the code as instructed, and click "Run" to see the results.

**How to use these exercises:**
1. Click the Playground link to open the starter code
2. Read the instructions and modify the code
3. Click "Run" to compile and execute
4. Experiment with variations - try breaking things to learn!
5. Use the "Share" button to save your solutions

---

## Exercise 1: Hello, World! Variations

**Objective:** Get comfortable with Rust's `println!` macro and basic syntax.

[▶ Open in Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++println%21%28%22Hello%2C+World%21%22%29%3B%0A%7D)

### Your Tasks:

1. **Basic modification**: Change the message to print your name
2. **Multiple lines**: Add a second `println!` to print your favorite programming language
3. **Variables**: Create a variable to store your name and print it using `{}`

**Example:**
```rust
fn main() {
    let name = "Alice";
    println!("Hello, {}!", name);
    println!("Welcome to Rust!");
}
```

### Your Turn:

Try creating variables for your name, age, and favorite hobby, then print them all in a formatted message.

<details>
<summary>💡 Click for Solution</summary>

[▶ Solution in Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+name+%3D+%22Alice%22%3B%0A++++let+age+%3D+20%3B%0A++++let+hobby+%3D+%22coding%22%3B%0A++++println%21%28%22Hi%2C+I%27m+%7B%7D+and+I%27m+%7B%7D+years+old.%22%2C+name%2C+age%29%3B%0A++++println%21%28%22I+love+%7B%7D%21%22%2C+hobby%29%3B%0A%7D)

</details>

---

## Exercise 2: Variables and Mutability

**Objective:** Understand Rust's immutability-by-default philosophy.

[▶ Open in Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+x+%3D+5%3B%0A++++println%21%28%22The+value+of+x+is%3A+%7B%7D%22%2C+x%29%3B%0A++++%2F%2F+Uncomment+the+next+line+to+see+the+error%0A++++%2F%2F+x+%3D+6%3B%0A%7D)

### Your Tasks:

1. **Observe immutability**: Uncomment the `x = 6;` line and click "Run". Read the error message carefully!
2. **Make it mutable**: Fix the code by adding `mut` to make `x` mutable
3. **Practice**: Create both a mutable and immutable variable for temperature

**Expected behavior:**
- Immutable variables cannot be changed
- Mutable variables (with `mut`) can be reassigned

### Your Turn:

Create a program that:
- Starts with a score of 0 (mutable)
- Increments the score by 10
- Prints the final score

<details>
<summary>💡 Click for Solution</summary>

[▶ Solution in Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+mut+score+%3D+0%3B%0A++++println%21%28%22Starting+score%3A+%7B%7D%22%2C+score%29%3B%0A++++%0A++++score+%3D+score+%2B+10%3B%0A++++println%21%28%22Updated+score%3A+%7B%7D%22%2C+score%29%3B%0A++++%0A++++score+%2B%3D+5%3B+%2F%2F+Shorthand+for+score+%3D+score+%2B+5%0A++++println%21%28%22Final+score%3A+%7B%7D%22%2C+score%29%3B%0A%7D)

</details>

---

## Exercise 3: Data Types - Integers and Floats

**Objective:** Practice working with different numeric types.

[▶ Open in Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+age%3A+i32+%3D+20%3B%0A++++let+temperature%3A+f64+%3D+72.5%3B%0A++++println%21%28%22Age%3A+%7B%7D%2C+Temperature%3A+%7B%7D%22%2C+age%2C+temperature%29%3B%0A%7D)

### Your Tasks:

1. **Explore integer types**: Try `i8`, `i32`, `i64`, `u32` (unsigned)
2. **Type inference**: Remove the type annotations and let Rust infer the types
3. **Arithmetic**: Calculate the sum, difference, product, and quotient of two numbers

**Key concepts:**
- `i` prefix = signed integers (can be negative)
- `u` prefix = unsigned integers (positive only)
- `f32`, `f64` = floating-point numbers

### Your Turn:

Create a simple calculator that:
- Defines two numbers: `a` and `b`
- Prints their sum, difference, product, and quotient
- Use meaningful variable names and proper types

<details>
<summary>💡 Click for Solution</summary>

[▶ Solution in Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+num1%3A+f64+%3D+10.0%3B%0A++++let+num2%3A+f64+%3D+3.0%3B%0A++++%0A++++let+sum+%3D+num1+%2B+num2%3B%0A++++let+difference+%3D+num1+-+num2%3B%0A++++let+product+%3D+num1+*+num2%3B%0A++++let+quotient+%3D+num1+%2F+num2%3B%0A++++%0A++++println%21%28%22%7B%7D+%2B+%7B%7D+%3D+%7B%7D%22%2C+num1%2C+num2%2C+sum%29%3B%0A++++println%21%28%22%7B%7D+-+%7B%7D+%3D+%7B%7D%22%2C+num1%2C+num2%2C+difference%29%3B%0A++++println%21%28%22%7B%7D+*+%7B%7D+%3D+%7B%7D%22%2C+num1%2C+num2%2C+product%29%3B%0A++++println%21%28%22%7B%7D+%2F+%7B%7D+%3D+%7B%7D%22%2C+num1%2C+num2%2C+quotient%29%3B%0A%7D)

</details>

---

## Exercise 4: Booleans and Characters

**Objective:** Work with boolean and character types.

[▶ Open in Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+is_student%3A+bool+%3D+true%3B%0A++++let+grade%3A+char+%3D+%27A%27%3B%0A++++println%21%28%22Student%3A+%7B%7D%2C+Grade%3A+%7B%7D%22%2C+is_student%2C+grade%29%3B%0A%7D)

### Your Tasks:

1. **Boolean operations**: Try `&&` (and), `||` (or), `!` (not)
2. **Comparisons**: Use `==`, `!=`, `<`, `>`, `<=`, `>=`
3. **Characters**: Try Unicode characters like emoji '😀'

**Remember:**
- Booleans are `true` or `false`
- Characters use single quotes `'a'`
- Strings use double quotes `"hello"`

### Your Turn:

Create a program that:
- Defines a score variable
- Uses comparison to create a boolean `is_passing` (score >= 60)
- Prints whether the student is passing

<details>
<summary>💡 Click for Solution</summary>

[▶ Solution in Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+score+%3D+75%3B%0A++++let+is_passing+%3D+score+%3E%3D+60%3B%0A++++%0A++++println%21%28%22Score%3A+%7B%7D%22%2C+score%29%3B%0A++++println%21%28%22Passing%3A+%7B%7D%22%2C+is_passing%29%3B%0A++++%0A++++%2F%2F+Bonus%3A+using+if+expression+%28preview+of+next+week%29%0A++++let+status+%3D+if+is_passing+%7B+%22PASS%22+%7D+else+%7B+%22FAIL%22+%7D%3B%0A++++println%21%28%22Status%3A+%7B%7D%22%2C+status%29%3B%0A%7D)

</details>

---

## Exercise 5: Tuples

**Objective:** Practice creating and destructuring tuples.

[▶ Open in Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+person%3A+%28%26str%2C+i32%2C+f64%29+%3D+%28%22Alice%22%2C+20%2C+3.8%29%3B%0A++++println%21%28%22Person%3A+%7B%3A%3F%7D%22%2C+person%29%3B%0A%7D)

### Your Tasks:

1. **Access elements**: Use `.0`, `.1`, `.2` to access tuple elements
2. **Destructuring**: Use pattern matching: `let (name, age, gpa) = person;`
3. **Create your own**: Make a tuple representing a book (title, author, year)

**Key concepts:**
- Tuples can hold different types
- Elements accessed by position
- Destructuring extracts values into variables

### Your Turn:

Create a program that:
- Defines a tuple for a student: (name, ID, GPA)
- Destructures the tuple into separate variables
- Prints each value on its own line

<details>
<summary>💡 Click for Solution</summary>

[▶ Solution in Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+student+%3D+%28%22Bob+Smith%22%2C+12345%2C+3.7%29%3B%0A++++%0A++++%2F%2F+Method+1%3A+Access+by+index%0A++++println%21%28%22Name%3A+%7B%7D%22%2C+student.0%29%3B%0A++++println%21%28%22ID%3A+%7B%7D%22%2C+student.1%29%3B%0A++++println%21%28%22GPA%3A+%7B%7D%22%2C+student.2%29%3B%0A++++%0A++++%2F%2F+Method+2%3A+Destructuring%0A++++let+%28name%2C+id%2C+gpa%29+%3D+student%3B%0A++++println%21%28%22%5CnStudent%3A+%7B%7D+%28%23%7B%7D%29+has+GPA%3A+%7B%7D%22%2C+name%2C+id%2C+gpa%29%3B%0A%7D)

</details>

---

## Exercise 6: Arrays

**Objective:** Work with fixed-size collections.

[▶ Open in Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+scores%3A+%5Bi32%3B+5%5D+%3D+%5B95%2C+87%2C+92%2C+88%2C+91%5D%3B%0A++++println%21%28%22Scores%3A+%7B%3A%3F%7D%22%2C+scores%29%3B%0A%7D)

### Your Tasks:

1. **Access elements**: Use indexing `scores[0]`, `scores[1]`, etc.
2. **Iterate**: Try a for loop: `for score in scores { ... }`
3. **Array creation shorthand**: Create an array of ten zeros: `[0; 10]`

**Remember:**
- Arrays have fixed size
- All elements must be the same type
- Index starts at 0

### Your Turn:

Create a program that:
- Defines an array of 5 test scores
- Prints the first and last score
- Calculates and prints the average

<details>
<summary>💡 Click for Solution</summary>

[▶ Solution in Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+scores+%3D+%5B88%2C+92%2C+75%2C+95%2C+89%5D%3B%0A++++%0A++++println%21%28%22First+score%3A+%7B%7D%22%2C+scores%5B0%5D%29%3B%0A++++println%21%28%22Last+score%3A+%7B%7D%22%2C+scores%5B4%5D%29%3B%0A++++%0A++++let+sum%3A+i32+%3D+scores.iter%28%29.sum%28%29%3B%0A++++let+average+%3D+sum+as+f64+%2F+scores.len%28%29+as+f64%3B%0A++++%0A++++println%21%28%22Average%3A+%7B%3A.2%7D%22%2C+average%29%3B+%2F%2F+.2+means+2+decimal+places%0A%7D)

</details>

---

## Exercise 7: Functions

**Objective:** Write functions with type annotations and return values.

[▶ Open in Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+greet%28name%3A+%26str%29+%7B%0A++++println%21%28%22Hello%2C+%7B%7D%21%22%2C+name%29%3B%0A%7D%0A%0Afn+main%28%29+%7B%0A++++greet%28%22Alice%22%29%3B%0A%7D)

### Your Tasks:

1. **Add a return type**: Modify `greet` to return a String instead of printing
2. **Create a math function**: Write `fn add(a: i32, b: i32) -> i32`
3. **Expression vs statement**: Practice returning without the `return` keyword

**Key concepts:**
- Parameters must have type annotations
- Return type specified with `->`
- Last expression without semicolon is automatically returned

### Your Turn:

Create these functions:
1. `multiply(a: i32, b: i32) -> i32` - returns the product
2. `is_even(n: i32) -> bool` - returns true if n is even
3. `max(a: i32, b: i32) -> i32` - returns the larger number

<details>
<summary>💡 Click for Solution</summary>

[▶ Solution in Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+multiply%28a%3A+i32%2C+b%3A+i32%29+-%3E+i32+%7B%0A++++a+*+b%0A%7D%0A%0Afn+is_even%28n%3A+i32%29+-%3E+bool+%7B%0A++++n+%25+2+%3D%3D+0%0A%7D%0A%0Afn+max%28a%3A+i32%2C+b%3A+i32%29+-%3E+i32+%7B%0A++++if+a+%3E+b+%7B%0A++++++++a%0A++++%7D+else+%7B%0A++++++++b%0A++++%7D%0A%7D%0A%0Afn+main%28%29+%7B%0A++++println%21%28%225+*+7+%3D+%7B%7D%22%2C+multiply%285%2C+7%29%29%3B%0A++++println%21%28%22Is+10+even%3F+%7B%7D%22%2C+is_even%2810%29%29%3B%0A++++println%21%28%22Is+7+even%3F+%7B%7D%22%2C+is_even%287%29%29%3B%0A++++println%21%28%22Max+of+42+and+17%3A+%7B%7D%22%2C+max%2842%2C+17%29%29%3B%0A%7D)

</details>

---

## Exercise 8: Introduction to Testing

**Objective:** Write simple tests to verify your functions work correctly.

[▶ Open in Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+add%28a%3A+i32%2C+b%3A+i32%29+-%3E+i32+%7B%0A++++a+%2B+b%0A%7D%0A%0A%23%5Bcfg%28test%29%5D%0Amod+tests+%7B%0A++++use+super%3A%3A*%3B%0A%0A++++%23%5Btest%5D%0A++++fn+test_add%28%29+%7B%0A++++++++assert_eq%21%28add%282%2C+3%29%2C+5%29%3B%0A++++%7D%0A%7D%0A%0Afn+main%28%29+%7B%0A++++println%21%28%222+%2B+3+%3D+%7B%7D%22%2C+add%282%2C+3%29%29%3B%0A%7D)

**Note:** Click "Run" to execute `main()`, or click the "▶" next to "Tests" dropdown and select "test_add" to run the test.

### Your Tasks:

1. **Add more tests**: Test with negative numbers, zero, large numbers
2. **Try `assert!`**: Write a test using `assert!(is_even(4))`
3. **Test edge cases**: What happens with the maximum i32 value?

**Key concepts:**
- `#[test]` attribute marks test functions
- `assert_eq!(left, right)` checks equality
- Tests should cover normal cases AND edge cases

### Your Turn:

Write a function `fn square(n: i32) -> i32` that returns n², then write three tests:
1. Test that `square(5)` returns `25`
2. Test that `square(0)` returns `0`
3. Test that `square(-3)` returns `9`

<details>
<summary>💡 Click for Solution</summary>

[▶ Solution in Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+square%28n%3A+i32%29+-%3E+i32+%7B%0A++++n+*+n%0A%7D%0A%0A%23%5Bcfg%28test%29%5D%0Amod+tests+%7B%0A++++use+super%3A%3A*%3B%0A%0A++++%23%5Btest%5D%0A++++fn+test_square_positive%28%29+%7B%0A++++++++assert_eq%21%28square%285%29%2C+25%29%3B%0A++++%7D%0A++++%0A++++%23%5Btest%5D%0A++++fn+test_square_zero%28%29+%7B%0A++++++++assert_eq%21%28square%280%29%2C+0%29%3B%0A++++%7D%0A++++%0A++++%23%5Btest%5D%0A++++fn+test_square_negative%28%29+%7B%0A++++++++assert_eq%21%28square%28-3%29%2C+9%29%3B%0A++++%7D%0A%7D%0A%0Afn+main%28%29+%7B%0A++++println%21%28%22square%285%29+%3D+%7B%7D%22%2C+square%285%29%29%3B%0A++++println%21%28%22square%280%29+%3D+%7B%7D%22%2C+square%280%29%29%3B%0A++++println%21%28%22square%28-3%29+%3D+%7B%7D%22%2C+square%28-3%29%29%3B%0A%7D)

</details>

---

## 🎓 Challenge Exercise: Temperature Converter

**Objective:** Combine everything you've learned into a mini-project.

### Requirements:

Create a temperature conversion program with:
1. Two functions:
   - `fn celsius_to_fahrenheit(c: f64) -> f64`
   - `fn fahrenheit_to_celsius(f: f64) -> f64`
2. Test both functions with at least 2 test cases each
3. In `main()`, demonstrate conversions with sample temperatures

**Formulas:**
- F = (C × 9/5) + 32
- C = (F - 32) × 5/9

**Starter code:**

[▶ Start Challenge in Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+celsius_to_fahrenheit%28c%3A+f64%29+-%3E+f64+%7B%0A++++%2F%2F+TODO%3A+Implement+this%0A++++0.0%0A%7D%0A%0Afn+fahrenheit_to_celsius%28f%3A+f64%29+-%3E+f64+%7B%0A++++%2F%2F+TODO%3A+Implement+this%0A++++0.0%0A%7D%0A%0A%23%5Bcfg%28test%29%5D%0Amod+tests+%7B%0A++++use+super%3A%3A*%3B%0A++++%0A++++%23%5Btest%5D%0A++++fn+test_celsius_to_fahrenheit%28%29+%7B%0A++++++++%2F%2F+TODO%3A+Write+tests%0A++++%7D%0A++++%0A++++%23%5Btest%5D%0A++++fn+test_fahrenheit_to_celsius%28%29+%7B%0A++++++++%2F%2F+TODO%3A+Write+tests%0A++++%7D%0A%7D%0A%0Afn+main%28%29+%7B%0A++++%2F%2F+TODO%3A+Demonstrate+conversions%0A++++println%21%28%22Temperature+Converter%22%29%3B%0A%7D)

<details>
<summary>💡 Click for Complete Solution</summary>

[▶ Full Solution in Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+celsius_to_fahrenheit%28c%3A+f64%29+-%3E+f64+%7B%0A++++%28c+*+9.0+%2F+5.0%29+%2B+32.0%0A%7D%0A%0Afn+fahrenheit_to_celsius%28f%3A+f64%29+-%3E+f64+%7B%0A++++%28f+-+32.0%29+*+5.0+%2F+9.0%0A%7D%0A%0A%23%5Bcfg%28test%29%5D%0Amod+tests+%7B%0A++++use+super%3A%3A*%3B%0A++++%0A++++%23%5Btest%5D%0A++++fn+test_c_to_f_freezing%28%29+%7B%0A++++++++assert_eq%21%28celsius_to_fahrenheit%280.0%29%2C+32.0%29%3B%0A++++%7D%0A++++%0A++++%23%5Btest%5D%0A++++fn+test_c_to_f_boiling%28%29+%7B%0A++++++++assert_eq%21%28celsius_to_fahrenheit%28100.0%29%2C+212.0%29%3B%0A++++%7D%0A++++%0A++++%23%5Btest%5D%0A++++fn+test_f_to_c_freezing%28%29+%7B%0A++++++++assert_eq%21%28fahrenheit_to_celsius%2832.0%29%2C+0.0%29%3B%0A++++%7D%0A++++%0A++++%23%5Btest%5D%0A++++fn+test_f_to_c_boiling%28%29+%7B%0A++++++++assert_eq%21%28fahrenheit_to_celsius%28212.0%29%2C+100.0%29%3B%0A++++%7D%0A%7D%0A%0Afn+main%28%29+%7B%0A++++let+temp_c+%3D+25.0%3B%0A++++let+temp_f+%3D+celsius_to_fahrenheit%28temp_c%29%3B%0A++++println%21%28%22%7B%7D%C2%B0C+%3D+%7B%7D%C2%B0F%22%2C+temp_c%2C+temp_f%29%3B%0A++++%0A++++let+temp_f2+%3D+77.0%3B%0A++++let+temp_c2+%3D+fahrenheit_to_celsius%28temp_f2%29%3B%0A++++println%21%28%22%7B%7D%C2%B0F+%3D+%7B%3A.2%7D%C2%B0C%22%2C+temp_f2%2C+temp_c2%29%3B%0A%7D)

</details>

---

## 📚 Additional Resources

- [The Rust Programming Language Book](https://doc.rust-lang.org/book/) - Chapter 3 covers all these concepts in depth
- [Rust by Example](https://doc.rust-lang.org/rust-by-example/) - Learn through annotated code examples
- [Rustlings](https://github.com/rust-lang/rustlings/) - Interactive exercises to practice Rust syntax
- [Rust Playground](https://play.rust-lang.org/) - Experiment anytime, anywhere

## 🎯 Next Steps

After completing these exercises:
1. Move on to [Lab 09](https://github.com/bgreenwell/is4010-course-template/tree/main/labs/lab09) to install Rust locally and create your first Cargo project
2. Review the [Week 09 Lecture Notes](./W09_Welcome_to_Rust_notes.md) for concept summaries
3. Experiment with the [Rust Book](https://doc.rust-lang.org/book/ch03-00-common-programming-concepts.html) for deeper understanding

---

**Happy Coding!** 🦀

*Remember: The Rust compiler is your friend. Read error messages carefully - they often tell you exactly how to fix the problem!*
