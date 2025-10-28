# Installing-Speckit-CLI-on-Termux

That's a great idea! Documenting the setup process, including the troubleshooting steps, creates an invaluable reference guide for Termux users.
Here is the complete process, including the errors and their solutions, documented in Markdown format.
# ⚙️ Spec Kit Setup on Termux: A Troubleshooting Guide

This document details the successful installation and configuration of the GitHub Spec Kit CLI and the Gemini CLI agent on the Termux environment (Android), including solutions for common Termux-specific errors.

---

## 1. Initial Spec Kit Installation and PATH Error

The process began with the installation of the `specify` tool via `uv` (a common Python tool installer).

### 🐛 Error Encountered: Command Not Found

After installation, running `specify check` failed:

```bash
$ specify check
No command specify found, did you mean:
 Command spectex in package mesa-demos from the x11-repo repository
 Command signify in package signify
 Command slugify in package slugify

✅ Solution: Fix the PATH
The executable was installed in a directory (~/.local/bin/) that was not in Termux's default execution path.
 * Add the directory to the PATH in your shell configuration file (e.g., ~/.bashrc):
   echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc

 * Apply the changes:
   source ~/.bashrc

2. Installing the Gemini CLI Agent
Spec Kit requires an AI agent (like Gemini CLI) to function. The Gemini CLI is installed via npm.
🐛 Error Encountered: android_ndk_path (GYP Compilation Failure)
Attempting to install the package failed because a dependency (node-pty) was trying to compile C++ code using a build system (node-gyp) that expected the Android NDK path to be defined, which is not standard in Termux.
gyp: Undefined variable android_ndk_path in binding.gyp while trying to load binding.gyp
gyp ERR! configure error
gyp ERR! stack Error: `gyp` failed with exit code: 1

✅ Solution: Bypass the NDK Check
This was solved by creating a global gyp configuration file to explicitly set the required variable to an empty string, satisfying the dependency check without needing the full NDK.
 * Install necessary build dependencies (if not already done):
   pkg install clang libtool automake make

 * Create the gyp configuration file to bypass the check:
   mkdir -p ~/.gyp
echo "{ 'variables': { 'android_ndk_path': '' } }" > ~/.gyp/include.gypi

 * Install the Gemini CLI globally:
   npm install -g @google/gemini-cli

✨ Verification
Installation confirmed by checking the version and running specify check:
$ gemini -v
0.10.0

$ specify check
# ... (output shows "Gemini CLI (available)")

3. Initializing a Project
The next step was to set up a new project directory using specify init.
🐛 Error Encountered: Missing Project Name/Context
Running the command without specifying a target failed:
$ specify init
Error: Must specify either a project name, use '.' for current directory, or use --here flag

✅ Solution: Specify a Project Name
A project name was provided, telling Spec Kit where to initialize the files.
$ specify init webview-app

🐛 Error Encountered: Git Author Identity
During initialization, Spec Kit attempts an initial Git commit, which failed because the user's global Git identity was not set:
Error: Author identity unknown
*** Please tell me who you are.

✅ Solution: Configure Git Identity
The error was fixed by setting the global user.name and user.email.
$git config --global user.email "foxxmusa@gmail.com"$ git config --global user.name "Fackson Musa"

4. Running Spec Kit Slash Commands
After initialization and navigating into the project, the first Spec Kit command was attempted.
🐛 Error Encountered: Slash Command Not Found
The user tried to run a slash command directly from the Termux shell:
$ cd webview-app
~/webview-app $ /speckit.constitution
bash: /speckit.constitution: No such file or directory

✅ Solution: Use Commands Inside the AI Agent
Spec Kit's slash commands (/speckit.*) are designed to be interpreted by the AI agent's CLI (in this case, gemini), not the standard bash shell.
 * Navigate to the project folder:
   cd webview-app

 * Start the Gemini CLI in interactive mode:
   gemini

   (Note: If this is the first time running gemini, you must run gemini --debug first, then /auth inside the session, copy the link, and complete the browser authentication.)
 * Once inside the gemini session (prompt is >), run the slash command:
