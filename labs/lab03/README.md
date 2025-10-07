# Lab 03: Python basics and automated testing

**Due Date: Sunday, September 15, 2024 at 11:59 PM**

## Objective

In this lab, you will practice Python fundamentals by building two small applications. More importantly, you will set up an automated testing and continuous integration (CI/CD) pipeline for your repository using `pytest` and GitHub Actions. This is a one-time setup that will automatically check your work for all future labs and establish professional development practices.

## Background

This lab marks your transition from basic Git workflows to professional Python development. You'll apply fundamental Python concepts through two engaging projects while establishing industry-standard testing practices.

**What you'll learn:**
- **Python fundamentals**: Variables, input/output, string formatting, and control flow
- **Interactive programming**: Building user-friendly applications with input validation
- **Professional testing**: Using pytest and GitHub Actions for continuous integration
- **Code quality**: Writing testable, maintainable code with proper documentation

This lab is divided into three parts:
- **Part 1**: Mad Libs generator (focus: variables, input, string manipulation)
- **Part 2**: Number guessing game (focus: loops, conditionals, random numbers)  
- **Part 3**: Automated testing setup (focus: professional development workflow)

---

## Part 1: The Mad Libs generator 🎭

Mad Libs is a classic word game where players provide words (without knowing the story context) that are then inserted into a story template, often creating hilarious results. You'll create a function that generates a story using provided words.

**Key concepts applied:**
- Function design and parameters
- String formatting with f-strings
- NumPy-style docstrings
- Writing testable code

### Requirements

Your function must:
- Accept exactly three string parameters: `adjective`, `noun`, `verb`
- Use **all three parameters** in the returned story
- Return a single string containing the complete story
- Use f-string formatting (not .format() or % formatting)
- Include proper NumPy-style documentation

### Instructions

1. In your `is4010-labs` repository, navigate to the `lab03/` folder and create a new file named `lab03.py`.
2. Copy the following function stub into your `lab03.py` file.
3. Replace the `pass` statement with your implementation.
4. Be creative! Write an engaging, fun story that uses all three words.

### Function specification

```python
def generate_mad_lib(adjective, noun, verb):
    """
    Generates a short story using the provided words.

    This function demonstrates string formatting and function design
    by creating a Mad Libs-style story from user-provided words.

    Parameters
    ----------
    adjective : str
        An adjective to use in the story (e.g., "silly", "brave", "colorful").
    noun : str
        A noun to use in the story (e.g., "cat", "computer", "adventure").
    verb : str
        A past-tense verb to use in the story (e.g., "jumped", "crashed", "danced").

    Returns
    -------
    str
        A formatted story string that incorporates all three input words.

    Examples
    --------
    >>> generate_mad_lib("silly", "cat", "jumped")
    "The silly cat jumped over the lazy dog and laughed."
    
    >>> generate_mad_lib("brave", "knight", "battled") 
    "Once upon a time, a brave knight battled dragons and saved the kingdom."
    """
    # TODO: Replace this with your creative story implementation
    # Must use f-string formatting and include all three parameters
    pass
```

**💡 Tips for success:**
- Make your story at least 10-15 words long for creativity points
- Ensure your story makes grammatical sense
- Test your function with different word combinations
- Remember: this function should NOT use `input()` - that makes it untestable

-----

## Part 2: The number guessing game 🎯

Build a classic interactive guessing game that demonstrates control flow, user interaction, and the random number generation. This game will challenge users to guess a secret number with helpful feedback.

**Key concepts applied:**
- While loops and loop control
- Conditional statements (if/elif/else)
- User input and type conversion
- Random number generation
- Game logic and user experience design

### Requirements

Your function must:
- Generate a random integer between 1 and 100 (inclusive)
- Use a `while` loop to continue until the correct guess
- Provide feedback: "Too high!", "Too low!", or success message
- Count and display the number of attempts
- Handle the game flow with clear, user-friendly prompts
- Use the `random` module for number generation

### Instructions

1. In the same `lab03/lab03.py` file, add the import statement and function below.
2. Complete the function implementation following the detailed requirements.
3. Add the provided runner code at the very bottom of your file.

### Function specification

