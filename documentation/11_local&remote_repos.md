# _*Local and Remote Repositories*_

- To create a copy of the original repo called ``hello/`` in another directory called ``clone_hello/``, using the command:

```bash
cd ..
# git clone <path_to_original_repository> cloned_hello
git clone hello/ cloned_hello
```

## _*Showing Logs for the Cloned Repository*_

```bash
cd cloned_hello
git log --oneline
```

Output:

```bash
    skisenge@bocal-ThinkPad-T480:~/work$ ls
    cloned_hello  documentation  hello
    skisenge@bocal-ThinkPad-T480:~/work$ cd cloned_hello/
    skisenge@bocal-ThinkPad-T480:~/work/cloned_hello$ git log --oneline
    c23b48a (HEAD -> master, origin/master, origin/greet, origin/HEAD) Added greeter.sh
    3ccf340 Asking for users name update
    fabcd2f Add README.md
    2e4f379 feat: add script into Makefile
    608709d style: move hello.sh file to lib/
    a94661e chore: Add author infomation
    82b3dd1 (tag: v1) feat: update name in line 4 & 5
    7890f3d (tag: v1-beta) chore: insert comment in line 3
    941d157 feat: added bash content
    skisenge@bocal-ThinkPad-T480:~/work/cloned_hello$ 

```

## _*Displaying Remote Repository Information*_

```bash
# display name
git remote -v
# display more information
git remote show origin
```

Output:

```bash
    skisenge@bocal-ThinkPad-T480:~/work/cloned_hello$ git remote
    origin
    skisenge@bocal-ThinkPad-T480:~/work/cloned_hello$ git remote -v
    origin /home/skisenge/work/hello/ (fetch)
    origin /home/skisenge/work/hello/ (push)
    skisenge@bocal-ThinkPad-T480:~/work/cloned_hello$ git remote show origin
    * remote origin
    Fetch URL: /home/skisenge/work/hello/
    Push  URL: /home/skisenge/work/hello/
    HEAD branch: master
    Remote branches:
        greet  tracked
        master tracked
    Local branch configured for 'git pull':
        master merges with remote master
    Local ref configured for 'git push':
        master pushes to master (up to date)

```

## _*Listing Remote and Local Branches*_

```bash
# list local branches
git branch
# list remote branches
git branch -r
# lisst all branches
git branch -a
```

Output:

```bash
    skisenge@bocal-ThinkPad-T480:~/work/cloned_hello$ git branch
    * master
    skisenge@bocal-ThinkPad-T480:~/work/cloned_hello$ git branch -r
    origin/HEAD -> origin/master
    origin/greet
    origin/master
    skisenge@bocal-ThinkPad-T480:~/work/cloned_hello$ git branch -a
    * master
    remotes/origin/HEAD -> origin/master
    remotes/origin/greet
    remotes/origin/master
    skisenge@bocal-ThinkPad-T480:~/work/cloned_hello$ 

```

## _*Making Changes to the Original Repository*_

- Make changes to the original repository by updating the README.md file with the provided content. Commit the changes using.

```bash
echo 'This is the Hello World example from the git project.' > README.md
echo '(changed in the original)' >> README.md 
git add README.md
git commit -m "Updated README.md in original"
```

## _*Fetching Changes from Remote Repository*_

- Inside the cloned repository, fetch the changes from the remote repository and display the logs using:

```bash
cd ../cloned_hello
git fetch origin
git log --all --decorate --oneline
# Alternatively
git log --oneline --graph --all
```

Output:

```bash
    skisenge@bocal-ThinkPad-T480:~/work/cloned_hello$ git log --all --decorate --oneline
    bdb775a (origin/master, origin/HEAD) Updated README.md in original
    c23b48a (HEAD -> master, origin/greet) Added greeter.sh
    3ccf340 Asking for users name update
    fabcd2f Add README.md
    2e4f379 feat: add script into Makefile
    608709d style: move hello.sh file to lib/
    a94661e chore: Add author infomation
    c1ef1f9 (tag: oops) Chore: commit unwanted changes to be reverted
    82b3dd1 (tag: v1) feat: update name in line 4 & 5
    7890f3d (tag: v1-beta) chore: insert comment in line 3
    941d157 feat: added bash content

```

- This includes commits from the hello repository.

## _*Merging Changes from Remote Main Branch into Local Main Branch*_

- Merge the changes from the remote main branch into the local main branch using:

```bash
git merge origin/main
```

