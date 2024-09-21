# _*Branching in Git*_

## _*Creating and Switching to a New Branch*_

- Create a local branch named ``greet`` and switch to it using the following Git command:

```bash
git branch greet
git checkout greet
```

Also can use a single command:

```bash
git checkout -b greet
```

Adding Changes to the greet Branch

- In the lib directory, create a new file named ``greeter.sh`` and add the provided and commit the changes:

```bash
#!/bin/bash

Greeter() {
    who="$1"
    echo "Hello, $who"
}
```

Adding Changes to the greeter.sh file

```bash
echo -e '#!/bin/bash\n\nGreeter() {\n\twho="$1"\n\techo "Hello, $who"\n}' > lib/greeter.sh
git add lib/greeter.sh
git commit -m "Added greeter.sh file"
```

- Next, update the lib/hello.sh file by adding the content below, staging and committing the changes:

```bash
#!/bin/bash

source lib/greeter.sh

name="$1"
if [ -z "$name" ]; then
    name="World"
fi

Greeter "$name"
```

Update changes:

```bash
echo -e '#!/bin/bash\n\nsource lib/greeter.sh\n\nname="$1"\nif [ -z "$name" ]; then\n\tname="World"\nfi\n\nGreeter "$name"' > lib/hello.sh
git add lib/hello.sh
git commit -m "Updated hello.sh to use Greeter"
```

## _*Updating the Makefile*_

```bash
echo "# Ensure it runs the updated lib/hello.sh file" >> Makefile
git add Makefile
git commit -m "Updated Makefile"
```

## _*Comparing Branches*_

- Switch back to the main branch using:

```bash
git checkout master
```

### _*Difference*_

- To compare and show the differences between branches in Git, you can use the ``git diff`` command with the ``--stat`` option:

```bash
(git diff <branch1> <branch2> --stat -- <file to compare>)
git diff master greet -- Makefile lib/hello.sh lib/greeter.sh

```

- This will show a summary of the changes, including the number of added, modified, and deleted lines of a specific file.

```bash
diff --git a/Makefile b/Makefile
index 5adf547..8268405 100644
--- a/Makefile
+++ b/Makefile
@@ -3,3 +3,4 @@ TARGET="lib/hello.sh"
 run:
        bash ${TARGET}
 
+# Ensure it runs the updated lib/hello.sh file
diff --git a/lib/greeter.sh b/lib/greeter.sh
new file mode 100644
index 0000000..28da219
--- /dev/null
+++ b/lib/greeter.sh
@@ -0,0 +1,6 @@
+#!/bin/bash
+
+Greeter() {
+       who=\"$1\"
+       echo \"Hello, $who\"
+}
diff --git a/lib/hello.sh b/lib/hello.sh
index 4d8865d..ca4823e 100644
--- a/lib/hello.sh
+++ b/lib/hello.sh
@@ -1,8 +1,10 @@
 #!/bin/bash
 
-# Default is World
-# Author: Jim Weirich <jimchy@gmail.com>
-name=${1:-"World"}
+source lib/greeter.sh
 
-echo "Hello, $name"
+name="$1"
+if [ -z "$name" ]; then
+       name="World"
+fi
 
+Greeter "$name"
```

## _*Create README.md*_

```bash
echo "This is the Hello World example from the git project." > README.md
git add README.md
git commit -m "Add README.md"
```

## _*Commit Tree Diagram*_

- To have a graphical representation of the commits, we run:

```bash
git log --graph master greet --oneline

(Alternatively)
git log --graph --oneline --all
```

Illustration:

```bash
skisenge@bocal-ThinkPad-T480:~/work/hello$ git log --graph --all --oneline
* fabcd2f (HEAD -> master) Add README.md
| * 4dccbcc (greet) Updated Makefile
| * aa37108 Updated hello.sh to use Greeter
| * 98f9cd7 Added greeter.sh
|/  
* 2e4f379 feat: add script into Makefile
* 608709d style: move hello.sh file to lib/
* a94661e chore: Add author infomation
| * c1ef1f9 (tag: oops) Chore: commit unwanted changes to be reverted
|/  
* 82b3dd1 (tag: v1) feat: update name in line 4 & 5
* 7890f3d (tag: v1-beta) chore: insert comment in line 3
* 941d157 feat: added bash content
skisenge@bocal-ThinkPad-T480:~/work/hello$ git log --graph master greet --oneline
* fabcd2f (HEAD -> master) Add README.md
| * 4dccbcc (greet) Updated Makefile
| * aa37108 Updated hello.sh to use Greeter
| * 98f9cd7 Added greeter.sh
|/  
* 2e4f379 feat: add script into Makefile
* 608709d style: move hello.sh file to lib/
* a94661e chore: Add author infomation
* 82b3dd1 (tag: v1) feat: update name in line 4 & 5
* 7890f3d (tag: v1-beta) chore: insert comment in line 3
* 941d157 feat: added bash content
skisenge@bocal-ThinkPad-T480:~/work/hello$ 

```
