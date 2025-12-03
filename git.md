# Git
Most usefull command in git 

When add file first time, file go **Untrack**
After **git add**, file go to **stage**
After change file, file go to **unstage**

- **--local** -> only set current project
- **--global** -> set main git

### stage
![stage-git]()

### branch
- [branch]()
Tree in git, every branch can many containe commit
Popular branch name:
- main/master
- develop
- feature
- hotfix


- [.gitignore](https://www.toptal.com/developers/gitignore)
> Add this file to directory like this .gitignore, file containes not to add git
- [add]()
> Add file to git
- [alias]()
> Set alias for git
- [commit]()
> Commit files to git
- [log]()
> See commit
- [show]()
> See details commit
- [remote]()
- [push]()
- [pull]()
- [merge]()

## .gitgnore
See this [generate]()

## add
```bash
git add .        # add all files in directory

git add *.py     # git add all file ends .py

git add f.py     # add files f.py

```

## log
```bash
git log 

git log --stat              # show minimal diff commit

git log --oneline --graph --all

git log --after="25-08-11"/--before="25-09-11"

git log --author="usef"
```


## show
Show more details commit 
```bash
git show 722b78
```

## alias
We can set alias for long command
save in .git/config
```bash
git config --local/--global alias.lgo "log --oneline --all --graph"
```

## commit
```bash
git commit -m "minimal detail"  # commit 

git commit -am "detail"     # first (git add . ) after commit
```

## branch
- [Fast-foward]

```bash
git branch                  # see all branch

git switch/chekout feature  # change branch

git branch -m main master   # change name main to master

git switch -c newFeature    # create and switch 

git branch -d newFeature    # remove branch
```

### Fast-forward
After create new branch and many commit on this branch that same time main 
branch not commit.
First switch to main branch. When **git merge feature** should Fast Foward

```bash
git switch main 

git merge feature
```


```bash

```


```bash

```


```bash

```


```bash

```


```bash

```


```bash

```


