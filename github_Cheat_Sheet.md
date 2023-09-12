# Git Cheat Sheet

## Hello World of Git

[Git Explained infrastructure in under 8 min](https://towardsdatascience.com/git-help-all-2d0bb0c31483)

### Check the Version

To check the version of Git installed on your system, use the following command:

```bash
git --version
```

### Create an Empty Git Repository

To create an empty Git repository in the current directory, use the `git init` command:

```bash
git init
```

### Show Modified Files in Working Directory

To display the status of modified files in your working directory, use the `git status` command:

```bash
git status
```

To display changes in a more compact way, you can use the `-s` option:

```bash
git status -s
```

The output will show the status of each file in the working directory. For example, untracked files will have a `??` next to them, newly added files will have an `A`, modified files will have an `M`, and so on. The left-hand column indicates the status of the staging area, and the right-hand column indicates the status of the working tree.

### Add Files to the Staging Area

To add specific files to the staging area (prepare them for the next commit), use the `git add` command followed by the file or directory names:

```bash
git add <file/directory name 1> <file/directory name 2> <...>
```

To stage all modified and new files in the working directory, you can use the following command:

```bash
git add .
```

### Commit Changes

To create a new commit with the changes staged in the previous step, use the `git commit` command followed by the commit message using the `-m` option:

```bash
git commit -m "Your commit message here"
```

If you omit the `-m` parameter, your default editor will open, allowing you to enter a more detailed commit message.

### Adding a Remote

To add a remote repository, use the `git remote add` command followed by the remote name and the repository URL:

```bash
git remote add <REMOTENAME> <repository URL>
```

For example:

```bash
git remote add origin https://github.com/username/repository.git
```

### Clone a Repository

To copy an existing Git repository from a server to your local machine, use the `git clone` command followed by the repository URL:

```bash
git clone <repository URL>
```

You can also specify a different name for the local directory using:

```bash
git clone <repository URL> <directory name>
```

### Share Code

To share your code with a remote repository, follow these steps:

1. Create a bare repository on the remote server:

   ```bash
   git init --bare /path/to/repo.git
   ```

2. On the local machine, add the remote repository:

   ```bash
   git remote add <REMOTENAME> <repository URL>
   ```

3. Push your code to the remote repository:

   ```bash
   git push --set-upstream <REMOTENAME> master
   ```

### Set Your User Name and Email

To set your user name and email, use the `git config` command with the `--global` flag for global configuration or without it for repository-specific configuration:

```bash
# Global configuration
git config --global user.name "Your Name"
git config --global user.email mail@example.com

# Repository-specific configuration
cd /path/to/my/repo
git config user.name "Your Login At Work"
git config user.email mail_at_work@example.com
```

To remove the global configuration:

```bash
git config --global --remove-section user.name
git config --global --remove-section user.email
```

To force Git to look for your identity only within a repository's settings, not in the global config:

```bash
git config --global user.useConfigOnly true
```

### Learning About a Command

To learn more about a specific Git command, you can use either of the following options:

```bash
git diff --help # Displays help for the 'diff' command
git help diff   # Displays help for the 'diff' command
```

These commands will provide you with detailed information about the specified command and its options.

Now you have the basics of Git to get started with version control and collaboration on your projects. Happy coding!

## Browsing Git Logs

#### Listing Git Logs

```shell
git log # It will display all your commits with the author and hash in reverse chronological
order. This will be shown over multiple lines per commit. Use the q key to exit the log.

git log -2 # Limit the logs to last 2 logs

git log --decorate --oneline --graph # To see the log in a prettier graph-like structure in one line

git config --global alias.lol "log --decorate --oneline --graph" # Since it's a pretty big command, you can assign an alias

git lol # history of current branch

git lol HEAD <REMOTENAME>/feature orign/master # combined history of active branch (HEAD), <REMOTENAME>/feature and <REMOTENAME>/master branches

git lol --all # combined history of everything in your repo
```

#### Log search

```bash
git log -S "#define SAMPLES" # Searches for addition or removal of specific string

git log -G "#define SAMPLES" # Searches for changes in lines containing a specific string matching provided REGEXP.

git log -- **/*.py # git log -- <file-path-pattern>

git log -- "New Text Document.txt" #All logs in which New Text Document.txt was modified

```

#### List all contributions

```bash
git shortlog # summarizes git log and groups by author

git shortlog -s (--summary)   # To simply see the number of commits and suppress the commit description

git shortlog -n (--numbered) # sort by number of commits

git shortlog -e (--email)   # To add email of committer
```

#### Searching commit string in git log

```bash
git log [options] --grep "search_string" # Searching git log using some string in log

git log --grep="add file" --invert-grep # Will show all commits that do not contain add file
```

> Both `--grep` and `-S` are options used with the `git log` command to filter the commit history based on specific criteria. However, they have different purposes:
>
> 1. `--grep`:
>
>    - The `--grep` option is used to search for commits whose commit message matches a specified pattern or regular expression which is **case sensitive**
>
>      ```bash
>      git log --grep="bug"
>      ```
>
> 2. `-S` (or `--pickaxe-regex`):
>
>    - The `-S` option is used to search for commits that introduced changes that add or remove lines that match a specified string.
>
>      ```bash
>      git log -S "example"
>      ```
>
> 3. `-G` (or `--pickaxe-regex`):
>
>    - The `-G` option is used to search for commits that introduced changes that add or remove lines that match a specified regular expression, just like the `-S` option.
>
>      ```bash
>      git log -G "(?i)example|sample"
>      ```

#### Log for a range of lines within a file

```bash
git log -L 1,20:index.html #display the commit history for a specific range of lines within a file
```

#### Filter logs

```bash
# Use --author=<author> to show commits by a specific author
git log --author="John Doe"

# Use --since or --until to filter commits within a specific date range
git log --since="2023-01-01" --until="2023-07-31"

# Use -- <file> to filter commits that modified a specific file
git log -- README.md

# Use <commit1>..<commit2> to view the commit range between two specific commits (inclusive)
git log abc123..def456

# Filter logs to show commits after a specific date (e.g., 3 days ago)
git log --after '3 days ago'

# An alias to --before is --until.
# An alias to --after is --since.
```

#### Log with changes inline

```bash
git log --patch #display the commit history along with the actual changes made in each commit
```

#### Log showing committed files

```bash
git log --stat #displays the commit history along with statistics about the changes made in each commit
```

#### Show the contents of a single commit

```bash
git show 48c83b3690dfc7b0e622fd220f8f37c26a77c934 
```

#### Git Log Between Two Branches

```bash
git log master..foo
```

#### One line showing committer name and time since commit

```bash
git config --global alias.log-all-name "log --oneline --decorate --source --pretty=format:'%Cblue %h %Cgreen %ar %Cblue %an %C(yellow)%d %Creset %s' --all --graph"

git log-all-name
```

## Working with Remotes  

[Git remote repository tutorial and with set-url <REMOTENAME> upstream example](https://www.youtube.com/watch?v=4AbJjvMHTZk)

[Git Remotes - Git and GitHub for Poets ](https://www.youtube.com/watch?v=lR_hYwCAaH4)

#### List Existing Remotes  

```bash
git remote
git remote --verbose
git remote -v
```

#### Deleting a Remote [Branch]  

```bash
git remote remove <REMOTENAME>
git push [remote-name] --delete [branch-name]
git push [remote-name] :[branch-name]
```

#### Changing Git Remote URL  

```bash
git remote set-url <REMOTENAME> https://github.com/username/repo2.git
```

#### Removing Local Copies of Deleted Remote Branches  

```bash
git fetch [remote-name] --prune

git fetch --all --prune
```

#### Updating from Upstream Repository  

```bash
git fetch remote-name
git merge remote-name/branch-name
git pull
git pull --rebase remote-name branch-name
```

#### ls-remote  

```bash
git ls-remote

git ls-remote --ref

```

#### Adding a New Remote Repository  

```bash
git remote add upstream git-repository-url
```

## Staging 

```bash
git add .
git add -A
git reset <filePath>
# Unstage a file that contains changes
git rm filename
```

#### Add changes by hunk  

```bash
git add -p (short for --patch)
```

| option | Meaning |
| ---- | ---- |
|y|stage this hunk for the next commit|
| n | do not stage this hunk for the next commit |
| q | quit; do not stage this hunk or any of the remaining hunks |
| a | d                                                          |
| d      | g                                                          |
| g      | /                                                          |
| /      | j                                                          |
|        | J                                                          |
|        |                                                            |

## Ignoring Files and Folders  

[glob pattern - Wikipedia](https://en.wikipedia.org/wiki/Glob_(programming))

```bash
# Lines starting with `#` are comments.
# Ignore files called 'file.ext'
file.ext
# Comments can't be on the same line as rules!
# The following line ignores files called 'file.ext # not a comment'
file.ext # not a comment
# Ignoring files with full path.
# This matches files in the root directory and subdirectories too.
# i.e. otherfile.ext will be ignored anywhere on the tree.
dir/otherdir/file.ext
otherfile.ext
# Ignoring directories
# Both the directory itself and its contents will be ignored.
bin/
gen/
# Glob pattern can also be used here to ignore paths with certain characters.
# For example, the below rule will match both build/ and Build/
[bB]uild/
# Without the trailing slash, the rule will match a file and/or
# a directory, so the following would ignore both a file named `gen`
# and a directory named `gen`, as well as any contents of that directory
bin
gen
# Ignoring files by extension
# All files with these extensions will be ignored in
# this directory and all its sub-directories.
*.apk
*.class
# It's possible to combine both forms to ignore files with certain
# extensions in certain directories. The following rules would be
# redundant with generic rules defined above.
java/*.apk
gen/*.class
# To ignore files only at the top level directory, but not in its
# subdirectories, prefix the rule with a `/`
/*.apk
/*.class
# To ignore any directories named DirectoryA
# in any depth use ** before DirectoryA
# Do not forget the last /,
# Otherwise it will ignore all files named DirectoryA, rather than directories
**/DirectoryA/
# This would ignore
# DirectoryA/
# DirectoryB/DirectoryA/
# DirectoryC/DirectoryB/DirectoryA/
# It would not ignore a file named DirectoryA, at any level
# To ignore any directory named DirectoryB within a
# directory named DirectoryA with any number of
# directories in between, use ** between the directories
DirectoryA/**/DirectoryB/
# This would ignore
# DirectoryA/DirectoryB/
# DirectoryA/DirectoryQ/DirectoryB/
# DirectoryA/DirectoryQ/DirectoryW/DirectoryB/
# To ignore a set of files, wildcards can be used, as can be seen above.
# A sole '*' will ignore everything in your folder, including your .gitignore file.
# To exclude specific files when using wildcards, negate them.
# So they are excluded from the ignore list:
!.gitignore
# Use the backslash as escape character to ignore files with a hash (#)
# (supported since 1.6.2.1)
\#*#

#If you ignore files by using a pattern but have exceptions, prefix an exclamation mark(!) to the exception. For example:
*.txt
!important.txt
```


> In software projects, 	**.gitignore** typically contains a listing of files and/or directories that are generated during the build process or at runtime. Entries in the **.gitignore** file may include names or paths pointing to:
>
> 1. temporary resources e.g. caches, log files, compiled code, etc.
> 2. local configuration files that should not be shared with other developers
> 3. files containing secret information, such as login passwords, keys and credentials
>
>
> When a file or directory is ignored, it will not be:
>
> 1. tracked by Git
> 2. reported by commands such as git status or git diff
> 3. staged with commands such as git add -A

#### Basics

```bash
git clean -Xnd # list all ignore files and folders

git clean -Xfd # clean all ignored files and folders permanently

git check-ignore example.o Readme.md example.o # Check if a file is ignored

git check-ignore * # list all ignore files

git status --ignored # This command displays the status of all files, including ignored ones. It will show a list of both tracked and untracked files, as well as ignored files.

git config --global core.excludesfile <Path_To_Global_gitignore_file> 
# Git ignore certain files across all repositories 
# local gitignore is prioritized on global .gitignore
# Its not a good practice to have global gitignore as it repository is cloned on multiple machines, then the global .gigignore must be loaded on all machines
```

#### Ignore files that have already been committed to a Git repository  

```bash
git rm --cached <file> #remove it from the index (stag). The --cached option will make sure that the file is not physically deleted.

```

## Section 6: Git Diff: Understanding and Utilizing Differences in Git

`git diff` is a powerful command in Git that allows you to view the differences between various versions of your code. It is essential for understanding changes made to your codebase and can be utilized in different scenarios. Here's a comprehensive guide on how to use `git diff` effectively:

### 1. Basic Usage:

#### a. Unstaged Changes:

To see the changes you've made but not yet staged for the next commit, simply use:

```bash
git diff
```

This command shows the unstaged changes since your last commit.

#### b. Staged Changes:

To see the changes you've staged that will go into your next commit, use:

```bash
git diff --staged
```

or its equivalent:

```bash
git diff --cached
```

### 2. Comparing Commits:

#### a. Between Two Commits:

You can view the changes between two specific commits using their hash identifiers:

```bash
git diff <hash_commit_old>..<hash_commit_new>
```

#### b. Recent Commits:

If you want to see the changes made in the last 3 commits, you can use the `@~3..@` syntax:

```bash
git diff @~3..@
```

### 3. Comparing Branches:

#### a. Between Two Branches:

To view the difference between two branches, use the following command:

```bash
git diff <branch1>..<branch2> or git diff <branch1>...<branch2>
#Show all changes on new since it branched from original

git diff original new
#Show the changes between the tip of new and the tip of original
```

### 4. Comparing Files or Directories:

#### a. Between Specific Files:

To see the changes between the previous commit of a specific file and the locally-modified version that has not yet been staged, use:

```bash
git diff myfile.txt

git diff myfolder
```

#### b. Between Two Commits and a Specific File:

If you want to compare a specific file between two separate commits, use:

```bash
git diff <commitId1>..<commitId2> myfile.txt
```

#### c. Between Two Commits and a Specific Directory:

To view files that changed in a specific folder after a certain commit, use:

```bash
git diff --name-only <commitId> <folder_path>
```

### 6. Other Useful Options:

#### a. Show Summary of Changes:

To view a summary of changes in the format of added and deleted lines, use:

```bash
git diff --stat <branch/commitId>
```

#### b. Show Files Changed After a Certain Commit:

To see a list of files that changed after a certain commit, use:

```bash
git diff --name-only <commitId>
```

#### c. Show Files Different Than a Branch:

To view files that are different than a specific branch, use:

```bash
git diff --name-only <branchName>
```

#### d. Word-Level Differences:

You can display word-level differences within lines instead of showing entire changed lines using `--word-diff`:

```bash
git diff --word-diff
```

####  d. Showing all Staged and Unstaged Changes:

``````bash
git diff HEAD
#To show all staged and unstaged changes

git status -vv
#To Show which changes are staged for commit and which are not.
``````

#### Difference Between Previous and Current Commit 

```bash
git diff HEAD^ HEAD #This will show the changes between the previous commit and the current commit
```

### 7. Example Usage:

```bash

git diff 27fa75e myfile.txt  # Shows the difference between a version of a file in a specific commit and the local HEAD version of the file

git diff branch1..branch2  # Compares the difference between two branches
```

Remember, `git diff` is a versatile command that can help you understand the history of your code and make informed decisions when collaborating with others. 

## Undoing 

#### Resetting staged File

```bash
git reset 

git checkout -- file.txt

git checkout <hash> -- file.txt
```

#### Undoing Commit 

```bash
git reset Head~n #Just Unstaged and uncommited the last n commits

git reset <hash> #Just Unstaged and uncommited the commit but do not delete content in repository  

git reset --hard <hash> #Also delete content in repository  
```

## Section 14: Branching

### Creating and Checking Out New Branches

#### Creating a new branch:

To create a new branch in Git, you can use the `git branch` command followed by the desired branch name. The branch name should not contain spaces and must adhere to other Git specifications.

```bash
git branch <name>
```

#### Switching to an existing branch:

To switch to an existing branch, you can use the `git checkout` command followed by the branch name.

```bash
git checkout <name>
```

#### Creating and switching to a new branch:

You can create a new branch and immediately switch to it using the `-b` option with the `git checkout` command.

```bash
git checkout -b <name>
```

#### Creating a branch from a specific commit:

To create a new branch starting from a specific commit (not the current branch's last commit, also known as HEAD), you can provide the `<start-point>` argument.

```bash
git branch <name> [<start-point>]
git checkout -b <name> [<start-point>]
```

### Listing Branches

#### List local branches:

```bash
git branch
```

#### List local branches with extra information:

```bash
git branch -v
```

#### List all branches (remote and local):

```bash
git branch -a
```

#### List all branches with extra information:

```bash
git branch -av
```

#### List only remote branches:

```bash
git branch -r
```

#### List remote branches with their latest commit:

```bash
git branch -rv
```

#### List merged branches:

```bash
git branch --merged
```

#### List unmerged branches:

```bash
git branch --no-merged
```

#### List branches containing a specific commit:

```bash
git branch --contains <commit>
```

### Deleting Branches

#### Delete a remote branch:

For Git version 1.5.0 and newer:

```bash
git push origin --delete <branchName>
```

#### Delete a remote-tracking branch:

```bash
git branch --delete --remotes <remote>/<branch>
git branch -dr <remote>/<branch> # Shorter
```

#### Delete a local branch:

```bash
git branch -d <branchName>
# Deletes the branch named "dev" if its changes are merged with another branch and will not be lost, else shows a failure message
```

#### Force delete a local branch (even with unmerged changes):

```bash
git branch -D <branchName>
# Force delete the branch "dev" irrespective of whether the changes are merged or not
```

### Quick Switch to the Previous Branch

```bash
git checkout -
```

### Check Out a New Branch Tracking a Remote Branch

```bash
git checkout --track -b feature origin/feature
git checkout -t origin/feature
git checkout feature # assuming no local feature branch and only one remote with the feature branch
```

To set upstream and track the remote branch, use:

```bash
git branch --set-upstream-to=<remote>/<branch> <branch>
git branch -u <remote>/<branch> <branch>
```

To verify branch tracking, use:

```bash
git branch -vv
```

### Renaming a Branch

```bash
git branch --move new_name
# Rename the branch you have checked out

git branch -m old new
# Rename the old branch to "new"
```

### Searching in Branches

```bash
git branch --contains <commit>
# To list local branches that contain a specific commit or tag

git branch -a --contains <commit>
# To list local and remote branches that contain a specific commit or tag
```

### Pushing a Branch to a Remote

```bash
git push <REMOTENAME> <BRANCHNAME>

git push -u <REMOTENAME> <BRANCHNAME> # short for --set-upstream

git push <REMOTENAME> <LOCALBRANCHNAME>:<REMOTEBRANCHNAME>
# Git pushes the local branch to a remote branch with the same name. To use a different name for the remote branch, append the remote name after the local branch name, separated by ":"
```

### Changing the current branch's HEAD to a specific commit

```bash
git reset --hard aabbcc
# Overwrites your branch's current commit, and its entire history. Resets the file to the state it was in at commit aabbcc.

git checkout aabbcc 
# Updates the file to the state it was in at commit aabbcc. Your changes will not be applied to the file until you stage them.
```

### Creating an Orphan Branch

```bash
git checkout --orphan <branch_name>
```

Creating an orphan branch allows you to start a new history separate from the existing branches. The first commit made on this new branch will have no parents, making it the root of a new and disconnected history. It can be useful for experimentation, prototyping, or maintaining separate versions of a project.

Remember, orphan branches can be challenging to manage if you have many of them, and merging them back into the main codebase can cause conflicts due to separate histories. Use orphan branches wisely based on your specific use case.	

[Git Example Messages - Google Docs](https://docs.google.com/document/d/1dfJyM8YzXlgw7KU-KON4TixUkIHO-OJ22gwhU7MMZ4U/edit)