```python
import random

def guessing_game():
    """
    Plays a number guessing game with the user.
    
    This interactive game demonstrates while loops, conditionals, and user input
    handling. The user attempts to guess a randomly generated number between
    1 and 100, receiving feedback after each guess.

    Game Flow:
    1. Generate a random secret number between 1 and 100 (inclusive)
    2. Prompt the user with clear instructions
    3. Use a while loop to continue until the user guesses correctly
    4. For each guess:
       - Convert user input to integer
       - Compare guess to secret number
       - Provide feedback: "Too high!", "Too low!", or success
       - Count attempts
    5. When correct, congratulate user and show number of attempts
    6. Exit the game

    Input Validation:
    - Assume user will enter valid integers (error handling not required)
    
    Example Game Session:
    --------
    Welcome to the Number Guessing Game!
    I'm thinking of a number between 1 and 100.
    Enter your guess: 50
    Too high! Try again.
    Enter your guess: 25
    Too low! Try again.
    Enter your guess: 37
    Congratulations! You guessed it in 3 attempts!
    """
    pass
```

### Game runner code

Add this code at the very bottom of your `lab03/lab03.py` file:

```python
if __name__ == '__main__':
    guessing_game()
```

**💡 Tips for success:**
- Start with a clear welcome message explaining the game
- Use descriptive variable names (`secret_number`, `attempts`, etc.)
- Test your game multiple times to ensure it works correctly
- Consider edge cases (guessing 1, guessing 100, etc.)
- The `random.randint(1, 100)` function generates inclusive ranges

-----

## Part 3: Setting up automated testing (CI/CD) 🔧

This is the **most important** part of the lab. You'll establish a professional testing workflow that will serve you throughout the course and in your career. Automated testing ensures your code works correctly and gives you instant feedback when you push changes to GitHub.

**Why automated testing matters:**
- **Quality assurance**: Catch bugs before they become problems
- **Confidence**: Make changes knowing tests will catch regressions
- **Professional practice**: Industry standard for all serious software projects
- **Instant feedback**: Know immediately if your code works correctly
- **Portfolio value**: Shows employers you understand professional development practices

### Step 3.1: Understanding and creating the test file 🧪

Tests verify that your functions work correctly by checking their outputs against expected results. We'll use `pytest`, Python's most popular testing framework.

**How tests work:**
1. Import your function from your main file
2. Call the function with known inputs
3. Check that the outputs are correct using `assert` statements
4. If all assertions pass, the test passes

**Testing concepts:**
- **Test discovery**: pytest automatically finds files starting with `test_`
- **Test functions**: Functions starting with `test_` are automatically run
- **Assertions**: `assert` statements check if conditions are True
- **Test isolation**: Each test runs independently

### Instructions for test file

1. In the `lab03/` folder of your `is4010-labs` repository, create a new file named `test_lab03.py`.
2. Copy the entire code block below into this new file.
3. **Do not modify the test file** - it's designed to work with any correct implementation.

