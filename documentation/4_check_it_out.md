# _*Checkout*_

## _*Restore First Snapshot*_

- Find the hash of the initial commit by running:

```bash
git rev-list --max-parents=0 HEAD
```

- Once you have the hash of the initial commit, detach the head to that commit and print the content:

```bash
git checkout <initial-commit-hash>
cat hello.sh
```

- To revert to initial version, run:

```bash
git checkout main/master
```

## _*Restore Second Recent Snapshot*_

- To revert the working tree to the second most recent snapshot and print the content of the hello.sh file, run:

```bash
git checkout HEAD~1
cat hello.sh
```

Also

```bash
git rev-list --skip=1 -n 1 HEAD
git checkout <second-recent-commit-hash>
cat hello.sh
```

- This will revert the working tree to the second most recent snapshot and display the content of the hello.sh file.

## _*Return to Latest Version*_

- To ensure that the working directory reflects the latest version of the hello.sh file present in the main branch, without referring to specific commit hashes, run:

```bash
git checkout main
cat hello.sh
```

- Note:
  - The ``HEAD~1`` syntax refers to the first parent commit of the current commit
  - ``HEAD~2`` refers to the second parent commit. By checking out these commits, you can revert to previous versions of your files.
  - After reverting to the initial commit, we cannot literally switch to the latest commit by the ``git checkout main`` command, since, the later commits were deleted. To reverse the process, you can track the latest commit hash by running ``git reflog`` and checkout revert to the hash, this will reset things back to normal.
  - ``git reflog:`` This command shows a log of changes to the tips of branches and other references in the repository. It includes actions like checkouts, commits, resets, and more.

  - ``git rev-list:`` This command lists commit objects in reverse chronological order.
  - ``--max-parents=0:`` This option filters the commits to only those with zero parents, which means it will list the root commits (initial commits) of the repository.
  - ``--skip=1:`` This option skips the first commit in the list. In this context, it skips the most recent commit.
  - ``-n 1:`` This option limits the output to only one commit.
  - ``HEAD:`` Refers to the latest commit in the current branch.
