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
> Semantic commit [here](https://www.conventionalcommits.org/en/v1.0.0/) and [here](https://gist.github.com/joshbuchea/6f47e86d2510bce28f8e7f42ae84c716)
- [log]()
> See commit
- [show]()
> See details commit
- [diff]()
- [checkout]()
- [clean]()
- [remote]()
- [push]()
- [pull]()
- [merge]()
- [restart]()
- [revert]()

## .gitgnore
See this [generate](https://www.toptal.com/developers/gitignore)

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

---
## show
Show more details commit 
```bash
git show 722b78
```

---
## alias
We can set alias for long command
save in .git/config
```bash
git config --local/--global alias.lgo "log --oneline --all --graph"
```
---
## commit
```bash
git commit -m "minimal detail"  # commit 

git commit -am "detail"     # first (git add . ) after commit
```
---
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

### None Fast forwarding
Two branch **fix branch** - **main branch** after many commit on **fix branch** , before
merge with **main** commit on **main** this is say **None fast forward**

perhabs conflict like this:

```text
<<<<<<<HEAD (new change)
...
...
...
>>>>>>> fix branch
```
---
## diff
We can see diffrent between current file(working directory) with stage area 
```bash
git diff

git diff HEAD/head                  # (last commit) diffrent (working directory)

git diff (idCommit1)..(idCommit2)

git diff (idCommit1)..(idCommit2) file.txt

git diff master..fixHot 

```

## checkout
Move HEAD pointer 
```bash
git checkout HEAD~3  # third commit

git checkout HEAD .  # remove all change to last commit

git checkout HEAD file  # remove change this file to last commit
```

## clean
Remove file in git 
```bash
git clean -help  # show help
```


## restart
Back change commit 

### soft
Back soft commit HEAD move to commit 
```bash
git reset --soft commitId
```

### hard
Back hard commit change file directory
```bash
git reset --hard commitId
```

## mixed
By default reset flag do soft and out file from stage go modified
```bash
git reset --mixed commitId
```


## revert
Remove specific commit 
```bash
git revert commitId
```


```bash

```


```bash

```


```bash

```


```bash

```