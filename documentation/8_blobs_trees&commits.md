# _*Blobs, trees and commits*_

- _Blobs_ are the contents of the files that we make Git aware about.
- _Trees_ are the working structure of a branch.

## _*Exploring the .git/ Directory*_

- ``cd`` into the ``.git/`` directory in your project and let's examine its contents.
- The `.git` repo contains all the metadata for the your local repository.
- We will find several subdirectories and files that play a crucial role in managing our Git repository.
- Let's explore each of them:

     **branches/:**

    This directory is used by older versions of Git for storing branch information. It's generally empty in modern Git versions because branches are now managed within the refs/ directory.

    **COMMIT_EDITMSG:**

    This file contains the commit message of the most recent commit. When you run git commit, Git opens this file in your text editor for you to edit the commit message.

    **config:**

    This file stores configuration settings for the repository. These settings can include user information, remotes, and other repository-specific settings.

    **description:**

    This file is used by GitWeb to provide a description of the repository. It's generally not used by standard Git operations.

    **HEAD:**

    This file points to the current branch reference. It typically contains a reference like ref: refs/heads/main, indicating the current active branch.

    **hooks/:**

    This directory contains client- or server-side scripts that are triggered by Git events, such as pre-commit, post-commit, pre-push, etc. These hooks can be used to enforce policies or automate workflows.

    **index:**

    This file is also known as the staging area. It contains information about what will go into the next commit, including file changes that have been added but not yet committed.

    **info/:**

    This directory contains auxiliary information. For example, the exclude file in this directory can be used to specify patterns for files to be ignored in this specific repository.

    **logs/:**

    This directory contains logs of changes to the tips of branches. Each file in logs/refs/ keeps a record of all commits made to the respective branch. This can be useful for recovering lost commits.

    **objects/:**

    This directory stores all the content (files and directories) in the repository in an object database. Each object is identified by its SHA-1 hash. The objects can be of four types: blobs (file data), trees (directories), commits (commit data), and tags (tag data).

    **ORIG_HEAD:**

    This file is used to store the original HEAD reference before a potentially dangerous operation like a rebase or merge. It's used to help you recover if something goes wrong.

    **packed-refs:**

    This file stores references in a packed format for efficiency. It's used to speed up operations on repositories with a large number of references (branches or tags).

    **refs/:**

    This directory contains references to commit objects. It's subdivided into heads/ for local branches, remotes/ for remote-tracking branches, and tags/ for tags.

### _Latest Object Hash_

- To find the latest object hash within the .git/objects/ directory, use the following Git command:

```bash
git rev-list --objects --all | git cat-file --batch-check='%(objectname)' | sort -k 2 -n | tail -n 1 | awk '{print $1}'
```

- Then, you can use the following command to determine the type and content of this object:

```bash
git cat-file -t <latest-object-hash> && git cat-file -p <latest-object-hash>
```

### _*Dumping Directory Tree*_

- Use Git commands to dump the directory tree referenced by this commit:

```bash
git ls-tree -r <latest-object-hash> 
```

- To dump the directory tree referenced by a specific commit and the contents of the lib/ directory and hello.sh file, you can use the following Git commands:

```bash
# Dump the directory tree of the latest commit
git ls-tree HEAD

# Dump the contents of the lib/ directory
git ls-tree HEAD:lib

# Show the content of hello.sh
git show HEAD:lib/hello.sh
```

- The output will be the actual contents of the hello.sh file

## _Note_

To get the latest commit;

```bash
git rev-parse HEAD

# Get the latest commit hash
latest_hash=$(git rev-parse HEAD)

# Print the type of the object
git cat-file -t $latest_hash

# Print the content of the object
git cat-file -p $latest_hash
```

## Working directory well displayed

![blob, tree & commits displayed well](blob_tree_commit.png)
