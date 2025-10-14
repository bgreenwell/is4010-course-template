# Week 8: Building Professional Python Applications

**Course:** IS4010 - AI-Enhanced Application Development
**Topic:** Command-Line Interfaces & Python Package Structure
**Instructor:** Brandon M. Greenwell

---

## 📚 Learning Objectives

By the end of this session, you should be able to:

1. Create professional CLI applications using Python's `argparse` library
2. Design intuitive command-line interfaces with arguments, flags, and subcommands
3. Structure Python projects as proper packages with clean imports
4. Understand and apply the `__name__ == "__main__"` pattern
5. Make your code installable using modern `pyproject.toml` configuration
6. Apply these patterns to your midterm project for professional-quality code

---

## Part 1: Command-Line Interfaces (CLIs)

### Why CLIs Matter

Command-line interfaces are essential tools in professional software development:

- **Automation**: Run repetitive tasks without manual interaction
- **Scripting**: Chain multiple commands together in scripts
- **Professional standard**: Git, pip, docker, AWS CLI - all use CLI interfaces
- **Developer productivity**: CLIs are faster than GUIs for many tasks
- **Career relevance**: Every Python job involves CLI tools

You've already been using CLIs throughout this course: `git`, `pip`, `python`, `jupyter notebook` - these are all command-line interfaces.

### Understanding argparse