```python
# test_lab03.py
import random
from unittest.mock import patch
from lab03 import generate_mad_lib, guessing_game

def test_generate_mad_lib():
    """
    Tests the generate_mad_lib function to ensure it uses the inputs correctly.
    
    This test verifies that:
    1. The function accepts three parameters
    2. All provided words appear in the returned story
    3. The function returns a string (not None or other type)
    """
    # Test case 1: Basic functionality
    adj = "silly"
    noun = "cat" 
    verb = "jumped"
    
    story = generate_mad_lib(adj, noun, verb)
    
    # Verify function returns a string
    assert isinstance(story, str), "Function should return a string"
    
    # Verify all words are used in the story
    assert adj in story, f"Adjective '{adj}' not found in story"
    assert noun in story, f"Noun '{noun}' not found in story"
    assert verb in story, f"Verb '{verb}' not found in story"
    
    # Test case 2: Different inputs
    adj2 = "brave"
    noun2 = "knight"
    verb2 = "battled"
    
    story2 = generate_mad_lib(adj2, noun2, verb2)
    
    assert isinstance(story2, str), "Function should return a string"
    assert adj2 in story2, f"Adjective '{adj2}' not found in story"
    assert noun2 in story2, f"Noun '{noun2}' not found in story"  
    assert verb2 in story2, f"Verb '{verb2}' not found in story"
    
    # Test case 3: Edge case with unusual inputs
    adj3 = "extraordinary"
    noun3 = "algorithm"
    verb3 = "computed"
    
    story3 = generate_mad_lib(adj3, noun3, verb3)
    
    assert isinstance(story3, str), "Function should return a string"
    assert adj3 in story3, f"Adjective '{adj3}' not found in story"
    assert noun3 in story3, f"Noun '{noun3}' not found in story"
    assert verb3 in story3, f"Verb '{verb3}' not found in story"


def test_guessing_game():
    """
    Tests the guessing_game function to ensure it handles the game flow correctly.
    
    This test uses mocking to simulate user input and verify that:
    1. The function can handle a winning game scenario
    2. Proper feedback is given for high/low guesses
    3. The game terminates when the correct number is guessed
    4. Attempt counting works correctly
    """
    # Mock random.randint in the lab03 module to return a predictable number (50)
    with patch('lab03.random.randint', return_value=50):
        # Mock input() to simulate user guesses: too high, too low, correct
        with patch('builtins.input', side_effect=['75', '25', '50']):
            # Mock print() to capture output
            with patch('builtins.print') as mock_print:
                # Run the guessing game
                guessing_game()
                
                # Verify that print was called (the game produced output)
                assert mock_print.called, "Game should produce output"
                
                # Check that the game printed some expected messages
                printed_output = [str(call) for call in mock_print.call_args_list]
                output_text = ' '.join(printed_output)
                
                # Verify game contains expected elements (flexible checking)
                # The game should mention numbers between 1 and 100
                contains_range = any('1' in output and '100' in output for output in printed_output)
                
                # Should contain some form of feedback
                contains_feedback = any(
                    'high' in output.lower() or 'low' in output.lower() or 
                    'congratulations' in output.lower() or 'correct' in output.lower()
                    for output in printed_output
                )
                
                assert contains_range or contains_feedback, "Game should provide range info or feedback"
    
    # Test edge case: immediate correct guess
    with patch('lab03.random.randint', return_value=42):
        with patch('builtins.input', side_effect=['42']):
            with patch('builtins.print') as mock_print:
                guessing_game()
                
                # Should still work with just one guess
                assert mock_print.called, "Game should work with immediate correct guess"
```

**💡 Understanding the tests:**

**Mad Libs test (`test_generate_mad_lib`):**
- Imports your function and calls it with different inputs
- Checks that all provided words appear somewhere in the returned story
- Verifies the function returns a string (not None or other types)
- Multiple test cases ensure your function works with various inputs

**Guessing Game test (`test_guessing_game`):**
- Uses advanced mocking techniques to test interactive functions
- Simulates user input with predetermined guesses
- Controls random number generation for predictable testing
- Verifies the game produces appropriate output and handles game flow
- Tests both multi-guess scenarios and immediate correct guesses

This demonstrates professional testing practices for interactive applications!

### Step 3.2: Create the GitHub Actions workflow ⚙️

GitHub Actions is a powerful automation platform built into GitHub. It allows you to run code, tests, and deployments automatically when certain events occur (like pushing code). This is called **Continuous Integration (CI)**.

**How GitHub Actions works:**
1. **Event triggers**: When you push code, GitHub detects the change
2. **Virtual machine**: GitHub spins up a fresh Ubuntu Linux computer in the cloud
3. **Environment setup**: Installs Python and your project dependencies  
4. **Test execution**: Runs your test suite using pytest
5. **Results reporting**: Shows green checkmark ✅ (success) or red X ❌ (failure)

**Why this matters:**
- **Automated quality control**: Tests run on every change automatically
- **Environment consistency**: Tests run in a clean environment every time
- **Collaboration safety**: Prevents broken code from being accepted
- **Professional workflow**: Same process used by major tech companies

### Instructions for GitHub Actions setup

**Step-by-step process:**

1. In the **root** of your `is4010-labs` repository, create a new folder named `.github`
   - Note the dot (`.`) at the beginning - this is important!
   - This is a hidden folder that GitHub uses for configuration

2. Inside the `.github` folder, create another new folder named `workflows`

3. Inside the `workflows` folder, create a new file named `main.yml`
   - The `.yml` extension stands for YAML (Yet Another Markup Language)
   - YAML is a human-readable data serialization format

4. Copy the entire code block below into your new `main.yml` file:

```yaml
# .github/workflows/main.yml
name: run-pytest

# Trigger: Run this workflow every time code is pushed to any branch
on: [push]

jobs:
  build:
    # Use the latest Ubuntu Linux virtual machine
    runs-on: ubuntu-latest
    
    strategy:
      matrix:
        # Test with Python 3.10 (matches course environment)
        python-version: ["3.10"]
    
    steps:
      # Step 1: Download your repository code
      - uses: actions/checkout@v3
      
      # Step 2: Set up Python environment
      - name: Set up python ${{ matrix.python-version }}
        uses: actions/setup-python@v4
        with:
          python-version: ${{ matrix.python-version }}
      
      # Step 3: Install Python dependencies
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install pytest
      
      # Step 4: Run the test suite
      - name: Test with pytest
        run: |
          pytest
```

