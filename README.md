# Installing Spec Kit CLI on Termux

This guide explains how to install Spec Kit's command-line interface, `specify-cli`, on Termux. The process involves setting up the Python environment, installing the `uv` package manager, and then using `uv` to install the tool from its GitHub repository.

---

### Step 1: Install Prerequisites (Python, Git, and uv)

Spec Kit requires Python 3.11+ and Git, and uses the `uv` tool for installation. You can install all necessary packages using Termux's package manager (`pkg`).

*   **Update Termux packages** to ensure you get the latest version of dependencies:
    ```bash
    pkg update && pkg upgrade
    ```

*   **Install Python, Git, and the `uv` package manager**:
    ```bash
    pkg install python git uv
    ```

---

### Step 2: Install Specify CLI (Spec Kit's Tool)

Once `uv` is installed, you can use the command provided in the Spec Kit documentation to install `specify-cli`.

*   **Run the persistent installation command**:
    ```bash
    uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
    ```

*   **(Optional) Verify the installation** by checking for required tools:
    ```bash
    specify check
    ```

---

### Step 3: Start a New Project

After installation, you can start a new project using the `specify init` command.

*   For example, to **initialize a new project** named `my-spec-project`:
    ```bash
    specify init my-spec-project
    ```

You can then navigate into the project and begin your spec-driven development workflow.

---

## Troubleshooting: `specify` Command Not Found

It looks like the `specify` command isn't in your Termux system's `$PATH` after running the installation command. This is a common issue when installing tools using `uv tool install` on Termux, as the executable is often placed in a directory that isn't automatically added to your environment path.

To fix this, you need to first find the installation directory and then add it to your Termux shell's path.

*   **Step 1: Find the Installation Directory**
    The `uv tool install` command typically places executables in `~/.local/bin/`.
    *   Check the contents of the `~/.local/bin/` directory:
        ```bash
        ls ~/.local/bin/
        ```
    You should see an executable file named `specify` (or possibly `specify-cli`) listed there.

*   **Step 2: Add the Directory to Your PATH**
    Since Termux often doesn't include `~/.local/bin` in the default path, you need to manually add it so your shell can find the `specify` command.
    *   Edit your shell startup file (e.g., `~/.bashrc` if you use Bash, or `~/.zshrc` if you use Zsh). Most Termux users use Bash by default.
        ```bash
        nano ~/.bashrc
        ```
    *   Add the following line to the end of the file:
        ```bash
        export PATH="$HOME/.local/bin:$PATH"
        ```
    *   Save the file (`Ctrl+O`, `Enter`) and Exit the editor (`Ctrl+X`).
    *   Reload your shell configuration to apply the change:
        ```bash
        source ~/.bashrc
        ```

*   **Step 3: Run the `specify check` Command**
    The `specify` command should now be recognized.
    ```bash
    specify check
    ```
    This should execute the Spec Kit check function without the "No command specify found" error.

---

### Example Output of `specify check`

```
Checking for installed tools...

Check Available Tools
├── ● Git version control (available)
├── ○ GitHub Copilot (IDE-based, no CLI check)
├── ● Claude Code (not found)
├── ● Gemini CLI (not found)
├── ○ Cursor (IDE-based, no CLI check)
├── ● Qwen Code (not found)
├── ● opencode (not found)
├── ● Codex CLI (not found)
├── ○ Windsurf (IDE-based, no CLI check)
├── ○ Kilo Code (IDE-based, no CLI check)
├── ● Auggie CLI (not found)
├── ● CodeBuddy (not found)
├── ○ Roo Code (IDE-based, no CLI check)
├── ● Amazon Q Developer CLI (not found)
├── ● Amp (not found)
├── ● Visual Studio Code (not found)
└── ● Visual Studio Code Insiders (not found)

Specify CLI is ready to use!
Tip: Install an AI assistant for the best experience
```

---

## Next Steps: Installing an AI Agent (Gemini CLI)

The message "Specify CLI is ready to use!" confirms that you successfully fixed the path issue, and the `specify` command is now working on your Termux setup.

The output shows that you have the core prerequisites (Git) but are missing the recommended AI assistants, which is what the next step is for. Since you've successfully installed and run the checks for Spec Kit, the next logical step is to install one of the supported AI agents so you can actually use the Spec Kit workflow commands like `/speckit.specify`.

The supported CLI agents are:
*   Claude Code
*   Gemini CLI
*   Auggie CLI
*   CodeBuddy

The Gemini CLI is a strong candidate for installation on Termux.

---

### Installing Gemini CLI on Termux

Now that the `specify` command is working, the next crucial step to use Spec Kit is installing one of the supported AI agents.

The Gemini CLI is an excellent choice for Termux. It's an open-source tool that brings the power of Gemini directly into your terminal, and Spec Kit is built to integrate with it.

Here is the step-by-step guide to install and set up Gemini CLI on Termux:

1.  **Install Node.js (Prerequisite for Gemini CLI)**
    The Gemini CLI is an npm package, so you need the Node.js package manager in Termux.
    ```bash
    pkg install nodejs
    ```

2.  **Install Gemini CLI**
    Use the Node Package Manager (npm) to install the Gemini CLI globally:
    ```bash
    npm install -g @google/gemini-cli
    ```
