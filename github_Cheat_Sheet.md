# Git Cheat Sheet

## Hello World of GIT

[Git Explained infrastructure in under 8 min](https://towardsdatascience.com/git-help-all-2d0bb0c31483)

#### Check the Version

```bash
git --version
```

#### Create an empty Git repository:

```bash
git init
```

#### Show modified files in working directory

```bash
git --version
```

#### Add a file as it looks now to your next commit (stage)

```bash
git add <file/directory name 1> <file/directory name 2> < ... >
```

#### Stage all files to be added to version control

```bash
git add .
```

#### Stage all files to be added to version control

```bash
git status   #display which files are in which state is the git status command.

git status -s  # display changes in a more compact way 

#New files that aren’t tracked have a ?? next to them, new files that have been added to the staging area have an A, modified files have an M and so on.  are two columns to the output — the left hand column indicates the status of the staging area and the right-hand column indicates the status of the working tree.
#A - The file has been added to the staging area.
#D - The file has been deleted from the staging area.
#M - The file has been modified, but not staged.
#R - The file has been renamed, but not staged.
#C - The file has been copied, but not staged.
#? - The file is not tracked by Git
```

> Remember that each file in your working directory can be in one of two states: 
>
> 1. Tracked :
>
>    Tracked files are files that were in the last snapshot, as well as any newly staged files; they can be unmodified, modified, or staged. In short, tracked files are files that Git knows about.
>
> 2. Untracked:
>
>    Untracked files are everything else — any files in your working directory that were not in your last snapshot and are not in your staging area. 
>
> When you first clone a repository, all of your files will be tracked and unmodified because Git just checked them out and you haven’t edited anything. As you edit files, Git sees them as modified, because you’ve changed them since your last commit. As you work, you selectively stage these modified files and then commit all those staged changes, and the cycle repeats.

#### This creates a new commit with the given message

```bash
git commit -m "message"
# If you omit the -m parameter, your default editor will open and you can edit and save the commit message there.
```

#### Adding a remote

```bash
git remote add origin https:// <your-git-service-address>/owner/repository.git
git remote add origin git@github.com:MS1034/gitExperiment.git
```

#### Copy an existing Git repository from a server to the local machine

```bash
cd <path where you would like the clone to create a directory>
git clone https://github.com/username/projectname.git
git clone https://github.com/username/projectname.git MyFolder # To specify a different name of the directory, e.g. MyFolder:
git clone https://github.com/username/projectname.git . # to clone in the current directory:
```

#### Sharing code

```bash
git init --bare /path/to/repo.git # On the remote server
git remote add origin git@github.com:MS1034/gitExperiment.git # On the local machine than --set-upstream (or -u)
git push --set-upstream origin master
```

> The commands **`git remote add origin` **and **`git push --set-upstream origin master`** are used when you already have a local repository and want to connect it to a remote repository on GitHub. On the other hand, **`git clone`** is used when you want to create a new local copy of an existing remote repository on GitHub.

#### Setting your user name and email

```bash
# global
git config --global user.name "Your Name"
git config --global user.email mail@example.com

# repository
cd /path/to/my/repo
git config user.name "Your Login At Work"
git config user.email mail_at_work@example.com

# remove global
git config --global --remove-section user.name
git config --global --remove-section user.email

# To force git to look for your identity only within a repository's settings, not in the global config:
git config --global user.useConfigOnly true
```

#### Learning about a command

```shell
git diff --help # git command --h
git help diff  # git help command
```

## Browsing Git Logs

#### Listing Git Logs

```shell
git log # It will display all your commits with the author and hash in reverse chronological
order. This will be shown over multiple lines per commit. Use the q key to exit the log.

git log -2 # Limit the logs to last 2 logs

git log --decorate --oneline --graph # To see the log in a prettier graph-like structure in one line

git config --global alias.lol "log --decorate --oneline --graph" # Since it's a pretty big command, you can assign an alias

git lol # history of current branch

git lol HEAD origin/feature orign/master # combined history of active branch (HEAD), origin/feature and origin/master branches

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

[Git remote repository tutorial and with set-url origin upstream example](https://www.youtube.com/watch?v=4AbJjvMHTZk)

[Git Remotes - Git and GitHub for Poets ](https://www.youtube.com/watch?v=lR_hYwCAaH4)

#### List Existing Remotes  

```bash
git remote
git remote --verbose
git remote -v
```

#### Deleting a Remote Branch  

```bash
git push [remote-name] --delete [branch-name]
git push [remote-name] :[branch-name]
git remote remove origin
```

#### Changing Git Remote URL  

```bash
git remote set-url origin https://github.com/username/repo2.git
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
git rm filename
```

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
gen/GoalKicker.com – Git® Notes for Professionals 25
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
> 4. 



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



## Git Diff

#### Diff 

```bash
git diff

git diff --staged
```



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