**💡 Understanding the workflow file:**
- **`name`**: Human-readable name for your workflow
- **`on: [push]`**: Triggers when you push code to GitHub
- **`runs-on: ubuntu-latest`**: Uses a fresh Linux virtual machine
- **`steps`**: Sequential tasks that run in order
- **`uses: actions/checkout@v3`**: Downloads your repository code
- **`uses: actions/setup-python@v4`**: Installs Python
- **`run: |`**: Executes shell commands on the virtual machine
- **`pytest`**: Runs all test files in the repository (discovers `test_*.py` files automatically)

**Important note about pytest discovery:**
- The command `pytest` (without specifying a directory) will automatically find and run ALL test files in your repository
- This means your workflow will work for Lab 03, Lab 04, Lab 05, and all future labs automatically
- No need to update the workflow file for each new lab!

-----

## Step 3.3: Create a professional README with CI/CD badge 📄

A professional README file serves as the front page of your repository. It's the first thing visitors see and should clearly communicate what your project is about. Adding a CI/CD badge shows the current test status at a glance - a standard practice in professional development.

**Why a README matters:**
- **First impressions**: Shows professionalism to potential employers and collaborators
- **Project overview**: Clearly communicates the purpose and structure of your repository
- **Status visibility**: CI/CD badge instantly shows if tests are passing
- **Portfolio value**: Well-documented repositories demonstrate communication skills
- **Industry standard**: All professional repositories have comprehensive README files

### Instructions for creating your README

1. In the **root** of your `is4010-labs` repository (not inside any lab folder), create a file named `README.md`
2. Copy the template below and customize it with your information

### README.md template

```markdown
# IS4010 Labs - [Your Name]

![CI/CD Pipeline](https://github.com/[YOUR-USERNAME]/[YOUR-REPO-NAME]/actions/workflows/main.yml/badge.svg)

This repository contains all lab assignments for **IS4010: AI-Enhanced Application Development** at the University of Cincinnati's Lindner College of Business.

## 📚 Course Information

- **Course**: IS4010 - AI-Enhanced Application Development
- **Instructor**: Brandon Greenwell
- **Semester**: Fall 2024
- **Institution**: University of Cincinnati, Lindner College of Business

## 🧪 Automated Testing

This repository uses **GitHub Actions** for continuous integration. The badge above shows the current status of all tests:
- ✅ **Green checkmark**: All tests passing
- ❌ **Red X**: Some tests failing

Tests automatically run on every push to ensure code quality and correctness.

## 📂 Repository Structure

```
is4010-[username]-labs/
├── .github/workflows/     # CI/CD automation
├── lab01/                 # Introduction to Git and GitHub
├── lab02/                 # AI-assisted Python development
├── lab03/                 # Python basics and automated testing
├── lab04/                 # [Future labs will be added here]
└── README.md             # This file
```

## 🚀 Labs Completed

- [x] **Lab 01**: Git and GitHub fundamentals
- [x] **Lab 02**: AI-assisted function development
- [x] **Lab 03**: Python basics, testing, and CI/CD setup
- [ ] **Lab 04**: [Coming soon]

## 🛠️ Technologies Used

- **Python 3.10+**: Primary programming language
- **pytest**: Testing framework for automated test execution
- **GitHub Actions**: CI/CD pipeline for automated testing
- **Git/GitHub**: Version control and collaboration

## 📝 Notes

This repository demonstrates modern software development practices including:
- Version control with Git
- Automated testing with pytest
- Continuous Integration/Continuous Deployment (CI/CD)
- AI-assisted development workflows
- Professional documentation standards

---

**About this course**: IS4010 explores application development enhanced by AI tools, covering Python fundamentals, testing practices, and modern development workflows. Students learn to leverage AI assistants while building strong programming fundamentals.
```

### Customizing your README

**Required replacements:**
1. **Line 1**: Replace `[Your Name]` with your actual name
2. **Line 3**: Replace `[YOUR-USERNAME]` with your GitHub username (e.g., `MaxwellMiller18`)
3. **Line 3**: Replace `[YOUR-REPO-NAME]` with your repository name (e.g., `Is4010-MaxwellMiller18-Lab`)

