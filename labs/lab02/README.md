# Lab 02: AI-Assisted Development

**Due Date: Sunday, September 8, 2024 at 11:59 PM**

## Objective

In this lab, you will gain hands-on experience with the two types of AI development tools we discussed in class: a specialized code assistant ([GitHub Copilot](https://github.com/features/copilot)) and conversational AI models ([Gemini](https://gemini.google.com/) or other large language models). You will learn how to leverage each tool for its specific strengths.

## Background

[GitHub Copilot](https://github.com/features/copilot) excels at generating code in the flow of your work, while conversational AI models are powerful partners for debugging, refactoring, and explaining complex topics. A modern developer is proficient with both.

A key concept for this lab is the **docstring**. A docstring is a special comment, wrapped in triple quotes (`"""..."""`), that explains what a function or class does. In this course, we will use the **[NumPy](https://numpy.org/) docstring style**, which is clean and highly structured. A good docstring is the best way to communicate your intent to an AI assistant. You can find a full reference at the [NumPy style guide](https://numpydoc.readthedocs.io/en/latest/format.html).

---

## Part 1: Copilot driving school

In this part, you will use [GitHub Copilot](https://github.com/features/copilot) to write the code for a series of [Python](https://www.python.org/) function "stubs."

### Instructions

1.  In your `is4010-[username]-labs` local repository, navigate to your repository folder and create a `lab02/` directory.
2.  Inside the `lab02/` folder, create a new file named `lab02.py`.
3.  Copy all the [Python](https://www.python.org/) function stubs from the section below into your `lab02.py` file.
4.  For each function, place your cursor inside the function body on a new line.
5.  Wait for [GitHub Copilot](https://github.com/features/copilot) to suggest an implementation based on the function name and the [NumPy](https://numpy.org/)-style docstring.
6.  Review the suggestion and press `Tab` to accept it.

### Python function stubs

```python
def factorial(n):
    """Calculate the factorial of a non-negative integer.

    Parameters
    ----------
    n : int
        The non-negative integer to calculate the factorial of.

    Returns
    -------
    int
        The factorial of n. Returns 1 for n = 0.
    """
    pass

def is_prime(number):
    """Check if a number is a prime number.

    Parameters
    ----------
    number : int
        The integer to check.

    Returns
    -------
    bool
        True if the number is prime, False otherwise.
    """
    pass

def reverse_string(s):
    """Reverse a given string.

    Parameters
    ----------
    s : str
        The string to be reversed.

    Returns
    -------
    str
        The reversed string.
    """
    pass
````

-----

## Part 2: The prompt engineering challenge

In this part, you will use a conversational AI model like [Google Gemini](https://gemini.google.com/) to debug, refactor, and document provided code snippets.

### Instructions

1.  In your `lab02/` folder, create a new [Markdown](https://www.markdownguide.org/) file named `lab02_prompts.md`.
2.  For each of the three problems below, you will craft a high-quality prompt following the "context, persona, task, format" model.
3.  In your `lab02_prompts.md` file, create a section for each problem. For each problem, you must include:
      * A heading for the problem (e.g., "\#\#\# Problem 1: Debugging").
      * The **exact prompt** you used, placed in a code block.
      * The **final, corrected code snippet** that the AI provided, also in a code block.

### Problems

#### Problem 1: Debugging a buggy function

This function is supposed to calculate the sum of all even numbers in a list, but it contains a logical error.

**Your task:** Craft a prompt that asks the AI to find and fix the bug.

```python
# Buggy code snippet
def sum_of_evens(numbers):
    """Calculates the sum of all even numbers in a list."""
    total = 0
    for num in numbers:
        if num % 2 == 1: # This line has a bug!
            total += num
    return total
```

#### Problem 2: Refactoring an unreadable function

This function works correctly, but it is written in a confusing way.

**Your task:** Craft a prompt that asks the AI to refactor this code to be more clear, concise, and "[Pythonic](https://peps.python.org/pep-0020/)."

```python
# Unreadable code snippet
def get_names_of_adults(users):
    """Given a list of user dictionaries, returns a list of names of users
    who are 18 or older."""
    results = []
    for i in range(len(users)):
        if users[i]['age'] >= 18:
            results.append(users[i]['name'])
    return results
```

#### Problem 3: Documenting a function

This function works, but it has no documentation.

**Your task:** Craft a prompt that asks the AI to write a professional, high-quality **[NumPy](https://numpy.org/)-style** docstring for this function.

```python
# Undocumented code snippet
def calculate_area(length, width):
    if length <= 0 or width <= 0:
        raise ValueError("Length and width must be positive numbers.")
    return length * width
```

-----

## Submission

## 🚨 Troubleshooting Guide

AI tools can sometimes be tricky! Here are solutions to common issues:

### **Problem: GitHub Copilot not showing suggestions**
- **Solution**: Check your [GitHub Copilot](https://github.com/features/copilot) setup
  - Make sure you're signed into [VS Code](https://code.visualstudio.com/) with your [GitHub](https://github.com/) account
  - Verify GitHub Copilot extension is installed and enabled
  - Check that you have an active GitHub Copilot subscription (free for students)
  - Try placing your cursor inside the function and waiting a moment

### **Problem: Copilot suggestions don't match what I want**
- **Solution**: Improve your docstrings and comments
  - Write more detailed and specific docstrings
  - Add clear comments describing your intent
  - Use descriptive function and parameter names
  - Press `Alt + ]` (Windows) or `Option + ]` (Mac) to cycle through alternatives

### **Problem: Conversational AI giving poor responses**
- **Solution**: Improve your prompts using the CPTF method
  - **Context**: Provide the actual code you're working with
  - **Persona**: Tell the AI to act as a senior [Python](https://www.python.org/) developer
  - **Task**: Be specific about what you want (debug, refactor, document)
  - **Format**: Specify how you want the response structured

### **Problem: Can't access Google Gemini or other AI tools**
- **Solution**: Try alternative conversational AI models
  - [ChatGPT](https://chat.openai.com/) - OpenAI's conversational AI
  - [Claude](https://claude.ai/) - Anthropic's helpful AI assistant
  - [Microsoft Copilot](https://copilot.microsoft.com/) - Microsoft's AI assistant
  - All have free tiers that work well for this assignment

### **Problem: Not sure if my folder structure is correct**
- **Solution**: Check your repository organization
  - Your repository root should contain both `lab01/` and `lab02/` folders
  - Use `ls` or `dir` to verify folder structure
  - `lab02/` should contain both `.py` and `.md` files

### **Still stuck? Use AI assistance! 🤖**

Don't hesitate to use AI tools to help with this lab - it's actually part of the learning process!

- **[ChatGPT](https://chat.openai.com/)** - Great for explaining [Python](https://www.python.org/) concepts and prompt engineering
- **[Claude](https://claude.ai/)** - Excellent for debugging code and improving prompts
- **[Gemini](https://gemini.google.com/)** - Helpful for understanding [NumPy](https://numpy.org/) docstring format

**Pro tip**: When asking AI for help, be specific about what you're trying to accomplish and include relevant context!

### **Example AI prompts that work well:**
- "I'm learning to use [GitHub Copilot](https://github.com/features/copilot). My function has a good docstring but Copilot isn't suggesting code. What should I check?"
- "Can you help me write a better prompt for debugging this [Python](https://www.python.org/) function? I want the AI to find the logical error."
- "I need to write a [NumPy](https://numpy.org/)-style docstring for a function that calculates area. Can you show me the proper format?"

---

## Submission

To complete this lab, submit your **repository URL** on Canvas.

**What to submit:** The main HTTPS URL to your repository (not a specific file or folder)

**Example submission URL:** `https://github.com/johndoe/is4010-johndoe-labs`

When you are finished with both parts of the lab, please commit and push your `lab02/` folder and its contents to your `is4010-[username]-labs` [GitHub](https://github.com/) repository.

Your `lab02/` folder should contain:
1.  `lab02.py` - Your [GitHub Copilot](https://github.com/features/copilot)-generated functions
2.  `lab02_prompts.md` - Your prompt engineering solutions

### Git workflow reminder:
```bash
# Navigate to your repository
cd is4010-[username]-labs

# Check what files have changed
git status

# Stage your lab02 folder and its contents
git add lab02/

# Commit with a descriptive message
git commit -m "Complete Lab 02: AI-assisted development"

# Push to GitHub
git push origin main
```

### Final checklist before submission

Before submitting on Canvas, verify your repository contains:

- [ ] Repository name follows format: `is4010-[your-username]-labs`
- [ ] Repository is set to **Private** (not public)
- [ ] `@bgreenwell` has been added as a collaborator
- [ ] `lab02/` folder exists in your repository
- [ ] `lab02/lab02.py` file exists and contains all three completed functions
- [ ] `lab02/lab02_prompts.md` file exists and contains all three prompt engineering solutions
- [ ] Each function in `lab02.py` has working code (not just `pass`)
- [ ] Each problem in `lab02_prompts.md` includes your prompt and the AI's corrected code
- [ ] Your changes have been successfully pushed to [GitHub](https://github.com/) (visible on the website)
- [ ] Your repository URL works when pasted into a browser

**⚠️ Double-check that your repository is PRIVATE and has the instructor as a collaborator - these are required for credit!**
