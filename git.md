# git cheatsheet

___
___

# Emergency 

## - Go back in time: Remove a specific commit from history

### Remove the last commit from git history

```
git reset --hard HEAD^
```

Removing multiple commits from the top

### Remove the last N commits

Remove the last two commits:

```
git reset --hard HEAD~2
git push origin -f
```

`~2` : up two levels in the hierarchy
if a commit has more than one parent, use the first parent 

`^2` : the second parent where a commit has more than one parent (i.e. because it's a merge)

`HEAD~2^3` : HEAD's grandparent commit's third parent commit

___
___




### - Update branch `develop`  (origin/master->develop)

```
git checkout develop
git fetch origin
git merge origin/master
```




### - add remote upstream (use when you fork a project to catch up with its latest updates)

```
git remote add upstream https://github.com/USERNAME/REPONAME.git
```

### - reverse `git remote add upstream` command

`git remote rm upstream`

check if it's gone: `git remote -v`

### - fetch newest from upstream

```
git fetch upstream
git checkout master
git merge upstream/master
```

### - reverse `git add FILE` command

```
git reset FILE
```

### - reverse `git add .`command

```
git reset
```

- discard all uncommitted changes
```
git reset --hard
```

### - add a specific git commit to the current working HEAD

```
git cherry-pick commitsSha
```


### - config to use ssh key for a specific repository

```
$ git remote -v
origin	https://github.com/isinaltinkaya/REPO.git (fetch)
origin	https://github.com/isinaltinkaya/REPO.git (push)
#change it to git
$ git remote set-url origin git@github.com:isinaltinkaya/REPO.git
```

### 
- use soft links to sync your code in github repository directory with the working directory
```
ln -s /my/github/repo/dir/code.sh /my/working/dir/code.sh 
```

bonus: you can use my bashrc script as well

add this to your `.bashrc`:
```
lns(){
    SRC=$(realpath ${1})
    CDIR=$(pwd)
    FNAME=$(basename ${1})
    ln -vs ${SRC} ${CDIR}/${FNAME}
}
```
then
```
> cd my_working_dir
> lns ../../my_git_repo_dir/script
```
Will generate this soft link:
```
"/full/path/to/my_git_repo_dir/script" -> "/full/path/to/my_working_dir/script"
```


### - Using submodules

```
git submodule add https://github.com/samtools/htslib.git
```

clone  repo with submodules:

```
git clone --recursive ${URL}
```

if already cloned:

```
git submodule init
git submodule update
```

if submodule contains another submodule:
(with git v2.13 and later)

```
git clone --recurse-submodules ${URL}
```

if already cloned but missing a submodule of the submodule
```
git submodule update --init --recursive
```

with old version of git (v1.6.5 to v2.13)
```
git clone --recursive 
```


### - use a specific version with submodule

```
cd submodule
git checkout v1
cd ..
git add . ; git commit -m "Changed submodule version to v1"; git push
```


### - Added a large file by mistake, remote rejects my push


```
git rm --cached MY_LARGE_FILES*
git commit --amend -C HEAD
git push
```


### - Add commit message template

```
git config --global commit.template ~/.gitmessage
```

Inside `.gitmessage`:
```
# [type](optional scope): Title
#################################################
# Title length: 50 chars - - - - - - - - - - -> #
#################################################

#
# Empty line between title and body
#

#
# Body: Explain *what* and *why* (not *how*) 
# Body length: Wrap at 72 chars  - - - - - - - - - - - - - - - - - -> #

#
#
# [type]:
# -------
# [feat] - A new feature
# [fix] - A bug fix
# [perf] - A code change that improves performance
# [test] - Add test
# [build] - Build related changes
# [chore] - Build process or auxiliary tool changes
# [doc] - Documentation-related changes
# [style] - Markup, formatting, typos etc
#
# Adapted from https://dev.to/helderburato/patterns-for-writing-better-git-commit-messages-4ba0
#
```



## Nice tutorials
- [gittutorial](https://mirrors.edge.kernel.org/pub/software/scm/git/docs/gittutorial.html)

- [Git for Computer Scientists](https://eagain.net/articles/git-for-computer-scientists/)