**Example of a correctly formatted badge URL:**
```markdown
![CI/CD Pipeline](https://github.com/MaxwellMiller18/Is4010-MaxwellMiller18-Lab/actions/workflows/main.yml/badge.svg)
```

**Optional customizations:**
- Add your major and graduation year to Course Information section
- Update the "Labs Completed" checklist as you finish each lab
- Add personal notes or learning reflections in the Notes section
- Include links to specific labs or projects you're proud of

### Understanding the CI/CD badge

The badge in your README shows real-time test status:
- **Badge URL format**: `https://github.com/[USERNAME]/[REPO]/actions/workflows/main.yml/badge.svg`
- **Updates automatically**: Changes from green to red if tests fail
- **Clickable**: Links directly to your GitHub Actions workflow runs
- **Professional standard**: Used by major open-source projects (Django, React, pandas, etc.)

The badge pulls live data from your GitHub Actions workflow named `main.yml`. When you push code:
1. GitHub Actions runs your tests
2. Badge updates to reflect pass/fail status
3. Anyone viewing your README sees current project health

-----

## Expected Repository Structure

By the end of this lab, your repository should have the following structure:

```
is4010-[your-username]-labs/
├── .github/
│   └── workflows/
│       └── main.yml          # GitHub Actions workflow for automated testing
├── lab01/
│   └── hello.py              # Simple "Hello World" program from Lab 01
├── lab02/
│   ├── lab02.py              # AI-assisted functions from Lab 02
│   └── lab02_prompts.md      # Prompt engineering solutions from Lab 02
├── lab03/
│   ├── lab03.py              # Mad Libs function and guessing game
│   └── test_lab03.py         # Test file for both functions
└── README.md                 # Professional repository documentation with CI/CD badge
```

**Key points about this structure:**
- **`.github/workflows/main.yml`**: Enables automated testing on every push (works for all labs automatically!)
- **`README.md`**: Professional repository overview with CI/CD badge showing test status
- **`lab01/hello.py`**: Your first Python program from Lab 01
- **`lab02/lab02.py`**: AI-assisted functions (factorial, prime checker, etc.) from Lab 02
- **`lab02/lab02_prompts.md`**: Prompt engineering solutions and AI debugging examples from Lab 02
- **`lab03/lab03.py`**: Contains both the `generate_mad_lib()` and `guessing_game()` functions
- **`lab03/test_lab03.py`**: Contains tests for both functions to ensure they work correctly
- **Hidden folder**: The `.github` folder starts with a dot, making it a hidden folder that GitHub uses for configuration

This organized structure makes it easy to find your work, presents a professional image to potential employers, and ensures the automated testing system can locate and run your tests properly.

-----

## Final step: Pushing and verification

1. You should now have **four** new/modified files:
   - `lab03/lab03.py` (Mad Libs and guessing game functions)
   - `lab03/test_lab03.py` (test suite)
   - `.github/workflows/main.yml` (CI/CD workflow)
   - `README.md` (professional repository documentation)

2. Use git commands to commit and push all files to your GitHub repository:
   ```bash
   git add .
   git commit -m "Complete Lab 03: Python basics, testing, CI/CD, and README"
   git push
   ```

3. Navigate to your repository page on GitHub and verify:
   - Click the **Actions** tab to see your workflow running
   - After 1-2 minutes, it should complete with a **green checkmark ✅**
   - Return to your repository home page
   - Verify your README displays correctly with the CI/CD badge showing

4. **Success indicators:**
   - ✅ Green checkmark in Actions tab (all tests passing)
   - ✅ CI/CD badge in README shows "passing" status
   - ✅ Professional README appears on repository home page
   - ✅ All four files committed and visible in repository

## Submission

**No submission is required on Canvas for this lab.** Since you provided your repository URL in Lab 01, we will automatically check your repository for completed work.

**What you need to do:** Simply commit and push your completed Lab 03 files to your GitHub repository before the due date. **Your grade is determined by the successful completion of the GitHub Actions workflow**, indicated by the green checkmark in your repository's Actions tab.

## 🚨 Troubleshooting Guide

Programming and automated testing can be challenging! Here are solutions to common issues:

### **Problem: "ModuleNotFoundError: No module named 'lab03'"**
- **Cause**: The test file can't find your `lab03.py` file
- **Solution**: 
  - Make sure `lab03.py` and `test_lab03.py` are both in the `lab03/` folder
  - Check that your file is named exactly `lab03.py` (not `Lab03.py` or `lab3.py`)
  - Ensure you've committed and pushed `lab03/lab03.py` to GitHub

