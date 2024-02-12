# Setup Your Environment

While our focus will be on building Git functionality from the ground up, we will utilize commands like `git log --oneline --graph` to inspect and understand the modifications within our Git repository.

This approach will help us visualize the commits and the branching structure.

## Prerequisites

- Basic familiarity with terminal commands.
- Access to a command-line interface:
  - **Windows**: Git Bash (recommended) or Command Prompt.
  - **Mac/Linux**: Terminal.

## Step 1: Install Git

Skip this if you have git installed.

To verify if git is installed run following in the terminal:

```
git --version
```

### Windows

1. Download Git from [git-scm.com](https://git-scm.com/download/win).
2. Run the installer and follow the prompts, choosing the default options.
3. Open Git Bash from the Start menu after installation.

### Mac

1. If you don't have Homebrew installed, visit [brew.sh](https://brew.sh) to set it up.
2. Install Git using Homebrew:
   ```
   brew install git
   ```

## Linux

- Open your terminal.
- For Debian/Ubuntu-based systems, update your package list and install Git:

  ```
  sudo apt-get update
  sudo apt-get install git
  ```