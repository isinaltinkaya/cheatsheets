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

- add a specific git commit to the current working HEAD
```
git cherry-pick commitsSha
```


- Nice tutorials
[gittutorial](https://mirrors.edge.kernel.org/pub/software/scm/git/docs/gittutorial.html)
[Git for Computer Scientists](https://eagain.net/articles/git-for-computer-scientists/)
