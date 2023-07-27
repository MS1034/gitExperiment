# Git Cheat Sheet

## Hello World of GIT 

###### Check the Version

```bash
git --version
```

###### Create an empty Git repository:  

```bash
git init
```

###### Show modified files in working directory

```bash
git --version
```

###### Add a file as it looks now to your next commit (stage)

```bash
git add <file/directory name #1> <file/directory name #2> < ... >
```

###### Stage all files to be added to version control

```bash
git add .
```

  ###### This creates a new commit with the given message  

```bash
git commit -m "message"
//If you omit the -m parameter, your default editor will open and you can edit and save the commit message there.
```

######  Adding a remote  

```bash
git remote add origin https://<your-git-service-address>/owner/repository.git
git remote add origin git@github.com:MS1034/gitExperiment.git
```

###### Copy an existing Git repository from a server to the local machine  

```bash
cd <path where you would like the clone to create a directory>
git clone https://github.com/username/projectname.git
git clone https://github.com/username/projectname.git MyFolder //To specify a different name of the directory, e.g. MyFolder:
git clone https://github.com/username/projectname.git . // to clone in the current directory:
```

###### Sharing code  

```bash
git init --bare /path/to/repo.git //On the remote server
git remote add origin git@github.com:MS1034/gitExperiment.git //On the local machine than --set-upstream (or -u)
git push --set-upstream origin master
```

Imp:

> The commands `git remote add origin` and `git push --set-upstream origin master` are used when you already have a local repository and want to connect it to a remote repository on GitHub. On the other hand, `git clone` is used when you want to create a new local copy of an existing remote repository on GitHub.

###### Setting your user name and email  

```bash
//global
git config --global user.name "Your Name"
git config --global user.email mail@example.com

//repository
cd /path/to/my/repo
git config user.name "Your Login At Work"
git config user.email mail_at_work@example.com

//remove global
git config --global --remove-section user.name
git config --global --remove-section user.email

//To force git to look for your identity only within a repository's settings, not in the global config:
git config --global user.useConfigOnly true
```

###### Learning about a command  

```bash
git diff --help //git command --h
git help diff  // git help command 
```