#### Common Issue: Troubleshooting `gyp` compilation error. (Bypass `android_ndk_path` Check)
```

gyp info spawn args   '/data/data/com.termux/files/usr/lib/node_modules/npm/node_modules/node-gyp/addon.gypi',
gyp info spawn args   '-I',
gyp info spawn args   '/data/data/com.termux/files/home/.cache/node-gyp/24.9.0/include/node/common.gypi',
gyp info spawn args   '-Dlibrary=shared_library',
gyp info spawn args   '-Dvisibility=default',
gyp info spawn args   '-Dnode_root_dir=/data/data/com.termux/files/home/.cache/node-gyp/24.9.0',
gyp info spawn args   '-Dnode_gyp_dir=/data/data/com.termux/files/usr/lib/node_modules/npm/node_modules/node-gyp',
gyp info spawn args   '-Dnode_lib_file=/data/data/com.termux/files/home/.cache/node-gyp/24.9.0/<(target_arch)/node.lib',
gyp info spawn args   '-Dmodule_root_dir=/data/data/com.termux/files/usr/lib/node_modules/@google/gemini-cli/node_modules/node-pty',
gyp info spawn args   '-Dnode_engine=v8',
gyp info spawn args   '--depth=.',
gyp info spawn args   '--no-parallel',
gyp info spawn args   '--generator-output',
gyp info spawn args   'build',
gyp info spawn args   '-Goutput_dir=.'
gyp info spawn args ]
gyp: Undefined variable android_ndk_path in binding.gyp while trying to load binding.gyp
gyp ERR! configure error
gyp ERR! stack Error: `gyp` failed with exit code: 1
gyp ERR! stack     at ChildProcess.<anonymous> (/data/data/com.termux/files/usr/lib/node_modules/npm/node_modules/node-gyp/lib/configure.js:317:18)
gyp ERR! stack     at ChildProcess.emit (node:events:508:28)
gyp ERR! stack     at ChildProcess._handle.onexit (node:internal/child_process:294:12)
gyp ERR! System Linux 4.19.157-perf+
gyp ERR! command "/data/data/com.termux/files/usr/bin/node" "/data/data/com.termux/files/usr/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /data/data/com.termux/files/usr/lib/node_modules/@google/gemini-cli/node_modules/node-pty
gyp ERR! node -v v24.9.0
gyp ERR! node-gyp -v v11.2.0
gyp ERR! not ok
```
This error occurs because the Gemini CLI (which depends on the `node-pty` package) requires native compilation during installation, and the build system is looking for a path to the Android Native Development Kit (NDK), which is not automatically set up in a standard Termux environment. The specific error is:
`gyp: Undefined variable android_ndk_path in binding.gyp`

    You need to create a global configuration file for `gyp` that sets the missing variable to an empty string (`''`).
    Run the following two commands:
    *   Create the required hidden directory:
        ```bash
        mkdir -p ~/.gyp
        ```
    *   Create the configuration file (`include.gypi`):
        ```bash
        echo "{ 'variables': { 'android_ndk_path': '' } }" > ~/.gyp/include.gypi
        ```
    This configuration tells `node-gyp` (which is run by `npm`) to use an empty path for the NDK variable, satisfying the dependency check.
3.  **Reinstall Gemini CLI**

Checking for installed tools...


Check Available Tools
├── ● Git version control (available)
├── ○ GitHub Copilot (IDE-based, no CLI check)
├── ● Claude Code (not found)
├── ● Gemini CLI (available)
├── ○ Cursor (IDE-based, no CLI check)
├── ● Qwen Code (not found)
├── ● opencode (not found)
├── ● Codex CLI (not found)
├── ○ Windsurf (IDE-based, no CLI check)
├── ○ Kilo Code (IDE-based, no CLI check)
├── ● Auggie CLI (not found)
├── ● CodeBuddy (not found)
├── ○ Roo Code (IDE-based, no CLI check)
├── ● Amazon Q Developer CLI (not found)
├── ● Amp (not found)
├── ● Visual Studio Code (not found)
└── ● Visual Studio Code Insiders (not found)


Specify CLI is ready to use!
```


Great!

You have successfully:
*   Fixed the `$PATH` issue for the `specify` command.
*   Bypassed the challenging `android_ndk_path` compilation error on Termux.
*   Installed and confirmed the Gemini CLI (version 0.10.0).
*   Run `specify check` and confirmed that Gemini CLI is now available for use with Spec Kit!

You now have a fully functional GitHub Spec Kit environment with one of the recommended AI agents on your Termux system.

---

### Final Steps: Authenticating and Using Spec Kit

The last step before you can start coding is to authenticate the Gemini CLI and then initialize a project with Spec Kit.

1.  **Authenticate Gemini CLI**
    The Gemini CLI is installed, but it needs your credentials to access the model. We'll use the debug mode method again, which works best on Termux:
    *   Start the Gemini CLI in debug mode:
        ```bash
        gemini --debug
        ```
    *   When the interactive prompt appears, type the following command to begin the OAuth flow:
        ```
        /auth
        ```
    *   The CLI will print a long login URL in your terminal. Copy the entire URL.
    *   Switch to your browser, paste the URL, and complete the Google login and authorization.
    *   Return to Termux. The `gemini` CLI should detect the successful login and confirm authentication.

2.  **Initialize a Spec Kit Project**
    Once authenticated, you are ready to create your first spec-driven development project using the `specify init` command.
    Navigate to the directory where you want to create your project (e.g., `~/projects/`) and run:
    ```bash
    specify init
    ```
    This command will:
    *   Create a `.speckit/` directory for configuration.
    *   Generate a `GEMINI.md` file where you can put project context and system prompts for the AI.
    *   Guide you through the initial setup for your project.
