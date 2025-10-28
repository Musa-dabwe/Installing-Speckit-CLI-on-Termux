# Getting Started with Spec Kit on Your Android Device

## Putting "Spec Kit" on Your Android Phone: A Simple Guide

This guide will walk you through setting up a tool called "Spec Kit" on your Android device using an app called "Termux." We'll explain each step in simple terms and help you get past common issues.

---

### 1. First, Let's Install "Spec Kit"

Think of this as installing a new app on your phone, but for the command line.

#### 🐛 Problem: The computer can't find the new tool.

After installing, you might get a "command not found" error. This is like putting a new book on a bookshelf but not telling the librarian where you put it. The computer doesn't know where to look for the "Spec Kit" tool you just installed.

✅ **Solution: Tell the computer where to find it.**

We need to give the computer the correct location of the tool.

- In Termux, type the following and press Enter:
  `echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc`

- Then, to make the changes take effect, type this and press Enter:
  `source ~/.bashrc`

### 2. Installing the "Gemini" Helper

"Spec Kit" needs a helper, which is an AI assistant called "Gemini."

#### 🐛 Problem: The installation gets stuck.

When you try to install Gemini, the process might fail. This is because the installer is looking for something related to Android development that isn't usually needed in Termux.

✅ **Solution: We can tell the installer to skip that step.**

- First, make sure you have the necessary tools for building software. Type this and press Enter:
  `pkg install clang libtool automake make`

- Next, we'll create a special configuration file to tell the installer not to worry about the missing information. Type these two commands, pressing Enter after each one:
  `mkdir -p ~/.gyp`
  `echo "{ 'variables': { 'android_ndk_path': '' } }" > ~/.gyp/include.gypi`

- Now, you can install Gemini. Type this and press Enter:
  `npm install -g @google/gemini-cli`

✨ **How to check if it worked:**

- Type `gemini -v` and press Enter. You should see a version number.
- Type `specify check` and press Enter. You should see a message saying "Gemini CLI (available)."

### 3. Starting a New Project

Now, let's create a new workspace for your project.

#### 🐛 Problem: The computer doesn't know what to name the project.

If you just type `specify init`, you'll get an error. The computer needs a name for your new project folder.

✅ **Solution: Give your project a name.**

- For example, to create a project called "webview-app," you would type:
  `specify init webview-app`

#### 🐛 Problem: The computer doesn't know who you are.

"Spec Kit" uses a system called "Git" to keep track of changes. Git needs to know your name and email address.

✅ **Solution: Introduce yourself to Git.**

- Type the following commands, but replace the examples with your own name and email address:
  `git config --global user.email "youremail@example.com"`
  `git config --global user.name "Your Name"`

### 4. Giving Commands to "Spec Kit"

"Spec Kit" has special commands that start with a slash (`/`), like `/speckit.constitution`.

#### 🐛 Problem: The regular command line doesn't understand these special commands.

If you type a slash command directly into the Termux command line, you'll get an error. These commands are meant for the Gemini helper, not for Termux itself.

✅ **Solution: Talk to the Gemini helper directly.**

1.  **Go to your project folder.** If you named your project "webview-app," you would type:
    `cd webview-app`

2.  **Start the Gemini helper.** Type the following and press Enter:
    `gemini`

    (If this is your first time, you might need to do a one-time login. The program will give you instructions.)

3.  **Now you can use the special commands.** Once you see the `>` symbol, you're talking to Gemini. You can now type your slash command, like:
    `> /speckit.constitution`

And that's it! You've successfully set up "Spec Kit" and are ready to start using it.