- After merging and we try to run the `git log --oneline` command again:

## _*Adding a Local Branch Tracking Remote Origin/Greet Branch*_

- Add a local branch named greet tracking the remote origin/greet branch using:

```bash
git checkout --track origin/greet
#git checkout -b greet --track origin/greet
```

- ``--track origin/greet`` : Sets the upstream branch for the greet branch to origin/greet, which means that the greet branch will track the remote origin/greet branch.
- ``git branch -vv`` command. This will show all the local branches along with their tracking configuration. You should see the greet branch listed with its upstream branch set to origin/greet.

## _*Adding a Remote and Pushing Branches to Remote*_

```bash
git remote add shared /path/to/shared/repo.git

git remote add shared https://learn.zone01kisumu.ke/git/skisenge/git.git
git push -u shared master
git push -u shared greet
# If you want to use 'origin' as name and is already set: see notes below under topic "## Using `Origin` as Name" 
git remote set-url origin https://learn.zone01kisumu.ke/git/skisenge/git.git
# Use git remote -v to check if well set the push the branches;
git push -u origin master
git push -u origin greet
```

- This command pushes the greet branch to the remote repository and sets the upstream branch for the local greet branch to the remote origin/greet branch.
- After running this command, any subsequent ``git push`` or ``git pull`` commands on the greet branch will automatically use the origin/greet branch as the upstream branch.

### _*Short Hand git command*_

- Well, the single command that will, fetch the latest version of the code from Git main branch, and then merge it with our new, local changes is:

```bash
git pull origin main
```

## **Understanding `git remote add`**

## Basic Syntax

The basic syntax for adding a remote in Git is:

```bash
git remote add <name> <url>
```

Here, `<name>` is a short name you choose to refer to the remote repository, and `<url>` is the URL of the remote repository.

## Why We Need a Name

1. **Multiple Remotes**: Git allows you to have multiple remote repositories connected to your local repository. The name helps distinguish between these remotes.

2. **Convenient Reference**: Instead of typing out the full URL every time, you can use the short name in Git commands.

3. **Clarity in Collaboration**: When working in teams, meaningful remote names can indicate the purpose or owner of each remote.

## Example

```bash
git remote add shared https://github.com/example/repo.git
```

Here, "shared" is the name we've chosen for this remote. We could have used any name: "origin", "upstream", "john_fork", etc.

## Common Remote Names

- `origin`: By convention, this usually refers to the main remote repository.
- `upstream`: Often used when you've forked a repository, to refer to the original repository.

## Using Remote Names

After adding a remote, you can use its name in other Git commands:

```bash
git fetch shared
git push shared master
git pull shared feature-branch
```

## What Happens Without a Name

If you try `git remote add <url>` without a name:

1. Git will throw an error because it expects a name.
2. You wouldn't have a convenient way to refer to this remote in future commands.

## Viewing Your Remotes

To see all remotes and their URLs:

```bash
git remote -v
```

This might show:

```bash
origin  https://github.com/your-username/your-repo.git (fetch)
origin  https://github.com/your-username/your-repo.git (push)
shared  https://github.com/example/repo.git (fetch)
shared  https://github.com/example/repo.git (push)
```

## Changing Remote Names

If you want to change a remote's name later:

```bash
git remote rename old-name new-name
```

## Removing a Remote

If you no longer need a remote:

```bash
git remote remove remote-name
```

## Conclusion

The name in `git remote add` is crucial for managing multiple remotes and simplifying Git commands. It's a label that represents the remote URL, making your Git workflow more efficient and understandable.

## Using `Origin` as Name

- 1. If you already have a remote named 'origin' (which is likely if you cloned this repository), you can't simply add another one with the same name.
- 2. If you want to replace the existing 'origin' with the new URL, you should use:

```bash
git remote set-url origin https://learn.zone01kisumu.ke/git/skisenge/git.git
```

- 3. If you want to add this as an additional remote while keeping the existing 'origin', you should use a different name, like:

```bash
git remote add shared https://learn.zone01kisumu.ke/git/skisenge/git.git
```

- 4. If you're certain you want to remove the existing 'origin' and add this new one, you can do:

```bash
git remote remove origin
git remote add origin https://learn.zone01kisumu.ke/git/skisenge/git.git
```

Before making any changes, it's a good idea to check your current remotes with git remote -v to understand your current setup.

Remember, changing 'origin' can affect your workflow, especially if you have existing branches tracking the old 'origin'. It's important to be careful and understand the implications of these changes.