### **Problem: "AttributeError: module 'lab03' has no attribute 'generate_mad_lib'"**
- **Cause**: Your function name doesn't match exactly what the test expects
- **Solution**: 
  - Check that your function is named exactly `generate_mad_lib` (not `generate_madlib` or `generateMadLib`)
  - Make sure there are no indentation errors that put the function inside another function

### **Problem: "AssertionError: Adjective 'silly' not found in story"**
- **Cause**: Your function doesn't include all the required words in the story
- **Solution**:
  - Make sure your function uses all three parameters (`adjective`, `noun`, `verb`)
  - Check that you're using f-string formatting correctly: `f"The {adjective} {noun} {verb}"`
  - Ensure you're returning the story string, not printing it

### **Problem: "SyntaxError" or "IndentationError"**
- **Cause**: Python syntax issues
- **Solution**:
  - Check that all parentheses, quotes, and brackets are properly closed
  - Ensure consistent indentation (use 4 spaces, not tabs)
  - Make sure your function definition is properly formatted
  - Use VS Code's Python extension for syntax highlighting and error detection

### **Problem: Function returns None instead of a string**
- **Cause**: Missing return statement or incorrect return value
- **Solution**:
  - Make sure your function has a `return` statement
  - Check that you're returning the story string, not printing it
  - Example: `return f"The {adjective} {noun} {verb}..."` not `print(f"The {adjective} {noun} {verb}...")`

### **Problem: CI/CD badge not showing or showing "no status"**
- **Cause**: Incorrect badge URL or workflow hasn't run yet
- **Solution**:
  - Verify the badge URL format exactly matches: `https://github.com/[USERNAME]/[REPO]/actions/workflows/main.yml/badge.svg`
  - Make sure you replaced `[USERNAME]` and `[REPO]` with your actual values (no brackets!)
  - Push a commit to trigger the workflow - the badge needs at least one workflow run
  - Check that your workflow file is named exactly `main.yml` (not `main.yaml` or `workflow.yml`)

### **Problem: Badge shows "failing" but tests pass locally**
- **Cause**: Different behavior between local and CI environment
- **Solution**:
  - Click the badge or go to Actions tab to see detailed error messages
  - Check that all files are committed and pushed (use `git status`)
  - Verify test file is in the correct location (`lab03/test_lab03.py`)
  - Make sure there are no `import` errors in the GitHub Actions log

### **Problem: README not displaying on repository home page**
- **Cause**: File not in root directory or incorrect filename
- **Solution**:
  - Make sure `README.md` is in the **root** of your repository, not inside `lab03/`
  - File must be named exactly `README.md` (all caps, `.md` extension)
  - Verify it's committed and pushed to GitHub
  - Refresh your browser or clear cache if you just pushed it

### **Still stuck? Use AI assistance! 🤖**

Don't hesitate to use AI tools to help debug issues:

- **[ChatGPT](https://chat.openai.com/)** - Great for explaining Python errors and debugging code
- **[Claude](https://claude.ai/)** - Excellent for step-by-step troubleshooting and code analysis
- **[Gemini](https://gemini.google.com/)** - Helpful for understanding pytest and GitHub Actions issues

### **Example AI prompts that work well:**

- "I'm getting this error in my Python code: [paste error message]. Here's my code: [paste code]. How do I fix it?"
- "My pytest tests are failing with this message: [paste error]. Can you help me understand what's wrong?"
- "I'm new to GitHub Actions and my workflow isn't running. Here's my .yml file: [paste content]. What should I check?"

### Final checklist before considering the lab complete

- [ ] `lab03/lab03.py` file exists and contains both required functions
- [ ] `lab03/test_lab03.py` file exists with the provided test code (unmodified)
- [ ] `.github/workflows/main.yml` file exists with the provided workflow configuration (uses `pytest` not `pytest lab03/`)
- [ ] `README.md` file exists in repository root with CI/CD badge
- [ ] Badge URL customized with your username and repository name
- [ ] All files have been committed and pushed to GitHub
- [ ] GitHub Actions workflow shows a **green checkmark ✅** in Actions tab
- [ ] CI/CD badge in README shows "passing" status
- [ ] You can run your guessing game locally by executing `python lab03/lab03.py`
