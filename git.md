# git cheatsheet

- add remote upstream (use when you fork a project to catch up with its latest updates)
```
git remote add upstream https://github.com/USERNAME/REPONAME.git
```

- reverse `git remote add upstream` command
`git remote rm upstream`

check if it's gone: `git remote -v`

- fetch newest from upstream
```
git fetch upstream
git checkout master
git merge upstream/master
```

- reverse `git add FILE` command
```
git reset FILE
```

- reverse `git add .`command
```
git reset
```

- discard all uncommitted changes
```
git reset --hard
```

- add a specific git commit to the current working HEAD
```
git cherry-pick commitsSha
```


- config to use ssh key for a specific repository
```
$ git remote -v
origin	https://github.com/isinaltinkaya/REPO.git (fetch)
origin	https://github.com/isinaltinkaya/REPO.git (push)
#change it to git
$ git remote set-url origin git@github.com:isinaltinkaya/REPO.git
```
- Nice tutorials
[gittutorial](https://mirrors.edge.kernel.org/pub/software/scm/git/docs/gittutorial.html)
[Git for Computer Scientists](https://eagain.net/articles/git-for-computer-scientists/)
