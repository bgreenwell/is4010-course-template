# Midterm Project: AI-Assisted CLI Application

**Due Date: Sunday, October 19, 2025 at 11:59 PM**

**Total Points: 17 (10% of final grade)**

## 📋 TL;DR - What You're Building

**In one sentence:** Build a command-line tool that fetches data from a public API, with professional testing, documentation, and CI/CD—all developed using AI assistance.

**Core deliverables:**
- ✅ **Working CLI application** using argparse (3+ commands)
- ✅ **API integration** (no auth required - Chuck Norris, PokeAPI, EmojiHub, or Ron Swanson recommended)
- ✅ **Comprehensive tests** with pytest (including mocked API calls)
- ✅ **Professional README** with setup, usage examples, and badges
- ✅ **AGENTS.md file** documenting your AI-assisted development process
- ✅ **GitHub Actions CI/CD** with passing tests (green checkmark)
- ✅ **Public repository** for portfolio purposes

**Key files you'll create:**
```
your-project/
├── AGENTS.md          # AI context file
├── README.md          # Professional docs
├── requirements.txt   # Dependencies
├── .github/workflows/tests.yml
├── src/
│   ├── main.py       # CLI entry point
│   └── api.py        # API functions
└── tests/
    ├── test_main.py
    └── test_api.py
```

**Success looks like:**
- 🟢 Green checkmark in GitHub Actions tab
- 🟢 `python -m src.main --help` runs without errors
- 🟢 README displays badge showing "passing" tests
- 🟢 All required sections documented in README

---

## Objective

Build a professional command-line interface (CLI) application that interacts with a public API, demonstrating your ability to leverage AI coding assistants throughout the entire development lifecycle. This project emphasizes **process over perfection** – you'll learn how to leverage AI tools like [GitHub Copilot](https://github.com/features/copilot), [Claude](https://claude.ai/), [Gemini](https://gemini.google.com/), and [ChatGPT](https://chat.openai.com/) to plan, scaffold, develop, test, and document a complete Python application.

## Background

Modern software development is increasingly AI-assisted. Professional developers don't write every line of code from scratch – they use AI tools to accelerate development, generate boilerplate, write tests, and create documentation. This project simulates a real-world development workflow where you'll partner with AI at every step.

**What you'll learn:**

