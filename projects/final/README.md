# Final Project: Solo CLI Application

**Due:** Sunday, December 1, 2024 at 11:59 PM (End of Week 14)
**Points:** 31 points (20% of your final grade)

## Objective

Build a complete, professional command-line application in **Python** or **Rust** that showcases everything you've learned this semester. This is your opportunity to create a portfolio piece that demonstrates your ability to design, develop, test, and document a real-world application using modern development practices and AI-assisted workflows.

## Background

Command-line applications are fundamental tools in software development and system administration. Many of the most powerful and widely-used tools—from [Git](https://git-scm.com/) to [ripgrep](https://github.com/BurntSushi/ripgrep) to [ffmpeg](https://ffmpeg.org/)—are CLI applications. They're efficient, scriptable, and often serve as the foundation for more complex systems.

This final project synthesizes all the skills you've developed throughout IS4010:
- **Python or Rust development** with professional code organization
- **Automated testing** with [pytest](https://docs.pytest.org/) or [cargo test](https://doc.rust-lang.org/cargo/commands/cargo-test.html)
- **CI/CD pipelines** using [GitHub Actions](https://docs.github.com/en/actions)
- **Professional documentation** with comprehensive README files
- **AI-assisted development** with strategic use of tools like GitHub Copilot and Gemini
- **Version control** with Git and GitHub

Unlike your previous labs, this project is **completely open-ended**—you choose what to build. The only requirements are that it's a working CLI application with tests, CI/CD, and professional documentation.

---

## Prerequisites

Before starting this project, ensure you have:

- ✅ Completed Labs 01-12 (or at least Labs 01-06 and Lab 09)
- ✅ [Python 3.10+](https://www.python.org/downloads/) **OR** [Rust toolchain](https://www.rust-lang.org/tools/install) installed
- ✅ [Git](https://git-scm.com/downloads) configured and working
- ✅ [VS Code](https://code.visualstudio.com/) (or your preferred editor)
- ✅ [pytest](https://docs.pytest.org/en/stable/getting-started.html) installed (if using Python)
- ✅ A [GitHub](https://github.com/) account
- ✅ Familiarity with [GitHub Actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions) from Lab 03

**💡 Need help with setup?** Check the [SETUP_GUIDE.md](../../resources/SETUP_GUIDE.md) in the course repository.

---

## Technical Requirements

Your final project must meet all of the following requirements:

### 1. **New Public GitHub Repository** 🌐

- Create a **NEW** public repository for this project (not your `is4010-labs` repo)
- Suggested naming: `is4010-final-[descriptive-name]` (e.g., `is4010-final-password-manager`)
- **Public visibility is required** so the project can serve as a portfolio piece
- Initialize with a README.md file

**Why public?** Unlike your labs (which use private repos to prevent academic integrity issues), this final project is meant to showcase your work to potential employers and the broader developer community.

### 2. **Programming Language** 💻

Choose **either** [Python 3.10+](https://www.python.org/) **or** [Rust](https://www.rust-lang.org/):

- **Python**: Modern, idiomatic Python with proper package structure
- **Rust**: Standard Cargo project with proper module organization

You cannot mix languages in a single project—pick one and commit to it.

### 3. **Functional CLI Application** ⚙️

Your application must:
- Run from the command line with clear usage instructions
- Accept user input (via command-line arguments, interactive prompts, or both)
- Produce meaningful output
- Handle errors gracefully (invalid input, missing files, network errors, etc.)
- Be **original work**—not a copy of an existing tutorial or lab

### 4. **Automated Testing** 🧪

- **Python projects**: Use [pytest](https://docs.pytest.org/) with tests in `test_*.py` files
- **Rust projects**: Use [cargo test](https://doc.rust-lang.org/cargo/commands/cargo-test.html) with tests in `src/` or `tests/`
- **Requirement**: Tests for all major features and functions
- Tests must pass both locally and in CI/CD
- Focus on testing core functionality, edge cases, and error handling

### 5. **GitHub Actions CI/CD Pipeline** 🔄

- Include a `.github/workflows/` directory with a workflow file (e.g., `tests.yml`)
- Workflow must:
  - Run automatically on every push to `main`
  - Execute all tests
  - Report pass/fail status
- **All tests must pass** in the final submission

**Reference your Lab 03 workflow** or use the examples in the [GitHub Actions documentation](https://docs.github.com/en/actions/automating-builds-and-tests).

### 6. **Professional README with Required Badges** 📄

Your README.md must include:
- **Project title and description**: What does your app do?
- **Three required badges** (explained in detail below):
  1. CI/CD status badge
  2. License badge
  3. Language/version badge
- **Installation instructions**: Step-by-step guide to get your app running
- **Usage examples**: Show how to use your app with actual command examples and expected output
- **Features list**: What can your application do?
- **Testing instructions**: How to run tests locally
- **License section**: Reference to your LICENSE file
- **AI-assisted development note**: Brief mention that this project was developed with AI assistance

See the "Professional README Requirements" section below for detailed guidance.

### 7. **LICENSE File** 📜

- Include a `LICENSE` file in your repository root
- Use the **[MIT License](https://choosealicense.com/licenses/mit/)** (recommended for educational/portfolio projects)
- Update the copyright year (2024) and your name

See the "Adding a License to Your Project" section below for step-by-step instructions.

### 8. **AI-Assisted Development Documentation** 🤖

- Create an `AGENTS.md` file documenting your AI tool usage
- Include:
  - Which AI tools you used (GitHub Copilot, Gemini, Claude, ChatGPT, etc.)
  - How you used them (code generation, debugging, learning new concepts, etc.)
  - Specific examples of helpful prompts
  - Reflection on how AI assistance impacted your development process
  - Any challenges or limitations you encountered with AI tools

This demonstrates your ability to use AI strategically and ethically in software development.

---

## Understanding Project Badges 🏷️

**What are badges?**
Badges are small visual indicators at the top of your README that communicate important information about your project at a glance. They're a standard convention in open-source development.

![Example badges](https://img.shields.io/badge/build-passing-brightgreen) ![License](https://img.shields.io/badge/license-MIT-blue) ![Python](https://img.shields.io/badge/python-3.10+-blue)

Professional developers use badges to show:
- Build/test status (is the code currently working?)
- License type (how can others use this code?)
- Language and version requirements
- Code coverage, dependencies, and more

**Why badges matter for your project:**
- They demonstrate professional development practices
- They make your project more credible and trustworthy
- They're expected in portfolio projects that employers will review
- They provide instant visibility into project health

### Required Badges for Your Project

You must include all three of these badges in your README:

#### 1. **CI/CD Status Badge** ✅

Shows whether your tests are currently passing. This is generated automatically by GitHub Actions.

**What it looks like:**
![Build Status](https://img.shields.io/badge/build-passing-brightgreen)

**How to add it:**

1. Go to your GitHub repository
2. Click on the "Actions" tab
3. Click on your workflow (e.g., "Run Tests")
4. Click the "..." menu (top right) and select "Create status badge"
5. Copy the markdown code and paste it at the top of your README

**Example markdown:**
```markdown
![Tests](https://github.com/your-username/your-repo/actions/workflows/tests.yml/badge.svg)
```

**AI assistance prompt:**
```
"How do I add a GitHub Actions status badge to my README for a workflow named 'tests.yml'?"
```

#### 2. **License Badge** 📜

Shows that your project has a clear license (MIT in this case).

**What it looks like:**
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)

**How to add it:**

Use [Shields.io](https://shields.io/) to generate a license badge. The markdown is simple:

```markdown
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
```

Or link it to your LICENSE file:
```markdown
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
```

**AI assistance prompt:**
```
"Show me the markdown for an MIT license badge from shields.io that links to my LICENSE file"
```

#### 3. **Language/Version Badge** 🐍 🦀

Shows which programming language and version your project uses.

**What it looks like:**
![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg) **or** ![Rust](https://img.shields.io/badge/rust-1.70+-orange.svg)

**How to add it:**

**For Python projects:**
```markdown
![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)
```

**For Rust projects:**
```markdown
![Rust](https://img.shields.io/badge/rust-1.70+-orange.svg)
```

Adjust the version number to match your project's requirements.

**AI assistance prompt:**
```
"How do I create a Python version badge showing 3.10+ using shields.io?"
```

### Putting It All Together

At the top of your README (right after your title), include all three badges:

```markdown
# My Amazing CLI Tool

![Tests](https://github.com/username/repo/actions/workflows/tests.yml/badge.svg)
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)

A brief description of what your tool does...
```

**💡 Pro tip:** You can explore more badge options at [Shields.io](https://shields.io/)—but stick to the three required badges to keep your README clean and professional.

---

## Adding a License to Your Project 📋

**What is an open-source license?**
A license tells others how they can legally use, modify, and distribute your code. Without a license, your code is technically "all rights reserved," meaning others can't legally use it—even if it's on public GitHub.

**Why does it matter?**
- **For you**: Protects your work while allowing others to learn from it
- **For employers**: Shows you understand professional development practices
- **For collaborators**: Makes it clear how they can use your code

**Which license should you use?**
We recommend the **[MIT License](https://choosealicense.com/licenses/mit/)** for educational projects because it's:
- Simple and easy to understand
- Permissive (allows others to use your code freely)
- Industry-standard for open-source projects
- Used by major projects like React, Node.js, and Rails

### Step-by-Step: Adding an MIT License

#### 1. Create a LICENSE File

In your repository root, create a new file named `LICENSE` (all caps, no file extension).

#### 2. Get the MIT License Text

Visit [choosealicense.com/licenses/mit](https://choosealicense.com/licenses/mit/) and copy the license text, **OR** use this template:

```
MIT License

Copyright (c) 2024 [Your Name]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

#### 3. Customize the License

Replace `[Your Name]` with your actual name. You can use your full name or GitHub username.

#### 4. Add License Section to README

At the bottom of your README.md, add a "License" section:

```markdown
## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```

#### 5. Add the License Badge

As described in the badges section above, add the MIT license badge to the top of your README:

```markdown
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
```

### Using AI Assistance for Licensing

**Helpful prompts:**

```
"Generate an MIT license file with my name [Your Name] and the year 2024"
```

```
"How do I properly reference my LICENSE file in my README?"
```

```
"What's the difference between MIT and Apache 2.0 licenses?"
```

**💡 Pro tip:** GitHub can automatically detect your LICENSE file and display it on your repository page, making it easy for visitors to understand how they can use your code.

---

## Professional README Requirements

Your README.md is the front door to your project. It should be **comprehensive, well-organized, and easy to follow**. Think of it as documentation for both users and potential employers reviewing your portfolio.

### Required Sections

Your README must include all of these sections in order:

#### 1. **Title and Description**

```markdown
# Project Title

Brief (1-2 sentence) description of what your application does and why it's useful.
```

#### 2. **Badges**

```markdown
![Tests](https://github.com/username/repo/actions/workflows/tests.yml/badge.svg)
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)
```

#### 3. **Table of Contents** (optional but recommended for longer READMEs)

```markdown
## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [Features](#features)
- [Testing](#testing)
- [License](#license)
```

#### 4. **Installation**

Step-by-step instructions to get your application running:

**For Python:**
```markdown
## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/username/repo.git
   cd repo
   ```

2. Create a virtual environment (recommended):
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
```

**For Rust:**
```markdown
## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/username/repo.git
   cd repo
   ```

2. Build the project:
   ```bash
   cargo build --release
   ```

3. The executable will be in `target/release/[your-app-name]`
```

#### 5. **Usage**

Show how to use your application with **real examples** and **expected output**:

```markdown
## Usage

Basic usage:
```bash
python my_app.py --input data.txt
```

Example with all options:
```bash
python my_app.py --input data.txt --output results.json --verbose
```

**Example output:**
```
Processing data.txt...
Found 150 entries
Generating report...
✓ Report saved to results.json
```
```

**💡 Include multiple examples** showing different features and use cases.

#### 6. **Features**

List what your application can do:

```markdown
## Features

- ✅ Parse and validate JSON data files
- ✅ Generate summary statistics
- ✅ Export results in multiple formats (JSON, CSV)
- ✅ Colorful terminal output for better readability
- ✅ Comprehensive error handling
```

#### 7. **Testing**

Explain how to run tests locally:

**For Python:**
```markdown
## Testing

Run the test suite with pytest:

```bash
pytest
```

For verbose output:
```bash
pytest -v
```
```

**For Rust:**
```markdown
## Testing

Run the test suite:

```bash
cargo test
```

For verbose output:
```bash
cargo test -- --show-output
```
```

#### 8. **AI-Assisted Development**

Brief note about AI usage:

```markdown
## AI-Assisted Development

This project was developed with assistance from AI tools including GitHub Copilot and Gemini. For details on how AI was used, see [AGENTS.md](AGENTS.md).
```

#### 9. **License**

Reference your LICENSE file:

```markdown
## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```

### README Template

Here's a complete template you can adapt:

```markdown
# [Your Project Title]

[Brief description of what your app does and why it exists]

![Tests](https://github.com/username/repo/actions/workflows/tests.yml/badge.svg)
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)

## Installation

[Step-by-step installation instructions]

## Usage

[Examples showing how to use your app]

## Features

- Feature 1
- Feature 2
- Feature 3

## Testing

[Instructions for running tests]

## AI-Assisted Development

This project was developed with assistance from AI tools including GitHub Copilot and Gemini. For details, see [AGENTS.md](AGENTS.md).

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```

**AI assistance prompts for README writing:**

```
"Help me write a professional README for a CLI app that [describe your app]. Include installation, usage, and features sections."
```

```
"What should I include in the Usage section of my README for a Python CLI tool?"
```

```
"Review my README and suggest improvements for clarity and professionalism"
```

---

## Project Scope Guidance

Since this is an open-ended project, you might wonder: "How complex should my project be?" Here's guidance to help you succeed:

### Recommended (Not Required) Characteristics

These are **suggestions to help you build something substantial**—not strict requirements:

✅ **Multiple features/commands**: Aim for 3+ distinct capabilities
✅ **Multiple files/modules**: Organize code into logical modules, not one giant file
✅ **External dependencies**: Use at least one external library/crate (e.g., `requests`, `clap`, `serde`)
✅ **Data persistence**: Save/load data from files, JSON, or a database
✅ **Error handling**: Gracefully handle invalid input, missing files, network errors

### Complexity Levels

Here's how to think about project scope:

**⭐ Simple** (Good for a passing grade):
- Single core feature with 1-2 variations
- Basic error handling
- Simple text I/O
- Example: Password generator with strength checker

**⭐⭐ Moderate** (Good for a strong grade):
- 3-4 related features
- File I/O or data persistence
- Good error handling
- Clean code organization
- Example: Task tracker with add/list/complete/delete commands

**⭐⭐⭐ Advanced** (Excellent portfolio piece):
- 5+ well-integrated features
- External API integration or complex data processing
- Comprehensive error handling and edge cases
- Professional code quality and documentation
- Example: GitHub repository analyzer with statistics and visualizations

**💡 Start simple and add features incrementally!** It's better to have a simple, polished project than an ambitious, broken one.

### Scope Management Tips

1. **Define your MVP** (Minimum Viable Product): What's the simplest version that works?
2. **Build incrementally**: Get one feature working before adding the next
3. **Test as you go**: Write tests for each feature as you build it
4. **Use AI strategically**: Let AI help with boilerplate, but understand every line
5. **Track your time**: This shouldn't take more than 10-15 hours total

**Don't overthink it!** If you're excited about the idea and can describe 3+ features it should have, you're on the right track.

---

## Example Project Ideas

Here are concrete examples to inspire you. You're **encouraged to propose your own ideas**—the best project is one you're genuinely excited to build!

### Python Project Ideas 🐍

#### 1. **Weather Dashboard CLI** ⭐⭐
**Description**: A command-line weather app that fetches current conditions and forecasts using a free weather API.

**Key features**:
- Fetch weather for any city using the [OpenWeatherMap API](https://openweathermap.org/api)
- Display current conditions (temp, humidity, conditions)
- 5-day forecast view
- Save favorite cities
- Colorful terminal output with [Rich](https://rich.readthedocs.io/) or [Colorama](https://pypi.org/project/colorama/)

**External libraries**: `requests`, `python-dotenv`, `rich` or `colorama`

**AI prompts to get started**:
```
"How do I use the OpenWeatherMap API in Python to get weather data?"
"Show me how to use the requests library to make API calls with error handling"
```

---

#### 2. **Markdown Note Manager** ⭐⭐
**Description**: A CLI tool for creating, organizing, and searching markdown notes.

**Key features**:
- Create new notes with automatic timestamps
- List all notes with previews
- Search notes by title or content
- Tag system for organization
- Export notes to HTML

**External libraries**: `markdown2`, `click` or `argparse`

**AI prompts to get started**:
```
"How do I implement a simple search function for markdown files in Python?"
"Show me how to use argparse to create a CLI with multiple subcommands"
```

---

#### 3. **CSV Data Analyzer** ⭐⭐
**Description**: A tool that reads CSV files and generates statistical summaries and visualizations.

**Key features**:
- Load and validate CSV files
- Generate summary statistics (mean, median, mode, etc.)
- Identify missing data and outliers
- Export results to JSON or formatted text
- Optional: simple ASCII charts

**External libraries**: `pandas`, `numpy`, `tabulate`

**AI prompts to get started**:
```
"How do I use pandas to read a CSV and generate summary statistics?"
"Show me how to create an ASCII chart in Python for displaying data"
```

---

#### 4. **Password Manager CLI** ⭐⭐⭐
**Description**: A secure local password manager with encryption.

**Key features**:
- Add/view/update/delete stored credentials
- Master password protection
- Encryption using `cryptography` library
- Password strength checker
- Generate strong random passwords
- Search stored credentials

**External libraries**: `cryptography`, `click`, `getpass`

**AI prompts to get started**:
```
"How do I use the Python cryptography library to encrypt and decrypt data?"
"Show me how to securely handle password input in a CLI application"
```

---

### Rust Project Ideas 🦀

#### 1. **File Organizer** ⭐⭐
**Description**: A CLI tool that organizes files in a directory by type, date, or custom rules.

**Key features**:
- Scan a directory for files
- Organize by extension (images, documents, videos, etc.)
- Organize by date (year/month folders)
- Dry-run mode to preview changes
- Undo last organization operation

**External crates**: `clap`, `walkdir`, `chrono`

**AI prompts to get started**:
```
"How do I use the walkdir crate in Rust to recursively scan directories?"
"Show me how to use clap to create a Rust CLI with subcommands"
```

---

#### 2. **Log File Analyzer** ⭐⭐⭐
**Description**: A fast log parser that extracts insights from server logs.

**Key features**:
- Parse common log formats (Apache, Nginx, JSON logs)
- Count occurrences of status codes, IP addresses, URLs
- Filter logs by date range or search term
- Generate summary reports
- Export results to JSON or CSV

**External crates**: `clap`, `regex`, `serde`, `serde_json`

**AI prompts to get started**:
```
"How do I use regex in Rust to parse Apache log file lines?"
"Show me how to use serde to serialize Rust structs to JSON"
```

---

#### 3. **Duplicate File Finder** ⭐⭐
**Description**: A tool that finds duplicate files in a directory tree using file hashing.

**Key features**:
- Recursively scan directories
- Calculate file hashes (SHA-256) to find duplicates
- Display duplicate groups with file sizes
- Option to delete duplicates (with confirmation)
- Dry-run mode

**External crates**: `clap`, `walkdir`, `sha2`, `hex`

**AI prompts to get started**:
```
"How do I calculate SHA-256 hashes of files in Rust?"
"Show me how to group files by their hash values using a HashMap in Rust"
```

---

#### 4. **Todo List Manager** ⭐
**Description**: A simple command-line todo list with persistence.

**Key features**:
- Add, list, complete, and delete tasks
- Mark tasks as high/medium/low priority
- Due dates for tasks
- Save/load from JSON file
- Filter by status or priority

**External crates**: `clap`, `serde`, `serde_json`, `chrono`

**AI prompts to get started**:
```
"How do I create a Rust struct for a todo item and serialize it to JSON?"
"Show me how to use clap to handle multiple subcommands in Rust"
```

---

### More Ideas

**Other Python ideas**: GitHub repository analyzer, expense tracker, URL shortener, RSS feed reader, quiz game generator, file encryption tool

**Other Rust ideas**: System monitor, download manager, text editor, grep clone, JSON formatter/validator, HTTP server

**💡 Pro tip:** Choose a project that solves a problem you actually have. You'll be more motivated, and it'll make a better portfolio piece!

---

## Expected Repository Structure

Your final project repository should follow professional code organization practices:

### Python Project Structure

```
is4010-final-my-app/
├── .github/
│   └── workflows/
│       └── tests.yml          # GitHub Actions workflow
├── src/                        # Source code directory (optional but recommended)
│   ├── __init__.py
│   ├── main.py                # Main entry point
│   └── utils.py               # Helper functions/modules
├── tests/                      # Test directory
│   ├── __init__.py
│   ├── test_main.py
│   └── test_utils.py
├── .gitignore                  # Ignore venv/, __pycache__/, etc.
├── AGENTS.md                   # AI usage documentation
├── LICENSE                     # MIT License file
├── README.md                   # Professional README with badges
└── requirements.txt            # Python dependencies
```

**Alternative simpler structure** (acceptable for smaller projects):
```
is4010-final-my-app/
├── .github/workflows/tests.yml
├── my_app.py                   # Main application file
├── test_my_app.py              # Tests
├── .gitignore
├── AGENTS.md
├── LICENSE
├── README.md
└── requirements.txt
```

### Rust Project Structure

```
is4010-final-my-app/
├── .github/
│   └── workflows/
│       └── tests.yml          # GitHub Actions workflow
├── src/
│   ├── main.rs                # Main entry point
│   ├── lib.rs                 # Library code (if applicable)
│   └── utils.rs               # Helper modules
├── tests/                      # Integration tests (optional)
│   └── integration_test.rs
├── .gitignore                  # Ignore target/, Cargo.lock (for binaries)
├── AGENTS.md                   # AI usage documentation
├── Cargo.toml                  # Dependencies and project metadata
├── LICENSE                     # MIT License file
└── README.md                   # Professional README with badges
```

**Key points:**
- **Clean organization**: Related code grouped logically
- **Tests separated**: Test files clearly identified
- **Dependencies explicit**: `requirements.txt` or `Cargo.toml` includes all dependencies
- **.gitignore present**: Don't commit venv/, __pycache__/, target/, etc.
- **All required files**: LICENSE, AGENTS.md, README.md, workflow file

---

## Testing Requirements 🧪

Your project must include automated tests that verify core functionality.

### Python Testing with pytest

**Minimum requirements**:
- Tests for all major functions/features
- Tests must pass locally when you run `pytest`
- Tests must pass in GitHub Actions CI/CD
- Use clear, descriptive test function names

**Example test structure**:

```python
# test_my_app.py
import pytest
from my_app import main_function, helper_function

def test_main_function_with_valid_input():
    """Test that main_function works with valid input."""
    result = main_function("valid input")
    assert result == expected_output

def test_main_function_with_invalid_input():
    """Test that main_function handles invalid input gracefully."""
    result = main_function("")
    assert result is None or result == ""

def test_helper_function_edge_case():
    """Test helper_function with edge case."""
    result = helper_function([])
    assert result == []
```

**Running tests**:
```bash
pytest                    # Run all tests
pytest -v                 # Verbose output
pytest test_my_app.py     # Run specific test file
```

**AI assistance prompts**:
```
"How do I write pytest tests for a function that [describe your function]?"
"Show me how to test error handling in pytest"
"How do I mock user input in pytest?"
```

### Rust Testing with cargo test

**Minimum requirements**:
- Tests for all major functions
- Tests must pass locally when you run `cargo test`
- Tests must pass in GitHub Actions CI/CD
- Use clear, descriptive test names

**Example test structure**:

```rust
// src/lib.rs or src/main.rs

pub fn add(a: i32, b: i32) -> i32 {
    a + b
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_add_positive_numbers() {
        assert_eq!(add(2, 3), 5);
    }

    #[test]
    fn test_add_negative_numbers() {
        assert_eq!(add(-2, -3), -5);
    }

    #[test]
    fn test_add_zero() {
        assert_eq!(add(0, 5), 5);
    }
}
```

**Running tests**:
```bash
cargo test                   # Run all tests
cargo test -- --show-output  # Show println! output
cargo test test_add          # Run specific test
```

**AI assistance prompts**:
```
"How do I write unit tests in Rust for a function that [describe your function]?"
"Show me how to test error cases in Rust using Result"
"How do I organize tests in a Rust project?"
```

### GitHub Actions Workflow

Your `.github/workflows/tests.yml` file should run tests automatically:

**Python example**:
```yaml
name: Run Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      - name: Install dependencies
        run: |
          pip install -r requirements.txt
      - name: Run tests
        run: |
          pytest
```

**Rust example**:
```yaml
name: Run Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up Rust
        uses: actions-rs/toolchain@v1
        with:
          toolchain: stable
      - name: Run tests
        run: cargo test
```

**💡 Pro tip:** Check your GitHub Actions tab after pushing to ensure tests pass. A green checkmark means success!

---

## 🚨 Troubleshooting Guide

Common issues you might encounter and how to solve them:

### **Problem: "My GitHub Actions badge shows 'failing'"**
- **Cause**: Tests are failing in CI/CD
- **Solution**:
  - Click on the badge or go to the "Actions" tab to see the error
  - Tests might pass locally but fail in CI due to missing dependencies
  - Ensure `requirements.txt` (Python) or `Cargo.toml` (Rust) lists all dependencies
  - Check that file paths work in the CI environment (use relative paths)

**AI assistance prompt**:
```
"My pytest tests pass locally but fail in GitHub Actions with this error: [paste error]. How do I fix it?"
```

---

### **Problem: "My badges aren't displaying in my README"**
- **Cause**: Incorrect markdown syntax or URL
- **Solution**:
  - Check for typos in the badge markdown
  - Ensure your repository is public (badges won't work on private repos for external viewers)
  - For the CI/CD badge, make sure the workflow file name matches (e.g., `tests.yml`)
  - Test badge URLs directly in your browser

**AI assistance prompt**:
```
"My GitHub Actions badge markdown isn't working. Here's what I have: [paste markdown]. What's wrong?"
```

---

### **Problem: "I don't know what to build"**
- **Cause**: Too many options can be overwhelming
- **Solution**:
  - Think about tasks you do repeatedly that could be automated
  - Look at the example projects and pick one that interests you
  - Start with something simple—you can always add features later
  - Ask yourself: "What would I actually use?"

**AI assistance prompt**:
```
"I need to build a CLI app for my final project. I'm interested in [your interests]. Suggest 5 specific project ideas."
```

---

### **Problem: "My tests work locally but not in GitHub Actions"**
- **Cause**: Environment differences between local and CI
- **Solution**:
  - Check Python version matches (use Python 3.10+ in both)
  - For Rust, ensure you're using stable toolchain
  - Look for hardcoded absolute paths (use relative paths instead)
  - Check for missing dependencies in requirements.txt or Cargo.toml
  - Review the full error output in the Actions tab

**AI assistance prompt**:
```
"My tests pass locally with pytest but fail in GitHub Actions. Here's the CI error: [paste error]. How do I debug this?"
```

---

### **Problem: "I'm getting import errors in my tests"**
- **Cause**: Python can't find your modules
- **Solution**:
  - For Python: Make sure your files are in the same directory, or use proper package structure with `__init__.py`
  - Check that your import statements match your actual file/module names
  - For Rust: Make sure you've declared modules correctly in `main.rs` or `lib.rs`

**AI assistance prompt**:
```
"I'm getting 'ModuleNotFoundError: No module named X' when running pytest. My project structure is [describe structure]. How do I fix imports?"
```

---

### **Problem: "My LICENSE file isn't showing up on GitHub"**
- **Cause**: Filename or location issue
- **Solution**:
  - File must be named exactly `LICENSE` (all caps, no extension)
  - Must be in repository root (not in a subdirectory)
  - Must contain valid license text
  - GitHub may take a few minutes to detect it after pushing

---

### **Problem: "I'm stuck on a bug and can't figure it out"**
- **Cause**: Welcome to programming! This happens to everyone.
- **Solution**:
  - **Read the error message carefully**: It usually tells you exactly what's wrong
  - **Use AI debugging**: Paste your error and relevant code into Gemini/Claude/ChatGPT
  - **Add print statements**: See what values your variables actually have
  - **Test with simple inputs**: Isolate the problem
  - **Take a break**: Sometimes stepping away helps

**AI assistance prompts**:
```
"I'm getting this error: [paste error]. Here's my code: [paste code]. What's causing this?"
```

```
"My function should do [expected behavior] but it's doing [actual behavior]. Here's my code: [paste code]. What's wrong?"
```

```
"Debug this code: [paste code]. It should [expected] but returns [actual]."
```

---

### **Problem: "My code works but is messy/hard to understand"**
- **Cause**: First draft code is rarely perfect
- **Solution**:
  - Refactor in small steps
  - Break long functions into smaller helper functions
  - Add comments explaining complex logic
  - Use meaningful variable names
  - Let AI help with refactoring

**AI assistance prompts**:
```
"Refactor this code to make it more readable: [paste code]"
```

```
"My function is too long and complex. How can I break it into smaller functions? [paste code]"
```

```
"Review this code and suggest improvements for clarity: [paste code]"
```

---

### **Problem: "I don't understand how to implement [feature]"**
- **Cause**: Learning new concepts is part of development
- **Solution**:
  - Break the feature into smaller steps
  - Search for examples (GitHub, Stack Overflow)
  - Ask AI to explain the concept and show examples
  - Look at official documentation for libraries you're using
  - Start with the simplest possible implementation

**AI assistance prompts**:
```
"Explain how to [feature you want to implement] in Python with a simple example"
```

```
"Show me step-by-step how to implement [feature] in Rust"
```

```
"I want to [describe feature]. What's the best approach and which libraries should I use?"
```

---

### **Still stuck? Here's your debugging checklist:**

- [ ] Read the full error message (don't just skim it)
- [ ] Search the error message on Google/Stack Overflow
- [ ] Check official documentation for any libraries you're using
- [ ] Try the same operation with simpler input
- [ ] Add print/debug statements to see what's happening
- [ ] Ask AI for help with the specific error
- [ ] If all else fails, ask during office hours or on the course forum

**💡 Pro tip:** Learning to debug effectively is one of the most valuable skills you'll develop. Embrace the struggle—it makes you a better developer!

---

## AI Integration Strategy 🤖

AI tools are **encouraged and expected** for this project. Use them strategically to accelerate development and learning.

### Recommended AI Tools

- **[GitHub Copilot](https://github.com/features/copilot)**: In-editor code completion and suggestions
- **[Gemini](https://gemini.google.com/)**: Planning, debugging, and conceptual help
- **[Claude](https://claude.ai/)**: Code review and refactoring suggestions
- **[ChatGPT](https://chat.openai.com/)**: General programming help and explanations

### Strategic AI Usage by Phase

**1. Planning Phase**
```
"I want to build a CLI app that [describe your idea]. What features should it have? What Python libraries would be useful?"
```

```
"Help me break down this project into smaller tasks: [describe project]"
```

**2. Development Phase**
```
"Show me how to [specific task] in Python/Rust"
```

```
"I need a function that [describe functionality]. Show me an implementation with error handling."
```

**3. Testing Phase**
```
"Write pytest tests for this function: [paste function]"
```

```
"What edge cases should I test for a function that [describe function]?"
```

**4. Debugging Phase**
```
"This code gives error: [error]. Here's my code: [code]. What's wrong?"
```

```
"My function returns [wrong result] instead of [expected result]. Debug this: [code]"
```

**5. Documentation Phase**
```
"Write a professional README for this project: [describe project]"
```

```
"Generate installation instructions for a Python CLI app with these dependencies: [list deps]"
```

### Documenting AI Usage in AGENTS.md

Your `AGENTS.md` file should include:

**1. Tools Used**
```markdown
## AI Tools Used

- **GitHub Copilot**: Code completion and boilerplate generation
- **Gemini**: Initial project planning and architecture decisions
- **Claude**: Code review and refactoring suggestions
```

**2. Specific Examples**
```markdown
## Example Prompts and Results

### Planning
**Prompt**: "Help me design a password manager CLI. What features should it have?"
**Result**: AI suggested encryption, master password, CRUD operations, and password generation features.

### Implementation
**Prompt**: "Show me how to use the cryptography library to encrypt/decrypt strings in Python"
**Result**: Provided working code using Fernet symmetric encryption.

### Debugging
**Prompt**: "Getting 'JSONDecodeError' when loading saved data. Code: [...]"
**Result**: AI identified that I wasn't handling empty files correctly. Fixed by adding file existence check.
```

**3. Reflection**
```markdown
## Reflection

### What Worked Well
- Copilot was excellent for generating boilerplate code and test structures
- Gemini helped me understand encryption concepts I hadn't used before
- AI debugging saved hours when I had import errors

### Challenges
- Sometimes AI suggestions were overcomplicated; I had to ask for simpler versions
- Had to verify that suggested libraries were actually available and up-to-date
- Needed to understand the code, not just copy it, to write effective tests

### Learning Impact
Using AI strategically made me more productive without sacrificing learning. I focused on understanding concepts and architecture while AI handled tedious boilerplate.
```

**💡 Pro tip:** Keep notes as you work—it's easier than trying to remember everything at the end!

---

## Submission Instructions 📬

### Final Checklist

Before submitting, verify **ALL** of these requirements:

- [ ] **Repository is public** (not private)
- [ ] **README.md complete** with all required sections
- [ ] **All 3 badges present** (CI/CD, License, Language)
- [ ] **LICENSE file exists** with MIT License and your name
- [ ] **AGENTS.md complete** with AI usage documentation
- [ ] **Tests written** for all major functionality
- [ ] **All tests passing** locally (`pytest` or `cargo test`)
- [ ] **GitHub Actions workflow exists** (`.github/workflows/tests.yml`)
- [ ] **CI/CD badge shows passing** (green checkmark)
- [ ] **Application runs** without errors
- [ ] **Installation instructions tested** (try following your own README)
- [ ] **Code is clean** and well-organized
- [ ] **Dependencies listed** (`requirements.txt` or `Cargo.toml`)
- [ ] **No sensitive data** in code (API keys, passwords, etc.)

### How to Submit

1. **Final commit and push**:
   ```bash
   git add .
   git commit -m "Final project submission"
   git push origin main
   ```

2. **Verify everything works**:
   - Visit your repository on GitHub
   - Check that badges are displaying
   - Click the "Actions" tab and confirm tests are passing
   - Verify LICENSE file is recognized by GitHub

3. **Submit to Canvas**:
   - Go to Canvas → IS4010 → Final Project assignment
   - Submit your **repository URL** (e.g., `https://github.com/username/is4010-final-my-app`)
   - **Due: Sunday, December 1, 2024 at 11:59 PM**

### After Submission

Your repository will serve as a **portfolio piece**. Consider:

- Adding it to your resume or LinkedIn as a project
- Sharing it with potential employers
- Continuing to improve it after the semester
- Using it as a foundation for future projects

**Congratulations!** You've completed a full software development project from concept to deployment. This demonstrates real-world development skills that employers value.

---

## Grading

Your final project will be graded on the following criteria (31 points total):

| Category | Points | Description |
|----------|--------|-------------|
| **Functionality** | 10 | Application runs without errors, implements core features as described |
| **Code Quality** | 6 | Clean, well-organized code following language conventions |
| **Testing** | 5 | Comprehensive tests covering major functionality, CI/CD passing |
| **Documentation** | 6 | Professional README, all badges present, clear installation/usage instructions |
| **AI Documentation** | 4 | Complete AGENTS.md showing strategic, thoughtful AI usage |

Detailed rubric available in the instructor materials.

---

## Questions?

- **Office hours**: Check Canvas for schedule
- **Course forum**: Post questions on Microsoft Teams
- **AI assistance**: Use Gemini/Claude/ChatGPT for technical help
- **Email**: [Instructor email] for private questions

---

**This is your chance to build something you're proud of. Make it count!** 🚀
