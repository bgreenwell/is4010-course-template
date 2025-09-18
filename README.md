# IS4010: AI-Enhanced Application Development

![Languages](https://img.shields.io/badge/languages-Python%20%7C%20Rust-blue.svg)
![AI Augmented](https://img.shields.io/badge/AI-Augmented-blueviolet.svg)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Hey everyone, and welcome to IS4010! This GitHub repository is your central hub for all code, labs, resources, and project submissions for the course. Please clone this repository, and be sure to pull frequently for updates.

## Course description

This course introduces students to a computer programming language with object-oriented programming (OOP) principles which include creating and manipulating classes and objects. Students will develop solutions to process data and implement algorithms in a modern integrated development environment (IDE) to support debugging and team development. Popular libraries and tools to support OOP programming, including AI-powered tools and libraries, will also be studied and applied to enhance problem-solving and application development. 

## 🚀 Quick links

* **Full syllabus:** [Read the full syllabus here](https://bgreenwell.github.io/is4010-instructor-materials/syllabus.html)
* **Canvas page:** [IS4010 Fall 2025 Course](https://uc.instructure.com/courses/1812798)
* **Class Teams channel:** [link to microsoft teams channel]

## 🛠️ Course tools

You will need the following software installed and configured by the end of the first week. For detailed instructions, please see the [**Setup Guide**](./resources/SETUP_GUIDE.md).

* Visual Studio Code (VS Code)
* Git & a GitHub account
* Python 3.10+
* The Rust Programming Language toolchain
* GitHub Copilot (via the Student Developer Pack)

## 📁 Repository structure

This repository is organized to make finding what you need simple.

* **/labs:** Contains starter code and instructions for weekly lab assignments.
* **/projects:** Contains specifications for the midterm and final collaborative projects. Your teams will create your own private repositories for these.
* **/resources:** Contains helpful code snippets, articles, and other resources.
* **/.gitignore:** The gitignore file for this course.
* **/README.md:** You are here!

## 🗺️ Course roadmap

This is a high-level overview of our journey this semester. A more detailed schedule is available on Canvas.

| Week | Module | Topic | Slides | Labs | Notebooks |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Weeks 1-2 | Foundations & modern tooling | Git, GitHub, and our AI code assistants (Copilot & Gemini) | [W01\_Introduction](https://bgreenwell.github.io/is4010-instructor-materials/IS4010_W01_Introduction.html#/title-slide), [W02\_AI\_Copilots](https://bgreenwell.github.io/is4010-instructor-materials/IS4010_W02_AI_Copilots.html) | [Lab 01](./labs/lab01/), [Lab 02](./labs/lab02/) | *Coming soon* |
| Weeks 3-6 | Python fundamentals w/ AI | Python basics, data structures, and OOP | [W03\_Python\_Basics](https://bgreenwell.github.io/is4010-instructor-materials/IS4010_W03_Python_Basics.html), [W04\_Data\_Structures](https://bgreenwell.github.io/is4010-instructor-materials/IS4010_W04_Data_Structures.html), [W05\_Functions\_and\_Errors](https://bgreenwell.github.io/is4010-instructor-materials/IS4010_W05_Functions_and_Errors.html), [W06\_OOP](https://bgreenwell.github.io/is4010-instructor-materials/IS4010_W06_OOP.html) | [Lab 03](./labs/lab03/), [Lab 04](./labs/lab04/), [Lab 05](./labs/lab05/), [Lab 06](./labs/lab06/) | *Coming soon*, [W04\_DataStructures](https://github.com/bgreenwell/is4010-instructor-materials/blob/main/notebooks/IS4010_W04_DataStructures.ipynb), *Coming soon*, *Coming soon* |
| Weeks 7-9 | Building a Python application | APIs, data handling, and the midterm project | [W07\_Working\_with\_Data](https://bgreenwell.github.io/is4010-instructor-materials/IS4010_W07_Working_with_Data.html) | [Lab 07](./labs/lab07/), Lab 08 (TBD), Lab 09 (TBD) | *Coming soon* |
| Weeks 10-12| New frontiers: Rust | Rust fundamentals, ownership, and a CLI app | [W10\_Welcome\_to\_Rust](https://bgreenwell.github.io/is4010-instructor-materials/IS4010_W10_Welcome_to_Rust.html), [W11\_The\_Soul\_of\_Rust](https://bgreenwell.github.io/is4010-instructor-materials/IS4010_W11_The_Soul_of_Rust.html), [W12\_Building\_a\_CLI\_App\_in\_Rust](https://bgreenwell.github.io/is4010-instructor-materials/IS4010_W12_Building_a_CLI_App_in_Rust.html) | [Lab 10](./labs/lab10/), [Lab 11](./labs/lab11/), [Lab 12](./labs/lab12/) | *Coming soon* |
| Week 13| Final project workshop | Collaborative work session and MVP check-ins | (Project workshop) | | |
| Week 14 | Final project polish | Presentation dry-runs and peer feedback | (Project workshop) | | |
| Exam week | Demo day\! | Final project presentations | (Presentations) | | |

## 🤖 Our AI policy: a quick reminder

This course operates on a new, modern principle: **use AI, but use it wisely.**

Unlike the previous version of this course which restricted AI use, the use of AI tools is not only permitted but encouraged. However, remember that the goal is for *you* to learn.

1.  **You are the pilot, AI is the co-pilot.** You are responsible for every line of code you submit.
2.  **Always understand the code.** If you use AI to generate something, you must be able to explain what it does. Use the AI to help you learn, not just to produce an answer.
3.  **Acknowledge your partner.** In your final project, your team will be required to document how you used AI tools in your development process.

## 📊 How grading works

This course uses an **automated grading system** that provides you with immediate, detailed feedback on your lab submissions. Here's what to expect:

### **Automatic assessment**
- Your [GitHub](https://github.com/) repository is automatically evaluated within 24-48 hours of submission
- The system checks code functionality, repository setup, documentation quality, and requirement compliance
- Scoring is objective and consistent across all students

### **GitHub issues feedback**
After grading, you'll receive personalized feedback as a **GitHub Issue** in your repository containing:
- 📊 **Point breakdown** - Exactly how points were earned/lost for each component
- ✅ **Success highlights** - Recognition for components that work correctly  
- 🔧 **Improvement guidance** - Specific next steps to address any issues
- 🧪 **Test results** - For code labs, see which functions pass/fail automated tests

### **What this means for you**
- **No waiting weeks for grades** - Get feedback quickly while the assignment is fresh in your mind
- **Learn from specific examples** - See exactly which parts of your code work and which need improvement
- **Professional development** - Experience automated testing and CI/CD practices used in industry
- **More instructor time** - Automated grading frees up office hours for higher-level concept discussion

### **Example feedback**
```
🎯 Lab 2 Submission Feedback - 8/10 points (80%)

✅ Repository Setup: 3/3 points - Private repo with instructor access
✅ Python Functions: 4/4 points - All three functions working perfectly! 
❌ Markdown Content: 0/1 points - Missing problem sections in lab02_prompts.md

Next Steps: Add the three required problem sections to your markdown file...
```

**💡 Pro tip**: Students with perfect scores (10/10) won't receive feedback issues since no improvements are needed!

## 🤔 Getting help

If you get stuck, help is always available. Please use the following channels:

1.  Ask a question in our class **Teams channel**.
2.  Come to my virtual or in-person office hours.
3.  Email me to schedule a separate meeting.
4.  **Review your GitHub Issues** - Automated feedback often answers common questions about your submission.

## 📚 Additional resources

This section provides essential tools and resources to support your learning journey in IS4010, from interactive coding environments to AI assistants.

### 🔬 Interactive learning tools

#### Jupyter Notebooks
Some course materials include **Jupyter Notebooks** - interactive documents that combine code, explanations, and visualizations in one place. These notebooks allow you to run and modify code examples from lectures directly in your browser.

- **[Jupyter Notebook Documentation](https://jupyter-notebook.readthedocs.io/en/latest/)** - Complete guide to using Jupyter notebooks
- **[Try Jupyter Online](https://jupyter.org/try)** - Test notebooks in your browser without installing anything
- **[JupyterLab](https://jupyterlab.readthedocs.io/)** - Next-generation interface for Jupyter notebooks

**Why use notebooks?**
- **Learn by doing**: Run code examples from slides and modify them to see what happens
- **Document your learning**: Combine notes, code, and outputs in one organized document
- **Professional skill**: Jupyter notebooks are widely used in data science and research industries
- **Course integration**: Some weeks include companion notebooks for hands-on practice

#### Python learning resources
- **[Python Tutor](https://pythontutor.com/)** - Visualize how your Python code executes step-by-step
- **[Replit](https://replit.com/)** - Online Python environment for quick experimentation
- **[Python.org Beginner's Guide](https://wiki.python.org/moin/BeginnersGuide)** - Official Python learning resources

### 🤖 AI-powered learning assistants

This section provides a summary of free Large Language Model (LLM) clients that are suitable for students. The landscape of AI tools is constantly changing, so some details may be out of date.

**💡 Pro tips for using AI in this course:**
- **Start specific**: Instead of "help me code," try "explain why this Python function returns None"
- **Share context**: Include your code, error messages, and what you're trying to accomplish
- **Learn actively**: Ask the AI to explain concepts, not just provide answers
- **Verify outputs**: Always test AI-generated code and understand what it does before submitting

| Client Name | Type | Key Features | Free Tier Details | Best For |
| :--- | :--- | :--- | :--- | :--- |
| **[ChatGPT](https://chat.openai.com/)** | Web UI | General-purpose conversational AI for a wide range of tasks. | Free access to a highly capable model, with some usage limits. | General Q&A, content creation, and exploring creative ideas. |
| **[Claude](https://claude.ai/)** | Web UI | Strong capabilities in creative writing, summarization, and analysis. | Free tier with daily message limits. | Sophisticated writing tasks and in-depth document analysis. |
| **[Gemini on the Web](https://gemini.google.com)** | Web UI | User-friendly interface for direct chat, content generation, and analysis. | Free access to a powerful model, with some limits on usage. | Everyday tasks, brainstorming, writing assistance, and learning LLM capabilities. |
| **[GitHub Copilot](https://github.com/features/copilot)** | IDE Extension | AI-powered code completion, suggestions, and chat within your editor. | Free for verified students, teachers, and maintainers of popular open-source projects. | Seamlessly integrating AI assistance into the software development workflow. |
| **[Gemini CLI](https://github.com/google/gemini-cli)** | Command-Line | Direct access to Gemini models, scripting, automation. | Free tier with rate limits (requests per minute). | Developers and power users for terminal-based tasks. |
| **[LM Studio](https://lmstudio.ai/)** | Desktop App | Run open-source LLMs locally, offline capability. | Completely free software; uses your computer's resources. | Running models offline and experimenting with privacy. |
| **[Ollama](https://ollama.ai/)** | CLI / Local Server | Easily run and manage open-source LLMs locally, provides an API. | Completely free software; uses your computer's resources. | Developers building applications on top of local LLMs. |
| **[LibreChat](https://librechat.ai/)** | Self-Hosted Web UI | ChatGPT-like interface, supports multiple AI backends. | Free software; you cover hosting/API costs (if any). | Creating a personal, customized chat platform. |
| **[Hugging Face Chat](https://huggingface.co/chat/)**| Web UI | Access and chat with a wide variety of open-source models. | Completely free to use. | Quickly trying out and comparing open-source models. |
| **[Poe by Quora](https.poe.com)** | Web & Mobile App | Access a mix of popular models (Claude, Gemini, etc.) in one app. | Free daily message limits for most models. | Comparing different flagship models, especially on mobile. |
| **[Google AI Studio](https://aistudio.google.com/)** | Web UI | Prototype prompts for the Gemini API, generate code. | Free tier with rate limits, same as the Gemini API. | Students learning to build with the Gemini API. |

#### 📝 Effective AI prompting for IS4010

**For debugging code:**
```
"I'm getting this error in my Python function: [paste error message].
Here's my code: [paste code]. The function should [explain what it's supposed to do].
What's wrong and how can I fix it?"
```

**For learning concepts:**
```
"Can you explain the difference between Python lists and dictionaries?
When should I use each one? Please include simple examples."
```

**For code review:**
```
"Can you review this Python function and suggest improvements?
Here's what it does: [explain purpose] and here's my code: [paste code]"
```

#### 🎯 AI tool recommendations by task

- **Quick code help**: GitHub Copilot (integrated into VS Code)
- **Debugging assistance**: ChatGPT or Claude (paste code + error messages)
- **Concept explanations**: Gemini or Claude (ask for step-by-step explanations)
- **Code review**: ChatGPT or Claude (ask for feedback and improvements)
- **Learning new topics**: Any of the above + follow-up questions

### 🔗 Additional learning resources

#### Course support
- **[Setup Guide](./resources/SETUP_GUIDE.md)** - Complete installation instructions for all course tools
- **[Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)** - Essential Git commands reference
- **[VS Code Tips](https://code.visualstudio.com/docs/getstarted/tips-and-tricks)** - Productivity tips for your IDE

#### Computer science fundamentals
- **[Big O Notation Guide](https://www.bigocheatsheet.com/)** - Algorithm complexity reference
- **[Data Structure Visualizations](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html)** - See how algorithms work step-by-step

**Disclaimer:** This list is not exhaustive and was last updated on September 18, 2025. The free tiers and features of these services are subject to change. Please refer to the official websites for the most current information.
