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

