# _*Conflicts, Merging, and Rebasing*_

## _*Merging Main into Greet Branch*_

- Switch to the greet branch and attempt to merge the changes from the main branch using:

```bash
git checkout greet
git merge master
```

- switch back to master and make changes to hello.sh and commit.

```bash
git checkout master
echo -e '#!/bin/bash\n\necho "What\'s your name"\nread my_name\n\necho "Hello, $my_name"' > lib/hello.sh
git add lib/hello.sh
git commit -m "Asking for user's name update"
```

## _*Merging Main into Greet Branch (Conflicts)*_

```bash
git checkout greet
git merge master
```

- This will create a conflict that need be resolved.

```bash
# Manual resolution of conflicts in lib/hello.sh in the editor and commit.
git add lib/hello.sh
git commit -m "Resolved merge conflicts"
```

Commits after merge conflict:

```bash
    skisenge@bocal-ThinkPad-T480:~/work/hello$ git log --oneline
    a884f04 (HEAD -> greet) Resolved merge conflicts
    3ccf340 (master) Asking for users name update
    7e7e26b Merge branch 'master' into greet
    fabcd2f Add README.md
    4dccbcc Updated Makefile
    aa37108 Updated hello.sh to use Greeter
    98f9cd7 Added greeter.sh
    2e4f379 feat: add script into Makefile
    608709d style: move hello.sh file to lib/
    a94661e chore: Add author infomation
    82b3dd1 (tag: v1) feat: update name in line 4 & 5
    7890f3d (tag: v1-beta) chore: insert comment in line 3
    941d157 feat: added bash content
```

## _*Rebasing Greet Branch*_

- Rebase is a Git command that replays your local commits onto a new base commit, effectively "rewriting" your commit history.
- To rebase the greet branch on top of the latest changes in the main branch, use:

```bash
git checkout greet
git reset --hard aa37108
git rebase master
# conflict arises then we solve conflict in the editor
git add lib/hello.sh
git rebase --continue
# Output: Successfully rebased and updated refs/heads/greet.
```

- This will reapply the commits from the greet branch on top of the latest changes in the main branch.

### _*Merging Greet into Main*_

- Switch to the main branch and merge the changes from the greet branch using:

```bash
git checkout master
git merge greet
```

- This will create a new merge commit that combines the changes from both branches.

### _*Understanding Fast-Forwarding and Differences*_

- Fast-forwarding occurs when you merge one branch into another and there are no conflicts. In this case, Git simply moves the branch pointer to point to the latest commit on the target branch.

- Merging and rebasing are two different ways to integrate changes from one branch into another. Merging creates a new commit that combines the changes from both branches, while rebasing rewrites the commits from one branch onto another. When you rebase a branch, you are effectively rewriting history, whereas merging preserves the original commit history.

- Here's a simple way to remember it:

  - `Merging:` Creates a new commit that combines changes from both branches.
  - ``Rebasing:`` Rewrites commits from one branch onto another, preserving history.
  - ``Fast-forwarding:`` No conflicts or rewriting of history occurs when merging or rebasing.