[argparse](https://docs.python.org/3/library/argparse.html) is Python's built-in library for creating CLIs. It provides:

- **Automatic help generation**: `--help` flag works automatically
- **Input validation**: Type checking and value constraints
- **Error handling**: Clear error messages for incorrect usage
- **Professional quality**: Used in production at major tech companies

### CLI Design Patterns

**Three types of inputs:**
1. **Positional arguments** (required, order matters): `git commit message.txt`
2. **Optional arguments/flags** (named, flexible order): `git commit --amend -m "Fix"`
3. **Subcommands** (different actions): `git add` vs `git commit`

**Design principles:**
- Keep interfaces intuitive (users should guess correct syntax)
- Follow conventions (`-h` for help, `-v` for verbose)
- Provide clear error messages
- Include comprehensive help text

### Basic argparse Structure

```python
import argparse

def main():
    # Create parser
    parser = argparse.ArgumentParser(description="Tool description")

    # Add arguments
    parser.add_argument("name", help="Positional argument")
    parser.add_argument("--flag", action="store_true", help="Optional flag")

    # Parse arguments
    args = parser.parse_args()

    # Use the arguments
    print(f"Hello, {args.name}!")

if __name__ == "__main__":
    main()
```

### Advanced Features

- **Type conversion**: `type=int` automatically converts and validates
- **Default values**: `default=10` provides fallback values
- **Choices**: `choices=["json", "csv"]` restricts valid options
- **Required flags**: `required=True` for mandatory optional arguments
- **Short and long forms**: `-o` and `--output` both work

### Subcommands

For tools with multiple operations (like `git add`, `git commit`):

```python
parser = argparse.ArgumentParser()
subparsers = parser.add_subparsers(dest="command")

# Add subcommands
init_parser = subparsers.add_parser("init")
build_parser = subparsers.add_parser("build")
```

This pattern enables scalable, Git-style CLIs.

### CLI Best Practices

- **Clear error messages**: Tell users exactly what went wrong and how to fix it
- **Verbose mode**: Add `--verbose` flag for debugging output
- **Exit codes**: Return 0 for success, non-zero for errors (enables scripting)
- **Confirmation prompts**: Ask before destructive operations
- **Progress indicators**: Show activity for long-running operations

---

## Part 2: Python Packages & Project Structure

### From Scripts to Packages

Most Python developers progress through these stages:

1. **Single file**: Everything in `script.py`
2. **Multiple files**: `api.py`, `utils.py`, `cli.py` in one folder
3. **Package structure**: Organized with `__init__.py` files (professional standard)
4. **Installable package**: Can `pip install` your own code

Professional projects always use Stage 3 or 4.

### What is a Package?

- **Module**: A single `.py` file
- **Package**: A directory containing an `__init__.py` file
- **Subpackage**: A package inside another package

The `__init__.py` file marks a directory as a Python package. It can be empty or contain initialization code.

### Why Package Structure Matters

- **Organization**: Logical grouping of related functionality
- **Reusability**: Import code across multiple projects
- **Collaboration**: Team members work on different modules without conflicts
- **Testing**: Easier to test individual components
- **Distribution**: Share code with others
- **Professionalism**: Signals you understand production Python

### Recommended Structure

```
my_project/
├── src/                      # Source code (modern best practice)
│   └── my_package/
│       ├── __init__.py       # Package marker
│       ├── api.py            # API client
│       ├── cli.py            # CLI interface
│       ├── models.py         # Data models
│       └── utils.py          # Helper functions
├── tests/                    # Test directory
│   ├── __init__.py
│   ├── test_api.py
│   └── test_cli.py
├── pyproject.toml            # Project configuration
├── README.md                 # Documentation
└── .gitignore               # Git exclusions
```

The `src/` layout is the modern Python standard recommended by the [Python Packaging Authority](https://packaging.python.org/).

### The `__name__ == "__main__"` Pattern

This pattern allows code to be both runnable and importable:

```python
def my_function():
    return "Hello"

def main():
    print(my_function())

# Runs when executed directly, NOT when imported
if __name__ == "__main__":
    main()
```

**When to use:**
- Every module that might be run as a script
- Entry points for CLI applications
- Testing individual modules during development

### Import Strategies

**Absolute imports** (preferred):
```python
from my_package.api import fetch_data
from my_package.utils import format_output
```

**Relative imports** (within packages):
```python
from .api import fetch_data        # Same directory
from ..parent import something     # Parent directory
```

**Best practice**: Use absolute imports unless paths become excessively long.

### Making Code Installable: pyproject.toml

Modern Python projects use [`pyproject.toml`](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/) (replaces old `setup.py`):

```toml
[project]
name = "my-tool"
version = "0.1.0"
dependencies = ["requests>=2.31.0"]

[project.scripts]
my-tool = "my_package.cli:main"  # Creates CLI command
```

**Install in editable mode:**
```bash
pip install -e .
```

This links your package so changes appear immediately without reinstalling.

### Modern Tooling: uv

[`uv`](https://github.com/astral-sh/uv) is a new, blazingly fast Python package installer (written in Rust!):

- 10-100× faster than pip
- Drop-in replacement: `uv pip install requests`
- Growing industry adoption

Optional but recommended for new projects.

---

## Integration: CLI + Package Structure

Professional applications combine both concepts:

```
my_project/
├── src/
│   └── my_tool/
│       ├── __init__.py
│       ├── api.py         # Business logic
│       ├── cli.py         # argparse interface
│       └── utils.py       # Helpers
└── pyproject.toml         # Defines CLI entry point
```

**In cli.py:**
```python
import argparse
from my_tool.api import fetch_data
from my_tool.utils import format_output

def main():
    parser = argparse.ArgumentParser()
    # ... add arguments ...
    args = parser.parse_args()

    data = fetch_data(args.resource)
    print(format_output(data))
```

**After `pip install -e .`:**
```bash
my-tool pokemon --format json
```

---

## Real-World Applications

### Where You'll Use These Skills

- **Web development**: Django's `manage.py`, Flask's `flask` command
- **Data science**: Command-line tools for data processing pipelines
- **DevOps**: Automation scripts and deployment tools
- **API clients**: Creating user-friendly interfaces for APIs
- **Internal tools**: Company-specific utilities and automation

### Industry Examples

- **Django**: Sophisticated CLI with subcommands (`runserver`, `migrate`, `makemigrations`)
- **AWS CLI**: Complex tool managing cloud infrastructure
- **Black**: Code formatter with intuitive CLI
- **Pytest**: Testing framework with rich CLI options

---

## Bridge to Rust (Next Week)

### Python's Manual Approach

What we did today:
- Manually create directory structure and `__init__.py` files
- Choose between multiple packaging tools
- Understand complex import rules
- Configure `pyproject.toml` with various options

### Rust's Automated Approach

Next week with [Cargo](https://doc.rust-lang.org/cargo/):
- One command: `cargo new my_project` creates perfect structure
- Built-in package management, building, testing, documentation
- No decisions needed - one standard way
- Everything "just works"

**Learning insight**: Understanding Python's manual approach will help you appreciate Rust's automation and understand *why* it matters.

---

## Applying to Your Midterm Project

### This Week's Action Items

1. **Restructure your code** into a proper package with `src/` layout
2. **Add CLI interface** with argparse for easy testing and demos
3. **Create `pyproject.toml`** to make your project installable
4. **Test installation**: Run `pip install -e .` and verify it works
5. **Update README**: Include installation and usage instructions

### Success Criteria

- ✅ Can run `pip install -e .` to install your project
- ✅ CLI works with intuitive arguments and helpful errors
- ✅ Code organized in logical modules with clean imports
- ✅ `--help` flag provides clear usage instructions
- ✅ README explains installation and demonstrates usage examples

### Tips for Success

- **Start simple**: Get basic structure working, then refine
- **Test frequently**: Run your CLI after each change
- **Use AI assistance**: Perfect for generating boilerplate and structure
- **Study examples**: Look at popular Python packages on GitHub for inspiration
- **Ask for help**: Use office hours for structure questions

---

## Resources

### Official Documentation

- **[argparse Tutorial](https://docs.python.org/3/howto/argparse.html)** - Step-by-step guide
- **[Python Packages](https://docs.python.org/3/tutorial/modules.html#packages)** - Modules and packages explained
- **[Packaging Projects](https://packaging.python.org/en/latest/tutorials/packaging-projects/)** - Official packaging tutorial
- **[pyproject.toml Specification](https://packaging.python.org/en/latest/specifications/pyproject-toml/)** - Configuration format

### Advanced Topics

- **[Click](https://click.palletsprojects.com/)** - Popular alternative CLI framework (used by Flask)
- **[Typer](https://typer.tiangolo.com/)** - Modern CLI with type hints (built on Click)
- **[Rich](https://rich.readthedocs.io/)** - Beautiful terminal output formatting
- **[PEP 8](https://peps.python.org/pep-0008/)** - Python style guide
- **[Src Layout vs Flat Layout](https://packaging.python.org/en/latest/discussions/src-layout-vs-flat-layout/)** - PyPA discussion

### Career Development

- **System design interviews** often include designing CLI tools
- **Portfolio projects** should demonstrate proper package structure
- **Open source contribution** requires understanding package standards
- **Professional Python** means professional project organization

---

## Key Takeaways

### Command-Line Interfaces

- argparse creates professional CLIs with minimal code
- Design intuitive interfaces following common conventions
- Subcommands enable scalable, Git-style tools
- Good CLIs have clear help text and error messages

### Python Packages

- Packages organize code into logical, reusable modules
- `__init__.py` marks directories as packages
- `__name__ == "__main__"` makes code both runnable and importable
- `pyproject.toml` is the modern standard for Python projects
- `src/` layout is recommended for new projects

### Integration

- Professional applications combine CLI + package structure
- Clean imports and modular design enable testing and maintenance
- Proper structure signals professional Python development skills
- These patterns apply to projects of all sizes

### Next Steps

- Apply these patterns to your midterm project this week
- Practice makes perfect - restructure and test iteratively
- Use AI tools to help generate boilerplate structure
- Come to office hours with specific questions
- Next week: See how Rust makes all of this automatic

---

## Additional Notes

### AI Assistance Strategies

**Effective prompts for CLIs:**
- "Create a Python argparse CLI for [describe your tool] with [list features]"
- "Add subcommands for fetch, list, and search operations"
- "Improve error handling and input validation for my CLI"

**Effective prompts for packages:**
- "Design a Python package structure for [describe project] with proper imports"
- "Create a pyproject.toml for my API client project"
- "Convert my single-file script into a proper Python package"

AI tools excel at generating boilerplate but you must understand the structure.

### Common Mistakes to Avoid

- Forgetting `__init__.py` files (makes imports fail)
- Using relative imports in main scripts (causes errors)
- Not testing CLI with various argument combinations
- Missing error handling in CLI functions
- Overly complex package structures for simple projects

### When to Keep It Simple

Not every project needs full package structure:
- **Quick scripts**: Single file is fine
- **Personal tools**: Simple is often better
- **Prototypes**: Structure can come later

But for your midterm and portfolio projects: use professional structure.

---

**Remember**: Professional Python development is about more than just code that works - it's about code that's organized, maintainable, and follows community standards. The patterns you learned today are used in every professional Python codebase.

Good luck with your midterm projects! 🚀
