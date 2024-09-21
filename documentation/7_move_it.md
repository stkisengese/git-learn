# _*Moving Files and Creating a Makefile*_

## _*Moving the hello.sh File*_

- Use the following Git commands to move the hello.sh file into a new directory named lib:

```bash
mkdir lib
git mv hello.sh lib/
```

- Commit the move:

```bash
git add .
git commit -m "Moved hello.sh to lib directory"
```

- Create a new file named Makefile:

```bash
touch Makefile
```

in the root directory of the repository with the following content:

```bash
echo -e "TARGET=\"lib/hello.sh\"\n\nrun:\n\tbash \${TARGET}" > Makefile
git add Makefile
git commit -m "Added Makefile"
```

- Commit the new file.
