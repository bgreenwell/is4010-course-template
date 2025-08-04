# IS4010 Setup Guide

Welcome to IS4010! This guide provides step-by-step instructions for setting up your computer with all the necessary tools for this course. Please follow these instructions carefully. If you run into any issues, please ask for help in our class teams channel.

---

## 1. Visual studio code (vs code)

This will be our primary code editor, or integrated development environment (ide), for the entire course. You can find step-by-step installation instructions for your operating system below [here](https://code.visualstudio.com/docs/setup/setup-overview). Here's the short version for each platform:

### Windows

1.  Navigate to the [vs code download page](https://code.visualstudio.com/download).
2.  Download the **user installer** for windows.
3.  Run the `.exe` file you downloaded.
4.  Accept the license agreement and click next through the installation steps. It is highly recommended that you leave the "add to path" option checked on the "select additional tasks" screen.

### macOS

1.  Navigate to the [vs code download page](https://code.visualstudio.com/download).
2.  Download the **mac universal** `.zip` file.
3.  Once downloaded, unzip the file.
4.  Drag the `visual studio code.app` file into your `applications` folder.
5.  Launch vs code. Open the command palette (`shift` + `command` + `p`) and type `shell command`. Select the option "shell command: install 'code' command in path" to make it available from your terminal.

### Linux

1.  Navigate to the [vs code download page](https://code.visualstudio.com/download).
2.  Download the `.deb` package (for ubuntu/debian-based distributions) or the `.rpm` package (for fedora/rhel-based distributions).
3.  Open your terminal, navigate to your downloads folder, and run the appropriate command:
    * For `.deb`: `sudo apt install ./<file_name>.deb`
    * For `.rpm`: `sudo rpm -i <file_name>.rpm`

### Verifying your installation

Open your terminal (or powershell on windows) and type the following command. You should see a version number printed.

`code --version`

---

## 2. Git

Git is the version control system we will use to track changes in our code and collaborate.

### Windows

1.  Navigate to the [git downloads page](https://git-scm.com/downloads).
2.  The download for "git for windows" should start automatically.
3.  Run the installer you downloaded.
4.  It is safe to accept the default options for all steps in the installation wizard. There are many steps, but you can simply click "next" through all of them.

### macOS

Git is often pre-installed. First, open your `terminal` app and type `git --version`.

* If you see a version number, you are all set!
* If it is not installed, your mac will pop up a window prompting you to install the "command line developer tools." Please click "install" and follow the steps. This will install git for you.

### Linux

Open your terminal and run the following command to install git using your system's package manager.

`sudo apt update && sudo apt install git`

### Verifying your installation

Open your terminal and type the following command. You should see a version number printed.

`git --version`

---

## 3. Python

Python is the first programming language we will master in this course.

### Windows

1.  Navigate to the [official python downloads page](https://www.python.org/downloads/).
2.  Download the latest stable version (e.g., python 3.12.x).
3.  Run the installer.
4.  **This is the most important step:** on the first screen of the installer, you **must** check the box at the bottom that says **"add python.exe to path"**.
5.  Click "install now" and proceed through the rest of the installation.

### macOS

While macOS includes a version of python, we will install our own to ensure we have the latest version and to not interfere with the system installation.

1.  Navigate to the [official python downloads page](https://www.python.org/downloads/).
2.  Download the latest stable version for macos.
3.  Run the `.pkg` installer and follow the on-screen instructions. It is a standard macos installation process.

### Linux

Open your terminal and run the following command to ensure you have python 3 and its package manager, pip.

`sudo apt update && sudo apt install python3 python3-pip`

### Verifying your installation

Open your terminal and type the following command. You should see a version number printed. Note that on macos and linux, you may need to use `python3`.

`python --version` or `python3 --version`

---

## 4. Rust

Rust is the second language we will explore for high-performance application development.

### Windows, macOS, and Linux

The installation process for rust is the same on all platforms, thanks to a tool called `rustup`.

1.  Navigate to the [official rust installation page](https://www.rust-lang.org/tools/install).
2.  The website will detect your operating system and provide a single line of code to copy.
3.  Open your terminal (or powershell on windows) and paste the command. Hit enter to run it.
4.  The installer will prompt you to choose an installation type. Press `1` and hit enter to select the "proceed with installation (default)" option.
5.  Once it is finished, you may need to close and reopen your terminal for the changes to take effect.

### Verifying your installation

Open a **new** terminal window and type the following command. You should see a version number printed.

`cargo --version`

---

## 5. Next steps: github copilot setup

Now that the tools are installed, the final step is to activate your ai co-pilot.

1.  If you haven't already, sign up for the [github student developer pack](https://education.github.com/pack). This will give you free access to github copilot.
2.  Open vs code.
3.  Click on the extensions icon on the left-hand sidebar (it looks like four squares).
4.  Search for `github copilot` in the marketplace search bar.
5.  Click "install" on the first official extension from github.
6.  You will be prompted to sign in with your github account to authorize the extension. Follow the on-screen instructions.
7.  Once complete, you should see the small copilot icon in the bottom status bar of vs code.

---

## 6. Recommended vs code extensions

To supercharge your development environment, we recommend installing the following extensions. You can install them by searching for the extension id in the extensions view (`ctrl+shift+x`) in vs code.

### Python

* **Extension name:** python
* **Publisher / id:** microsoft / `ms-python.python`
* **Description:** this is the essential, all-in-one extension that provides rich language support including intellisense (pylance), linting, debugging, and more.

### Rust

* **Extension name:** rust-analyzer
* **Publisher / id:** the rust programming language / `rust-lang.rust-analyzer`
* **Description:** this is the official language server for rust. it provides autocompletion, error checking, and "go to definition" functionality that makes writing rust much easier.

### General quality of life

* **Extension name:** prettier - code formatter
* **Publisher / id:** prettier / `esbenp.prettier-vscode`
* **Description:** this is a very popular code formatter that will help keep other file types, like markdown (`.md`) and json, clean and consistently formatted.

You are now fully set up for the course. Great work! 🚀