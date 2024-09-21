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