- **AI-assisted planning**: Using conversational AI to design software architecture
- **Context management**: Creating project documentation (`AGENTS.md`) that guides AI assistance
- **CLI development**: Building user-friendly command-line tools with [argparse](https://docs.python.org/3/library/argparse.html)
- **API integration**: Working with external data sources and handling responses
- **Professional practices**: Testing, documentation, and CI/CD pipelines

**Key technologies:**

- [Python](https://www.python.org/) for application logic
- [argparse](https://docs.python.org/3/library/argparse.html) for CLI argument parsing
- [pytest](https://docs.pytest.org/) for automated testing
- [GitHub Actions](https://docs.github.com/en/actions) for continuous integration
- AI coding assistants ([Copilot](https://github.com/features/copilot), [gemini-cli](https://github.com/google-gemini/generative-ai-python), [Claude](https://claude.ai/), [Gemini](https://gemini.google.com/), [ChatGPT](https://chat.openai.com/))

---

## Core Requirements

Your CLI application must include:

### **1. API Integration**
- Interact with at least one public API
- **Must use APIs that don't require authentication or API keys** (keeps setup simple and makes grading easier)

### **2. Command-Line Interface**
- Built using [argparse](https://docs.python.org/3/library/argparse.html) for argument parsing
- Runnable from the terminal with clear, intuitive commands
- Must be executable via: `python -m your_project_name [command] [options]`

### **3. Professional Code Quality**
- Well-organized functions and/or classes
- [Docstrings](https://docs.python.org/3/tutorial/controlflow.html#documentation-strings) for all functions and classes
- Clean, readable code following [PEP 8](https://peps.python.org/pep-0008/) style guidelines

### **4. Testing**
- Comprehensive test suite using [pytest](https://docs.pytest.org/)
- Tests must pass both locally and in CI/CD pipeline
- Use AI assistance to write tests and learn [mocking](https://docs.python.org/3/library/unittest.mock.html) for API calls

### **5. Professional Documentation**
- High-quality README with setup instructions, usage examples, and API documentation
- Clear explanation of what the application does and how to use it

### **6. CI/CD Pipeline**
- [GitHub Actions](https://docs.github.com/en/actions) workflow that runs tests automatically
- Passing tests indicated by green checkmark badge in README

### **7. Repository Standards**
- **Public repository** (for portfolio purposes)
- Professional repository structure with organized directories
- Relevant badges in README (tests, license, etc.)

---

## Choose Your API

**For this project, choose a public API that doesn't require authentication.** This keeps setup simple and lets you focus on the development workflow.

### 🌟 Recommended APIs (No Setup Required)

I've curated these fun, well-documented APIs that should work great for CLI projects:

#### **1. Chuck Norris Jokes API**
- **URL:** https://api.chucknorris.io/
- **What it does:** Random Chuck Norris jokes, searchable by category
- **CLI command ideas:**
  - `chuck random` - Get a random Chuck Norris joke
  - `chuck categories` - List all available joke categories
  - `chuck search [query]` - Search for jokes containing a word
- **Why it's great:** Simple, funny, perfect for learning API basics

#### **2. EmojiHub API**
- **URL:** https://github.com/cheatsnake/emojihub
- **What it does:** Emoji data with names, categories, and groups
- **CLI command ideas:**
  - `emoji random` - Get a random emoji with its info
  - `emoji get grinning-face` - Get a specific emoji by name (e.g., 💀 "skull")
  - `emoji category smileys-emotion` - List all emojis in a category
  - `emoji group face-smiling` - Get emojis by group
- **Why it's great:** Visual, fun data structure, good for practicing data parsing

#### **3. Ron Swanson Quotes API**
- **URL:** https://github.com/jamesseanwright/ron-swanson-quotes
- **What it does:** Random quotes from Parks and Recreation's Ron Swanson
- **CLI command ideas:**
  - `ron quote` - Get a random Ron Swanson quote
  - `ron multiple [count]` - Get multiple quotes at once
  - `ron search [query]` - Search for quotes containing a word
  - `ron save [filename]ave favorite quotes to a file
- **Why it's great:** Simple API, room for creative features

#### **4. PokeAPI**
- **URL:** https://pokeapi.co/
- **What it does:** Comprehensive Pokemon data (stats, types, abilities, sprites)
- **CLI command ideas:**
  - `pokemon info [name]` - Get detailed Pokemon information
  - `pokemon random` - Get a random Pokemon
  - `pokemon type [type]` - List all Pokemon of a specific type
- **Why it's great:** Rich data, well-documented, very popular

### 💡 Want Something Different?

**Explore thousands of public APIs at:**
https://github.com/public-apis/public-apis

**When browsing, filter for:**
- **Auth = No** (no API key required - keeps it simple!)
- **HTTPS = Yes** (secure connections)

**Before choosing an API from this list, consider verifying the following:**
- ✅ Returns JSON data (easier to work with)
- ✅ Has clear, readable documentation
- ✅ Provides multiple endpoints for interesting commands
- ✅ API is actively maintained and reliable

**🤖 AI Prompt to help evaluate an API:**
```
You're an expert Python API developer who excels at developing simple CLI apps using argparse. I'm considering using the [API name] API available at [API URL] for a Python CLI project. Can you help me understand: What data does it provide? What interesting CLI commands could I build with it? Is the documentation clear enough for a beginner?"
```

💡 **Pro tip:** Start with one of our recommended APIs to get up and running quickly. You can always switch or add complexity later!

---

## ✅ Quick-Start Checklist

Use this condensed checklist to track your progress. Each item links to detailed instructions below.

### **Phase 1: Planning & Setup** ⏱️ ~1-2 hours
- [ ] **Choose your API** from [recommended list](#choose-your-api) (Chuck Norris, EmojiHub, Ron Swanson, or PokeAPI)
- [ ] **Plan with AI** - Brainstorm CLI commands and architecture ([Step 2](#step-2-plan-your-application-with-ai))
- [ ] **Create AGENTS.md** - Document project context for AI assistants ([Step 3](#step-3-create-agentsmd-context-file))
- [ ] **Set up repository** - Initialize with proper structure ([Project Structure](#project-structure))

### **Phase 2: Core Development** ⏱️ ~3-4 hours
- [ ] **Scaffold project** - Create src/, tests/, and key files ([Step 4](#step-4-scaffold-project-with-ai-assistance))
- [ ] **Implement API integration** - Write functions to fetch data ([Step 5](#step-5-implement-core-functionality))
- [ ] **Build CLI with argparse** - Create 3+ commands ([Step 5](#step-5-implement-core-functionality))
- [ ] **Add docstrings** - Document all functions and classes

### **Phase 3: Testing & CI/CD** ⏱️ ~2-3 hours
- [ ] **Write pytest tests** - Use mocking for API calls (AI will help!) ([Step 6](#step-6-write-tests-with-ai-assistance))
- [ ] **Tests pass locally** - Run `pytest tests/` successfully
- [ ] **Set up GitHub Actions** - Configure CI/CD workflow ([Step 8](#step-8-set-up-cicd-pipeline))
- [ ] **Green checkmark in Actions** - Verify tests pass in CI

### **Phase 4: Documentation & Polish** ⏱️ ~1-2 hours
- [ ] **Write professional README** - Include all required sections ([Step 7](#step-7-create-professional-readme))
- [ ] **Add status badges** - Display test status and Python version ([Step 9](#step-9-add-badges-to-readme))
- [ ] **Verify CLI works** - Test `python -m src.main --help` and all commands
- [ ] **Repository is public** - Check visibility settings
- [ ] **Final review** - Use [submission checklist](#repository-checklist) to verify completeness

### **Ready to Submit?**
✅ All boxes checked above
✅ Green checkmark in GitHub Actions
✅ Public repository with professional README
✅ Tests pass both locally and in CI

**Estimated total time:** 7-11 hours spread across ~1 week

---

## Step-by-Step Development Guide

Follow this AI-assisted workflow to build your project systematically:

### **Step 1: Choose Your API**

1. Pick one of our recommended APIs (Chuck Norris, EmojiHub, Ron Swanson, or PokeAPI) or find your own (e.g., from [Public APIs](https://github.com/public-apis/public-apis)).
2. Read the API documentation to understand:
   - What data it provides
   - How to make requests (GET, POST, etc.)
   - Response format (usually JSON)
   - Any rate limits or restrictions

**🤖 AI Prompt Examples:**
```
"I'm building a CLI application using the Chuck Norris Jokes API available at https://api.chucknorris.io/. Can you help me brainstorm 3-4 interesting commands I could implement? I want to go beyond just 'get random joke'."

"I chose the PokeAPI for my project, which is available at https://pokeapi.co/. What are some creative CLI commands I could build that would make this a useful tool for Pokemon fans?"

"I found an interesting API called [API name] in the Public APIs list, The API documentation is available at [API URL]. Help me evaluate if it's good for a CLI project - does it have enough endpoints for multiple commands?"
```

### **Step 2: Plan Your Application with AI**

Use a conversational AI to iterate on your project design:

1. Open [Claude](https://claude.ai/), [ChatGPT](https://chat.openai.com/), or [Gemini](https://gemini.google.com/)
2. Describe your project idea and ask for architecture suggestions (e.g., functions, classes, CLI commands)
3. Iterate on CLI command design
4. Discuss data structures and code organization
5. Save this conversation for reference

DOn't be afraid to ask for multiple iterations or clarifications!

**🤖 AI Prompt Examples:**
```
"I want to build a simple Python-based CLI tool that uses the Chuck Norris API available at https://api.chucknorris.io/. The CLI should have commands like 'random', 'categories', and 'search'. Help me design the application architecture and suggest a good, but simple project structure."

"I'm building a simple Python-based EmojiHub CLI application which is documented at https://github.com/cheatsnake/emojihub. I want commands for displaying information about specific emojis, random emoji, search, and category browsing. What's a good way to structure the code with separate modules for API calls, data processing, and CLI interface?"
```

### **Step 3: Create `AGENTS.md` Context File**

Based on your planning conversation, create an `AGENTS.md` file in your project root. This file guides AI coding assistants with project context. Ask your chat AI (e.g., Claude, ChatGPT, or Gemini) to help you write it!

**What to include in `AGENTS.md`:**
- Project overview and goals
- API being used and key endpoints
- CLI commands and their purposes
- Code organization strategy
- Technology stack (Python, argparse, pytest, etc.)
- Coding standards and conventions
- Any specific requirements or constraints

**🤖 AI Prompt Example:**
```
"Based on our discussion about my Python-based Ron Swanson Quotes CLI tool, help me write a comprehensive `AGENTS.md` file that AI coding assistants can use for context. Include project overview, architecture decisions, CLI command structure, and coding standards."
```

**Example `AGENTS.md` structure:**
```markdown
# Project Name: Ron Swanson Quotes CLI

## Overview
A command-line tool to fetch and display random Ron Swanson quotes from Parks and Recreation.
Users can get single quotes, multiple quotes, or save favorites to a local file.

## API Integration
- **API:** Ron Swanson Quotes API
- **Base URL:** https://ron-swanson-quotes.herokuapp.com/v2/quotes
- **Key endpoints:**
  - `/quotes` - Get one random quote
  - `/quotes/[count]` - Get multiple quotes
- **Data format:** JSON array of strings

## CLI Commands
- `ron quote` - Get a single random quote
- `ron multiple [count]` - Get multiple quotes (1-100)
- `ron save [filename]` - Save a quote to a file

## Technical Stack
- Python 3.10+
- argparse for CLI argument parsing
- requests library for API calls
- pytest for testing with mocking

## Code Organization
- `src/main.py` - Entry point and argparse setup
- `src/api.py` - API interaction functions
- `src/utils.py` - Helper functions (file saving, formatting)
- `tests/` - Test files with mocked API responses

## Standards
- Use docstrings for all functions and classes
- Follow PEP 8 style guidelines
- Handle errors gracefully with try/except blocks
- Mock all API calls in tests (no real requests during testing)
```

### **Step 4: Scaffold Project with AI Assistance**

Now use VS Code with AI tools to build your project structure:

#### **Using GitHub Copilot in VS Code:**
1. Open VS Code in your project directory
2. Create your project structure (folders: `src/`, `tests/`)
3. Create files: `src/main.py`, `src/api.py`, `requirements.txt`, `README.md`
4. Reference `@AGENTS.md` in Copilot Chat for context-aware suggestions
5. Use Copilot's inline suggestions while writing code

#### **Using gemini-cli in your terminal:**
```bash
gemini "Create a Python function that calls the [API endpoint] and returns JSON data"
```

#### **Using AI Chat interfaces:**
- Open your `AGENTS.md` file in one window
- Open your AI chat in another window
- Reference the `AGENTS.md` content in your prompts for consistent context

**🤖 AI Prompt Example:**
```
"I'm working on a Chuck Norris jokes CLI as described in my AGENTS.md file. Help me create the main.py file with argparse setup for these commands: 'random', 'categories', and 'search'. Here's my AGENTS.md content: [paste content]"
```

### **Step 5: Implement Core Functionality**

Build your application incrementally, using AI assistance:

1. **Start with API integration:**
   ```python
   # src/api.py
   import requests

   def fetch_data(endpoint):
       """Fetch data from API endpoint."""
       # Use AI to help implement error handling
       pass
   ```

2. **Build CLI with argparse:**
   ```python
   # src/main.py
   import argparse

   def main():
       parser = argparse.ArgumentParser(description="...")
       # Use AI to help set up subcommands
       pass
   ```

3. **Keep it simple and clean:**
   - Write clear, descriptive function names
   - Add docstrings as you go (AI can generate these)
   - Break complex logic into smaller functions

**🤖 AI Prompt Examples:**
```
"Help me write a function that fetches data from the Chuck Norris API endpoint https://api.chucknorris.io/jokes/random using the requests library. Include error handling for network errors and invalid responses."

"I need to add a 'search' subcommand to my argparse CLI that takes a query argument for the Chuck Norris API. Show me how to implement this."

"I'm working with the PokeAPI and need to parse the JSON response to extract just the Pokemon's name, types, and abilities. Help me write a clean function for this."

"Generate a docstring for this function: [paste function code]"
```

### **Step 6: Write Tests with AI Assistance**

Since we haven't covered mocking in class, this is where AI becomes essential:

1. Create `tests/test_main.py` and `tests/test_api.py`
2. Ask AI to help you understand and implement mocking for API calls
3. Write tests that don't make real API requests (use mocks)

**🤖 AI Prompt Examples:**
```
"I need to write pytest tests for my API functions, but I don't want to make real API calls during testing. Help me understand how to use unittest.mock to mock the requests.get function."

"Here's my function that calls an API: [paste code]. Write a pytest test that mocks the API response and verifies the function works correctly."

"Create a test file for my CLI application. It uses argparse and calls API functions. Show me how to test the CLI without making real API calls."
```

**Example test structure:**
```python
import pytest
from unittest.mock import patch, MagicMock

@patch('src.api.requests.get')
def test_fetch_data(mock_get):
    # AI will help you set up the mock
    mock_response = MagicMock()
    mock_response.json.return_value = {'data': 'test'}
    mock_get.return_value = mock_response

    # Your test logic here
    pass
```

### **Step 7: Create Professional README**

Your README is crucial for portfolio purposes. Use AI to help structure and polish it:

**Required README sections:**
- **Project title and description**
- **Features** - What can users do with your CLI?
- **Installation** - Step-by-step setup instructions
- **Usage** - Command examples with expected output
- **API Information** - Credits and links to the API used
- **Testing** - How to run tests locally
- **Technologies** - List of technologies and libraries used
- **Badges** - Test status, license, etc.

**🤖 AI Prompt Example:**
```
"Help me write a professional README for my CLI application. The project is a [description] that uses [API name]. Include installation instructions, usage examples, and badges for tests and license. Here's my AGENTS.md for context: [paste content]"
```

### **Step 8: Set Up CI/CD Pipeline**

Use AI to help configure GitHub Actions for automated testing:

1. Create `.github/workflows/tests.yml`
2. Configure workflow to run pytest on every push
3. Ensure tests pass in CI environment

**🤖 AI Prompt Example:**
```
"Create a GitHub Actions workflow file that runs pytest tests for my Python project. The tests are in the 'tests/' directory and require dependencies from requirements.txt. The workflow should run on push and pull requests."
```

**Example workflow structure:**
```yaml
name: Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      - run: pip install -r requirements.txt
      - run: pytest
```

### **Step 9: Add Badges to README**

Use AI to help you add professional badges showing test status:

**🤖 AI Prompt Example:**
```
"Show me how to add GitHub Actions status badges to my README. My workflow is called 'Tests' and my repository is [username/repo-name]."
```

**Example badges:**
```markdown
![Tests](https://github.com/username/repo-name/workflows/Tests/badge.svg)
![Python](https://img.shields.io/badge/python-3.10+-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
```

### **Step 10: Final Testing & Polish**

1. **Run tests locally:**
   ```bash
   pytest tests/
   ```

2. **Test your CLI manually:**
   ```bash
   python -m your_project_name --help
   python -m your_project_name [command] [args]
   ```

3. **Verify CI/CD:**
   - Check GitHub Actions tab for green checkmark
   - Fix any failing tests

4. **Polish with AI:**
   - Ask AI to review your code for improvements
   - Request suggestions for better error messages
   - Get help with code formatting and style

**🤖 AI Prompt Example:**
```
"Review this code for improvements. Look for error handling issues, code clarity, and any best practices I might be missing: [paste code]"
```

---

## Project Structure

Your repository should follow this structure:

```
your-project-name/
├── .github/
│   └── workflows/
│       └── tests.yml          # CI/CD pipeline configuration
├── src/
│   ├── __init__.py            # Makes src a package
│   ├── main.py                # Entry point with argparse CLI
│   ├── api.py                 # API interaction functions
│   └── models.py              # Data classes (optional)
├── tests/
│   ├── __init__.py
│   ├── test_main.py           # CLI tests
│   └── test_api.py            # API function tests
├── .gitignore                 # Ignore __pycache__, .env, etc.
├── AGENTS.md                  # AI assistant context file
├── README.md                  # Professional project documentation
├── requirements.txt           # Python dependencies
└── LICENSE                    # MIT or other open source license
```

**Making your project runnable:**
- Add `__init__.py` files to make directories into packages
- Use `python -m src.main` to run your CLI, or
- Add a `__main__.py` file for `python -m your_project_name` execution

---

## Grading Criteria

Your project will be assessed on the following easily-gradable criteria:

### **✅ Automated Assessment (Easy to Grade)** - 8 points

| Criterion | Points | How We Check |
|-----------|--------|--------------|
| **Repository exists and is public** | 1 | GitHub URL submission |
| **CI/CD pipeline configured and passing** | 2 | Green checkmark in Actions tab |
| **All tests pass** | 1 | GitHub Actions status |
| **README.md exists with all required sections** | 1 | File presence and section headers |
| **`AGENTS.md` exists with project context** | 1 | File presence and content |
| **requirements.txt exists** | 1 | File presence |
| **Tests directory exists with test files** | 1 | Directory and file check |

### **📋 Manual Assessment (Moderate Grading Effort)** - 5 points

| Criterion | Points | How We Check |
|-----------|--------|--------------|
| **CLI runs successfully** | 1 | Execute: `python -m project_name --help` |
| **API integration works** | 2 | Run CLI commands and verify output |
| **Code has docstrings** | 1 | Scan for docstring presence |
| **Error handling implemented** | 1 | Check for try/except blocks |

### **🔍 Quality Assessment (Detailed Review)** - 4 points

| Criterion | Points | How We Check |
|-----------|--------|--------------|
| **Professional README quality** | 1 | Content clarity, examples, completeness |
| **Test coverage and quality** | 1 | Review test files for mocking and assertions |
| **Code quality and style** | 1 | PEP 8 compliance, readability |
| **Overall functionality and creativity** | 1 | Does it work well and solve a useful problem? |

**💡 Grading priorities:**
1. **Does it work?** - Tests pass, CLI runs without errors
2. **Is it professional?** - Good documentation, clean code, proper structure
3. **Is it complete?** - All required components present and functional
4. **Is it thoughtful?** - Good use of AI assistance, creative implementation

---

## 🚨 Troubleshooting & Common Issues

### **Setup & Structure Issues**

#### **Problem: "ImportError: No module named 'src'"**
- **Cause**: Python can't find your source code modules
- **Solution**:
  - Ensure `__init__.py` files exist in `src/` and `tests/` directories
  - Run commands from project root: `python -m src.main` not `python src/main.py`
  - Check your import statements: `from src.api import fetch_data` not `from api import fetch_data`
  - Verify directory structure matches the [project structure](#project-structure)

**🤖 AI Prompt:**
```
"I'm getting 'ModuleNotFoundError: No module named src' when running my CLI. Here's my directory structure: [paste]. How should I structure my imports?"
```

#### **Problem: "My CLI won't run with `python -m src.main`"**
- **Cause**: Missing `__main__.py` or incorrect package structure
- **Solution**:
  - Add `if __name__ == "__main__":` block to `src/main.py`
  - Or create `src/__main__.py` file that imports and calls `main()`
  - Ensure `src/` has `__init__.py` file

**🤖 AI Prompt:**
```
"How do I make my Python package runnable with 'python -m package_name'? My entry point is in src/main.py."
```

### **API Integration Issues**

#### **Problem: "API requests fail in tests but work when I test manually"**
- **Cause**: Mocks not set up correctly, or real API calls happening in tests
- **Solution**:
  - Verify you're patching the correct import path: `@patch('src.api.requests.get')` not `@patch('requests.get')`
  - Check that mock return value structure matches real API response
  - Use `mock_response.json.return_value = {...}` for JSON APIs
  - Ensure you're not making real HTTP requests in tests

**🤖 AI Prompt:**
```
"My tests are making real API calls instead of using mocks. Here's my test: [paste code]. The function being tested is in src/api.py and uses requests.get(). How do I mock it correctly?"
```

#### **Problem: "KeyError or AttributeError when parsing API response"**
- **Cause**: API response structure doesn't match expectations
- **Solution**:
  - Print or log the actual API response: `print(response.json())`
  - Check API documentation for exact response format
  - Use `.get()` method for dictionaries: `data.get('key', default_value)`
  - Handle missing keys gracefully with try/except

**🤖 AI Prompt:**
```
"I'm getting KeyError: 'results' when parsing this API response: [paste response]. How should I handle this safely?"
```

### **Testing & Mocking Issues**

#### **Problem: "I don't understand how mocking works"**
- **Cause**: Mocking is a complex topic not yet covered in class (this is expected!)
- **Solution**:
  - Use AI extensively to learn mocking concepts
  - Start with simple examples before complex scenarios
  - Focus on mocking `requests.get()` or `requests.post()` calls
  - Use `unittest.mock.patch` as a decorator or context manager

**🤖 AI Prompt:**
```
"Explain Python mocking in pytest like I'm a beginner. Show me a complete example of mocking requests.get() for this function: [paste function]. Include the imports and test structure."
```

#### **Problem: "Tests pass locally but fail in GitHub Actions"**
- **Cause**: Environment differences between local and CI
- **Solution**:
  - Check `requirements.txt` includes ALL dependencies
  - Ensure Python version matches in workflow (3.10+ recommended)
  - Verify file paths are relative, not absolute
  - Check for OS-specific issues (Windows vs. Linux)
  - Look at GitHub Actions logs for specific error messages

**🤖 AI Prompt:**
```
"My pytest tests pass locally on [Mac/Windows] but fail in GitHub Actions. Here's the CI error: [paste error]. Here's my workflow file: [paste YAML]. What could be wrong?"
```

#### **Problem: "Mock objects don't have the attributes I expect"**
- **Cause**: Mock not configured to match real object structure
- **Solution**:
  - Use `MagicMock()` for objects with multiple attributes
  - Set up return values: `mock_obj.method.return_value = expected_value`
  - For chained calls: `mock.response.json.return_value = {...}`
  - Use `spec=` parameter to create mocks that match real objects

**🤖 AI Prompt:**
```
"I'm mocking an API response but getting AttributeError: 'Mock' object has no attribute 'json'. Here's my mock setup: [paste code]. How do I make it have a json() method?"
```

### **CI/CD & GitHub Actions Issues**

#### **Problem: "GitHub Actions workflow never runs"**
- **Cause**: Workflow file not in correct location or has syntax errors
- **Solution**:
  - Verify file is at `.github/workflows/tests.yml` (exact path required)
  - Check YAML syntax is valid (indentation matters!)
  - Ensure workflow has `on: [push]` trigger
  - Look for red X in commits (indicates workflow failed to run)

**🤖 AI Prompt:**
```
"My GitHub Actions workflow isn't running. Here's my .github/workflows/tests.yml file: [paste]. What's wrong with the syntax or setup?"
```

#### **Problem: "Badge shows 'no status' or doesn't update"**
- **Cause**: Badge URL incorrect or workflow hasn't completed
- **Solution**:
  - Verify badge URL format: `![Tests](https://github.com/username/repo/workflows/WorkflowName/badge.svg)`
  - Workflow name in URL must match `name:` in YAML file exactly (case-sensitive)
  - Push a commit to trigger workflow - badge needs at least one run
  - Check if workflow is named "Tests" or "run-pytest" (must match badge URL)

**🤖 AI Prompt:**
```
"My GitHub Actions badge isn't showing in README. My workflow is named 'Tests' and my repo is username/repo-name. What's the correct badge URL?"
```

#### **Problem: "Dependencies install fails in CI"**
- **Cause**: Missing or incorrectly formatted `requirements.txt`
- **Solution**:
  - Generate requirements: `pip freeze > requirements.txt`
  - Ensure no platform-specific packages (like `pywin32` on Windows)
  - Pin versions for consistency: `requests==2.31.0` not just `requests`
  - Test locally: `pip install -r requirements.txt` in fresh virtualenv

**🤖 AI Prompt:**
```
"GitHub Actions fails when installing dependencies with error: [paste error]. Here's my requirements.txt: [paste]. How do I fix this?"
```

### **CLI & argparse Issues**

#### **Problem: "argparse subcommands not working as expected"**
- **Cause**: Subparser setup incorrect or not calling the right functions
- **Solution**:
  - Use `subparsers = parser.add_subparsers(dest='command')` to capture command name
  - Create subparser for each command: `parser_random = subparsers.add_parser('random')`
  - Check which command was called: `if args.command == 'random':`
  - Set required=True on subparsers if user must provide a command

**🤖 AI Prompt:**
```
"My argparse CLI has commands 'random', 'search', and 'categories' but they're not working. Here's my argparse setup: [paste code]. How do I fix the subcommands?"
```

#### **Problem: "CLI shows no output or unexpected output"**
- **Cause**: Missing print statements or incorrect return vs. print
- **Solution**:
  - Ensure CLI commands use `print()` to display results
  - Functions can return data, but CLI must print it
  - Check for silent failures (API errors not being shown to user)
  - Add error messages for when things go wrong

**🤖 AI Prompt:**
```
"My CLI runs without errors but shows no output. Here's my main function: [paste code]. What's wrong?"
```

### **Documentation & README Issues**

#### **Problem: "I don't know what to write in my README"**
- **Cause**: Unclear on what makes a professional README
- **Solution**:
  - Follow the [required README sections](#step-7-create-professional-readme)
  - Look at popular open-source projects for examples
  - Include: project description, installation, usage examples, API credits
  - Use code blocks to show example commands and output
  - Add screenshots or GIFs if possible

**🤖 AI Prompt:**
```
"Help me write a professional README for my CLI project. It's a [description] using [API name]. Include installation steps, usage examples with output, and a features section. Here's my AGENTS.md for context: [paste]."
```

#### **Problem: "AGENTS.md feels incomplete or unhelpful"**
- **Cause**: Not enough project context for AI to assist effectively
- **Solution**:
  - Include: project overview, API details, CLI commands, file structure, coding standards
  - Be specific about architecture decisions
  - Document any constraints or requirements
  - Update as your project evolves

**🤖 AI Prompt:**
```
"Review my AGENTS.md and suggest what's missing: [paste content]. The project is a CLI tool using [API] with [X] commands."
```

### **General Development Issues**

#### **Problem: "I don't know which API to choose"**
- **Solution:**
  - Start with one of our 4 recommended APIs (Chuck Norris, EmojiHub, Ron Swanson, PokeAPI)
  - Choose something you find interesting or fun
  - Don't overthink it – the goal is to learn the workflow, not build a complex app

**🤖 AI Prompt:**
```
"I need to choose an API for a beginner CLI project. Here are my options:
1. Chuck Norris API (https://api.chucknorris.io/)
2. EmojiHub API (https://github.com/cheatsnake/emojihub)
3. Ron Swanson Quotes (https://github.com/jamesseanwright/ron-swanson-quotes)
4. PokeAPI (https://pokeapi.co/)

Which would be best for learning argparse and API integration? What interesting CLI commands could I build with each?"
```

### **Problem: "I've never used argparse before"**
- **Solution:**
  - Start with the [argparse tutorial](https://docs.python.org/3/tutorial/stdlib.html#command-line-arguments)
  - Use AI to generate boilerplate code
  - Begin with a simple command, then add complexity

**🤖 AI Prompt:**
```
"I'm new to argparse. Show me how to create a simple CLI with two commands: 'search' (takes a query string) and 'random' (no arguments). Include help text."
```

### **Problem: "I don't understand mocking for tests"**
- **Solution:**
  - This is expected! We haven't covered it in class
  - Use AI extensively to learn and implement mocking
  - Focus on mocking the `requests.get()` or `requests.post()` calls

**🤖 AI Prompt:**
```
"Explain mocking in pytest like I'm a beginner. Then show me how to mock a requests.get() call that returns JSON data. Include a complete example test."
```

### **Problem: "My tests fail in GitHub Actions but pass locally"**
- **Solution:**
  - Check that `requirements.txt` includes all dependencies
  - Ensure file paths are relative, not absolute
  - Verify Python version matches (3.10+ recommended)

**🤖 AI Prompt:**
```
"My pytest tests pass locally but fail in GitHub Actions. Here's my workflow file: [paste]. Here's the error: [paste]. What could be wrong?"
```

### **Problem: "I'm stuck on implementation and AI suggestions aren't helping"**
- **Solution:**
  - Break the problem into smaller pieces
  - Ask AI to explain concepts, not just generate code
  - Try different AI tools – Claude, ChatGPT, and Gemini have different strengths
  - Review your `AGENTS.md` and make your prompts more specific

**🤖 Better Prompting Strategy:**
```
# Instead of:
"Write code for my API function"

# Try:
"I'm building a function that calls the PokeAPI to get Pokemon data.

API Documentation: https://pokeapi.co/docs/v2

The function should:
1. Take a Pokemon name as input
2. Make a GET request to https://pokeapi.co/api/v2/pokemon/{name}
3. Return the Pokemon's types and abilities
4. Handle cases where the Pokemon doesn't exist

Show me how to structure this function with error handling."
```

**💡 Always include:**
- The API name and documentation URL
- The specific endpoint you're working with
- What data you need to extract
- Any error cases to handle

### **Problem: "How do I make my CLI actually runnable?"**
- **Solution:**
  - Add `if __name__ == "__main__":` block to `main.py`
  - Use `python -m src.main` to run your CLI
  - Or create a `__main__.py` file in your package

**🤖 AI Prompt:**
```
"How do I make my Python CLI package runnable with 'python -m package_name'? Show me the file structure and code needed."
```

### **Problem: "My README feels incomplete or unprofessional"**
- **Solution:**
  - Look at professional open-source projects for inspiration
  - Use AI to review and enhance your README
  - Include screenshots or example output (code blocks)

**🤖 AI Prompt:**
```
"Review this README and suggest improvements for clarity and professionalism: [paste README]. The project is a CLI tool for [description]."
```

---

## Example Project Reference

> **Note:** Your instructor will provide a complete example repository demonstrating all requirements. Use it as a reference for structure and quality, but **do not copy it** – your project must be original!

**Example project features to expect:**
- Clean argparse CLI with 3+ subcommands
- API integration with proper error handling and JSON parsing
- Comprehensive pytest tests with mocked API calls
- Professional README with installation, usage examples, and badges
- Passing CI/CD pipeline with GitHub Actions
- Well-structured `AGENTS.md` file with project context
- Organized code structure (src/, tests/, etc.)

**Example project idea (for reference):**
A Chuck Norris Jokes CLI that fetches random jokes, lists categories, searches jokes by keyword, and saves favorites to a local file. Demonstrates all core requirements while being fun and approachable.

**Link to example repository:** [TBD - will be provided]

---

## AI Tools Recommendations

### **For Planning & Architecture:**
- **[Claude](https://claude.ai/)** - Excellent for architectural discussions and design decisions
- **[ChatGPT](https://chat.openai.com/)** - Great for brainstorming and explaining concepts
- **[Gemini](https://gemini.google.com/)** - Good for technical explanations

### **For Coding:**
- **[GitHub Copilot](https://github.com/features/copilot)** - Best for inline code completion in VS Code
- **[gemini-cli](https://github.com/google-gemini/generative-ai-python)** - Terminal-based code generation
- **Copilot Chat in VS Code** - Context-aware coding assistance with @AGENTS.md reference

### **For Testing:**
- **Claude or ChatGPT** - Excellent for explaining mocking and generating test code
- **Copilot** - Good for test boilerplate generation

### **For Documentation:**
- **Any of the above** - All are capable of generating professional README content

---

## 🎯 Progress Tracker & Self-Assessment

Use this milestone checklist to verify you're meeting all grading criteria before submission. Each item maps directly to how your project will be graded.

### **✅ Automated Grading Criteria** (Easy to verify)

- [ ] **Repository is public** - Check settings → Visibility → Public
- [ ] **GitHub Actions configured** - `.github/workflows/tests.yml` exists
- [ ] **CI/CD passing** - Green checkmark in Actions tab (not red X)
- [ ] **All tests pass** - GitHub Actions shows success status
- [ ] **README.md exists** - Professional documentation in repository root
- [ ] **AGENTS.md exists** - AI context file with project details
- [ ] **requirements.txt exists** - Lists all dependencies (run `pip freeze > requirements.txt`)
- [ ] **Tests directory exists** - `tests/` folder with `test_*.py` files
- [ ] **Status badge in README** - Shows "passing" or "failing" CI status

**Quick verification commands:**
```bash
# Verify structure
ls -la .github/workflows/
ls -la tests/
ls README.md AGENTS.md requirements.txt

# Verify tests pass locally
pytest tests/ -v

# Check for all required files
git ls-files | grep -E "(README|AGENTS|requirements|tests|workflows)"
```

### **📋 Manual Assessment Criteria** (Test yourself)

- [ ] **CLI runs successfully** - Execute: `python -m src.main --help` (no errors)
- [ ] **All commands work** - Test each subcommand produces expected output
- [ ] **API integration functional** - Commands fetch and display real data
- [ ] **Error handling present** - Try invalid inputs (doesn't crash, shows error messages)
- [ ] **Docstrings on all functions** - Every function/class has NumPy-style docstring
- [ ] **Code organization clear** - Logical file structure, descriptive names

**Self-test checklist:**
```bash
# Test CLI help text
python -m src.main --help

# Test each command (replace with your commands)
python -m src.main random
python -m src.main search "test query"
python -m src.main categories

# Test error handling
python -m src.main invalid_command
```

### **🔍 Quality Assessment Criteria** (Polish check)

- [ ] **README is professional** - Clear description, install steps, usage examples, API credits
- [ ] **README has all sections** - Title, description, features, installation, usage, testing, technologies, badges
- [ ] **Usage examples clear** - Include command examples with expected output
- [ ] **Test coverage comprehensive** - Tests cover main functionality, edge cases, errors
- [ ] **Mocking implemented** - Tests use `unittest.mock` to avoid real API calls
- [ ] **Code follows PEP 8** - Run `pylint src/` or use VS Code linter
- [ ] **AGENTS.md is detailed** - Includes project overview, API info, CLI commands, architecture
- [ ] **Creative implementation** - Goes beyond minimum requirements, shows thoughtfulness

**Quality verification questions:**
- Can someone clone my repo and run it in 5 minutes?
- Would I be proud to show this to an employer?
- Does my README explain what the project does without needing to read code?
- Do my tests actually test the important functionality?
- Did I document my AI-assisted development process in AGENTS.md?

### **🚀 Final Pre-Submission Checklist**

**Complete these steps before submitting:**

1. **Fresh clone test** (most important!)
   ```bash
   cd /tmp
   git clone <your-repo-url>
   cd <repo-name>
   pip install -r requirements.txt
   pytest tests/
   python -m src.main --help
   ```
   ✅ Everything should work in this fresh environment

2. **Verify GitHub Actions**
   - Go to repository → Actions tab
   - Check latest workflow run has green checkmark
   - If red X, click to see error and fix

3. **Check README rendering**
   - View README on GitHub repository page
   - Verify badge shows correctly
   - Check that all links work
   - Ensure code blocks display properly

4. **Validate test coverage**
   - Run: `pytest tests/ -v`
   - Verify all tests pass
   - Check that you're testing the right things (not just trivial tests)

5. **Code quality review**
   - Run: `pylint src/` (fix any critical issues)
   - Check for hardcoded values (API keys, file paths)
   - Verify consistent code style

6. **Documentation completeness**
   - README has installation, usage, and examples
   - AGENTS.md documents AI assistance
   - Docstrings on all functions
   - Comments explain complex logic

**Ready to submit if:**
- ✅ All checkboxes above are checked
- ✅ Fresh clone test succeeded
- ✅ Green checkmark in GitHub Actions
- ✅ README looks professional on GitHub
- ✅ You can explain how every part of your code works

---

## Submission Instructions

### **What to Submit:**

Submit your **public GitHub repository URL** to Canvas by **Sunday, October 19, 2025 at 11:59 PM**.

**Canvas submission format:**
1. Navigate to the Midterm Project assignment on Canvas
2. Submit the URL to your public GitHub repository (e.g., `https://github.com/yourusername/your-project-name`)
3. Add a brief description (1-2 sentences) about what your CLI does in the Canvas comments box

**Example submission:**
```
Repository URL: https://github.com/student123/chuck-norris-cli
Description: A command-line tool that fetches Chuck Norris jokes by category,
provides random jokes, and allows searching jokes by keyword.
```

### **Repository Checklist:**

Before submitting, verify your repository has:

- [ ] **Public visibility** - Set in repository settings
- [ ] **All code files** - Organized in proper structure
- [ ] **`AGENTS.md`** - Project context for AI assistants
- [ ] **README.md** - Professional documentation with all required sections
- [ ] **requirements.txt** - All Python dependencies listed
- [ ] **tests/** directory with test files
- [ ] **.github/workflows/** with CI/CD configuration
- [ ] **Passing tests** - Green checkmark in Actions tab
- [ ] **Badges in README** - At minimum: test status badge
- [ ] **LICENSE file** - MIT or similar open source license

### **Verification Steps Before Canvas Submission:**

1. **Clone your repository fresh** in a new location
2. **Install dependencies:** `pip install -r requirements.txt`
3. **Run tests:** `pytest tests/`
4. **Run CLI:** `python -m src.main --help`
5. **Check GitHub Actions** for green checkmark
6. **Review README** - Is it clear and complete?

---

## Tips for Success

### **🎯 Start Simple, Iterate**
- Get a basic working version first
- Add features incrementally
- Test each addition before moving forward

### **🤖 Use AI Strategically**
- Reference your `AGENTS.md` file for consistent context
- Ask AI to explain, not just generate code
- Review and understand AI-generated code before using it

### **📝 Document as You Go**
- Write your README alongside development
- Keep `AGENTS.md` updated with decisions
- Add docstrings immediately after writing functions

### **🧪 Test Early, Test Often**
- Write tests alongside features
- Use AI to learn mocking – it's okay you haven't covered it!
- Fix failing tests immediately

### **💬 Ask for Help**
- Use AI tools extensively – that's the point!
- Experiment with different prompting strategies
- Try multiple AI tools if one isn't helping

### **🏆 Make It Portfolio-Worthy**
- Choose an API you find interesting
- Write a README you'd be proud to show employers
- Add creative features that showcase your skills

---

## Resources

### **Documentation:**
- [Python argparse tutorial](https://docs.python.org/3/tutorial/stdlib.html#command-line-arguments)
- [pytest documentation](https://docs.pytest.org/)
- [unittest.mock guide](https://docs.python.org/3/library/unittest.mock.html)
- [GitHub Actions quickstart](https://docs.github.com/en/actions/quickstart)
- [requests library](https://requests.readthedocs.io/)

### **Learning Resources:**
- [Real Python: Command Line Interfaces](https://realpython.com/command-line-interfaces-python-argparse/)
- [Real Python: Mocking in Python](https://realpython.com/python-mock-library/)
- [Writing good README files](https://www.makeareadme.com/)

### **API Resources:**
- [Public APIs list](https://github.com/public-apis/public-apis)
- [API list with no auth required](https://mixedanalytics.com/blog/list-actually-free-open-no-auth-needed-apis/)

### **AI Assistance:**
- [Claude](https://claude.ai/) - Advanced reasoning and explanations
- [ChatGPT](https://chat.openai.com/) - Versatile coding assistant
- [Gemini](https://gemini.google.com/) - Google's AI assistant
- [GitHub Copilot](https://github.com/features/copilot) - AI pair programmer

---

## Academic Integrity

- **AI assistance is encouraged** - This is an AI-enhanced development course
- **Your code must be original** - Don't copy other students' work
- **Understand what you submit** - Be able to explain any code in your project
- **Document AI usage** - `AGENTS.md` shows how you leveraged AI tools
- **Reference the example** - Learn from it, but don't copy it

Using AI tools is not cheating in this course – it's a required skill! However, blindly copying code you don't understand (from AI or elsewhere) without learning from it defeats the purpose.

---

**🎉 Good luck!** This project is your opportunity to build something genuinely useful while learning modern AI-assisted development workflows. Remember: the goal is to learn the process, not to build the perfect application. Embrace the AI tools, ask lots of questions, and have fun!
