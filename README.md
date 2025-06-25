# Setting Up Git: A Comprehensive Guide

## Installing Git

To use Git, you'll need to install it on your local machine. Follow these steps based on your operating system:

### Windows

1. Download Git from the official Git website: [https://git-scm.com/downloads](https://git-scm.com/downloads)
2. Run the installer and follow the prompts.
3. After installation, you can use Git from the Command Prompt or PowerShell.
4. Git Bash, a Unix-like command line interface, is also installed and can be used as an alternative.

### macOS

1. Open the Terminal app.
2. Check if Git is already installed by running:

   ```bash
   git --version
   ```

3. If Git is not installed, you have two options:
   a. Install using Homebrew (if you have it installed):

      ```bash
      brew install git
      ```

   b. Download the installer from the official Git website: [https://git-scm.com/downloads](https://git-scm.com/downloads)

### Linux

Open a terminal and run one of the following commands:

- For Ubuntu-based systems:

  ```bash
  sudo apt-get install git
  ```

- For RHEL-based systems:

  ```bash
  sudo yum install git
  ```

## Configuring Git

After installing Git, configure it with your username and email address:

```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

Replace "Your Name" and "<your_email@example.com>" with your actual name and email address.

### Setting Default Branch Name

Many Git installations now default to 'main' instead of 'master'. Set your default branch name:

```bash
git config --global init.defaultBranch <default_branch>
git config --global init.defaultBranch master
```

### Verifying the Configuration

To verify your configuration:

```bash
git config --global --list
```

This will output a list of your configuration settings, including your username and email address.

## Advanced Setup (Optional)

### Setting Up SSH Keys

If you're using a Git hosting service like GitHub, you may want to set up SSH keys for secure, password-less authentication:

1. Generate an SSH key:

   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```

2. Add the SSH key to your SSH agent:

   ```bash
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_ed25519
   ```

3. Add the public key to your Git hosting service account.

### Global .gitignore

Create a global .gitignore file to specify files that Git should ignore across all repositories:

```bash
git config --global core.excludesfile ~/.gitignore_global
```

Then, edit `~/.gitignore_global` to add file patterns to ignore.

## Git GUI Clients

While Git is primarily used via command line, there are several GUI clients available for those who prefer graphical interfaces:

- GitHub Desktop
- Sourcetree
- GitKraken
- Tower

Choose one that suits your preferences and workflow.

## Conclusion

You're now set up to use Git on your local machine! Remember to regularly update Git to the latest version for security patches and new features.

---

# Git Commits to Commit

## Step 1: Create a Subdirectory and File

Within the work directory, establish a subdirectory named hello. Inside this directory, generate a file titled hello.sh and input the following content:

```bash
echo "Hello, World" >> hello.sh
```

## Initialize Git Repository and Check Status

- Initialize the Git repository in the hello directory using the command:

```bash
git init
```

- Check the status of the repository using the command:

```bash
git status
```

- The output should indicate that the directory is empty.

## Modify File and commit Changes

- Modify the hello.sh file to include comments and stage the changes:

```bash
#!/bin/bash

# Default is "World"
name=${1:-"World"}
echo "Hello, $name"
```

- Stage the changed file, but in patches, the first should include the line 3 comment while the other should noe include the rest of the lines 4 and 5. Use the command:

```bash
git add -p
```

## Commit Changes

- Commit 1: Commit the comment added in line 3.

```bash
git commit -m "add comment here"
```

- When we git status after this, we realize we have the same file in the staging area and as untracked, to mean we committed the first change but did not the later changes in the file. Commit 2: Commit changes made to lines 4 and 5.

```bash
git add hello.sh
git commit -m "Modified hello.sh script"
```

- The working tree should now be clean.

---

# _*History*_

## _*Show History*_

- To show the history of the working directory, run:

```bash
git log
```

### _*One-Line History*_

- To view a condensed one-line history showing only commit hashes and messages, run:

```bash
git log --oneline
```

### _*Customized Log Output*_

- To customize the log output, specify the number of entries or a time range. To display the last 2 entries, run:

```bash
git log -n 2
```

- To view the commits made within the last 5 minutes, run:

```bash
git log --since=5minutes
```

### _*Personalized Format*_

- To show logs in a personalized format, including the commit hash, date, message, branch information, and author name, run:

```bash
git log --pretty=format:"* %h %ad | %s (%d) [%an]" --date=short
```

- This will display the output in a format resembling:

```bash
* e4e3645 2023-06-10 | Added a comment (HEAD -> main) [John Doe]
```

- Note:
  - ``%h`` represents the commit hash
  - ``%as``  represents the date in the short format.
  - ``%ad`` represents the date in the long format.
  - ``%s`` represents the commit message
  - ``%d``  represents the abbreviated commit ref name (e.g. main)
  - ``%cr`` represents the commit message duration
  - ``%an``  represents the author name.

## Attached Display

![image](history.png)

---