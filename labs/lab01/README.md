# Lab 01: Git and github fundamentals

**Due Date: Sunday, September 1, 2024 at 11:59 PM**

## Objective

The goal of this lab is to complete the fundamental git workflow. You will create a github account and personal access token (pat), create a remote repository on github, connect it to a local repository on your computer, make a change, and push that change back to github.

## Background

In modern software development, we keep our code in a central, cloud-based location called a **remote repository** (on [GitHub](https://github.com/)). We make copies of this repository on our own computers, called **local repositories**. We work on the code locally, and once we are happy with our changes, we "push" them to the remote repository. This lab walks you through that entire cycle for the first time.

## Prerequisites

Before you begin, please ensure you have completed the following from our course setup guide:

- You have successfully installed [Git](https://git-scm.com/) on your computer.
- You have created a free [GitHub](https://github.com/) account.

## Instructions

Please follow these steps carefully.

### Step 1: Create a new repository on github

1.  In your web browser, navigate to [github.com](https://github.com) and log in.
2.  In the top-right corner, click the `+` icon and select **new repository**.
3.  For the "repository name", enter `is4010-[your-github-username]-labs`. For example, if your GitHub username is "johndoe", name it `is4010-johndoe-labs`.
4.  Provide a brief, one-sentence description. For example: "Lab assignments for IS4010."
5.  Select **private** to maintain academic integrity while allowing instructor access.
6.  **Important:** Do **not** check the box to "add a README file," "add .gitignore," or "choose a license." We want to start with a completely empty repository.
7.  Click the **create repository** button.

### Step 2: Add instructor as collaborator

Since your repository is private, you need to give your instructor access to review and grade your work.

1.  On your new repository's GitHub page, click the **Settings** tab.
2.  In the left sidebar, click **Collaborators**.
3.  Click the **Add people** button.
4.  In the search box, type `bgreenwell` and select the user.
5.  Click **Add bgreenwell to this repository**.
6.  Your instructor will automatically have access to your private repository for grading and feedback.

### Step 3: Create a personal access token (pat)

To push code from your computer to GitHub, you need a special password called a [personal access token (PAT)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens). Let's create one now.

1.  In the top-right corner of any GitHub page, click your profile photo, then click **[Settings](https://github.com/settings)**.
2.  In the left sidebar, scroll down and click **<> developer settings**.
3.  In the left sidebar, under "personal access tokens," click **tokens (classic)**.
4.  Click the **generate new token** button, and select **generate new token (classic)**.
5.  In the "note" field, give your token a descriptive name, like `is4010-laptop`.
6.  For "expiration," select **90 days**.
7.  Under "select scopes," check the box next to **`repo`**. This gives the token permission to access your repositories.
8.  Scroll down and click the **generate token** button.
9.  **CRITICAL STEP:** GitHub will now show you your token. This is the **only time** you will ever see it. Copy the token immediately and save it somewhere safe, like a [password manager](https://www.pcmag.com/picks/the-best-password-managers) or a private text file. If you lose it, you will have to delete it and create a new one.

### Step 4: Clone the repository to your computer

Now that you have a repository and a token, let's get a local copy of the project.

1.  On your new repository's GitHub page, click the green **[<> Code](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository)** button.
2.  Ensure you are on the **https** tab, and click the copy icon next to the url. It should look something like `https://github.com/your-username/is4010-labs.git`.
3.  Open your terminal (or [Git Bash](https://git-scm.com/downloads) on Windows) and navigate to a folder where you want to store your school work.
4.  Run the `git clone` command with the url you copied:
    ```
    git clone https://github.com/your-username/is4010-[your-username]-labs.git
    ```

### Step 5: Set up folder structure and create your first file

To keep your labs organized throughout the semester, we'll create a folder structure now.

1.  In your terminal, navigate into your new project folder:
    ```
    cd is4010-[your-username]-labs
    ```
2.  Create a folder for this lab:
    ```
    mkdir lab01
    cd lab01
    ```
3.  Open this folder in [VS Code](https://code.visualstudio.com/) and create a new file named `hello.py`.
4.  Add the following line of code to `hello.py` and save it:
    ```python
    print("hello from [your name]!")
    ```
5.  Navigate back to your repository root:
    ```
    cd ..
    ```
6.  Check the state of your repository by running `git status`. You should see `lab01/hello.py` listed as an "untracked file."
7.  Stage the file for your next commit:
    ```
    git add lab01/hello.py
    ```
8.  Commit the staged file to your local repository's history:
    ```
    git commit -m "Add hello.py for lab 01"
    ```

### Step 6: Push your commit to github

The final step is to "push" your local commit to the remote repository.

1.  In your terminal, run the following command:
    ```
    git push origin main
    ```
2.  You will be prompted for your username and password.
    * For "username," enter your github username.
    * For "password," paste the **personal access token (pat)** you copied in step 2.
3.  Once the push is complete, refresh your repository's page on github. You should now see your `hello.py` file!

## ⚠️ CRITICAL REQUIREMENTS ⚠️

**Before submitting, you MUST verify these two essential steps are completed:**

1. **✅ Repository is PRIVATE** - Public repositories violate academic integrity policy and will result in a grade of zero
2. **✅ Instructor added as collaborator** - Without `@bgreenwell` as a collaborator, your work cannot be graded

**Double-check these requirements now!** Go to your repository settings and confirm:
- Repository visibility shows "Private" 
- Collaborators section shows "bgreenwell" as a collaborator

**Failure to complete either step will result in automatic deduction of points.**

## 🚨 Troubleshooting Guide

Git and GitHub can be tricky the first time! Here are solutions to common issues:

### **Problem: "Permission denied" or authentication errors**
- **Solution**: Double-check your [Personal Access Token (PAT)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)
  - Make sure you copied the entire token correctly
  - Verify the token hasn't expired
  - Ensure you're using the token as your password, not your GitHub password

### **Problem: "Repository not found" when cloning**
- **Solution**: Check your repository URL
  - Make sure the repository name matches exactly: `is4010-[your-username]-labs`
  - Verify you're logged into the correct GitHub account
  - Confirm the repository was created successfully

### **Problem: Can't see files after cloning**
- **Solution**: Navigate to the correct directory
  - Use `pwd` to see your current location
  - Use `cd is4010-[your-username]-labs` to enter your repository
  - Use `ls` to list files and folders

### **Problem: "Nothing to commit" or files not showing**
- **Solution**: Check file location and git status
  - Make sure `hello.py` is inside the `lab01/` folder
  - Run `git status` to see what Git detects
  - Use `git add lab01/hello.py` to stage the specific file

### **Problem: Can't add instructor as collaborator**
- **Solution**: Repository settings access
  - Make sure you're on your repository's main page
  - Look for the "[Settings](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features)" tab (it might be in a dropdown if on mobile)
  - If you can't find Settings, try accessing GitHub on a computer instead of mobile

### **Still stuck? Use AI assistance! 🤖**

Don't hesitate to use AI tools to help debug issues. They're excellent for troubleshooting:

- **[ChatGPT](https://chat.openai.com/)** - Great for explaining Git concepts and debugging commands
- **[Claude](https://claude.ai/)** - Excellent for step-by-step troubleshooting and code explanations  
- **[Gemini](https://gemini.google.com/)** - Helpful for understanding error messages and Git workflow

**Pro tip**: When asking AI for help, copy and paste the exact error message you're seeing. The more specific your question, the better help you'll get!

### **Example AI prompts that work well:**
- "I'm getting this error when trying to push to GitHub: [paste error here]. How do I fix it?"
- "I'm new to [Git](https://git-scm.com/) and [GitHub](https://github.com/). Can you explain what '[git add](https://git-scm.com/docs/git-add)' does in simple terms?"
- "I created a private repository but I can't find how to add a collaborator. Can you walk me through the steps?"

## Submission

To complete this lab, submit your **repository URL** on Canvas.

**What to submit:** The main HTTPS URL to your repository (not a specific file or folder)

**Example submission URL:** `https://github.com/johndoe/is4010-johndoe-labs`

### Final checklist before submission

Before submitting on Canvas, verify your repository contains:

- [ ] Repository name follows format: `is4010-[your-username]-labs`
- [ ] Repository is set to **Private** (not public)
- [ ] `@bgreenwell` has been added as a collaborator
- [ ] `lab01/` folder exists in your repository
- [ ] `lab01/hello.py` file exists and contains your print statement
- [ ] Your changes have been successfully pushed to GitHub (visible on the website)
- [ ] Your repository URL works when pasted into a browser

**⚠️ Double-check the repository is PRIVATE and has the instructor as a collaborator - these are required for credit!**
