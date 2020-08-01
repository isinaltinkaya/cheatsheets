# git cheatsheet

### add remote upstream
#### use when you fork a project to catch up with its latest updates
```
git remote add upstream https://github.com/USERNAME/REPONAME.git
```

### fetch newest from upstream
```
git fetch upstream
git checkout master
git merge upstream/master
```

### reverse `git add FILE`
```
git reset FILE
```

### reverse `git add .`
```
git reset
```

