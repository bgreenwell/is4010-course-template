# Lab 11: Building a student management system

**Due:** Sunday, November 9, 2025, at 11:59 PM
**Points:** 10

## 📋 Enhanced objective

Build a complete [student management system](https://en.wikipedia.org/wiki/Student_information_system) in Rust that demonstrates:
- **Module organization** with the [Rust module system](https://doc.rust-lang.org/book/ch07-00-managing-growing-projects-with-packages-crates-and-modules.html)
- **Custom data types** using [structs](https://doc.rust-lang.org/book/ch05-00-structs.html) and [enums](https://doc.rust-lang.org/book/ch06-00-enums.html)
- **Error handling** with [`Option<T>`](https://doc.rust-lang.org/std/option/enum.Option.html) and [`Result<T, E>`](https://doc.rust-lang.org/std/result/enum.Result.html)
- **Collections** including [`Vec<T>`](https://doc.rust-lang.org/std/vec/struct.Vec.html), [`String`](https://doc.rust-lang.org/std/string/struct.String.html), and [`HashMap<K, V>`](https://doc.rust-lang.org/std/collections/struct.HashMap.html)
- **Ownership principles** applied to complex data structures

This lab synthesizes everything you've learned about Rust's type system, ownership model, and data structuring capabilities into a real-world application.

---

## 🎯 Background

### Why student management systems matter

[Student information systems](https://en.wikipedia.org/wiki/Student_information_system) (SIS) are critical infrastructure for educational institutions. They manage:
- Student enrollment and demographics
- Course registration and scheduling
- Grade recording and transcription
- Performance tracking and analytics

Real-world SIS platforms include:
- [Blackboard](https://www.blackboard.com/) - Used by many universities
- [Canvas](https://www.instructure.com/canvas) - Popular learning management system
- [PowerSchool](https://www.powerschool.com/) - K-12 student information system
- [Ellucian Banner](https://www.ellucian.com/solutions/ellucian-banner) - Higher education ERP

### Technical concepts in focus

**[Modules](https://doc.rust-lang.org/book/ch07-02-defining-modules-to-control-scope-and-privacy.html):**
- Organize code into logical units
- Control visibility with [`pub` keyword](https://doc.rust-lang.org/std/keyword.pub.html)
- Create maintainable project structure

**[Structs and methods](https://doc.rust-lang.org/book/ch05-03-method-syntax.html):**
- Model entities (students, courses, grades)
- Encapsulate behavior with methods
- Use [associated functions](https://doc.rust-lang.org/book/ch05-03-method-syntax.html#associated-functions) for constructors

**[Enums with pattern matching](https://doc.rust-lang.org/book/ch06-02-match.html):**
- Represent alternatives (grade letters, enrollment status)
- Extract data with [`match` expressions](https://doc.rust-lang.org/reference/expressions/match-expr.html)
- Make impossible states unrepresentable

**[Error handling](https://doc.rust-lang.org/book/ch09-00-error-handling.html):**
- `Option<T>` for values that might not exist
- `Result<T, E>` for operations that can fail
- [The `?` operator](https://doc.rust-lang.org/book/ch09-02-recoverable-errors-with-result.html#a-shortcut-for-propagating-errors-the--operator) for error propagation

**[Collections](https://doc.rust-lang.org/book/ch08-00-common-collections.html):**
- `Vec<T>` for dynamic lists of students
- `HashMap<K, V>` for fast lookups by ID
- `String` vs [`&str`](https://doc.rust-lang.org/std/primitive.str.html) for text data

### Real-world applications

**Performance-critical systems:**
- Rust's zero-cost abstractions enable fast data processing
- No garbage collection pauses for time-sensitive operations
- Memory safety prevents data corruption bugs

**Data integrity:**
- Type system prevents invalid states
- Ownership ensures no data races
- Compiler catches bugs before deployment

---

## 🔧 Prerequisites

### Required tools

- **Rust toolchain** (rustup, cargo, rustc) - [Installation guide](../../resources/SETUP_GUIDE.md#rust-installation)
- **Git** for version control - [Git setup](../../resources/SETUP_GUIDE.md#git-installation)
- **GitHub account** with private repository access
- **Code editor** (VS Code with rust-analyzer recommended) - [Editor setup](../../resources/SETUP_GUIDE.md#code-editor-setup)

### Required knowledge

- Rust ownership and borrowing (Lab 10)
- Basic Rust syntax (Lab 09)
- Git workflow for commits and pushes
- Comfort with command-line operations

### Verify your setup

```bash
# Check Rust version (should be 1.70+)
rustc --version

# Check Cargo (Rust's package manager)
cargo --version

# Navigate to your labs repository
cd path/to/your/is4010-labs

# Ensure you're on the main branch
git status
```

If any commands fail, see the [SETUP_GUIDE.md](../../resources/SETUP_GUIDE.md) troubleshooting section.

---

## 📂 Part 1: Project structure and modules

### Background: The module system

Rust's [module system](https://doc.rust-lang.org/book/ch07-00-managing-growing-projects-with-packages-crates-and-modules.html) helps organize code as projects grow. Key concepts:

- **[Package](https://doc.rust-lang.org/book/ch07-01-packages-and-crates.html):** A Cargo project with `Cargo.toml`
- **[Crate](https://doc.rust-lang.org/book/ch07-01-packages-and-crates.html):** Compilation unit (library or binary)
- **[Module](https://doc.rust-lang.org/book/ch07-02-defining-modules-to-control-scope-and-privacy.html):** Namespace within a crate

**Privacy rules:**
- Items are private by default
- Use [`pub`](https://doc.rust-lang.org/std/keyword.pub.html) to make items public
- Child modules can access parent's private items

### Instructions

**Step 1: Create the project**

```bash
# From your is4010-labs directory
cargo new lab11 --bin
cd lab11
```

This creates a new [binary crate](https://doc.rust-lang.org/book/ch07-01-packages-and-crates.html#packages-and-crates) (executable program) with this structure:

```
lab11/
├── Cargo.toml          # Package manifest
└── src/
    └── main.rs         # Entry point with main()
```

**Step 2: Create a module file**

Create a new file `src/student.rs`:

```bash
touch src/student.rs
```

**Step 3: Declare the module**

In `src/main.rs`, add this at the top:

```rust
mod student;  // Tells Rust to include src/student.rs

fn main() {
    println!("Student Management System");
}
```

The [`mod` keyword](https://doc.rust-lang.org/std/keyword.mod.html) tells Rust to look for `student.rs` in the same directory.

**Step 4: Test the module setup**

```bash
cargo build
```

If successful, your module is properly connected!

### AI assistance for module organization

**Example prompts:**
- "Explain how Rust modules work with the mod keyword"
- "How do I organize a Rust project with multiple modules?"
- "What's the difference between mod student; and mod student {...}?"
- "Should I use separate files or inline modules for this code?"

**Common patterns:**
```rust
// Declaring a module from a file
mod student;  // Looks for src/student.rs

// Bringing items into scope
use student::Student;

// Making items public
pub struct Student { ... }
pub fn create_student(...) -> Student { ... }
```

---

## 🎓 Part 2: Defining the Student struct

### Background: Structs with methods

[Structs](https://doc.rust-lang.org/book/ch05-01-defining-structs.html) let you create custom data types by grouping related data. [Methods](https://doc.rust-lang.org/book/ch05-03-method-syntax.html) add behavior to structs.

**Method types:**
- **Instance methods**: Take `&self`, `&mut self`, or `self`
- **Associated functions**: No `self` parameter (like constructors)

### Instructions

**Step 1: Define the Student struct**

In `src/student.rs`, add:

```rust
pub struct Student {
    pub id: String,
    pub name: String,
    pub email: String,
    pub credits_earned: u16,
}
```

All fields are public ([`pub`](https://doc.rust-lang.org/std/keyword.pub.html)) so they can be accessed from `main.rs`.

**Step 2: Add a constructor**

Add an [associated function](https://doc.rust-lang.org/book/ch05-03-method-syntax.html#associated-functions) for creating students:

```rust
impl Student {
    pub fn new(id: String, name: String, email: String) -> Student {
        Student {
            id,
            name,
            email,
            credits_earned: 0,  // New students start with 0 credits
        }
    }
}
```

Notice:
- No `self` parameter (it's a constructor)
- Called with `Student::new(...)` using [`::`](https://doc.rust-lang.org/book/ch05-03-method-syntax.html#associated-functions)
- Returns a `Student` instance

**Step 3: Add methods**

Add these methods to the `impl Student` block:

```rust
impl Student {
    // ... new() from above ...

    /// Returns the student's class standing based on credits
    pub fn class_standing(&self) -> &str {
        match self.credits_earned {
            0..=29 => "Freshman",
            30..=59 => "Sophomore",
            60..=89 => "Junior",
            _ => "Senior",
        }
    }

    /// Adds credits when a course is completed
    pub fn add_credits(&mut self, credits: u16) {
        self.credits_earned += credits;
    }

    /// Checks if student qualifies for graduation (120+ credits)
    pub fn can_graduate(&self) -> bool {
        self.credits_earned >= 120
    }
}
```

**Key concepts:**
- `&self`: Immutable borrow (read-only)
- `&mut self`: Mutable borrow (can modify)
- [Range patterns](https://doc.rust-lang.org/book/ch18-03-pattern-syntax.html#matching-ranges-of-values-with-) in `match` expressions

**Step 4: Test in main**

Update `src/main.rs`:

```rust
mod student;
use student::Student;

fn main() {
    let mut student = Student::new(
        String::from("S001"),
        String::from("Alice Johnson"),
        String::from("alice@example.com"),
    );

    println!("Name: {}", student.name);
    println!("Standing: {}", student.class_standing());

    student.add_credits(30);
    println!("After 30 credits: {}", student.class_standing());

    student.add_credits(90);
    println!("Can graduate? {}", student.can_graduate());
}
```

**Step 5: Run and verify**

```bash
cargo run
```

Expected output:
```
Name: Alice Johnson
Standing: Freshman
After 30 credits: Sophomore
Can graduate? true
```

### AI assistance for structs and methods

**Example prompts:**
- "How do I add a method to a Rust struct?"
- "What's the difference between &self and &mut self?"
- "Help me implement a method that calculates GPA from grades"
- "Should this field be String or &str in a struct?"

**Common pitfalls:**
- Forgetting `pub` when items need to be accessed from other modules
- Using `&self` when you need `&mut self` to modify fields
- Confusion between `String` (owned) and `&str` (borrowed)

---

## 📊 Part 3: Grade enumeration with pattern matching

### Background: Enums in Rust

[Enums](https://doc.rust-lang.org/book/ch06-01-defining-an-enum.html) define types that can be one of several variants. Rust enums are more powerful than in other languages - they can [carry data](https://doc.rust-lang.org/book/ch06-01-defining-an-enum.html#enum-values).

[Pattern matching](https://doc.rust-lang.org/book/ch06-02-match.html) with [`match`](https://doc.rust-lang.org/reference/expressions/match-expr.html) is exhaustive - you must handle all variants.

### Instructions

**Step 1: Define the Grade enum**

Add to `src/student.rs`:

```rust
#[derive(Debug, Clone, PartialEq)]
pub enum Grade {
    A,
    B,
    C,
    D,
    F,
}
```

**About the derives:**
- [`Debug`](https://doc.rust-lang.org/std/fmt/trait.Debug.html): Enables printing with `{:?}`
- [`Clone`](https://doc.rust-lang.org/std/clone/trait.Clone.html): Allows `.clone()` to duplicate
- [`PartialEq`](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html): Enables `==` comparison

**Step 2: Add methods to Grade**

```rust
impl Grade {
    /// Convert grade letter to GPA points
    pub fn to_gpa_points(&self) -> f32 {
        match self {
            Grade::A => 4.0,
            Grade::B => 3.0,
            Grade::C => 2.0,
            Grade::D => 1.0,
            Grade::F => 0.0,
        }
    }

    /// Parse a grade from a string
    pub fn from_string(s: &str) -> Option<Grade> {
        match s.to_uppercase().as_str() {
            "A" => Some(Grade::A),
            "B" => Some(Grade::B),
            "C" => Some(Grade::C),
            "D" => Some(Grade::D),
            "F" => Some(Grade::F),
            _ => None,  // Invalid grade string
        }
    }

    /// Check if grade is passing (C or better)
    pub fn is_passing(&self) -> bool {
        match self {
            Grade::A | Grade::B | Grade::C => true,
            Grade::D | Grade::F => false,
        }
    }
}
```

**New concepts:**
- [`Option<T>`](https://doc.rust-lang.org/std/option/enum.Option.html): Returns `Some(value)` or `None`
- [Pattern alternatives](https://doc.rust-lang.org/book/ch18-03-pattern-syntax.html#multiple-patterns) with `|` (logical OR)

**Step 3: Test grade functionality**

Add to `main()` in `src/main.rs`:

```rust
use student::Grade;

// ... existing code ...

// Test grade parsing
match Grade::from_string("B") {
    Some(grade) => {
        println!("Grade: {:?}", grade);
        println!("GPA points: {}", grade.to_gpa_points());
        println!("Passing? {}", grade.is_passing());
    }
    None => println!("Invalid grade"),
}
```

**Step 4: Run and verify**

```bash
cargo run
```

### AI assistance for enums

**Example prompts:**
- "How do I define an enum in Rust with data in variants?"
- "Explain pattern matching with match in Rust"
- "How do I return Option from a function in Rust?"
- "What's the best way to convert strings to enum variants?"

**Common patterns:**
```rust
// Enum with data-carrying variants
enum Status {
    Active,
    Suspended { reason: String },
    Graduated { date: String },
}

// Exhaustive pattern matching
match status {
    Status::Active => println!("Currently enrolled"),
    Status::Suspended { reason } => println!("Suspended: {}", reason),
    Status::Graduated { date } => println!("Graduated on {}", date),
}
```

---

## 📚 Part 4: CourseGrade struct combining concepts

### Background: Composing types

Real applications combine multiple custom types. A course grade needs:
- Course information (code, name, credits)
- The grade earned
- Both struct and enum working together

### Instructions

**Step 1: Define CourseGrade struct**

Add to `src/student.rs`:

```rust
#[derive(Debug, Clone)]
pub struct CourseGrade {
    pub course_code: String,    // e.g., "IS4010"
    pub course_name: String,    // e.g., "App Dev with AI"
    pub credits: u16,           // e.g., 3
    pub grade: Grade,           // Our enum from Part 3
}
```

**Step 2: Add constructor and methods**

```rust
impl CourseGrade {
    pub fn new(course_code: String, course_name: String, credits: u16, grade: Grade) -> CourseGrade {
        CourseGrade {
            course_code,
            course_name,
            credits,
            grade,
        }
    }

    /// Calculate quality points (credits × GPA points)
    pub fn quality_points(&self) -> f32 {
        self.credits as f32 * self.grade.to_gpa_points()
    }
}
```

**Concept: [Type casting](https://doc.rust-lang.org/rust-by-example/types/cast.html)**
- `self.credits as f32`: Converts `u16` to `f32` for calculation

**Step 3: Add grade tracking to Student**

Update the `Student` struct:

```rust
pub struct Student {
    pub id: String,
    pub name: String,
    pub email: String,
    pub credits_earned: u16,
    pub grades: Vec<CourseGrade>,  // NEW: Vector of grades
}
```

Update the constructor:

```rust
impl Student {
    pub fn new(id: String, name: String, email: String) -> Student {
        Student {
            id,
            name,
            email,
            credits_earned: 0,
            grades: Vec::new(),  // Start with empty vector
        }
    }

    // ... existing methods ...
}
```

**Step 4: Add methods for grade management**

Add to `impl Student`:

```rust
    /// Add a course grade to the student's transcript
    pub fn add_grade(&mut self, course_grade: CourseGrade) {
        self.credits_earned += course_grade.credits;
        self.grades.push(course_grade);
    }

    /// Calculate cumulative GPA
    pub fn calculate_gpa(&self) -> f32 {
        if self.grades.is_empty() {
            return 0.0;
        }

        let total_quality_points: f32 = self.grades
            .iter()
            .map(|cg| cg.quality_points())
            .sum();

        let total_credits: f32 = self.grades
            .iter()
            .map(|cg| cg.credits as f32)
            .sum();

        if total_credits > 0.0 {
            total_quality_points / total_credits
        } else {
            0.0
        }
    }
```

**New concepts:**
- [`.iter()`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.iter): Create iterator over references
- [`.map()`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.map): Transform each element
- [`.sum()`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.sum): Add up all elements
- [Closures](https://doc.rust-lang.org/book/ch13-01-closures.html): `|cg| cg.quality_points()`

**Step 5: Test grade tracking**

Update `main()`:

```rust
mod student;
use student::{Student, Grade, CourseGrade};

fn main() {
    let mut student = Student::new(
        String::from("S001"),
        String::from("Alice Johnson"),
        String::from("alice@example.com"),
    );

    // Add some course grades
    student.add_grade(CourseGrade::new(
        String::from("IS4010"),
        String::from("App Dev with AI"),
        3,
        Grade::A,
    ));

    student.add_grade(CourseGrade::new(
        String::from("IS3050"),
        String::from("Database Design"),
        3,
        Grade::B,
    ));

    student.add_grade(CourseGrade::new(
        String::from("IS2000"),
        String::from("Intro to IS"),
        3,
        Grade::A,
    ));

    println!("Student: {}", student.name);
    println!("Credits: {}", student.credits_earned);
    println!("GPA: {:.2}", student.calculate_gpa());
    println!("Standing: {}", student.class_standing());

    // Print all grades
    println!("\nTranscript:");
    for course_grade in &student.grades {
        println!("  {}: {} - {:?} ({:.1} quality points)",
            course_grade.course_code,
            course_grade.course_name,
            course_grade.grade,
            course_grade.quality_points(),
        );
    }
}
```

**Step 6: Run and verify**

```bash
cargo run
```

Expected output:
```
Student: Alice Johnson
Credits: 9
GPA: 3.67
Standing: Freshman

Transcript:
  IS4010: App Dev with AI - A (12.0 quality points)
  IS3050: Database Design - B (9.0 quality points)
  IS2000: Intro to IS - A (12.0 quality points)
```

### AI assistance for complex data structures

**Example prompts:**
- "How do I add a Vec field to a struct in Rust?"
- "Help me calculate a weighted average from a vector of structs"
- "How do iterators work in Rust with map and sum?"
- "Why do I need to borrow with & in the for loop?"

---

## 🗄️ Part 5: Student database with HashMap

### Background: Collections for data management

[`HashMap<K, V>`](https://doc.rust-lang.org/std/collections/struct.HashMap.html) provides fast lookups by key. Perfect for managing students by ID.

**Performance:**
- Insert: O(1) average
- Lookup: O(1) average
- Better than `Vec` for ID-based access

### Instructions

**Step 1: Create StudentDatabase struct**

Add to `src/student.rs`:

```rust
use std::collections::HashMap;

pub struct StudentDatabase {
    students: HashMap<String, Student>,  // Key: student ID
}
```

**Step 2: Implement database methods**

```rust
impl StudentDatabase {
    pub fn new() -> StudentDatabase {
        StudentDatabase {
            students: HashMap::new(),
        }
    }

    /// Add a student to the database
    pub fn add_student(&mut self, student: Student) -> Result<(), String> {
        if self.students.contains_key(&student.id) {
            return Err(format!("Student {} already exists", student.id));
        }
        self.students.insert(student.id.clone(), student);
        Ok(())
    }

    /// Find a student by ID
    pub fn find_student(&self, id: &str) -> Option<&Student> {
        self.students.get(id)
    }

    /// Find a student by ID (mutable reference)
    pub fn find_student_mut(&mut self, id: &str) -> Option<&mut Student> {
        self.students.get_mut(id)
    }

    /// Get total number of students
    pub fn student_count(&self) -> usize {
        self.students.len()
    }

    /// Calculate average GPA across all students
    pub fn average_gpa(&self) -> f32 {
        if self.students.is_empty() {
            return 0.0;
        }

        let total: f32 = self.students
            .values()
            .map(|s| s.calculate_gpa())
            .sum();

        total / self.students.len() as f32
    }

    /// List all students sorted by name
    pub fn list_students(&self) -> Vec<&Student> {
        let mut students: Vec<&Student> = self.students.values().collect();
        students.sort_by(|a, b| a.name.cmp(&b.name));
        students
    }
}
```

**Key concepts:**
- [`Result<T, E>`](https://doc.rust-lang.org/std/result/enum.Result.html): Returns `Ok(value)` or `Err(error)`
- [`.get()`](https://doc.rust-lang.org/std/collections/struct.HashMap.html#method.get): Safe lookup returning `Option<&V>`
- [`.get_mut()`](https://doc.rust-lang.org/std/collections/struct.HashMap.html#method.get_mut): Mutable access
- [`.values()`](https://doc.rust-lang.org/std/collections/struct.HashMap.html#method.values): Iterate over values
- [`.sort_by()`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.sort_by): Sort with custom comparison

**Step 3: Test the database**

Update `main()`:

```rust
use student::{Student, Grade, CourseGrade, StudentDatabase};

fn main() {
    let mut db = StudentDatabase::new();

    // Create and add students
    let mut alice = Student::new(
        String::from("S001"),
        String::from("Alice Johnson"),
        String::from("alice@example.com"),
    );
    alice.add_grade(CourseGrade::new(
        String::from("IS4010"),
        String::from("App Dev with AI"),
        3,
        Grade::A,
    ));

    let mut bob = Student::new(
        String::from("S002"),
        String::from("Bob Smith"),
        String::from("bob@example.com"),
    );
    bob.add_grade(CourseGrade::new(
        String::from("IS3050"),
        String::from("Database Design"),
        3,
        Grade::B,
    ));

    // Add students to database
    match db.add_student(alice) {
        Ok(()) => println!("Added Alice"),
        Err(e) => println!("Error: {}", e),
    }

    match db.add_student(bob) {
        Ok(()) => println!("Added Bob"),
        Err(e) => println!("Error: {}", e),
    }

    // Database statistics
    println!("\nDatabase Statistics:");
    println!("Total students: {}", db.student_count());
    println!("Average GPA: {:.2}", db.average_gpa());

    // List all students
    println!("\nAll Students:");
    for student in db.list_students() {
        println!("  {} - {} (GPA: {:.2})",
            student.id,
            student.name,
            student.calculate_gpa(),
        );
    }

    // Find specific student
    if let Some(student) = db.find_student("S001") {
        println!("\nFound student: {}", student.name);
        println!("  Email: {}", student.email);
        println!("  Credits: {}", student.credits_earned);
        println!("  GPA: {:.2}", student.calculate_gpa());
    }
}
```

**Step 4: Run and verify**

```bash
cargo run
```

### AI assistance for HashMap operations

**Example prompts:**
- "How do I use HashMap in Rust?"
- "What's the difference between get() and get_mut() for HashMap?"
- "Help me handle the Result from inserting into HashMap"
- "How do I iterate over HashMap values and sort them?"
- "Why do I need to clone() the student ID when inserting?"

**Common patterns:**
```rust
// Check if key exists
if map.contains_key(&key) { ... }

// Insert and handle duplicate
if map.insert(key, value).is_some() {
    // Key already existed
}

// Safe lookup with Option
match map.get(&key) {
    Some(value) => { /* use value */ },
    None => { /* key not found */ },
}

// Update existing value
if let Some(value) = map.get_mut(&key) {
    *value = new_value;
}
```

---

## ✅ Part 6: Adding comprehensive tests

### Background: Testing in Rust

[Cargo's built-in test framework](https://doc.rust-lang.org/book/ch11-00-testing.html) makes testing easy:
- Tests live in `#[cfg(test)]` modules
- Use `#[test]` attribute to mark test functions
- Run with [`cargo test`](https://doc.rust-lang.org/cargo/commands/cargo-test.html)

### Instructions

**Step 1: Add test module**

At the bottom of `src/student.rs`, add:

```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_student_creation() {
        let student = Student::new(
            String::from("S001"),
            String::from("Test Student"),
            String::from("test@example.com"),
        );
        assert_eq!(student.id, "S001");
        assert_eq!(student.name, "Test Student");
        assert_eq!(student.credits_earned, 0);
        assert!(student.grades.is_empty());
    }

    #[test]
    fn test_class_standing() {
        let mut student = Student::new(
            String::from("S001"),
            String::from("Test"),
            String::from("test@example.com"),
        );
        assert_eq!(student.class_standing(), "Freshman");

        student.add_credits(30);
        assert_eq!(student.class_standing(), "Sophomore");

        student.add_credits(30);
        assert_eq!(student.class_standing(), "Junior");

        student.add_credits(30);
        assert_eq!(student.class_standing(), "Senior");
    }

    #[test]
    fn test_graduation_eligibility() {
        let mut student = Student::new(
            String::from("S001"),
            String::from("Test"),
            String::from("test@example.com"),
        );
        assert!(!student.can_graduate());

        student.add_credits(120);
        assert!(student.can_graduate());
    }

    #[test]
    fn test_grade_parsing() {
        assert_eq!(Grade::from_string("A"), Some(Grade::A));
        assert_eq!(Grade::from_string("a"), Some(Grade::A));
        assert_eq!(Grade::from_string("B"), Some(Grade::B));
        assert_eq!(Grade::from_string("F"), Some(Grade::F));
        assert_eq!(Grade::from_string("Z"), None);
        assert_eq!(Grade::from_string(""), None);
    }

    #[test]
    fn test_grade_gpa_points() {
        assert_eq!(Grade::A.to_gpa_points(), 4.0);
        assert_eq!(Grade::B.to_gpa_points(), 3.0);
        assert_eq!(Grade::C.to_gpa_points(), 2.0);
        assert_eq!(Grade::D.to_gpa_points(), 1.0);
        assert_eq!(Grade::F.to_gpa_points(), 0.0);
    }

    #[test]
    fn test_passing_grades() {
        assert!(Grade::A.is_passing());
        assert!(Grade::B.is_passing());
        assert!(Grade::C.is_passing());
        assert!(!Grade::D.is_passing());
        assert!(!Grade::F.is_passing());
    }

    #[test]
    fn test_quality_points() {
        let course = CourseGrade::new(
            String::from("IS4010"),
            String::from("App Dev"),
            3,
            Grade::A,
        );
        assert_eq!(course.quality_points(), 12.0);

        let course2 = CourseGrade::new(
            String::from("IS3050"),
            String::from("Database"),
            4,
            Grade::B,
        );
        assert_eq!(course2.quality_points(), 12.0);
    }

    #[test]
    fn test_gpa_calculation() {
        let mut student = Student::new(
            String::from("S001"),
            String::from("Test"),
            String::from("test@example.com"),
        );

        // No grades = 0.0 GPA
        assert_eq!(student.calculate_gpa(), 0.0);

        // Add one A (4.0 GPA)
        student.add_grade(CourseGrade::new(
            String::from("CS101"),
            String::from("Intro"),
            3,
            Grade::A,
        ));
        assert_eq!(student.calculate_gpa(), 4.0);

        // Add one B (3.0 GPA) -> average 3.5
        student.add_grade(CourseGrade::new(
            String::from("CS102"),
            String::from("Data Structures"),
            3,
            Grade::B,
        ));
        assert_eq!(student.calculate_gpa(), 3.5);
    }

    #[test]
    fn test_database_add_student() {
        let mut db = StudentDatabase::new();
        let student = Student::new(
            String::from("S001"),
            String::from("Test"),
            String::from("test@example.com"),
        );

        assert!(db.add_student(student).is_ok());
        assert_eq!(db.student_count(), 1);
    }

    #[test]
    fn test_database_duplicate_student() {
        let mut db = StudentDatabase::new();
        let student1 = Student::new(
            String::from("S001"),
            String::from("Test1"),
            String::from("test1@example.com"),
        );
        let student2 = Student::new(
            String::from("S001"),
            String::from("Test2"),
            String::from("test2@example.com"),
        );

        assert!(db.add_student(student1).is_ok());
        assert!(db.add_student(student2).is_err());
        assert_eq!(db.student_count(), 1);
    }

    #[test]
    fn test_database_find_student() {
        let mut db = StudentDatabase::new();
        let student = Student::new(
            String::from("S001"),
            String::from("Test"),
            String::from("test@example.com"),
        );
        db.add_student(student).unwrap();

        assert!(db.find_student("S001").is_some());
        assert!(db.find_student("S999").is_none());
    }

    #[test]
    fn test_database_average_gpa() {
        let mut db = StudentDatabase::new();

        // Empty database
        assert_eq!(db.average_gpa(), 0.0);

        // Add students with known GPAs
        let mut student1 = Student::new(
            String::from("S001"),
            String::from("Alice"),
            String::from("alice@example.com"),
        );
        student1.add_grade(CourseGrade::new(
            String::from("CS101"),
            String::from("Intro"),
            3,
            Grade::A,  // 4.0 GPA
        ));

        let mut student2 = Student::new(
            String::from("S002"),
            String::from("Bob"),
            String::from("bob@example.com"),
        );
        student2.add_grade(CourseGrade::new(
            String::from("CS101"),
            String::from("Intro"),
            3,
            Grade::B,  // 3.0 GPA
        ));

        db.add_student(student1).unwrap();
        db.add_student(student2).unwrap();

        // Average should be 3.5
        assert_eq!(db.average_gpa(), 3.5);
    }
}
```

**Step 2: Run all tests**

```bash
cargo test
```

You should see output like:

```
running 12 tests
test tests::test_class_standing ... ok
test tests::test_database_add_student ... ok
test tests::test_database_average_gpa ... ok
test tests::test_database_duplicate_student ... ok
test tests::test_database_find_student ... ok
test tests::test_gpa_calculation ... ok
test tests::test_grade_gpa_points ... ok
test tests::test_grade_parsing ... ok
test tests::test_graduation_eligibility ... ok
test tests::test_passing_grades ... ok
test tests::test_quality_points ... ok
test tests::test_student_creation ... ok

test result: ok. 12 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out
```

**Step 3: Run specific tests**

```bash
# Run tests with "grade" in the name
cargo test grade

# Run tests with verbose output
cargo test -- --show-output

# Run tests and display println! output
cargo test -- --nocapture
```

### Testing best practices

**AAA pattern:**
1. **Arrange**: Set up test data
2. **Act**: Execute the code being tested
3. **Assert**: Verify the result

**Assertion macros:**
- [`assert!`](https://doc.rust-lang.org/std/macro.assert.html): Check boolean condition
- [`assert_eq!`](https://doc.rust-lang.org/std/macro.assert_eq.html): Check equality
- [`assert_ne!`](https://doc.rust-lang.org/std/macro.assert_ne.html): Check inequality

### AI assistance for testing

**Example prompts:**
- "Help me write tests for my Student struct in Rust"
- "How do I test functions that return Result in Rust?"
- "What's the best way to test error cases in Rust?"
- "How do I test private functions in Rust modules?"

---

## 🚀 Part 7: GitHub Actions CI/CD setup

### Background: Continuous Integration

[GitHub Actions](https://docs.github.com/en/actions) automatically runs your tests on every push. This ensures:
- Tests pass before merging code
- Changes don't break existing functionality
- Code quality is maintained

### Instructions

**Step 1: Create workflow directory**

```bash
# From your is4010-labs repository root
mkdir -p .github/workflows
```

**Step 2: Create workflow file**

Create `.github/workflows/lab11.yml`:

```yaml
name: Lab 11 Tests

on:
  push:
    paths:
      - 'lab11/**'
  pull_request:
    paths:
      - 'lab11/**'

jobs:
  test:
    name: Run Lab 11 Tests
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Install Rust
        uses: actions-rs/toolchain@v1
        with:
          toolchain: stable
          override: true

      - name: Build lab11
        run: cargo build --manifest-path lab11/Cargo.toml --verbose

      - name: Run lab11 tests
        run: cargo test --manifest-path lab11/Cargo.toml --verbose

      - name: Run cargo check
        run: cargo check --manifest-path lab11/Cargo.toml
```

**Step 3: Commit and push workflow**

```bash
git add .github/workflows/lab11.yml
git commit -m "Add Lab 11 CI/CD workflow"
git push origin main
```

**Step 4: Verify on GitHub**

1. Go to your repository on GitHub
2. Click **Actions** tab
3. You should see "Lab 11 Tests" workflow running
4. Green checkmark = tests passed! ✅

### Debugging failed CI builds

If tests fail on GitHub but pass locally:

1. **Check Rust version:** GitHub might use different toolchain
2. **Review error logs:** Click on failed job for details
3. **Test platform differences:** Paths, line endings, etc.

**Common fixes:**
```bash
# Update Rust locally to match CI
rustup update stable

# Check for warnings that become errors in CI
cargo build --all-warnings
```

---

## 📦 Expected repository structure

Your `is4010-labs` repository should now have this structure:

```
is4010-labs/
├── .github/
│   └── workflows/
│       ├── lab09.yml           # From Lab 09
│       ├── lab10.yml           # From Lab 10
│       └── lab11.yml           # NEW: Lab 11 CI/CD
├── lab09/                      # Previous lab
│   └── ...
├── lab10/                      # Previous lab
│   └── ...
├── lab11/                      # NEW: This lab
│   ├── Cargo.toml             # Package manifest
│   ├── Cargo.lock             # Dependency lock file (auto-generated)
│   ├── target/                # Build outputs (gitignored)
│   └── src/
│       ├── main.rs            # Entry point with main()
│       └── student.rs         # Student management module
├── .gitignore                 # Should include target/
└── README.md                  # Lab portfolio documentation
```

**Important files:**
- `src/student.rs`: All types (Student, Grade, CourseGrade, StudentDatabase)
- `src/main.rs`: Demo usage in `main()` function
- `.github/workflows/lab11.yml`: CI/CD configuration

**Verify before submitting:**

```bash
# From lab11 directory
cargo build        # Should build without errors
cargo test         # Should pass all tests
cargo run          # Should execute demonstration
```

---

## 🔧 Comprehensive troubleshooting guide

### Compilation errors

**Error: "cannot find value `student` in this scope"**
```
Solution: Ensure you've imported the module:
  use student::Student;
```

**Error: "cannot borrow as mutable"**
```
Solution: Variable must be declared with `mut`:
  let mut student = Student::new(...);
```

**Error: "the trait `From<&str>` is not implemented for `String`"**
```
Solution: Convert &str to String:
  String::from("text")  // or "text".to_string()
```

**Error: "no method named `push` found for struct `Vec`"**
```
Solution: Vec must be mutable to modify:
  let mut grades: Vec<Grade> = Vec::new();
```

### Ownership errors

**Error: "value borrowed here after move"**
```
Solution 1: Use a reference instead of moving:
  db.add_student(&student);  // If function accepts &Student

Solution 2: Clone the value:
  db.add_student(student.clone());  // Must derive Clone

Solution 3: Move is intentional, don't use after:
  db.add_student(student);
  // Don't reference student after this point
```

**Error: "cannot borrow as mutable because it is also borrowed as immutable"**
```
Solution: Ensure immutable borrows are done before mutable borrow:
  let data = &student.name;  // Immutable borrow
  println!("{}", data);      // Last use of immutable borrow
  student.add_credits(3);    // Now mutable borrow is OK
```

### Test failures

**Test fails: "assertion failed: student.calculate_gpa() == 3.5"**
```
Debug steps:
1. Print actual value:
   println!("Actual GPA: {}", student.calculate_gpa());

2. Check calculation logic in calculate_gpa()
3. Verify test data is correct
```

**Error: "no method named `add_grade` found"**
```
Solution: Ensure method is public and imported:
  pub fn add_grade(&mut self, grade: CourseGrade) { ... }
```

### Module and import issues

**Error: "unresolved import `student::Student`"**
```
Solution: Ensure Student is public in student.rs:
  pub struct Student { ... }
```

**Error: "file not found for module `student`"**
```
Solution: Check file is named correctly:
  src/student.rs  (not students.rs or Student.rs)
```

### HashMap and collection errors

**Error: "the trait `Hash` is not implemented for `Student`"**
```
Solution: For HashMap keys, type must implement Hash.
For Student as key, derive Hash:
  #[derive(Hash, Eq, PartialEq)]
  pub struct Student { ... }

Or use String ID as key instead (it implements Hash):
  HashMap<String, Student>
```

**Error: "cannot move out of `HashMap` value"**
```
Solution: HashMap.get() returns &V (reference), not V:
  if let Some(student_ref) = db.find_student("S001") {
      // Use student_ref (a reference)
  }
```

### CI/CD and GitHub Actions issues

**Tests pass locally but fail on GitHub**
```
Common causes:
1. Different Rust version
   Fix: Update locally with `rustup update`

2. Platform-specific code
   Fix: Test on Linux if possible, or use #[cfg(target_os = "linux")]

3. Hardcoded paths
   Fix: Use relative paths or std::env::current_dir()
```

**Workflow doesn't run**
```
Check:
1. File is in .github/workflows/
2. File has .yml or .yaml extension
3. Syntax is valid (use YAML validator)
4. Push triggered on correct paths
```

### Cargo and build issues

**Error: "could not compile `lab11`"**
```
Steps:
1. Read error message carefully (Rust errors are helpful!)
2. Fix the indicated file and line
3. Run `cargo check` for faster feedback
4. Run `cargo build` when fixed
```

**Error: "package `lab11` cannot be built because it requires rustc 1.70"**
```
Solution: Update Rust:
  rustup update stable
```

### Get more help

If stuck after trying these solutions:
1. **Read the full error message** - Rust errors include helpful hints
2. **Use `cargo check`** - Faster than `cargo build` for finding errors
3. **Check the [Rust Book](https://doc.rust-lang.org/book/)** - Official comprehensive guide
4. **Ask AI:** "I'm getting this Rust error: [paste error]. How do I fix it?"
5. **Post on Teams** - Share your error and what you've tried
6. **Review lecture notes** - [Week 11 Notes](../../resources/lecture-notes/W11_Structuring_Code_and_Data_notes.md)

---

## 🤖 Strategic AI assistance

### When to use AI

**Design and planning:**
- "Help me design a struct for representing course enrollments"
- "Should I use an enum or a struct for modeling user roles?"
- "How should I organize modules for a library management system?"

**Understanding concepts:**
- "Explain when to use Option vs Result in Rust"
- "Why does HashMap require keys to implement Hash trait?"
- "What's the difference between Vec and HashMap for storing students?"

**Debugging:**
- "I'm getting error E0382. What does 'value borrowed after move' mean?"
- "Help me fix this borrow checker error: [paste error]"
- "Why doesn't my test compile? [paste test code]"

**Code review:**
- "Is this the idiomatic way to implement this in Rust?"
- "Can you suggest improvements to my struct design?"
- "How can I make this code more efficient?"

### Example AI conversations

**Conversation 1: Designing data structures**

```
You: I need to model students with grades in Rust. Each student has an
ID, name, email, and a list of course grades. Each grade has a course
code, course name, credits, and a letter grade (A-F). What's the best
way to structure this?

AI: I'd recommend:
1. A Grade enum with variants A, B, C, D, F
2. A CourseGrade struct with course_code: String, course_name: String,
   credits: u16, grade: Grade
3. A Student struct with id: String, name: String, email: String,
   grades: Vec<CourseGrade>

This lets you:
- Use type safety for grades (only valid letters)
- Store multiple courses per student
- Calculate GPA by iterating over grades

You: How do I calculate GPA from these structures?

AI: Add a method to Student:
impl Student {
    pub fn calculate_gpa(&self) -> f32 {
        if self.grades.is_empty() {
            return 0.0;
        }
        let total_points: f32 = self.grades
            .iter()
            .map(|cg| cg.credits as f32 * cg.grade.to_gpa_points())
            .sum();
        let total_credits: f32 = self.grades
            .iter()
            .map(|cg| cg.credits as f32)
            .sum();
        total_points / total_credits
    }
}

And add to_gpa_points() method to Grade enum.
```

**Conversation 2: Fixing ownership error**

```
You: I'm getting this error:
error[E0382]: borrow of moved value: `student`
  --> src/main.rs:10:20
   |
8  |     db.add_student(student);
   |                    ------- value moved here
10 |     println!("{}", student.name);
   |                    ^^^^^^^^^^^ value borrowed here after move

How do I fix this?

AI: The add_student() method takes ownership of student (moves it), so you
can't use student afterward. Two options:

Option 1: Don't use student after adding:
  db.add_student(student);
  // Don't reference student here

Option 2: Change add_student to borrow instead:
  pub fn add_student(&mut self, student: &Student) {
      self.students.insert(student.id.clone(), student.clone());
  }
  // Now call with:
  db.add_student(&student);
  println!("{}", student.name);  // OK now

Option 1 is more efficient (no clone), but Option 2 keeps student available.

You: OK I'll use Option 1 since I don't need student after adding. Thanks!
```

**Conversation 3: Testing strategy**

```
You: How should I test my Student struct? It has methods for adding grades
and calculating GPA.

AI: Here's a comprehensive testing strategy:

1. Test constructor:
   - Verify fields are set correctly
   - Check initial state (empty grades, 0 credits)

2. Test individual methods:
   - add_grade(): Check credits increase, grade is added
   - calculate_gpa(): Test with 0, 1, and multiple grades
   - class_standing(): Test boundary values (29, 30, 59, 60, etc.)

3. Test edge cases:
   - Empty grade list (GPA should be 0.0)
   - All A's (GPA should be 4.0)
   - All F's (GPA should be 0.0)
   - Mixed grades (known GPA)

4. Test error conditions:
   - Invalid grade strings
   - Duplicate student IDs in database

Example test:
#[test]
fn test_gpa_with_multiple_grades() {
    let mut student = Student::new(...);
    student.add_grade(...A grade...);
    student.add_grade(...B grade...);
    let gpa = student.calculate_gpa();
    assert!((gpa - 3.5).abs() < 0.01);  // Float comparison with tolerance
}

You: Why use (gpa - 3.5).abs() < 0.01 instead of assert_eq?

AI: Floating-point arithmetic can have tiny rounding errors. Instead of
exact equality (which might fail due to rounding), we check if the
difference is less than a small threshold (0.01). This is called an
"epsilon" comparison and is standard practice for float tests.

Alternatively, you can round before comparing:
assert_eq!((gpa * 100.0).round() / 100.0, 3.5);
```

### Prompt templates

**For design:**
```
I'm building [description of system]. I need to model [entities] with
[properties/relationships]. What Rust data structures (structs, enums,
collections) should I use? Consider [constraints like performance,
mutability, ownership].
```

**For debugging:**
```
I'm getting this Rust error: [paste full error message including error
code like E0382]. Here's my code: [paste relevant code]. What does this
error mean and how do I fix it?
```

**For testing:**
```
I need to test [function/method name] which [description of what it does].
What test cases should I write to ensure it works correctly? Consider
edge cases like [empty inputs, boundary values, error conditions].
```

**For optimization:**
```
Here's my implementation: [paste code]. Is this idiomatic Rust? Can you
suggest improvements for [performance/readability/safety]?
```

---

## ✅ Submission checklist

Before submitting, verify:

**Code functionality:**
- [ ] `cargo build` completes without errors or warnings
- [ ] `cargo test` passes all 12+ tests
- [ ] `cargo run` executes and shows expected output
- [ ] All required structs implemented: Student, Grade, CourseGrade, StudentDatabase
- [ ] All required methods implemented and working

**Code organization:**
- [ ] Proper module structure (main.rs and student.rs)
- [ ] Public items marked with `pub`
- [ ] Imports use `use` statements correctly
- [ ] Code follows Rust naming conventions ([snake_case](https://rust-lang.github.io/api-guidelines/naming.html) for functions/variables)

**Testing:**
- [ ] Test module exists with `#[cfg(test)]`
- [ ] At least 12 tests covering different functionality
- [ ] Tests use assertions (`assert!`, `assert_eq!`)
- [ ] Edge cases tested (empty data, boundary values)

**Version control:**
- [ ] All files committed to Git
- [ ] Meaningful commit messages
- [ ] Changes pushed to GitHub
- [ ] GitHub Actions CI passing (green checkmark)

**Repository structure:**
- [ ] lab11/ directory exists in is4010-labs
- [ ] Contains Cargo.toml and src/ directory
- [ ] .github/workflows/lab11.yml exists
- [ ] Follows structure shown in "Expected repository structure" section

**Documentation:**
- [ ] Code includes comments for complex logic
- [ ] Struct fields and methods have doc comments (`///`)
- [ ] README.md updated (if you maintain one for labs)

---

## 📤 Final submission

### Step 1: Final build and test

```bash
cd lab11

# Clean and rebuild
cargo clean
cargo build

# Run tests
cargo test

# Verify executable runs
cargo run
```

### Step 2: Commit your work

```bash
# From is4010-labs root
git add lab11/
git add .github/workflows/lab11.yml

# Descriptive commit message
git commit -m "Complete Lab 11: Student management system with modules, structs, enums, and collections"
```

### Step 3: Push to GitHub

```bash
git push origin main
```

### Step 4: Verify on GitHub

1. Go to your repository: `https://github.com/yourusername/is4010-labs`
2. Check lab11 directory is present
3. Go to **Actions** tab
4. Verify "Lab 11 Tests" workflow passed (green checkmark)
5. If red X, click on it to see errors and fix them

### Step 5: Submit URL

Submit your repository URL on Canvas:
```
https://github.com/yourusername/is4010-labs
```

**The GitHub Actions must be passing (green checkmark) for full credit.**

---

## 🎯 Grading rubric

| Category | Points | Criteria |
|----------|--------|----------|
| **Module organization** | 1 | Proper module structure with student.rs, correct `pub` usage |
| **Student struct** | 2 | Complete struct with all fields, methods (new, class_standing, add_credits, can_graduate) |
| **Grade enum** | 1 | Enum with all variants (A-F), from_string, to_gpa_points, is_passing methods |
| **CourseGrade struct** | 1 | Correct struct with quality_points method |
| **StudentDatabase** | 2 | HashMap-based database with add, find, stats methods, proper error handling |
| **GPA calculation** | 1 | Accurate calculate_gpa implementation using iterators |
| **Tests** | 1 | Comprehensive test suite (12+ tests) all passing |
| **CI/CD** | 1 | GitHub Actions workflow configured and passing |
| **Total** | **10** | |

**Deductions:**
- -1: Compiler warnings present
- -2: Tests failing
- -2: CI/CD not set up or failing
- -3: Missing required functionality
- -5: Code doesn't compile

---

## 🚀 Going further (optional challenges)

Want to extend your skills? Try these:

### Challenge 1: Search functionality
Add search methods to StudentDatabase:
- Find students by name (partial match)
- Find students with GPA above threshold
- Find students who can graduate

### Challenge 2: Academic warnings
Add method to flag students:
- On academic probation (GPA < 2.0)
- At risk (GPA < 2.5)
- Dean's list (GPA >= 3.5)

### Challenge 3: Course enrollment
Add a Course struct and enrollment management:
- Students can enroll in courses
- Courses have max capacity
- Track current enrollments

### Challenge 4: Data persistence
Save and load student data:
- Serialize to JSON with [serde](https://serde.rs/)
- Write to file
- Read from file on startup

### Challenge 5: CLI interface
Build a command-line interface:
- Interactive menu
- Commands: add student, find student, list all, quit
- Use [std::io](https://doc.rust-lang.org/std/io/) for input

---

## 📚 Additional resources

### Official documentation
- [The Rust Programming Language Book](https://doc.rust-lang.org/book/)
- [Rust by Example](https://doc.rust-lang.org/rust-by-example/)
- [Rust Standard Library Documentation](https://doc.rust-lang.org/std/)
- [Cargo Book](https://doc.rust-lang.org/cargo/)

### Week 11 course materials
- [Week 11 Slides](../../slides/IS4010_W11_Structuring_Code_and_Data.qmd)
- [Week 11 Lecture Notes](../../resources/lecture-notes/W11_Structuring_Code_and_Data_notes.md)
- [Week 11 Interactive Exercises](../../resources/lecture-notes/W11_Structuring_Code_and_Data_exercises.md)

### Testing resources
- [Rust Testing Guide](https://doc.rust-lang.org/book/ch11-00-testing.html)
- [Cargo Test Documentation](https://doc.rust-lang.org/cargo/commands/cargo-test.html)
- [Test Organization](https://doc.rust-lang.org/book/ch11-03-test-organization.html)

### Community help
- [Rust Users Forum](https://users.rust-lang.org/)
- [r/rust subreddit](https://www.reddit.com/r/rust/)
- [Rust Discord](https://discord.gg/rust-lang)
- Course Microsoft Teams channel

---

**Remember:** This lab brings together everything you've learned about Rust so far. Take your time, use AI tools strategically, and don't hesitate to ask for help. The goal is to build understanding, not just get it working!

**Good luck!** 🦀

---

**Lab created:** 2025-01-26
**Last updated:** 2025-01-26
**Course:** IS4010 - AI-Enhanced Application Development
**Instructor:** Brandon M. Greenwell
