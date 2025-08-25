# IS4010 Setup Guide

Welcome to IS4010! This guide provides step-by-step instructions for setting up your computer with all the necessary tools for this course. Please follow these instructions carefully. If you run into any issues, please ask for help in our class teams channel.

---

## Table of contents

1.  [Visual Studio Code (VS Code)](#1-visual-studio-code-vs-code)
2.  [Git](#2-git)
3.  [GitHub Account & Student Benefits](#3-github-account--student-benefits)
4.  [Python](#4-python)
5.  [Rust](#5-rust)
6.  [Gemini CLI (requires Node.js)](#6-gemini-cli)
7.  [GitHub Copilot Setup](#7-next-steps-github-copilot-setup)
8.  [Recommended VS Code Extensions](#8-recommended-vs-code-extensions)
9.  [Installing Course Packages](#9-installing-course-packages)

---

## 1. Visual Studio Code (VS Code)

This will be our primary code editor, or integrated development environment (IDE), for the entire course. You can find step-by-step installation instructions for your operating system below [here](https://code.visualstudio.com/docs/setup/setup-overview). Here's the short version for each platform:

### Windows

1.  Navigate to the [VS Code download page](https://code.visualstudio.com/download).
2.  Download the **user installer** for Windows.
3.  Run the `.exe` file you downloaded.
4.  Accept the license agreement and click next through the installation steps. It is highly recommended that you leave the "add to PATH" option checked on the "Select Additional Tasks" screen.

### macOS

1.  Navigate to the [VS Code download page](https://code.visualstudio.com/download).
2.  Download the **Mac Universal** `.zip` file.
3.  Once downloaded, unzip the file.
4.  Drag the `Visual Studio Code.app` file into your `Applications` folder.
5.  Launch VS Code. Open the command palette (`Shift` + `Command` + `P`) and type `shell command`. Select the option "Shell Command: Install 'code' command in PATH" to make it available from your terminal.

### Linux

1.  Navigate to the [VS Code download page](https://code.visualstudio.com/download).
2.  Download the `.deb` package (for Ubuntu/Debian-based distributions) or the `.rpm` package (for Fedora/RHEL-based distributions).
3.  Open your terminal, navigate to your Downloads folder, and run the appropriate command:
    * For `.deb`: `sudo apt install ./<file_name>.deb`
    * For `.rpm`: `sudo rpm -i <file_name>.rpm`

### Verifying your installation

Open your terminal (or PowerShell on Windows) and type the following command. You should see a version number printed.

`code --version`

---

## 2. Git

Git is the version control system we will use to track changes in our code and collaborate.

### Windows

1.  Navigate to the [Git downloads page](https://git-scm.com/downloads).
2.  The download for "Git for Windows" should start automatically.
3.  Run the installer you downloaded.
4.  It is safe to accept the default options for all steps in the installation wizard. There are many steps, but you can simply click "Next" through all of them.

### macOS

Git is often pre-installed. First, open your `Terminal` app and type `git --version`.

* If you see a version number, you are all set!
* If it is not installed, your Mac will pop up a window prompting you to install the "Command Line Developer Tools." Please click "Install" and follow the steps. This will install Git for you.

### Linux

Open your terminal and run the following command to install Git using your system's package manager.

`sudo apt update && sudo apt install git`

### Verifying your installation

Open your terminal and type the following command. You should see a version number printed.

`git --version`

### Recommendations for Windows Users

For Windows users, we **strongly recommend** using Windows Terminal with Git Bash as your primary terminal. This gives you a modern terminal experience with Unix-like commands that match your macOS and Linux classmates.

#### Why Windows Terminal + Git Bash?

1. **Consistency Across Platforms**: Git Bash provides Unix-like commands that match macOS/Linux environments
2. **Course Compatibility**: All course examples (Python, Rust, Git commands) work identically across platforms
3. **Modern Experience**: Windows Terminal provides tabs, better fonts, easy copy/paste, and customizable themes
4. **Industry Standard**: Most tutorials and documentation assume Unix-like environments
5. **Future-Proof**: Students learn transferable skills that work on any platform

#### Install Windows Terminal

Windows Terminal should already be installed on Windows 11. For Windows 10 users:

1. Open the **Microsoft Store**
2. Search for **"Windows Terminal"** 
3. Install the official Microsoft app
4. Pin it to your taskbar for easy access

#### Configure Git Bash Profile

**Modern Git Installation (Recommended):**
If you installed Git for Windows 2.42.0 or later, simply:
1. Re-run the Git installer 
2. Check the box: **"Add a Git Bash profile to Windows Terminal"**
3. Complete the installation

**Manual Profile Setup:**
If the automatic option isn't available:
1. Open Windows Terminal
2. Click the dropdown arrow next to the `+` tab button
3. Select **"Settings"**
4. Click **"Add a new profile"** → **"New empty profile"**
5. Configure these settings:
   - **Name**: `Git Bash`
   - **Command line**: `"C:\Program Files\Git\bin\bash.exe" --login -i`
   - **Starting directory**: `C:\Users\%USERNAME%` (or your preferred project folder)
   - **Icon**: `C:\Program Files\Git\mingw64\share\git\git-for-windows.ico`
6. Click **"Save"**

#### Set as Default (Recommended)

1. In Windows Terminal settings, go to **"Startup"**
2. Set **"Default profile"** to **"Git Bash"**
3. Set **"Default terminal application"** to **"Windows Terminal"**

#### Verification

Open Windows Terminal and you should see:
- Git Bash as your default shell
- A prompt ending with `$` (not `>`)
- Unix-like commands work: `ls`, `pwd`, `grep`, etc.

Test with: `git --version` and `python --version`

> **Why Git Bash?** This gives you the same terminal commands as your macOS and Linux classmates (and your professor!), making course examples work identically across all platforms. You'll avoid having to "translate" between PowerShell commands and Unix commands throughout the course.

---

## 3. GitHub Account & Student Benefits

GitHub is the platform we'll use for all code submissions and collaboration throughout this course.

### Create Your GitHub Account

1.  Navigate to [github.com](https://github.com) and click **Sign up**.
2.  Choose a **professional username** that you'd be comfortable using throughout your career. This will be visible to instructors, future employers, and collaborators.
3.  **Use your UC email address** for account verification and to qualify for student benefits.
4.  Complete the account setup process and verify your email address.

### Enable Two-Factor Authentication (Recommended)

For security, we strongly recommend enabling two-factor authentication:

1.  Go to your GitHub account **Settings** (click your profile photo > Settings).
2.  In the left sidebar, click **Password and authentication**.
3.  Under "Two-factor authentication," click **Enable two-factor authentication**.
4.  Follow the setup process using either an authenticator app or SMS.

### Get Free Developer Tools (GitHub Student Developer Pack)

As a UC student, you qualify for free access to premium developer tools:

1.  Visit the [GitHub Student Developer Pack](https://education.github.com/pack).
2.  Click **Get Student benefits**.
3.  Sign in with your GitHub account if prompted.
4.  **Verify your student status** using your UC email address.
5.  Once approved, you'll have free access to:
    * **GitHub Copilot** (normally $10/month) - AI code completion
    * **GitHub Pro** features - unlimited private repositories
    * Many other premium developer tools and services

### What's Next

You'll learn to create repositories, manage code, and collaborate using Git and GitHub workflows in **Lab 01: Git and GitHub Fundamentals**. The account setup you just completed is a prerequisite for that lab.

---

## 4. Python

Python is the first programming language we will master in this course.

### Windows

1.  Navigate to the [official Python downloads page](https://www.python.org/downloads/).
2.  Download **Python 3.13.x** (latest stable version) or **Python 3.10+** (minimum requirement for this course).
3.  Run the installer.
4.  **This is the most important step:** on the first screen of the installer, you **must** check the box at the bottom that says **"Add python.exe to PATH"**.
5.  Click "Install Now" and proceed through the rest of the installation.

### macOS

While macOS includes a version of Python, we will install our own to ensure we have the latest version and to not interfere with the system installation.

1.  Navigate to the [official Python downloads page](https://www.python.org/downloads/).
2.  Download **Python 3.13.x** (latest stable version) or **Python 3.10+** (minimum requirement for this course) for macOS.
3.  Run the `.pkg` installer and follow the on-screen instructions. It is a standard macOS installation process.

### Linux

Open your terminal and run the following command to ensure you have Python 3 and its package manager, pip.

`sudo apt update && sudo apt install python3 python3-pip`

### Verifying your installation

Open your terminal and type the following command. You should see a version number printed. Note that on macOS and Linux, you may need to use `python3`.

`python --version` or `python3 --version`

## 9. Installing course packages

This course requires a few external Python packages. You can install them all with a single command.

1.  Make sure you are in the root directory of your `is4010-course-template` project in your terminal.
2.  Run the following command:
    `pip install -r requirements.txt`

This will read the `requirements.txt` file and install the correct versions of all necessary libraries.

---

## 5. Rust

Rust is the second language we will explore for high-performance application development.

### Windows, macOS, and Linux

The installation process for Rust is the same on all platforms, thanks to a tool called `rustup`.

1.  Navigate to the [official Rust installation page](https://www.rust-lang.org/tools/install).
2.  The website will detect your operating system and provide a single line of code to copy.
3.  Open your terminal (or PowerShell on Windows) and paste the command. Hit Enter to run it.
4.  The installer will prompt you to choose an installation type. Press `1` and hit Enter to select the "Proceed with installation (default)" option.
5.  Once it is finished, you may need to close and reopen your terminal for the changes to take effect.

### Verifying your installation

Open a **new** terminal window and type the following command. You should see a version number printed.

`cargo --version`

---

## 6. Gemini CLI

The Gemini CLI is a powerful command-line interface that allows you to interact with Google's Gemini models directly from your terminal. It's built with Node.js and offers generous free tier access when you sign in with your Google account.

### Prerequisites

The Gemini CLI requires **Node.js version 20 or higher**. Check if you have Node.js installed by running:

`node --version`

If you don't have Node.js or have an older version, download and install it from [nodejs.org](https://nodejs.org/) (choose the LTS version).

### Installation

You have three installation options:

#### Option 1: Quick Install (Recommended for Testing)
```
npx @google/gemini-cli
```
This runs the CLI directly without installing it globally.

#### Option 2: Global NPM Install (Recommended for Course Use)
```
npm install -g @google/gemini-cli
```
This installs the `gemini` command globally on your system.

#### Option 3: Homebrew (macOS/Linux Only)
```
brew install gemini-cli
```

### Authentication (Google Account - Recommended)

For this course, we'll use **Google account authentication**, which gives you generous free access:
- **60 requests per minute**
- **1,000 requests per day**
- Access to **Gemini 2.5 Pro** with 1 million token context window

#### Setup Steps:
1.  Open your terminal
2.  Run the command: `gemini`
3.  The CLI will automatically open your web browser for Google authentication
4.  **Sign in with your personal Google account** (the same one you might use for Gmail, YouTube, etc.)
5.  Grant permission when prompted
6.  Return to your terminal - you should now be authenticated!

### Verifying your installation

Test that everything is working by running:

`gemini`

You should see the Gemini CLI interface. Try asking a simple question:

`What is 2+2?`

If you get a response, you're all set!

> **Troubleshooting Tips:** 
> - If you get "command not found," try closing and reopening your terminal
> - If Node.js version is too old, update from [nodejs.org](https://nodejs.org/)
> - For authentication issues, make sure you're signing in with a personal Google account (not a UC/institutional account)

---

## 7. Next Steps: GitHub Copilot Setup

Now that the tools are installed, the final step is to activate your AI co-pilot.

1.  If you haven't already completed the **GitHub Account & Student Benefits** section above, make sure you've signed up for the [GitHub Student Developer Pack](https://education.github.com/pack). This gives you free access to GitHub Copilot.
2.  Open VS Code.
3.  Click on the Extensions icon on the left-hand sidebar (it looks like four squares).
4.  Search for `GitHub Copilot` in the marketplace search bar.
5.  Click "Install" on the first official extension from GitHub.
6.  You will be prompted to sign in with your GitHub account to authorize the extension. Follow the on-screen instructions.
7.  Once complete, you should see the small Copilot icon in the bottom status bar of VS Code.

---

## 8. Recommended VS Code Extensions

To supercharge your development environment, we recommend installing the following extensions. You can install them by searching for the extension ID in the Extensions view (`Ctrl+Shift+X`) in VS Code.

### Python

* **Extension name:** Python
* **Publisher / ID:** Microsoft / `ms-python.python`
* **Description:** This is the essential, all-in-one extension that provides rich language support including IntelliSense (Pylance), linting, debugging, and more.

### Rust

* **Extension name:** rust-analyzer
* **Publisher / ID:** The Rust Programming Language / `rust-lang.rust-analyzer`
* **Description:** This is the official language server for Rust. It provides autocompletion, error checking, and "Go to Definition" functionality that makes writing Rust much easier.

### General Quality of Life

* **Extension name:** Prettier - Code formatter
* **Publisher / ID:** Prettier / `esbenp.prettier-vscode`
* **Description:** This is a very popular code formatter that will help keep other file types, like Markdown (`.md`) and JSON, clean and consistently formatted.

You are now fully set up for the course. Great work! 🚀
