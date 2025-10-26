# Week 10: The Soul of Rust - Interactive Exercises

**Course:** IS4010 - AI-Enhanced Application Development
**Topic:** Hands-on Practice with Ownership, Borrowing, and Lifetimes
**Companion Materials:** [Slides](../IS4010_W10_The_Soul_of_Rust.qmd) | [Lecture Notes](./W10_The_Soul_of_Rust_notes.md) | [Lab 10](https://github.com/bgreenwell/is4010-course-template/tree/main/labs/lab10)

---

## 📋 How to Use These Exercises

Each exercise includes:
- **Concept focus:** What you're practicing
- **Exercise description:** What to implement or fix
- **Rust Playground link:** Click to start coding in your browser
- **AI prompting tips:** Effective ways to get help if you're stuck
- **Learning goals:** What you should understand after completing the exercise

**Recommended approach:**
1. Read the exercise description
2. Try to solve it on your own first (use the Playground link)
3. If stuck, read the Rust compiler error carefully
4. Use the AI prompting tips to get unstuck
5. Understand the solution - don't just copy-paste!

---

## Exercise 1: Understanding Moves

### Concept Focus
Basic ownership transfer (move semantics)

### Exercise Description
Fix the code below so it compiles. The problem is that `s1` is used after its ownership has moved to `s2`.

```rust
fn main() {
    let s1 = String::from("hello");
    let s2 = s1;
    println!("s1: {}, s2: {}", s1, s2);
}
```

[🔗 Try it in Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+s1+%3D+String%3A%3Afrom%28%22hello%22%29%3B%0A++++let+s2+%3D+s1%3B%0A++++println%21%28%22s1%3A+%7B%7D%2C+s2%3A+%7B%7D%22%2C+s1%2C+s2%29%3B%0A%7D)

### Possible Solutions
- Option A: Clone `s1` so both variables own their own data
- Option B: Keep `s1` as the owner and create a reference for `s2`
- Option C: Don't use `s1` after the move

### AI Prompting Tips
If you're stuck:
- *"Why does Rust complain about using s1 after moving it to s2?"*
- *"What's the difference between move and copy in Rust? Why does String move?"*
- *"How can I use a String value in multiple places without moving it?"*

### Learning Goals
- ✅ Understand that `String` doesn't implement `Copy`
- ✅ Recognize "value used after move" errors
- ✅ Know the difference between `clone()` and borrowing

---

## Exercise 2: Copy vs. Move

### Concept Focus
Understanding which types copy and which types move

### Exercise Description
Predict which of these code blocks will compile. Then test your predictions in Rust Playground.

```rust
// Block A
fn main() {
    let x = 5;
    let y = x;
    println!("x: {}, y: {}", x, y);
}

// Block B
fn main() {
    let s1 = String::from("hello");
    let s2 = s1;
    println!("s1: {}, s2: {}", s1, s2);
}

// Block C
fn main() {
    let tuple = (5, String::from("hello"));
    let tuple2 = tuple;
    println!("{:?}", tuple);
}
```

[🔗 Try Block A in Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+x+%3D+5%3B%0A++++let+y+%3D+x%3B%0A++++println%21%28%22x%3A+%7B%7D%2C+y%3A+%7B%7D%22%2C+x%2C+y%29%3B%0A%7D)

[🔗 Try Block B in Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+s1+%3D+String%3A%3Afrom%28%22hello%22%29%3B%0A++++let+s2+%3D+s1%3B%0A++++println%21%28%22s1%3A+%7B%7D%2C+s2%3A+%7B%7D%22%2C+s1%2C+s2%29%3B%0A%7D)

[🔗 Try Block C in Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+tuple+%3D+%285%2C+String%3A%3Afrom%28%22hello%22%29%29%3B%0A++++let+tuple2+%3D+tuple%3B%0A++++println%21%28%22%7B%3A%3F%7D%22%2C+tuple%29%3B%0A%7D)

### AI Prompting Tips
- *"Which Rust types implement the Copy trait and why?"*
- *"Why does a tuple containing a String move instead of copy?"*
- *"Explain the difference between stack and heap memory in the context of Copy vs Move"*

### Learning Goals
- ✅ Know which primitive types implement `Copy`
- ✅ Understand that `Copy` requires all fields to be `Copy`
- ✅ Recognize the relationship between heap allocation and move semantics

---

## Exercise 3: Borrowing Basics

### Concept Focus
Using immutable references to avoid moves

### Exercise Description
Implement the `calculate_length` function that takes a reference to a `String` and returns its length. The function should NOT take ownership of the string.

```rust
fn main() {
    let s = String::from("hello world");
    let len = calculate_length(/* your code here */);
    println!("The length of '{}' is {}.", s, len);
}

fn calculate_length(/* your function signature here */) -> usize {
    // your implementation here
}
```

[🔗 Try it in Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+s+%3D+String%3A%3Afrom%28%22hello+world%22%29%3B%0A++++let+len+%3D+calculate_length%28%2F*+your+code+here+*%2F%29%3B%0A++++println%21%28%22The+length+of+%27%7B%7D%27+is+%7B%7D.%22%2C+s%2C+len%29%3B%0A%7D%0A%0Afn+calculate_length%28%2F*+your+function+signature+here+*%2F%29+-%3E+usize+%7B%0A++++%2F%2F+your+implementation+here%0A%7D)

### AI Prompting Tips
- *"How do I pass a String to a function without transferring ownership?"*
- *"What's the syntax for a function parameter that borrows a String?"*
- *"Explain the difference between &String and String as a parameter"*

### Learning Goals
- ✅ Use the `&` operator to create references
- ✅ Understand that references don't take ownership
- ✅ Know when to use `&T` in function signatures

---

## Exercise 4: Mutable References

### Concept Focus
Using mutable references to modify borrowed data

### Exercise Description
Fix the `append_world` function to modify the string in place using a mutable reference. The function should add ", world!" to the end of the string.

```rust
fn main() {
    let mut s = String::from("hello");
    append_world(/* your code here */);
    println!("{}", s); // Should print: hello, world!
}

fn append_world(/* your function signature here */) {
    // your implementation here
    // Hint: use push_str method
}
```

[🔗 Try it in Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+mut+s+%3D+String%3A%3Afrom%28%22hello%22%29%3B%0A++++append_world%28%2F*+your+code+here+*%2F%29%3B%0A++++println%21%28%22%7B%7D%22%2C+s%29%3B%0A%7D%0A%0Afn+append_world%28%2F*+your+function+signature+here+*%2F%29+%7B%0A++++%2F%2F+your+implementation+here%0A%7D)

### AI Prompting Tips
- *"How do I create a mutable reference in Rust?"*
- *"What's the difference between &String and &mut String?"*
- *"Why do I need both 'let mut' and '&mut'?"*

### Learning Goals
- ✅ Create mutable references with `&mut`
- ✅ Understand that the variable must be declared `mut`
- ✅ Know when to use mutable vs immutable references

---

## Exercise 5: The Borrow Checker - Multiple Mutable References

### Concept Focus
Understanding the "one mutable reference at a time" rule

### Exercise Description
This code has a borrow checker error. Fix it by restructuring the code to follow Rust's borrowing rules.

```rust
fn main() {
    let mut s = String::from("hello");

    let r1 = &mut s;
    let r2 = &mut s;  // Problem: two mutable references!

    println!("{}, {}", r1, r2);
}
```

[🔗 Try it in Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+mut+s+%3D+String%3A%3Afrom%28%22hello%22%29%3B%0A++++%0A++++let+r1+%3D+%26mut+s%3B%0A++++let+r2+%3D+%26mut+s%3B%0A++++%0A++++println%21%28%22%7B%7D%2C+%7B%7D%22%2C+r1%2C+r2%29%3B%0A%7D)

### Possible Approaches
- Use scopes to limit the lifetime of `r1`
- Use only one mutable reference
- Refactor to not need both references simultaneously

### AI Prompting Tips
- *"Why can't I have two mutable references to the same data?"*
- *"How do I fix 'cannot borrow as mutable more than once'?"*
- *"Explain Rust's borrowing rules for mutable references"*

### Learning Goals
- ✅ Understand the "one mutable reference" rule
- ✅ Use scopes to limit reference lifetimes
- ✅ Recognize that this rule prevents data races

---

## Exercise 6: The Borrow Checker - Mixing Mutable and Immutable

### Concept Focus
Understanding the "no mixing" rule for references

### Exercise Description
Fix this code that tries to have both immutable and mutable references active at the same time.

```rust
fn main() {
    let mut s = String::from("hello");

    let r1 = &s;      // Immutable reference
    let r2 = &s;      // Another immutable reference (OK)
    let r3 = &mut s;  // Mutable reference (ERROR!)

    println!("{}, {}, {}", r1, r2, r3);
}
```

[🔗 Try it in Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+mut+s+%3D+String%3A%3Afrom%28%22hello%22%29%3B%0A++++%0A++++let+r1+%3D+%26s%3B%0A++++let+r2+%3D+%26s%3B%0A++++let+r3+%3D+%26mut+s%3B%0A++++%0A++++println%21%28%22%7B%7D%2C+%7B%7D%2C+%7B%7D%22%2C+r1%2C+r2%2C+r3%29%3B%0A%7D)

### Hint
Remember that with Non-Lexical Lifetimes (NLL), a reference's scope ends at its last use, not at the closing brace.

### AI Prompting Tips
- *"Why can't I borrow as mutable while immutable borrows exist?"*
- *"Explain Non-Lexical Lifetimes in Rust"*
- *"How do I restructure code to satisfy the borrow checker?"*

### Learning Goals
- ✅ Understand the "XOR" rule: mutable XOR immutable
- ✅ Leverage Non-Lexical Lifetimes
- ✅ Restructure code to eliminate conflicts

---

## Exercise 7: Preventing Dangling References

### Concept Focus
Understanding how Rust prevents use-after-free bugs

### Exercise Description
This code attempts to return a reference to data that will be dropped. Fix it by returning the owned value instead of a reference.

```rust
fn dangle() -> &String {
    let s = String::from("hello");
    &s  // ERROR: s will be dropped, but we're returning a reference to it!
}

fn main() {
    let reference = dangle();
    println!("{}", reference);
}
```

[🔗 Try it in Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+dangle%28%29+-%3E+%26String+%7B%0A++++let+s+%3D+String%3A%3Afrom%28%22hello%22%29%3B%0A++++%26s%0A%7D%0A%0Afn+main%28%29+%7B%0A++++let+reference+%3D+dangle%28%29%3B%0A++++println%21%28%22%7B%7D%22%2C+reference%29%3B%0A%7D)

### AI Prompting Tips
- *"What is a dangling reference and why is it dangerous?"*
- *"How does Rust prevent use-after-free bugs?"*
- *"When should I return a reference vs an owned value from a function?"*

### Learning Goals
- ✅ Understand dangling references
- ✅ Know when to return owned values vs references
- ✅ Appreciate how Rust prevents use-after-free at compile time

---

## Exercise 8: Basic Lifetimes

### Concept Focus
Understanding when lifetime annotations are needed

### Exercise Description
Implement the `longest` function that returns the longer of two string slices. You'll need to add lifetime annotations.

```rust
fn main() {
    let string1 = String::from("long string is long");
    let string2 = String::from("short");

    let result = longest(&string1, &string2);
    println!("The longest string is: {}", result);
}

fn longest(/* add lifetime parameter and signatures */) -> /* add return type */ {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```

[🔗 Try it in Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++let+string1+%3D+String%3A%3Afrom%28%22long+string+is+long%22%29%3B%0A++++let+string2+%3D+String%3A%3Afrom%28%22short%22%29%3B%0A++++%0A++++let+result+%3D+longest%28%26string1%2C+%26string2%29%3B%0A++++println%21%28%22The+longest+string+is%3A+%7B%7D%22%2C+result%29%3B%0A%7D%0A%0Afn+longest%28%2F*+add+parameters+*%2F%29+-%3E+%2F*+add+return+type+*%2F+%7B%0A++++if+x.len%28%29+%3E+y.len%28%29+%7B%0A++++++++x%0A++++%7D+else+%7B%0A++++++++y%0A++++%7D%0A%7D)

### AI Prompting Tips
- *"Why does this function need a lifetime annotation?"*
- *"What does 'a mean in Rust function signatures?"*
- *"How do I add lifetime parameters to a function?"*
- *"Explain Rust lifetime elision rules"*

### Learning Goals
- ✅ Understand when explicit lifetimes are needed
- ✅ Use lifetime syntax: `'a`, `'b`, etc.
- ✅ Know that lifetimes describe relationships, not durations

---

## Exercise 9: Scope and Ownership

### Concept Focus
Understanding scope-based automatic cleanup

### Exercise Description
Predict when each `drop()` will be called in this code. Then uncomment the println statements and see which ones cause errors.

```rust
fn main() {
    {
        let s1 = String::from("inner scope");
        // println!("s1: {}", s1);
    } // s1 dropped here

    // println!("s1: {}", s1); // Will this work?

    let s2 = String::from("outer scope");
    // println!("s2: {}", s2);

    {
        let s3 = String::from("nested");
        // println!("s2: {}, s3: {}", s2, s3);
    } // s3 dropped here

    // println!("s2: {}, s3: {}", s2, s3); // Will this work?
} // s2 dropped here
```

[🔗 Try it in Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+main%28%29+%7B%0A++++%7B%0A++++++++let+s1+%3D+String%3A%3Afrom%28%22inner+scope%22%29%3B%0A++++++++%2F%2F+println%21%28%22s1%3A+%7B%7D%22%2C+s1%29%3B%0A++++%7D%0A++++%0A++++%2F%2F+println%21%28%22s1%3A+%7B%7D%22%2C+s1%29%3B%0A++++%0A++++let+s2+%3D+String%3A%3Afrom%28%22outer+scope%22%29%3B%0A++++%2F%2F+println%21%28%22s2%3A+%7B%7D%22%2C+s2%29%3B%0A++++%0A++++%7B%0A++++++++let+s3+%3D+String%3A%3Afrom%28%22nested%22%29%3B%0A++++++++%2F%2F+println%21%28%22s2%3A+%7B%7D%2C+s3%3A+%7B%7D%22%2C+s2%2C+s3%29%3B%0A++++%7D%0A++++%0A++++%2F%2F+println%21%28%22s2%3A+%7B%7D%2C+s3%3A+%7B%7D%22%2C+s2%2C+s3%29%3B%0A%7D)

### AI Prompting Tips
- *"Explain variable scope and automatic cleanup in Rust"*
- *"What is RAII and how does Rust implement it?"*
- *"When exactly is drop() called on a variable?"*

### Learning Goals
- ✅ Understand scope-based ownership
- ✅ Know when variables are automatically dropped
- ✅ Use scopes strategically to control lifetimes

---

## Exercise 10: Clone vs Reference

### Concept Focus
Choosing between cloning and borrowing

### Exercise Description
Complete this exercise by choosing the best approach for each scenario. Consider performance and ownership requirements.

```rust
fn print_length(s: /* &String or String? */) {
    println!("Length: {}", s.len());
}

fn modify_string(s: /* &mut String or String? */) {
    // Should modify the original string
    s.push_str(" - modified");
}

fn take_ownership(s: /* String */) {
    // Should take ownership and drop at end
    println!("Taking: {}", s);
}

fn main() {
    let mut original = String::from("test");

    // Call each function appropriately
    print_length(/* ? */);
    modify_string(/* ? */);
    // Can we still use original after these calls?

    take_ownership(/* ? */);
    // Can we still use original now?
}
```

[🔗 Try it in Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+print_length%28s%3A+%2F*+%26String+or+String%3F+*%2F%29+%7B%0A++++println%21%28%22Length%3A+%7B%7D%22%2C+s.len%28%29%29%3B%0A%7D%0A%0Afn+modify_string%28s%3A+%2F*+%26mut+String+or+String%3F+*%2F%29+%7B%0A++++s.push_str%28%22+-+modified%22%29%3B%0A%7D%0A%0Afn+take_ownership%28s%3A+String%29+%7B%0A++++println%21%28%22Taking%3A+%7B%7D%22%2C+s%29%3B%0A%7D%0A%0Afn+main%28%29+%7B%0A++++let+mut+original+%3D+String%3A%3Afrom%28%22test%22%29%3B%0A++++%0A++++%2F%2F+Complete+this%0A%7D)

### AI Prompting Tips
- *"When should I use &String vs String as a parameter?"*
- *"What's the performance difference between clone() and borrowing?"*
- *"How do I decide between moving, borrowing, or cloning?"*

### Learning Goals
- ✅ Choose appropriate parameter types
- ✅ Understand performance implications
- ✅ Make intentional ownership decisions

---

## Bonus Challenge: String Slices and Lifetimes

### Concept Focus
Advanced: Working with string slices and lifetime relationships

### Exercise Description
Implement a function that returns the first word from a string. The return value should be a string slice that references the original string.

```rust
fn first_word(s: &str) -> &str {
    // Return everything up to the first space
    // Hint: Use .find(' ') and slicing with &s[0..index]
    // What if there's no space? Return the whole string.
}

fn main() {
    let sentence = String::from("Hello world from Rust");
    let word = first_word(&sentence);
    println!("First word: {}", word);

    // Bonus: Why is this signature safe without explicit lifetime annotations?
}
```

[🔗 Try it in Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&code=fn+first_word%28s%3A+%26str%29+-%3E+%26str+%7B%0A++++%2F%2F+your+implementation%0A%7D%0A%0Afn+main%28%29+%7B%0A++++let+sentence+%3D+String%3A%3Afrom%28%22Hello+world+from+Rust%22%29%3B%0A++++let+word+%3D+first_word%28%26sentence%29%3B%0A++++println%21%28%22First+word%3A+%7B%7D%22%2C+word%29%3B%0A%7D)

### AI Prompting Tips
- *"How do string slices work in Rust?"*
- *"What's the difference between &str and &String?"*
- *"Explain lifetime elision rules for functions with one reference parameter"*

### Learning Goals
- ✅ Work with string slices (`&str`)
- ✅ Understand lifetime elision
- ✅ Return borrowed data safely

---

## Next Steps

After completing these exercises, you should be ready to tackle **Lab 10**, which builds on these concepts with:
- The Borrow Checker Game (fixing intentional errors)
- Ownership exercises (implementing correct code from scratch)
- Testing with `cargo test`
- Applying AI debugging strategies

**Additional Practice Resources:**
- [Rustlings Ownership Exercises](https://github.com/rust-lang/rustlings/tree/main/exercises/move_semantics)
- [Rust by Example - Ownership](https://doc.rust-lang.org/rust-by-example/scope.html)
- [The Rust Book - Chapter 4 Exercises](https://doc.rust-lang.org/book/ch04-00-understanding-ownership.html)

**Remember:** The goal isn't just to make the code compile - it's to understand WHY the ownership system works this way. Use AI to deepen your understanding, not to skip the learning process!

---

**Questions?** Reach out on [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/group-chat-software) - we're here to help you master Rust's ownership system!
