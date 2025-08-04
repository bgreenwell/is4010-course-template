# Lab 01: Git and github fundamentals

## Objective

The goal of this lab is to complete the fundamental git workflow. You will create a github account and personal access token (pat), create a remote repository on github, connect it to a local repository on your computer, make a change, and push that change back to github.

## Background

In modern software development, we keep our code in a central, cloud-based location called a **remote repository** (on github). We make copies of this repository on our own computers, called **local repositories**. We work on the code locally, and once we are happy with our changes, we "push" them to the remote repository. This lab walks you through that entire cycle for the first time.

## Prerequisites

Before you begin, please ensure you have completed the following from our course setup guide:

- You have successfully installed git on your computer.
- You have created a free github account.

## Instructions

Please follow these steps carefully.

### Step 1: Create a new repository on github

1.  In your web browser, navigate to [github.com](https://github.com) and log in.
2.  In the top-right corner, click the `+` icon and select **new repository**.
3.  For the "repository name", enter `is4010-labs`.
4.  Provide a brief, one-sentence description. For example: "Lab assignments for IS4010."
5.  Select **public** so your work can be reviewed.
6.  **Important:** Do **not** check the box to "add a README file," "add .gitignore," or "choose a license." We want to start with a completely empty repository.
7.  Click the **create repository** button.

### Step 2: Create a personal access token (pat)

To push code from your computer to github, you need a special password called a personal access token. Let's create one now.

1.  In the top-right corner of any github page, click your profile photo, then click **settings**.
2.  In the left sidebar, scroll down and click **<> developer settings**.
3.  In the left sidebar, under "personal access tokens," click **tokens (classic)**.
4.  Click the **generate new token** button, and select **generate new token (classic)**.
5.  In the "note" field, give your token a descriptive name, like `is4010-laptop`.
6.  For "expiration," select **90 days**.
7.  Under "select scopes," check the box next to **`repo`**. This gives the token permission to access your repositories.
8.  Scroll down and click the **generate token** button.
9.  **CRITICAL STEP:** Github will now show you your token. This is the **only time** you will ever see it. Copy the token immediately and save it somewhere safe, like a password manager or a private text file. If you lose it, you will have to delete it and create a new one.

### Step 3: Clone the repository to your computer

Now that you have a repository and a token, let's get a local copy of the project.

1.  On your new repository's github page, click the green **<> code** button.
2.  Ensure you are on the **https** tab, and click the copy icon next to the url. It should look something like `https://github.com/your-username/is4010-labs.git`.
3.  Open your terminal (or git bash on windows) and navigate to a folder where you want to store your school work.
4.  Run the `git clone` command with the url you copied:
    ```
    git clone [https://github.com/your-username/is4010-labs.git](https://github.com/your-username/is4010-labs.git)
    ```

### Step 4: Create and commit your first file

1.  In your terminal, navigate into your new project folder:
    ```
    cd is4010-labs
    ```
2.  Create a new file named `hello.py` by opening the folder in vs code.
3.  Add the following line of code to `hello.py` and save it:
    ```python
    print("hello from [your name]!")
    ```
4.  Now, back in your terminal, check the state of your repository by running `git status`. You should see `hello.py` listed as an "untracked file."
5.  Stage the file for your next commit:
    ```
    git add hello.py
    ```
6.  Commit the staged file to your local repository's history:
    ```
    git commit -m "Add hello.py for lab 01"
    ```

### Step 5: Push your commit to github

The final step is to "push" your local commit to the remote repository.

1.  In your terminal, run the following command:
    ```
    git push origin main
    ```
2.  You will be prompted for your username and password.
    * For "username," enter your github username.
    * For "password," paste the **personal access token (pat)** you copied in step 2.
3.  Once the push is complete, refresh your repository's page on github. You should now see your `hello.py` file!

## Submission

To complete this lab, submit the **https url** to your `is4010-labs` github repository on canvas.
